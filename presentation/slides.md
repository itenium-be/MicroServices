---
theme: ./theme
title: MicroServices
subTitle: "MicroServices Patterns"
transition: fade
session-time: 120min
track: Architecture
type: Theoretical
first: 2024-10-17
lastUpdate: 2026-04-09
---

# Micro
# Services

::image::

![](./images/cover-art.jpg)

---
layout: agenda
textSize: sm
items:
  - The Monolith
  - MicroServices
  - Interprocess Communication
  - Business Logic
  - Queries
  - External APIs
  - Production Ready
  - Deployment
---
---
layout: default-aside
disabled: true
---

# Chapters

<v-clicks>

- The Monolith
- Interprocess Communication
- Transactions
- Business Logic
- Queries
- External APIs
- Testing
- Deployment
- Decomposition & Refactoring

</v-clicks>

::image::

![](./images/chapters-decorative.jpg)

---
layout: two-col-image-text
image: ./images/book-microservices-patterns.jpg
---

# Microservices Patterns

## Tis een halve boekbespreking

::content::

<v-clicks depth="2">

- With examples in Java
- 470 pages on everything MicroServices
- By Chris Richardson: microservices.io
- Describes a collection of Patterns

</v-clicks>
---
layout: default-aside
---

# Microservices Patterns

## Design Patterns... Again?

<v-clicks depth="2">

- FORCES
  - What we must address
- RESULTING CONTEXT
  - Benefits -- what did we gain
  - Drawbacks -- what did we lose
  - Issues -- new problems we introduced
- FOR
  - Application And Infrastructure

</v-clicks>

::image::

![](./images/patterns-decorative.jpg)

---
layout: section
---

# The Monolith

::subtitle::

Monolithic Architecture

---
layout: default-aside
---

# Monolithic Architecture

<v-clicks depth="2">

- For example n-tier or Hexagonal
- Why you should build a Monolith
  - It's easy -- your IDE handles it well
  - It's easy -- everyone has experience creating one
  - It's easy -- to write unit & integration tests
  - It's easy -- to deploy
  - It's easy -- to scale (typically)
  - It's easy -- to make big changes

</v-clicks>

<div v-click class="text-center italic mt-8 text-primary">
Typically a good top level architecture to start with
</div>

::image::

![](./images/monolith-clouds.jpg)
---
layout: default-aside
disabled: true
---

# 4+1 View Model

- Implementation View:
  - Monolith: a single exe
  - MicroServices: multiple exes
- Logical View:
  - Both are layered or hexagonal

::image::

![](./images/no-silver-bullet-wooden.jpg)

---
layout: statement
disabled: true
---

Organizations which design systems … are constrained to produce designs which are copies of the communication structures of these organizations

::author::

**Melvin Conway**

Reverse Conway Maneuver

::image::

![](./images/no-silver-bullet-wooden.jpg)

<!--
https://en.wikipedia.org/wiki/Conway%27s_law

https://www.thoughtworks.com/insights/blog/customer-experience/inverse-conway-maneuver-product-development-teams
-->
---
layout: statement
---

If your application is very successful, the monolith may turn out to be not such a great idea after all

::image::

![](./images/monolith-vs-success.jpg)

<!--
The team grew, the codebase grew, the product grew
-->
---
layout: two-col-image-text
---

# Monolithic Hell

::image::

![](./images/monolith-hell.jpg)

::content::

<v-clicks>

- The codebase intimidates developers
- Development is slow
  - Edit-build-run-test loop takes a long time
- The road to deploy is long and arduous
- Locked in an increasingly obsolete stack

</v-clicks>
---
layout: two-col-image-text
---

# The Scale Cube

## Scaling may turn out to be not that easy (anymore)

::image::

![](./images/scale-cube.jpg)

---
layout: statement
---

Maintainability, extensibility and testability suffer

::image::

![](./images/monolith-hell-fire.jpg)

---
layout: section
---

# MicroServices

::subtitle::

So... MicroServices?

