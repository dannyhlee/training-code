# Scala Library List


## [Akka Cluster](https://developer.lightbend.com/docs/akka-platform-guide/concepts/akka-cluster.html)
If you have a set of actor systems that cooperate to solve some business problem, then you likely want to manage these set of systems in a disciplined way. Akka Cluster gives you the ability to organize these actor systems into a “meta-system” tied together by a membership protocol.

Challenges the Cluster module solves include the following:

-   How to maintain a set of actor systems (a cluster) that can communicate with each other and consider each other as part of the cluster.
    
-   How to introduce a new system safely to the set of already existing members.
    
-   How to reliably detect systems that are temporarily unreachable.
    
-   How to remove failed hosts/systems (or scale down the system) so that all remaining members agree on the remaining subset of the cluster.
    
-   How to distribute computations among the current set of members.
    
-   How to designate members of the cluster to a certain role, in other words, to provide certain services and not others.

## [Akka HTTP](https://doc.akka.io/docs/akka-http/current/introduction.html)

The Akka HTTP modules implement a full server- and client-side HTTP stack on top of _akka-actor_ and _akka-stream_. It’s not a web-framework but rather a more general toolkit for providing and consuming HTTP-based services. While interaction with a browser is of course also in scope it is not the primary focus of Akka HTTP.

## [Akka Persistence](https://doc.akka.io/docs/akka/current/typed/persistence.html?_ga=2.154320952.1841112150.1608304780-1567924520.1607644201)

Akka Persistence enables stateful actors to persist their state so that it can be recovered when an actor is either restarted, such as after a JVM crash, by a supervisor or a manual stop-start, or migrated within a cluster. The key concept behind Akka Persistence is that only the _events_ that are persisted by the actor are stored, not the actual state of the actor (though actor state snapshot support is also available). The events are persisted by appending to storage (nothing is ever mutated) which allows for very high transaction rates and efficient replication. A stateful actor is recovered by replaying the stored events to the actor, allowing it to rebuild its state. This can be either the full history of changes or starting from a checkpoint in a snapshot which can dramatically reduce recovery times.


## [Akka actors](https://doc.akka.io/docs/akka/current/typed/actors.html)
The [Actor Model](https://en.wikipedia.org/wiki/Actor_model) provides a higher level of abstraction for writing concurrent and distributed systems. It alleviates the developer from having to deal with explicit locking and thread management, making it easier to write correct concurrent and parallel systems. Actors were defined in the 1973 paper by Carl Hewitt but have been popularized by the Erlang language, and used for example at Ericsson with great success to build highly concurrent and reliable telecom systems. The API of Akka’s Actors has borrowed some of its syntax from Erlang.

## [Caliban](https://ghostdogpr.github.io/caliban/)

**Caliban**  is a purely functional library for creating GraphQL backends in Scala. It relies on  [Magnolia (opens new window)](https://github.com/propensive/magnolia)to automatically derives GraphQL schemas from your data types,  [Fastparse (opens new window)](https://github.com/lihaoyi/fastparse)to parse queries and  [ZIO (opens new window)](https://github.com/zio/zio)to handle various effects.

The design principles behind the library are the following:

-   pure interface: errors and effects are returned explicitly (no exceptions thrown), all returned types are referentially transparent (no  `Future`).
-   clean separation between schema definition and implementation: schema is defined and validated at compile-time (no reflection) using Scala standard types, resolver is a simple value provided at runtime.
-   minimal amount of boilerplate: no need to manually define a schema for every type in your API.

Caliban can also be used to build GraphQL frontends: see the  [dedicated section](https://ghostdogpr.github.io/caliban/docs/client.html)  for more details.

## [Cask]
## [Cats]
## [Cats-effect]
## [Circe]
## [Doobie]
## [Finagle]
## [Finatra]
## [Monix]
## [Monocle]
## [Munit]
## [Play]
## [Play-json]
## [Quicklens]
## [Quill]
## [Requests-scala]
## [Sangria]
## [Scalaj]
## [Scalatest]
## [Slick]
## [Spray-json]
## [Zio]
## [Zio-streams]
## [Zio-test]
## [fs2]
## [http4s]
## [json4s]
## [sttp]
## [tapir]
## [utest]
