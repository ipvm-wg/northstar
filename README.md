# 🌟 North Star 

# Meta

> If your starting-point is unknown, and your end-point and intermediate stages are woven together out of unknown material, there may be coherence, but knowledge is completely out of the question.
> 
> — Plato, The Republic

This document is an informal description of IPVM's high-level goals. It forms the basis for reasoning about the project from first principles. It expected to only rarely change.

This is meant to provide the basis for reasoning from first principles, but it is written in prose and not first-order logic. It "merely" provides a basis for aligning the people working on the project. Principles often contain some limited internal tension: use your best judgment and discuss with your peers when ambiguities inevitably arise.

This text should be kept short, to the point, and as unambiguous as possible. Define any project-specific jargon, avoid editorializing, and limit subtle language. Use diagrams and imagery where appropriate.

# Raison d'Être

> Had the [Web] been proprietary, and in my total control, it would probably not have taken off. You can’t propose that something be a universal space and at the same time keep control of it.
>
> — Tim Berners-Lee

IPVM intends to do nothing less than connect all of the world's users and services. It can be thought of as "the HTTP of compute": open, interoperable, and everywhere. Following the model of the Web being the network of linked documents, IPVM is the network of linked computation. It allows anyone to permissionlessly tie into the network without prenegotiation.

TCP/IP and HTTP were successful for a number of reasons. Networking was always possible, but doing this from scratch for every application is infeasible. Hypertext provided a single mechanism for many applications to interconnect. Application agnosticism is a major pillar of such an approach: anything can run on this substrate, and it's easy to join. IPVM works equally well with traditional Cloud-based services as it does local-first compute and trustless architectures. To be successful, IPVM must have a path towards becoming substantially better than a pure Cloud architecture. It does not stand in opposition to the Cloud, but rather extends and contains it.

The internet is no longer purely client/server. Consumer devices are now significantly more powerful than when the LAMP stack and Cloud infrastructure were being co-developed. Devices today are heterogeneous: there are powerful browsers, heavy servers, microservices, edge PoPs, tiny IoT devices, smartphones, and commons networks like BitTorrent, IPFS, and blockchains. IPVM provides a way to tie applications together with robust invocation, routing, and trust layers. The volume of data that modern applications requires leads to a situation known as data gravity. Given the speed of light, the amount of data that we produce and modify grows faster than is possible to sync to all locations, and .

# Audience

IPVM is intended for general distributed computation, but excels at tasks that would be found in systems like Lambda Step functions. The IPVM network itself is focused on machine-to-machine interaction — where each node acts as the user's agent — but is not expected to be interacted with directly when on the happy path.

# Goals

IPVM means to provide:

- Task matchmaking network / marketplace
- Pluggable execution engine
- A trust layer (e.g. verifiable compute, encryption, PKI, capabilities)
- Seamlessly tie together external services
- Interfaces open to extension
- First-class P2P payments

It is application agnostic, but intends to abstract concerns of locality away from the programmer.

## Antigoals

IPVM will not attempt to develop into a:

- replacement of IPFS internals
- high level language for distributed applications
- custom Wasm runtime
- blockchain or other global consensus mechanism

IPVM's focus is on execution, networking, data flow, and safety. It is important to make the internals debuggable and friendly where possible, but only when it doesn't conflict with the core aim at this layer: efficiency and abstracting away distributed systems concerns.

IPVM's primary focus is on machines and efficiency. Human-friendliness is important, but many human-oriented features should be pushed into higher layers. These may include high-level APIs, language integration, etc.

# Design Principles

> You can prove anything you want by coldly logical reason — if you pick the proper postulates.
> 
> — Asimov, "I, Robot"

1. Proliferate!
2. Open world / extension without prenegotiation
3. Participatory: anyone can consume, serve, or both
4. Learn into our strengths: IPVM is not k8s, so don't try to be
5. Common tasks should be simple, and complex things should be possible
6. Handle low-level details (networking, failure, trust) so that others can focus on business logic
7. Build in layers with clear audiences (machine-to-machine, end-user, etc)

When in doubt, optimize for proliferation. Get implementations into many hands, find services that already tie-in at the RPC and trust layers (UCAN), and avoid having the core IPVM team become a bottleneck for extending the network. [Richard Gabriel] described Unix and C as being like (helpful) computer viruses due to how they spread and integrate with other systems.

IPVM simplifies distributed dataflow. It's tempting to think of it as moving single threaded local code to a logically centralized executor, but ultimately it's lowering the barrier of entry to distributed code.

[Homestar] is the reference implementation for the [IPVM] network. It is intended to be largely self-contained, and to run on as many systems as possible.

## Easy for Who?

> Simplicity is a prerequisite for reliability
> 
> — Dijkstra

> Every application has an inherent amount of complexity that cannot be removed or hidden. Instead, it must be dealt with, either in product development or in user interaction. 
>
> — [Tesler's Law]

The word "simple" is often used to mean "to make a common use case easy". This is goal directed: "simple for who or what?" IPVM aims to make distributed computing easy by abstracting away the common challenges of that context. In the same way that TCP/IP handles machine-to-machine networking concerns in an application agnostic way, IPVM doesn't attempt to enforce what can be run on it.

Per [Tesler's Law], solving these common problems for the distributed setting does mean that something has to be traded off. Running arbitrary code designed for local-only execution doesn't work in these settings. Much like depending on techniques like read-your-writes or CRDTs at the data layer, IPVM requires low-level implementations use certain tools and techniques. Following the tactic of "do one thing well", concerns of providing familiarity is pushed above the network layer to good libraries and tools.

# Appendix

## Eight Fallacies of Distributed Computing

IPVM intends to make computing more accessible in a distributed context. Recall the [8 Fallacies of Distributed Computing]:

1. The network is reliable
2. Latency is zero
3. Bandwidth is infinite
4. The network is secure
5. Topology doesn't change
6. There is one administrator
7. Transport cost is zero
8. The network is homogeneous

Some strategies include: constraining expressivity to a safe subset (similar to the approach taken by [structured programming]), providing a robust standard library, and static analysis.

## World Wide Web Foundation's Principles

The early web was founded on the [following principles][W3F Principles]:

### Decentralization

No permission is needed from a central authority to post anything on the web, there is no central controlling node, and so no single point of failure … and no “kill switch”! This also implies freedom from indiscriminate censorship and surveillance.

### Non-discrimination

If I pay to connect to the internet with a certain quality of service, and you pay to connect with that or a greater quality of service, then we can both communicate at the same level. This principle of equity is also known as Net Neutrality.

### Bottom-up design

Instead of code being written and controlled by a small group of experts, it was developed in full view of everyone, encouraging maximum participation and experimentation.

### Universality

For anyone to be able to publish anything on the web, all the computers involved have to speak the same languages to each other, no matter what different hardware people are using; where they live; or what cultural and political beliefs they have. In this way, the web breaks down silos while still allowing diversity to flourish.

### Consensus

For universal standards to work, everyone had to agree to use them. Tim and others achieved this consensus by giving everyone a say in creating the standards, through a transparent, participatory process at W3C.

<!-- Internal Links -->

<!-- External Links -->

[Homestar]: https://github.com/ipvm-wg/homestar/
[Richard Gabriel]: https://en.wikipedia.org/wiki/Richard_P._Gabriel
[Tesler's Law]: https://en.wikipedia.org/wiki/Law_of_conservation_of_complexity
[W3F Principles]: https://webfoundation.org/about/vision/history-of-the-web/