---
layout: default-aside
textSize: xl
---

# So... MicroServices?

<v-clicks>

- Each service is small and easily maintained
- Can be independently deployed
- Can be independently scaled
- Teams can work autonomously
- Better fault isolation
- Easy experimentation and adoption of new technologies

</v-clicks>

::image::

![](./images/no-silver-bullet.jpg)

<!--
Each service can be X & Z scaled
-->

---
layout: default-aside
textSize: xl
---

# How Micro is a MicroService?

<v-clicks depth="2">

- The size of a MicroService is not relevant
  - A team could be responsible for a single MicroService
  - So maybe it's not "Micro" at all!
- What is important
  - Minimal lead time
  - Minimal collaboration with other teams

</v-clicks>

::image::

![](./images/how-micro.jpg)

<!--
**Lead time**: from request to deployment
-->


---
layout: default-aside
---

# No Silver Bullet

There are significant drawbacks & challenges

<v-clicks depth="2">

- Finding the right services is challenging
- Distributed systems are complex
  - Other services are down or unavailable
  - Deployment needs coordination
  - Writing tests spanning multiple services
  - Additional operational complexity
- What about cross-cutting concerns

</v-clicks>

::image::

![](./images/no-silver-bullet-wooden.jpg)

<!--
**Complexity**:  
What to do when the other system is down, unavailable or crashes?
-->
---
layout: default-aside
---

# No Silver Bullet

## There are significant drawbacks & challenges

<v-clicks>
If you need to collaborate with different teams for the smallest of changes

If you constantly need to make changes because of changes in other services

**You have just built yourself a distributed monolith**

</v-clicks>

<v-clicks>

- All of the drawbacks
- None of the benefits

</v-clicks>

::image::

![](./images/no-silver-bullet-wooden.jpg)
---
layout: quote-image
---

::image::

![](./images/meme-murder-mystery.jpg)
---
layout: default-aside
---

# Loosely Coupled Services

<v-clicks>

- Communication via APIs or Messaging
- Internals are hidden
- Each service has its own database
- ✅ Can change independently
- ✅ No locks by other services
- ⚠️ Queries are harder
- ⚠️ Maintaining data consistency

</v-clicks>

::image::

![](./images/loosely-coupled.jpg)

<!--
**Internals are hidden**: Information Hiding / Encapsulation at a higher level
-->
---
layout: default-aside
---

# Obstacles

<v-clicks>

- Network latency & chatty services
  - Batch calls or combine services?
- Synchronous Interprocess Communication
  - Reduces availability
- Maintain data consistency
  - Distributed Transactions vs Saga
- Consistent view of data
  - Letting go of the monolithic ACID

</v-clicks>

::image::

![](./images/obstacles-boulder.jpg)

<!--
**Chatty Services**:  
To get Order + Consumer => 2 calls  
OR: /v1/order/5?expand=consumer => 1 call (less chatty) -> or use GraphQL

**Synchronous Interprocess Communication**:
- Reduced availability: if one service is down, you are down
- Synchronous API call? -> Because you are waiting for it!

**ACID**: Atomic, Consistent, Isolated, Durable  
MicroServices only has ACD
-->
---
layout: section
---

# Interprocess Communication
---
layout: default
---

# Interprocess Communication

<v-clicks depth="2">

- Monolith: in process calls (<1ms)
- MicroServices: interprocess (10-500ms)
  - Synchronous: REST (JSON/XML), gRPC
  - Async: AMQP, STOMP
    - Allows one-to-many
- Binary vs Human Readable
  - Verbosity: cost, longer parsing, performance

</v-clicks>

<!--
**Interprocess**: network latency, de(serialization) and server processing + potential packet loss/retries & network congestion

gRPC: Google Remote Procedure Call  
AMQP: Advanced Message Queuing Protocol  
STOMP: Simple (or Streaming) Text Oriented Messaging Protocol

**One-to-many**: with publish/subscribe
-->
---
layout: default
---

