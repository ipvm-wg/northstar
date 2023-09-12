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
> — Berners-Lee, [FAQ][TBL FAQ]

IPVM intends to do nothing less than connect all of the world's users and services. It can be thought of as "the HTTP of compute": open, interoperable, and everywhere. Following the model of the Web being the network of linked documents, IPVM is the network of linked computation. It allows anyone to permissionlessly tie into the network without prenegotiation.

TCP/IP and HTTP were successful for a number of reasons. Networking was always possible, but doing this from scratch for every application is infeasible. Hypertext provided a single mechanism for many applications to interconnect. Application agnosticism is a major pillar of [such an approach][W3F Principles]: anything can run on this substrate, and it's easy to join. IPVM works equally well with traditional Cloud-based services as it does local-first compute and trustless architectures. To be successful, IPVM must have a path towards becoming substantially better than a pure Cloud architecture. It does not stand in opposition to the Cloud, but rather extends and contains it.

The internet is no longer purely client/server. Consumer devices are now significantly more powerful than when the LAMP stack and Cloud infrastructure were being co-developed. Devices today are heterogeneous: there are powerful browsers, heavy servers, microservices, edge PoPs, tiny IoT devices, smartphones, and commons networks like BitTorrent, IPFS, and blockchains. IPVM provides a way to tie applications together with robust invocation, routing, and trust layers.

Finally: the volume of data that modern applications requires leads to a situation known as data gravity. Given the speed of light, the amount of data that we produce and modify grows faster than is possible to sync to all locations, and the rate of change makes it physically impossible to ever catch up. There are also still many cases where the data is small and.or infrequent enough to be practical to move around on the network. To meet the needs of such a heterogeneous network, IPVM provides a flexible model that takes into account the [costs and trade-offs of distributed computing][Fallacies of Distributed Computing] by ad hoc moving data to where the code lives, as well as ad hoc moving code to where the data lives.

# Audience

> Every application has an inherent amount of complexity that cannot be removed or hidden. Instead, it must be dealt with, either in product development or in user interaction. 
>
> — [Tesler's Law]

> I think that, collectively, we are infatuated with these two notions of easy ["near-at-hand" and "in your current skill set"]. We are just so self-involved in these two aspects; it's hurting us tremendously.
>
> — Hickey, [Simple Made Easy]

IPVM is intended for general distributed computation, but excels at tasks that would be found in systems like [AWS Lambda Step functions], [Fastly Compute@Edge], and [Temporal Cloud]. The IPVM network itself is focused on machine-to-machine interaction — where each node acts as the user's agent — but is not expected to be interacted with directly when on the happy path.

The word "simple" is often used interchangeably with "easy" to mean making a common use case require little effort. This is goal directed: "easy for who or what?" IPVM aims to make distributed computing easy by [abstracting away][Fault Oblivious] the common challenges of that context. In the same way that TCP/IP handles machine-to-machine networking concerns in an application agnostic way, IPVM doesn't attempt to enforce which kinds of services can be interconnected.

Standardizing on Wasm also highlights IPVM's core audience. At time of writing, there is comparatively little Wasm written; but the belief is that will change quickly. IPVM uses Wasm in its emphasis to  decompose compute into simpler units that are composable, cacheable, reusable, and tractable for a distributed setting. Per [Tesler's Law], solving these [common problems for the distributed setting][Fallacies of Distributed Computing] means that something else has to be traded off. Running arbitrary code designed for local-only execution doesn't work in these settings. Much like depending on techniques like read-your-writes or CRDTs at the data layer, IPVM requires low-level implementations use certain tools and techniques. Following the tactic of "do one thing well", concerns of providing familiarity is pushed above the network layer to good libraries and tools.

# Goals

IPVM means to provide:

- Task matchmaking network / marketplace
- A trust layer (e.g. verifiable compute, encryption, PKI, capabilities)
- The ability to tie together external services seamlessly
- Interfaces open to extension
- First-class P2P payments
- The ability to run everywhere (servers, browsers, mobile applications, etc)
- Application agnostic
- Abstract concerns of locality away from the programmer

## Antigoals

IPVM will _not_ attempt to develop into a:

- replacement or upgrade of IPFS internals
- high level language for distributed applications
- custom Wasm runtime
- blockchain or other global consensus mechanism
- a web server framework

IPVM focuses on execution, networking, dataflow, and trust. It is important to make the internals debuggable and friendly where possible, but only when it doesn't conflict with the core aim at this layer: efficiency and abstracting away distributed systems concerns. Human-friendliness is important, but many human-oriented features should be pushed into higher layers. These may include high-level APIs, language integration, etc.

# Design Principles

> You can prove anything you want by coldly logical reason — if you pick the proper postulates.
> 
> — Asimov, "I, Robot"

1. Proliferate!
2. Open world / extension without prenegotiation
3. Participatory: anyone can consume, serve, or both
4. Learn into our strengths: IPVM is not k8s, so don't try to be
5. Common things should be simple, and complex things should be possible
6. Handle low-level details (networking, failure, trust) so that others can focus on business logic
7. Build in layers with clear audiences (machine-to-machine, end-user, etc)

When in doubt, optimize for proliferation. Get implementations into many hands, find services that already tie-in at the RPC and trust layers ([UCAN]), and avoid having the core IPVM team become a bottleneck for extending the network. Unix and C have been describes as being like [(helpful) computer viruses][Models of Software Acceptance] due to how they spread and integrate with other systems.

IPVM simplifies distributed dataflow. It's tempting to think of it as moving unconstrained centralized code to a logically centralized executor, but IPVM actually lowers the barrier of entry to distributed code. A distributed context is fundamentally different from writing code for a single machine[^LamportsProblem].

[Homestar] is the reference implementation of the IPVM protocol. Homestar is intended to be largely self-contained, and to run on as many systems as possible.

[^LamportsProblem]: As Leslie Lamport says, "a distributed system is one in which the failure of a machine you have never heard of can cause your own machine to become unusable".

<!-- Internal Links -->

<!-- External Links -->

[AWS Lambda Step functions]: https://docs.aws.amazon.com/lambda/latest/dg/lambda-stepfunctions.html
[Fallacies of Distributed Computing]: https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing
[Fastly Compute@Edge]: https://docs.fastly.com/products/compute-at-edge
[Fault Oblivious]: https://rebelsky.cs.grinnell.edu/~rebelsky/Courses/CS302/Fun/fault-oblivious.html 
[Homestar]: https://github.com/ipvm-wg/homestar/
[How do we tell truths that might hurt?]:https://www.cs.virginia.edu/~evans/cs655/readings/ewd498.html 
[Models of Software Acceptance]: https://dreamsongs.com/Files/AcceptanceModels.pdf
[Richard Gabriel]: https://en.wikipedia.org/wiki/Richard_P._Gabriel
[Simple Made Easy]: https://www.infoq.com/presentations/Simple-Made-Easy/
[TBL FAQ]:https://www.w3.org/People/Berners-Lee/FAQ.html 
[Temporal Cloud]: https://temporal.io/
[Tesler's Law]: https://en.wikipedia.org/wiki/Law_of_conservation_of_complexity
[UCAN]: https://github.com/ucan-wg
[W3F Principles]: https://webfoundation.org/about/vision/history-of-the-web/
[structured programming]: https://en.wikipedia.org/wiki/Structured_programming
