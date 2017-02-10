# IoP CAN Wiki Home

This is the knowledge base for the content addressed network component of the Internet of People network.

## Table of contents

- [Introduction](#introduction)
- [The Naming System](#the-naming-system)
- [The Proposed Implementation](#the-proposed-implementation)
  - [Use-Cases for Authenticated Systems](#use-cases-for-authenticated-systems)
  - [Use-Cases for Anyone](#use-cases-for-anyone)
  - [Typical Scenario](#typical-scenario)

## Introduction

Strictly speaking the content addressed network (CAN) only supports 2 operations:

- *Upload:* Client stores some content on the network and gets back a hash only based on that content. Note, that if
  different nodes store the same content at different times independently from each other, they get back the same hash,
  because that hash is only dependent on the content itself.
- *Download:* Clients presents a hash for the network and therefore can retrieve the content that generates that hash.

This simple interface has many advantages:

- Uploading content will form a so-called swarm for its hash. If someone else tries to upload the same content, no
  matter how they got the content, it will join the existing swarm. This means the network de-duplicates popular
  contents, the download requests will be shared among all machines that have that content. The content itself will move
  through the network only when someone actually downloads it.
- The downloading nodes are able to cache popular contents without worrying about invalidation, because the content is
  immutable.
- Anyone who has an interest keeping some content available for the network is able to do so without a permission from
  any parties.
- It is enough to sign or just share the hash of a larger content on an external system, because it is equivalent to
  signing or sharing the whole content.

This simplicity has some drawbacks, too:

- Cannot share a hash in an external system and then update the content without re-sharing the new hash of the new
  updated content.
- Cannot delete a compromising uploaded content from the network if others still have an interest keeping it on the
  network

For fixing the first drawback, we need a key-value store a.k.a naming system. The second drawback is by design, we need
to address that in the application layer or in real life.

## The Naming System

We need a way of creating a mutable link into the CAN, so that the clients could lookup the current version of a mutable
content. We also need to authorize changes to that link. In a decentralized system, signing an operation is the usual
form of authorization. Looking at 2 different versions of that link, we also need to decide which version is more
recent. All of these are solved by a key-value store, where the key is deterministically calculated from the public key
of the key-pair used for authorizing changes, and this is used as a name for a mutable content, and the value consists
of the following fields:

- hash of the current version of the content on the CAN
- sequence number that is increased with each version
- signature on the 2 previous fields made using the private key that belongs to this name

So for each mutable content we either need a separate key-pair or we would need a way to know which name can be changed
by which keys. The former design will be implemented in our CAN. [The later](AlternativeNamingSystems.md) is also a
solved, but slightly more complex design, which needs an immutable log of security related events, usually implemented
as a blockchain.

## The Proposed Implementation

Re-implementing these systems from scratch is a considerable effort. It seems to be more efficient to build on top of an
existing system like IPFS (see https://ipfs.io) and adapt it to our needs. The IPFS has 2 independent, but compatible
implementations in JavaScript and Go. The Go implementation is more mature currently and provides us with a CAN without
significant changes. For our naming system use-cases it has a solution called IPNS that is not suitable for our needs,
so we need to [spend some efforts extending it](https://github.com/ipfs/notes/issues/206).

### Use-Cases for Authenticated Services

Establishing a relation between a CAN node and a service happens out-of-band, it does not happen through the network.
Every service must either have a CAN node on the same system, or have an agreement with a CAN node. Therefore there is
no need for a special "register service public key" message, the public key of the profile service needs to be just
added to the configuration of the CAN node. All other messages on this interface needs to be
[authenticated with some of those configured service public keys](AuthenticationOfMessages#current-state).

- *Publish Content:* Input is an opaque byte array. If the content was successfully published on IPFS, the client gets
  back the hash IPFS calculated for that content and the CAN makes sure this content is available on the network at
  least as long as an unpublish message is received for this content.
- *Unpublish Content:* Input is the hash returned by the "publish content" message. Calling this message frees up
  storage and bandwidth for contents not needed any more for providing the service.
- *Publish Name:* Since the profile service knows which application profiles are paid for and are valid, it must
  register the public keys of those profiles on its CAN node. This is done when the first profile publishing is done.
  Input is a record serialized into a well-defined format that contains the signature. Output is either just success, or
  in case there is a more recent version already on the network, the sequence number of that version is returned in an
  error. Other possible errors might contain problems with the signature or the hash does not point to a valid
  application profile version.
- *Unpublish Name:* Since the profile service knows which application profiles are cancelled, it must stop publishing
  the name as soon as the application profile leaves the profile service. In case the profile was moved to a new profile
  service, unpublishing the name on the old CAN node saves bandwidth for the whole network. Publishing a new content for
  the same name on the new CAN node will succeed even without unpublishing it on the old node, but it wastes resources.

### Use-Cases for Anyone

- *Provide Node Addresses:* Input is empty, output is a random selection of 5 CAN nodes this CAN node is connected to.
- *Download Content:* Input is a hash of a content. Output is a byte array.
- *Download Name:* Input is a name. Output is a record serialized into a well-defined format that contains the hash of
  the current version of the content, the sequence number of the current version and the signature authenticating this
  version of the name.

### Typical Scenario

In the typical scenario for creating a new application profile on a profile service,

- The CAN node configuration contains the public key for the profile service or others IoP services in general.
- The profile service authenticates itself on a network connection to the CAN node.
- The profile service calls *publish content* with a serialized format of the application profile.
- The profile service asks the client to authenticate this change by sending the hash of the new profile data to it.
- The client might optionally download the content and check whether it agrees with the changes.
- The client sends the profile service a signed message that contains the hash of the profile data and a sequence number
  that is incremented with each profile update done by the client.
- The profile service sends this signed structure to the CAN node in a *publish name* message.