# Interprocess Communication
## Defining APIs

New incompatible version deployed becomes a runtime exception rather than a compilation error

<v-clicks>

- Need for IDL: Interface Definition Language
- Need for a strategy to evolve APIs
  - Can't force other teams to upgrade (immediately)
  - Run versions side-by-side -- no lockstep upgrades needed
    - Semantic versioning
  - Robustness Principle

</v-clicks>

<!--
**IDL:** OpenApi Specification (from Swagger)

**Semantic Version**: Major.Minor.Patch

Often done: putting the major version in the url

Put major in header,MIME type, …

**Robustness Principle**

Be conservative in what you do, be liberal in what you accept

Provide defaults for new request properties (that conserve the initial behavior)

Ignore new response properties
-->
---
layout: default
---
# Interprocess Communication
## Defining APIs

Pattern: Proxy & Adapter

<v-clicks>

- Hide that it is a Remote Procedure Invocation
- Hide the address, port and protocol used

</v-clicks>

<!--
REST levels:

Level 2: GET, POST, PUT and Resources

Level 3: HATEOS: GET returns urls for operations
-->
---
layout: default-aside
---

# Interprocess Communication
## Circuit Breaker

A proxy that rejects invocations for x time after y consecutive failures

<v-clicks>

- Network timeouts
- Limit outstanding requests to server
- Exceeded threshold → Fail immediately

</v-clicks>

::image::

![](./images/circuit-breaker.jpg)

<!--
**Circuit Breakers**: Netflix Hystrix, Polly
-->
---
layout: default
---

# Interprocess Communication
## Failure Recovery

<v-clicks>

- Essential → Fail
- Return a default value
- Return a cached response

</v-clicks>

Decide on a case per case basis...

<!--
**Default Value**: if it’s not that important

**Cached Response**: if stale data is ok

The client or frontend can maybe still work with partial data.
-->
---
layout: default
---

# Interprocess Communication
## Service Discovery

<v-clicks>

- What is the URL
  - Monolith: a config file
  - MicroService: cloud and/or dynamic

</v-clicks>

<!--
Dynamic URL:

Auto-Scaling

Failures  and auto-restarts

(Rolling) Upgrades
-->
---
layout: default
---

# Interprocess Communication
## Service Discovery

The solution, as so many times with MicroServices, is to... add another service

**"Service Registry"**
---
layout: default-aside
---

# Interprocess Communication
## Service Registry

<v-clicks>

- Self-Registration
  - A service registers itself + health check & heartbeat
- Client-Side Discovery
  - Query the Service Registry + cache
  - + Load balancing
- Prefer a platform-provided solution

</v-clicks>

::image::

![](./images/service-registry.jpg)

<!--
Example: Netflix Eureka + Ribbon Http client, Pivotal Spring Cloud

Platform provided: Docker & Kubernetes  The deployment system handles it
-->
---
layout: section
---

# Asynchronous Messaging

::subtitle::

Interprocess Communication

---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

<v-clicks depth="2">

- Message Broker
  - The intermediary between services
  - Another service 😉
- Exchange messages over a channel
- Types of messages
  - Document: receiver interprets
  - Command: point-to-point
  - Event: publish/subscribe

</v-clicks>

::image::

![](./images/message-broker.jpg)

<!--
ActiveMQ, RabbitMQ, Kafka, AWS Kinesis, AWS SQS

Events or Broadcasts
-->
---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Brokerless Messaging:

- ✅ Broker is not the bottleneck or single point of failure
- ✅ More lightweight
- ⚠️ Tighter coupling between services
- ⚠️ Reduced availability
- ⚠️ Guaranteed delivery is trickier

::image::

![](./images/brokerless.jpg)

<!--
**Brokerless**: (ex: ZeroMQ)

Send messages directly from server to receiver

**Reduced availability**: both sender and receiver need to be available
-->
---
layout: default
---

# Interprocess Communication
## Asynchronous Messaging

<v-clicks>

