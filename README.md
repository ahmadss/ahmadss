<h1 align="center">Achmad Saifuddin</h1>

<p align="center">
  <b>Senior Backend Engineer</b> · Jakarta, Indonesia<br>
  <sub>Payment switching · distributed systems · Go &amp; Java</sub>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/achmad-saifuddin-434a748b/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
  <a href="mailto:saifuddinahmad12@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white"></a>
  <a href="https://ahmadss.github.io/yaudah/arsitektur/zentara-arsitektur.html#ringkasan"><img alt="Architecture writeup" src="https://img.shields.io/badge/Architecture_Writeup-14615E?style=flat-square&logo=readthedocs&logoColor=white"></a>
</p>

---

I build transaction systems that cannot afford to be wrong.

Ten years in, most of that time has gone into the parts users never see — payment switching that talks ISO 8583 to bank hosts, mobile banking and brokerage APIs, and wallet ledgers where a half-completed transfer is not an option.

```
Open to  ·  senior backend roles — Go, Java, fintech, high-throughput systems
Based    ·  Jakarta / Tangerang, Indonesia — on-site, hybrid or remote
```

---

## Go

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-244c5a?style=flat-square&logo=grpc&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-008ECF?style=flat-square&logo=go&logoColor=white)
![Uber fx](https://img.shields.io/badge/Uber_fx-000000?style=flat-square&logo=uber&logoColor=white)
![Protobuf](https://img.shields.io/badge/Protobuf-E24B26?style=flat-square&logo=googlecloud&logoColor=white)
![pgx](https://img.shields.io/badge/pgx-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![NATS](https://img.shields.io/badge/NATS-27AAE1?style=flat-square&logo=natsdotio&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7?style=flat-square&logo=opentelemetry&logoColor=white)

My main language. I write services that run unattended for weeks, so the shape of the code matters as much as what it does.

**Clean architecture, applied rather than quoted.**
Each service is layered `domain → usecase → repository → transport`, with the business rules in the middle knowing nothing about gRPC, Postgres or Redis. Dependencies are wired at the edge with **Uber fx**, so a repository is swapped for a fake in tests without touching a single line of the logic under test. Background work — outbox relays, consumers, sweepers — lives in its own `worker` layer with its own lifecycle hooks, started and stopped by the container rather than by `init()`.

**Transport.**
gRPC over HTTP/2 with protobuf contracts between services, and a grpc-gateway shard translating REST at the edge. Interceptors carry authentication, tracing and rate limits so no handler re-implements them.

**WebSocket, built for connections that must not silently die.**
Long-lived sockets are the part people get wrong. Mine run a ping ticker with `WriteControl`, a `PongHandler` that pushes the read deadline forward, and write deadlines on every frame — so a half-open connection is detected instead of quietly hanging. Origin is checked at the upgrader, reads are size-limited, and messages fan out through a hub that survives a slow client without blocking the others. The ping loop and the fan-out both have their own tests, because "it worked on my laptop" is not a guarantee for something that has to hold for hours.

**Concurrency with an owner.**
Goroutines are started with a context that can cancel them and a shutdown path that waits for them. Redis-backed limiters cap concurrent work across replicas, not just inside one process.

---

## Java

![Java](https://img.shields.io/badge/Java-E76F00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![Hibernate](https://img.shields.io/badge/JPA_/_Hibernate-59666C?style=flat-square&logo=hibernate&logoColor=white)
![Vert.x](https://img.shields.io/badge/Vert.x-782A90?style=flat-square&logo=eclipseide&logoColor=white)
![Netty](https://img.shields.io/badge/Netty-4A90D9?style=flat-square&logo=java&logoColor=white)
![ISO 8583](https://img.shields.io/badge/ISO_8583-5B5B5B?style=flat-square)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white)

Where I go when a system is close to the metal or close to a bank.

**Spring Boot for the platforms.** Mobile banking and brokerage APIs — Spring Security for the auth surface, JPA/Hibernate over the transactional core, and Vert.x where the traffic profile called for an event loop rather than a thread per request. Regulated reporting — stock agreements, tax and transaction statements — generated with JasperReports.

**Netty for the protocol work.** Payment switching lives on long-lived TCP links, so the transport is hand-built: custom length-prefixed and network-byte-order frame codecs, a selectable epoll / kqueue / io_uring multiplexer with JDK NIO as the portable fallback, connection caps, and sign-on / echo / sign-off keep-alive per host.

**ISO 8583 dispatch that scales with the message set.** Incoming messages route through a trie matched on field patterns with wildcard and regex support, declared by annotation. Adding a message type is a declaration, not a new branch in a growing switch.

**Multi-module Maven** with the shared framework — state machine, limiters, routing, ACL, load-balanced endpoints with health checks — separated from the endpoint modules that speak ISO 8583, gRPC and HTTP.

---

## Databases

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![ScyllaDB](https://img.shields.io/badge/ScyllaDB-6DB33F?style=flat-square&logo=apachecassandra&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white)
![MinIO](https://img.shields.io/badge/MinIO-C72E49?style=flat-square&logo=minio&logoColor=white)

I pick a store per workload and can explain the choice.

| Engine | Where it earns its place |
|---|---|
| **PostgreSQL** | transactional core — pgx behind PgBouncer, PITR for recovery |
| **MySQL** | balance rows updated in place — GTID replication, ProxySQL routing, binlog pipelines |
| **ScyllaDB** | timelines and feeds under write-heavy load |
| **ClickHouse** | audit trails and risk events, queried analytically |
| **Redis** | GEO, pub/sub, cache and streams — split across instances by workload |
| **OpenSearch** | catalog and message search |
| **MinIO** | object storage, S3-compatible |

The rules I hold to: one service owns one database, no cross-service joins, and the hot path decides the engine. Balances sit in MySQL precisely because InnoDB updates the hottest rows in place instead of leaving dead tuples behind — a Postgres habit would have cost vacuum pressure exactly where it hurts.

Connection handling is part of the design, not an afterthought: pooling through PgBouncer, prepared-statement limits tuned to the pooler, and read traffic routed to replicas with causal consistency where correctness allows it.

---

## Saga orchestration

Distributed transactions are where systems quietly lose money, so I run them through a saga engine with durable state.

- **Workflows survive the process.** Instance state lives in the database, not in the request. A restart mid-flight resumes from the exact step it stopped at.
- **Steps park on the real world.** A workflow can sit in `WAITING` for a driver to accept a trip, a KYC check to clear, or an approval to land — for as long as it takes — then be picked up and continued by any process.
- **Failure unwinds cleanly.** When a step fails, completed steps are compensated in reverse order rather than left half-applied.
- **Retries are safe.** Idempotency keys are derived deterministically from the transaction, so a retry lands on the same row instead of creating a second one.
- **Scale.** 80+ step executors across nine domains — payments, top-up, QRIS, wallet, mobility, commerce and more.

For money specifically: funds are held before they move, and escrow is sealed and split inside a single settlement transaction — never released and then re-collected, so there is no window where the money exists twice or not at all.

---

## Building the system around it

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Consul](https://img.shields.io/badge/Consul-F24C53?style=flat-square&logo=consul&logoColor=white)
![Vault](https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)

**Event-driven by default.** Services publish through an outbox written in the same transaction as the state change, so an event is never lost when the process dies between commit and publish. Kafka, NATS and Redis Streams each carry the traffic that suits them, with dead-letter handling for what cannot be retried.

**Reads separated from writes.** Hot read paths are served by their own services and stores, so a heavy feed query never contends with a write that has to be correct.

**Observable before it breaks.** Every service is instrumented with OpenTelemetry — traces into Tempo, logs into Loki, metrics into Prometheus, all read through Grafana, with tail sampling so the interesting traces survive. Alerting and dead-letter monitors are wired in from the start, not bolted on after the first incident.

**Runs on bare metal.** The platform I operate moved off managed Kubernetes onto a self-hosted cluster behind Cloudflare — which means I own the ingress, the pooling, the backups and the restore drill, not just the manifests.

**Delivered continuously.** Containerised services, GitHub Actions pipelines, and migrations versioned alongside the code.

---

## Reference

A full system architecture I designed and operate, written up end to end — flow maps, service catalog, data layer, encryption schemes:

📐 **[Architecture writeup →](https://ahmadss.github.io/yaudah/arsitektur/zentara-arsitektur.html#ringkasan)** &nbsp;<sub>in Bahasa Indonesia</sub>

<p align="center">
  <img height="160" alt="stats" src="https://github-readme-stats.vercel.app/api?username=ahmadss&show_icons=true&hide_border=true&include_all_commits=true&theme=graywhite&title_color=14615E&icon_color=14615E">
  <img height="160" alt="languages" src="https://github-readme-stats.vercel.app/api/top-langs/?username=ahmadss&layout=compact&hide_border=true&langs_count=8&theme=graywhite&title_color=14615E">
</p>

<sub>Most of my recent work lives in private repositories — the public ones here are older. The writeup above is the better window into what I build today.</sub>

---

<p align="center">
  <sub>Open to senior backend engineering roles · <a href="mailto:saifuddinahmad12@gmail.com">saifuddinahmad12@gmail.com</a></sub>
</p>
