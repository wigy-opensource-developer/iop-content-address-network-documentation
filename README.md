![alt text](https://raw.githubusercontent.com/Fermat-ORG/media-kit/00135845a9d1fbe3696c98454834efbd7b4329fb/MediaKit/Logotype/fermat_logo_3D/Fermat_logo_v2_readme_1024x466.png "Fermat Logo")

# IoP CAN

> Content addressed network for the Internet of People based on the IPFS network

This repository only contains documentation and the issue tracking for the IoP CAN. You can find the source codes in
other repositories referred to in the [implementation documentation](ImplementationEfforts.md).

* [Specification](Specification.md)
* [Implementation efforts and status](ImplementationEfforts.md)

## Installation

We have binary packages for [Linux](https://github.com/DeCentral-Budapest/go-ipfs/releases/download/iop-QmQPrdEJpMvD5mdHZh2UAha78cZxcqAg97JundCrgbN6mF/iop-can-linux-amd64-ad911eb.tgz)
and [Windows](https://github.com/DeCentral-Budapest/go-ipfs/releases/download/iop-QmQPrdEJpMvD5mdHZh2UAha78cZxcqAg97JundCrgbN6mF/iop-can-windows-amd64-ad911eb.zip)
that you can get from our [download pages](https://github.com/DeCentral-Budapest/go-ipfs/releases) and extract into any
folder on your computer.

If you feel strong enough and you have some experience in Go development, you can build the packages from sources.
Before doing that, please read ahead and investigate how the [upstream IPFS source code can be built on different
platforms](https://github.com/ipfs/go-ipfs#build-from-source). Be warned that it has some learning curve though.

## Usage

Start the node with `ipfs daemon` or create a script that starts it on your platform after the machine has booted up.
Before the first time you start the node, you need to run `ipfs init` to create the identity of this node on the IoP
content addressed network.

You can also refer to the upstream [Getting Started](https://ipfs.io/docs/getting-started/) manual, because most of the things behave the same in our fork.

## Contributions

Feel free to send pull requests to the corresponding repositories. If you fixed something in the features added by the
Internet of People project, send the PR to our repositories. If you touched a feature that originally exists in IPFS or
you want to add a feature that would be useful to all IPFS users, we encourage you to send the PR to the upstream IPFS
repositories. If they reject something, feel free to send us a PR to discuss it also with us.

## License

[MIT](LICENSE) © 2016 [Fermat Foundation](http://www.fermat.org/)