- Competing Message Broker Capabilities
  - Language support
  - Ordered delivery vs Latency
  - Persistence: survive a system crash
  - Durability: receive missed messages after service restart
  - Competing consumers
  - Guaranteed delivery: deliver at least once

</v-clicks>

<!--
**Competing capabilities**: pick a broker that supports what you need

Ordered delivery typically means increased latency

Guaranteed delivery: Typically a broker promises to deliver a message at least once (receive, handle, crash before acknowledging handled)
-->
---
layout: default
---

# Interprocess Communication
## Asynchronous Messaging

Deliver AT LEAST ONCE? 😱😱😱

<v-clicks>

- Write idempotent message handlers
- Track messages and discard duplicates
  - Pattern: Transactional Outbox
  - Save the message id in an outbox table and commit this as part of the database transaction
  - Send the message by polling the outbox
  - Or by log tailing the database transaction log

</v-clicks>

<!--
**Database Transaction Log Tailing:**

Debezium (Kafka), LinkedIn Databus, DynamoDB Streams, Eventuate Tram
-->
---
layout: default
---

# Interprocess Communication
## Asynchronous Messaging

Try to eliminate synchronous interactions

<v-clicks>

- Send a message and return a response immediately
- Replicate data instead of querying
- Use a Saga

</v-clicks>

<!--
**Replicate data**:

By subscribing to changed events. CQRS covered later on.
-->
---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Saga: a message driven sequence of local transactions in order to maintain data consistency

<v-clicks>

- Countermeasures for missing Isolation
- Choreography vs Orchestration

</v-clicks>

::image::

![](./images/saga-warrior.jpg)

<!--
**Countermeasures**:

Implement countermeasures to prevent or reduce impact of concurrency anomalies

**Choreography**:

Participants of the saga exchange messages without central point of control

**Orchestration**:

Centralized controller tells participants what to do
-->
---
layout: default
---

# Interprocess Communication
## Asynchronous Messaging

Saga alternative: Distributed Transaction

X/Open XA: Two-phase commit (2PC)

All participants commit or rollback

- ✅ No data consistency anomalies
- ⚠️ We're basically synchronous again
- ⚠️ Reduced availability
- ⚠️ Not supported by MongoDb, RabbitMQ, Kafka

<!--
Basically an Anti-Pattern

**Data consistency anomalies**:

Lost updates: overwrite something from another saga

Dirty reads: read half finished saga

Non-repeatable reads: two steps of the saga see something different

**Reduced availability**: all participants must be available!
-->
---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Saga: each service commits

<v-clicks>

- We need compensating messages
- Compensatable Transactions
- Pivot Transactions
- Retriable Transactions

</v-clicks>

::image::

![](./images/saga-compensating.jpg)

<!--
**For when things go wrong…**

**Compensatable Transactions**:

Transactions that can be rolled back by compensating transactions

**Pivot Transactions**:

The go/no-go point of the sage (ex: payment)

**Retriable Transactions**:

After the pivot transaction, if one of these fails, we will try them again
-->
---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Saga: Choreography

<v-clicks>

- Service handles and sends the next message
- Must use "Transactional Outbox"!
- Correlation ID for event mapping

</v-clicks>

::image::

![](./images/saga-choreography.jpg)
---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Saga: Choreography

- ✅ Loosely coupled & Simple
- ⚠️ Flow is defined in multiple places
- ⚠️ What has (already) happened?
- ⚠️ Risk of tight coupling

::image::

![](./images/saga-choreography.jpg)

---
layout: default-aside
---

# Interprocess Communication
## Asynchronous Messaging

Saga: Orchestration

<v-clicks>

- Orchestrator is a State Machine
- Orchestrator sequences between states and not contain any logic

</v-clicks>

✅ Easy to test

✅ Recommended

::image::

![](./images/orchestration.jpg)

---
layout: section
---

# Business Logic

---
layout: default-aside
---

# Business Logic

<v-clicks>

- Transaction Script
- Domain Model
- EventSourcing

