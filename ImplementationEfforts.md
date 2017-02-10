## go-ipfs

IPFS implementation in the Go language.

> https://github.com/DeCentral-Budapest/go-ipfs

* Added `ipfs name upload`
* Added `ipfs swarm discover`
* Using a forked libp2p to have a network independent of the main IPFS network
* PRs were sent for the 1 added features, but they are not accepted yet by the
  upstream IPFS project

## ipfs-key

A tool to generate IPFS private keys (identities)

> https://github.com/DeCentral-Budapest/ipfs-key

* Integrated ed25519 cryptography for supporting IoP identities
* PR was accepted and merged back

## ipns-gen

A tool to generate and sign IPNS records on one machine, which can be then
published on the IPFS network with `ipfs name upload` on another machine without
sharing the private key of the IPNS record.

> https://github.com/DeCentral-Budapest/ipns-gen

* This is a sample implementation that can be reimplemented in other languages
* It also can be integrated into applications as an external command-line
  process

## go-libp2p

Go implementation of the libp2p framework that enables building peer-to-peer
overlay networks that are bootstrapped from some seed nodes.

> https://github.com/DeCentral-Budapest/go-libp2p

* Changed the protocol identifier, the default port numbers and the hardcoded
  seed nodes.
* This change will never be merged back to https://github.com/libp2p/go-libp2p
* If all other features are merged back, we might consider rebasing our CAN
  implementation onto the original IPFS network. Then we do not need to maintain
  this fork and the separate infrastructure.
* Forks that are needed, because they depend on this repository:
  * https://github.com/DeCentral-Budapest/go-floodsub
  * https://github.com/DeCentral-Budapest/go-libp2p-kad-dht

## multibase

Specification for interoperable implementations for transforming 8-bit binary
buffers into formats that are easier to transfer over limited channels. Some of
them are human readable, some of them are just prepared for technical
limitations of a protocol that cannot transfer 8-bit binary.

> https://github.com/DeCentral-Budapest/multibase

* Added "identity" encoding for channels that are capable of transfering
  8-bit binaries
* PR is accepted, but was not merged back yet

## go-multibase

Implementation of multibase in the Go language.
 
> https://github.com/multiformats/go-multibase/commits?author=wigy-opensource-developer

* Added "identity" encoding for channels that are capable of transfering
  8-bit binaries
* PR was accepted and merged back to https://github.com/multiformats/go-multibase

## iptb

A tool for creating and managing a cluster of sandboxed IPFS nodes locally on a
single computer for end-to-end testing.

> https://github.com/whyrusleeping/iptb

* This tool depends on https://github.com/ipfs/go-ipfs so it needs to be forked
  with our version of it to get all end-to-end tests passing
* This change will never be merged back

