## go-ipfs

IPFS implementation in the Go language.

> [Our fork](https://github.com/Fermat-ORG/iop-content-address-network)

* Added `ipfs name upload` ([PR](https://github.com/ipfs/go-ipfs/pull/3547))
* Added `ipfs swarm discover` ([PR](https://github.com/ipfs/go-ipfs/pull/3540))
* Using a forked [libp2p](#go-libp2p) to have a network independent of the main IPFS network
* PRs were sent for the 2 added features, but they are not accepted yet by the
  upstream IPFS project

## ipfs-key

A tool to generate IPFS private keys (identities).

> [Our contributions](https://github.com/whyrusleeping/ipfs-key/commits?author=wigy-opensource-developer)

* Integrated ed25519 cryptography for supporting IoP identities
* [PR](https://github.com/whyrusleeping/ipfs-key/pull/6) was accepted and merged back
* This is a sample implementation that can be reimplemented in other languages
* It can also be integrated into applications as an external command-line
  process

## ipns-gen

A tool to generate and sign IPNS records on one machine, which can be then
published on the IPFS network with `ipfs name upload` on another machine without
sharing the private key of the IPNS record.

> [Our source code](https://github.com/Fermat-ORG/iop-content-address-network-iptb)

* This is a sample implementation that can be reimplemented in other languages
* It can also be integrated into applications as an external command-line
  process

## go-libp2p

Go implementation of the libp2p framework that enables building peer-to-peer
overlay networks that are bootstrapped from some seed nodes.

> [Our fork](https://github.com/Fermat-ORG/iop-content-address-network-go-libp2p)

* Changed the protocol identifier, the default port numbers and the hardcoded
  seed nodes.
* This change will never be merged back to https://github.com/libp2p/go-libp2p
* If all other features are merged back, we might consider rebasing our CAN
  implementation onto the original IPFS network. Then we do not need to maintain
  this fork and the separate infrastructure.
* Forks that are needed, because they depend on this repository:
  * [go-floodsub](https://github.com/Fermat-ORG/go-floodsub)
  * [go-libp2p-kad-dht](https://github.com/Fermat-ORG/go-libp2p-kad-dht)

## multibase

Specification for interoperable implementations for transforming 8-bit binary
buffers into formats that are easier to transfer over limited channels. Some of
them are human readable, some of them are just prepared for technical
limitations of a protocol that cannot transfer 8-bit binary.

> [Our contributions](https://github.com/multiformats/multibase/commits?author=wigy-opensource-developer)

* Added "identity" encoding for channels that are capable of transferring
  8-bit binaries
* [PR](https://github.com/multiformats/multibase/pull/19) was accepted and was merged back

## go-multibase

Implementation of [multibase](#multibase) in the Go language.
 
> [Our contributions](https://github.com/multiformats/go-multibase/commits?author=wigy-opensource-developer)

* Added "identity" encoding for channels that are capable of transferring
  8-bit binaries
* [PR](https://github.com/multiformats/go-multibase/pull/6) was accepted and merged back

## iptb

A tool for creating and managing a cluster of sandboxed IPFS nodes locally on a
single computer for end-to-end testing.

> [Our fork](https://github.com/Fermat-ORG/iptb)

* This tool depends on https://github.com/ipfs/go-ipfs so it needs to be forked
  with our version of it to get all end-to-end tests passing
* This change will never be merged back to https://github.com/whyrusleeping/iptb