</v-clicks>

::image::

![](./images/business-logic.jpg)

<!--
**Transaction Script**:

If it’s simple, keep it simple.

**Domain Model**:

Aggregates map to Services.

Also here challenges: what does it mean to delete an entity? (Fuzzy Boundaries)

 We’ll have DDD sessions 😀

**EventSourcing**:

A developer might forget to send an EntityUpdated event after processing his BL  Use EventSourcing to update aggregates instead!

 See our CQRS session!
-->
---
layout: default-aside
---

# Business Logic
## Domain Events

EntityUpdated events

<v-clicks>

- Noteworthy changes on aggregates
- Notify for the next step in the process
- Send notifications (email, SMS, ...)
- Analyze events for user behavior

</v-clicks>

::image::

![](./images/domain-events.jpg)
---
layout: default-aside
---

# Business Logic
## Domain Events

EntityUpdated events

<v-clicks>

- ID Only
  - ✅ Small messages
  - ⚠️ Consumers need to request
- Enrichment
  - ⚠️ Less stable events

</v-clicks>

::image::

![](./images/domain-events.jpg)
---
layout: break
---

# ☕ Break

::timer::

<Timer minutes="10" />

::image::

![](./images/cover-art.jpg)

---
layout: quote-image
---

# How Micro is a MicroService?

::image::

![](./images/comic-microservice-size.jpg)

<!--
**Lead time**: from request to deployment
-->
---
layout: section
---

# Queries

---
layout: two-col-image-text
---

# Queries
## Pattern: API Composition

<v-clicks>

- Query multiple services and combine the results

</v-clicks>

- ✅ Easy to implement
- ⚠️ Network and computing overhead
- ⚠️ Lack of transactional data consistency
- ⚠️ Reduced availability
  - Cached fallbacks
  - Return incomplete data

::image::

![](./images/api-composition.jpg)
---
layout: default-aside
---

# Queries
## Pattern: CQRS

<v-clicks>

- Maintain read-only Elastic/Solr for complex queries
- Might be inefficient to select everything
  - Too much data
  - Join large datasets in memory

</v-clicks>

::image::

![](./images/cqrs-mirror.jpg)

<!--
**Example**:

Restaurant app & database does nor support geospatial datatypes (findAvailableRestaurants)
-->
---
layout: section
---

# External APIs

::subtitle::

Internal & External Clients

---
layout: default-aside
---

# External APIs
## Internal & External Clients

Don't expose the microservices

<v-clicks>

- Difficult to use, bad dev xp
- Difficult to force upgrades of 3rd parties

</v-clicks>

Solution: **API Gateway**

::image::

![](./images/external-apis.jpg)

<!--
**Internal Admin App**: High bandwidth LAN

**External Clients**: Lower performing internet
-->
---
layout: default-aside
---

# External APIs
## API Gateway

<v-clicks>

- API Composition
- Authentication & other edge functions
- Routing
- Protocol Translation
- One-size-fits-all or data depends on client
  - Pattern: Backends for Frontends

</v-clicks>

::image::

![](./images/api-gateway.jpg)

<!--
**Edge functions**:

Authentication, Authorization, Rate limiting, Caching, Metrics collection, Request logging

**Protocol translation**: Internal service might use gRPC

**Depends on client**: return less data for a mobile client

**Backends for frontends**: Netflix Falcor
-->
---
layout: default-aside
---

# External APIs
## API Gateway

- Handle partial failures
- Uses Service Discovery Patterns
- Potential bottleneck
- Off the shelf or GraphQL

::image::

![](./images/api-gateway.jpg)

<!--
**Off the shelf**: Netflix Zuul, Traefik, Spring Cloud Gateway, AWS API Gateway, AWS Application Load Balancer
-->
---
layout: section
---

# Production Ready

::subtitle::

Developing production-ready Services

---
layout: default-aside
---

# Production Ready

<v-clicks>

- Security
- Configurability
- Observability

</v-clicks>

::image::

