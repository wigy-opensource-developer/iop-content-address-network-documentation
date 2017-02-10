# Authentication of Messages

IPFS does not seem to have authentication on single messages. On the readonly interface there is no need for
authentication. The admin interface is hidden behind a firewall, so only owners of the node should be able to access it.
The swarm connections form an [Byzantine p2p network](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance), so there
is no real trust to any other peer. Bitswap binds peer ids to reputation of the nodes, so there is an authentication on
swarm connections, but not on the admin or readonly gateway interfaces.

The only special case seems to be the signed IPNS record which can be treated as an authenticated message. Till recently
only 1 such record could be distributed by a given peer, so that authentication was based on the node's identity. The
[keystore feature](https://github.com/ipfs/go-ipfs/pull/3472) that was recently added decouples keys used for IPNS from
keys used as peer identity. Of course our additions to IPNS with
[`ipns-gen`](https://github.com/DeCentral-Budapest/ipns-gen) and `ipfs name upload` is similar to the keystore feature,
but it also moves the keys out from the nodes.

## Current state

As of January 2017, we do not have short-term plans to implement key-based authentication for the admin interface or a
separate interface for authenticated read-write users.
[IoP Profile Server](https://github.com/Fermat-ORG/iop-profile-server/) acts as an authentication layer for read-write
users and relays some messages to the CAN node. Also, the admin interface of the CAN node need to be hidden from public
and only contracted services should be able to connect to them.

- The simplest solution for this is to put a CAN node on the same system as the profile server and bind the admin
  endpoint to localhost
- If the CAN node is hosted in a datacenter, not co-located with the profile server, the admin endpoint needs to be
  bound to a VLAN that is only accessible through a VPN connection for contracted services.