# MicroServices

## Abstract

A guided tour through Chris Richardson's *Microservices Patterns*: when (not) to break up
the monolith, what changes when in-process calls become network hops, and the patterns
that keep a distributed system from collapsing into a distributed monolith. Covers
Sagas, API Gateways, CQRS, the Service Registry, and the operational reality of running
many small services in production.

## Target Audience

Backend and full-stack developers, architects, and tech leads who are considering — or
already living with — a microservices architecture. No prior microservices experience
required, but comfort with REST, databases, and basic distributed-systems vocabulary
helps.

## Key Takeaways

- Why "the monolith is bad" is the wrong starting point — and the symptoms that
  actually justify a split
- Interprocess communication patterns: synchronous REST/gRPC vs asynchronous messaging,
  Circuit Breakers, Service Discovery
- How to maintain data consistency without distributed transactions: Sagas
  (Choreography vs Orchestration), the Transactional Outbox, and CQRS for queries
- Production-ready concerns most demos skip: configurability, observability, the
  MicroService Chassis and Service Mesh patterns
- A pragmatic refactoring playbook for strangling an existing monolith without
  rewriting it

## Session Format

120 minutes — theoretical, with a short break in the middle. No hands-on coding;
discussion-friendly.