![](./images/production-ready.jpg)
---
layout: default-aside
---

# Production Ready
## Security

<v-clicks>

- Authentication & Authorization
- Auditing
- Secure Communication (TLS)
- Access Token (by API Gateway)
  - JWT or Oauth 2.0

</v-clicks>

::image::

![](./images/security-key.jpg)

<!--
Spring Security, Apache Shino, NodeJS Passport
-->
---
layout: default-aside
---

# Production Ready
## Configurability

<v-clicks>

- Externalized Configuration
  - Push Model
    - CI passes configuration to the service
  - Pull Model
    - Service reads config from a service

</v-clicks>

::image::

![](./images/configurability.jpg)

<!--
**Push:** using environment variables or files. Files: there are files everywhere.

**Pull**: using git, a DB, Spring Cloud Config

**Sensitive data**: Hashicorp Vault, AWS Parameter Store

Pull is centralized, dynamic reconfiguration, transparent decryption, yet another service
-->
---
layout: default-aside
---

# Production Ready
## Observability

<v-clicks depth="2">

- Healthchecks
  - Simple 200/500
  - Or more detailed
    - Watch out for oversharing
  - Used by the deployment infrastructure

</v-clicks>

::image::

![](./images/observability-eye.jpg)

<!--
Ex: HealthChecks.NET, Spring Boot Actuator

Checked by: Docker, Kubernetes, Netflix Eureka

More detailed:

Do a db query

Check external services are available
-->
---
layout: default-aside
---

# Production Ready
## Observability

<v-clicks>

- Log Aggregation
  - Elastic, Splunk, DataDog, ...
- Distributed Tracing
  - Log a request ID!
- Application Metrics
  - CPU, memory, disk utilization
- Exception Tracking & Alerting

</v-clicks>

::image::

![](./images/log-aggregation.jpg)

<!--
You don’t want to go checking log files on different servers

**Application Metrics**: Heartbeats & Prometheus

**Exception Tracking**: de-duplicate exceptions. Alerting with for example Sentry.IO
-->
---
layout: default
disabled: true
---

# Production Ready
## Audit Logging

<v-clicks>

- Customer Support
- Ensure Compliance
- Detect suspicious behavior
- "Easy" with EventSourcing

</v-clicks>

---
layout: quote-image
---

# Cross-Cutting Concerns

Circuit Breaker, Tracing, Logging, Service Discovery, Health checks, Configuration, ...

::image::

![](./images/one-million-microservices.jpg)
---
layout: default-aside
---

# Production Ready

<v-clicks>

- Pattern: MicroService Chassis
  - Combine all cross-cutting concerns
- Pattern: Service Mesh
  - Route all traffic through a layer that does the chassis stuff + load balancing, routing, ...

</v-clicks>

::image::

![](./images/chassis.jpg)

<!--
**Chassis**: GoKit, Micro

**Mesh**: Istio, Conduit, Linkerd
-->
---
layout: section
---

# Deployment

::subtitle::

It needs to be highly automated

---
layout: default-aside
---

# Deployment

Deploying a million services manually is not feasible

DevOps Teams

<v-clicks>

- Pets vs Cattle
- Snowflake vs Phoenix

</v-clicks>

::image::

![](./images/deployment.jpg)

---
layout: default
---

# Deployment
## Language-Specific Package Pattern

Copy the code & start

- ✅ Easy & fast
- ✅ Good way to get started
- ⚠️ Different versions of .NET / SDK
- ⚠️ Service crashes on same machine can impact others
- ⚠️ A service can utilize all CPU
- ⚠️ Manually decide on what machines to put which services

---
layout: default
---

# Deployment
## A Virtual Machine (VM)

Ship the whole thing: OS, Dependencies & App

- ✅ Got everything & the right versions too!
- ✅ Fixed amount of CPU & memory
- ⚠️ Overhead of an entire OS
- ⚠️ Slower: need to send a lot of bytes
- ⚠️ Must maintain the machines (patches & updates)
- ⚠️ Might be paying for lots of unused resources

