---
layout: home
title: Cord
---

Cord is a data streaming platform for composing, aggregating and distributing arbitrary
streams. It uses a publish-subscribe model that allows multiple publishers to share their
streams via a [Cord Broker](https://github.com/cord-proj/cord-broker). Subscribers can
then compose custom sinks using a regex-like pattern to access realtime data based on
their individual requirements.

To interact with the Broker, Cord provides the
[Cord Client](https://github.com/cord-proj/cord-client), which comprises a library and a
CLI. As the project matures, this library will form the basis of a suite of adaptors for
common technologies.

## Modules

The Cord Project comprises three modules (_crates_ in Rust parlance):

1.  **[Cord Broker](https://github.com/cord-proj/cord-broker)** - the server binary that
    aggregates and distributes arbitrary streams
2.  **[Cord Client](https://github.com/cord-proj/cord-client)** - provides a library and
    CLI for interacting with Cord brokers
3.  **[Cord Message](https://github.com/cord-proj/cord-message)** - an internal crate
    that defines the message envelope and codec for transmitting messages over the wire

## Usage

First, start a new [Cord Broker](https://github.com/cord-proj/cord-broker):

**Docker**

```console
docker run -d -p 7101:7101 --rm cord-broker
```

**Cargo**

```console
cargo install cord-broker
cord-broker &
```

Next, use the [Cord Client](https://github.com/cord-proj/cord-client) to interact with
the Broker. You can implement Cord within your own project using the
Client library ([docs.rs](https://docs.rs/cord-client)), however the easiest way to get
started is by using the CLI.

Subscribe to a namespace:

**Docker**

```console
docker run --rm cord-client -a <broker_addr> sub /names
```

**Cargo**

```console
cargo install cord-client
cord-client sub /namespaces
```

Publish to this namespace:

**Docker**

```console
docker run -it --rm cord-client -a <broker_addr> pub /names
```

**Cargo**

```console
cord-client pub /names
```

## Etymology

Cord derives its name from the _spinal cord_. The long term goal of this project is to
aggregate data from every part of your environment, so that the decisions you make within
that environment are better informed. This is akin to the central nervous system, which
uses the spinal cord to aggregate electrical feedback from nerve endings.
