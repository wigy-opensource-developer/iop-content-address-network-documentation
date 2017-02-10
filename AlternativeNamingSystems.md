# Alternative Naming Systems

This is a stub to show alternatives to IPNS records currently used as a [naming system](Specification.md#naming-system)
in the IoP CAN.

# Pubsub

For fast-changing mutable content with regular updates, it makes sense to subscribe to changes and multicast these
changes. Usually these systems call the thing you can subscribe to as a *topic*. There are centralized solutions for
pubsub like [redis](https://redis.io/). Also, IPFS guys experiment with their decentralized
[floodsub implementation](https://github.com/ipfs/js-ipfs/issues/580).

Pros:

- No polling is needed
- Latency of changes is only limited by event-propagation speed on the overlay network

Cons:

- New subscribers get only the next event, so there needs to be an alternative way to read the current state
- Decentralized solutions are not mature enough to be resilient

# Blockchain

You could write the current hash that belongs to a key onto a blockchain and index that blockchain to lookup the latest
legitimate updates. This index could also provide pubsub features.

> Luis, I lost the link to the technology you mentioned that implements this concept. Could you please remind me?

Note, that decentralized blockchains are built on top of a pubsub mechanism that propagates at least the latest blocks.
Remembering the whole history of changes might be beneficial or a problematic based on your use-case.

Pros:

- History if you need that
- Can be bound to payment
- Best studied pubsub mechanisms are implemented for blockchains

Cons:

- History if you want to hide changes
- Usually there is a transaction cost in some currency per change