<!--
Elastic Beanstalk, Packer for VirtualBox, VMWare, Aminator, …
-->
---
layout: default
---

# Deployment
## A Container Image

Build image, push to registry, start container

- ✅ Isolated
- ✅ Can specify CPU & Memory
- ✅ More lightweight than a VM
- ⚠️ You're responsible for the Image administration

<!--
Ex: Docker, Podman

Registry: Docker Cloud Registry, AWS EC2 Container Registry
-->
---
layout: default
---

# Deployment
## Kubernetes

Docker Orchestration: uses a set of machines with Docker as a pool of resources as if it were a single machine.

Service Management: named & versioned services

<v-clicks>

- Zero downtime deployments: rolling updates / rollbacks
- Have x healthy instances of a service (health checks)
- Load balancing

</v-clicks>

Scheduling: Checks service requirements to select a machine

(Anti)-Affinity: services to (not) run on the same machine

<!--
**Service Mesh**: Separate deployment from release

Deploy, test and only then release

Maybe next Architecture/Cloud sessions on Kubernetes…
-->
---
layout: default
---

# Deployment
## Serverless

- ✅ Only pay for what you use
- ✅ Eliminate sysadmin tasks
- ✅ Elasticity: spin up as needed to handle the load
- ⚠️ Cold startup
- ⚠️ Not intended for long running processes

<!--
AWS Lambda, Azure Functions

**Long running processes**: don’t put a message handler on serverless
-->
---
layout: section
---

# Refactoring

::subtitle::

When to move to MicroServices

---
layout: default-aside
---

# Refactoring
## When to move to MicroServices

Don't!

<v-clicks>

- Slow Delivery & Deployment?
  - → Automated testing!
- Poor Scalability?
  - → Scale Cube!
  - → First try simpler solutions!

</v-clicks>

::image::

![](./images/refactoring.jpg)
---
layout: default-aside
---

# Refactoring
## When to move to MicroServices

If you find yourself in a hole, stop digging

::image::

![](./images/stop-digging.jpg)
---
layout: default-aside
---

# Refactoring
## Moving to MicroServices

Strangle the monolith

<v-clicks>

- Don't attempt a rewrite
- Migrate high value areas
  - These can then evolve independently
- You don't need all the MicroService infrastructure (right away)

</v-clicks>

::image::

![](./images/strangle-monolith.jpg)

<!--
**Rewrite**:

Moving target

Or no more delivery for a long time

**High value areas**:

Can demo benefit to the business quickly

Extract a service on an area that is actively being developer
-->
---
layout: default-aside
---

# Refactoring
## Moving to MicroServices

<v-clicks>

- Split the UI
- Splitting the domain
  - Potentially major surgery
  - Hexagonal: limit changes to in/out adapters
- Database Refactorings
  - Move data
  - Replicate with triggers

</v-clicks>

::image::

![](./images/strangle-monolith.jpg)

<!--
**Move data**: to the new services

**Replicate**: and make the monolith data read-only

Or: Write new features as services

Or: Focus o

Timebox service architectures.
-->
---
layout: default-aside
---

# Refactoring
## Moving to MicroServices

Minimize changes to the monolith

<v-clicks>

- API Gateway
- Integration Glue Code
- Anti-Corruption Layer

</v-clicks>

::image::

![](./images/strangle-monolith.jpg)

<!--
**API Gateway**: Route to monolith or a MicroService

**Glue Code**: Messaging or Invoke REST APIs from the Monolith
-->
---
layout: end
---

---
layout: socials
---

---
layout: default
---

# Powerpoint Source

<div class="flex flex-col items-center justify-center h-full -mt-16">
  <div class="w-64 h-64">
    <QRCode url="https://github.com/itenium-be/MicroServices" color="#343434" />
  </div>
  <a href="https://github.com/itenium-be/MicroServices" class="mt-4 text-lg">github.com/itenium-be/MicroServices</a>
</div>
