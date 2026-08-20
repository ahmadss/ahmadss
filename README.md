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

Ten years in, most of that time has gone into the parts users never see — payment switching that talks ISO 8583 to bank hosts, mobile banking and brokerage APIs, and wallet ledgers where a half-completed transfer is not an option. These days I work mainly in **Go**, with **Java** still in reach when a system asks for it.

```
Open to  ·  senior backend roles — Go, Java, fintech, high-throughput systems
Based    ·  Jakarta / Tangerang, Indonesia — on-site, hybrid or remote
```

---

## What I can do

**Design and run backend services**
Microservice architectures in Go and Java — gRPC over HTTP/2 with protobuf contracts, REST gateways, and clean architecture that survives a team touching it. I take a service from schema design through deployment, not just the handler layer.

**Move money without losing it**
Wallet ledgers with hold-first idempotency, escrow and split settlement, refund and reversal paths, and reconciliation that can replay history. I've built QRIS MPM switching end to end: MPAN inquiry, payment credit, check status, refund, reversal.

**Speak binary protocols over TCP**
ISO 8583 over long-lived host links — custom frame codecs, sign-on and echo keep-alive, automatic reconnect and health-checked failover, running on Netty with selectable epoll / io_uring transports.

**Orchestrate work that spans services**
Durable saga orchestration with compensating transactions: workflows that park on external events, resume where they stopped after a restart, and unwind cleanly in reverse when a step fails.

**Choose the right store, and prove it**
PostgreSQL, MySQL, ScyllaDB, ClickHouse, Redis, OpenSearch — picked per workload rather than by habit, with the connection pooling, replication and failover to keep them upright in production.

**Make systems observable before they break**
OpenTelemetry tracing with tail sampling into Tempo, Loki, Grafana and Prometheus, plus alerting and dead-letter monitoring. If it can fail at 3am, it should page someone with a trace attached.

**Ship the client too**
Flutter and native Android, which keeps my API design honest — I've been the one consuming my own endpoints.

---

## Stack

**Languages**

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Java](https://img.shields.io/badge/Java-E76F00?style=for-the-badge&logo=openjdk&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

**Services &amp; messaging**

![gRPC](https://img.shields.io/badge/gRPC-244c5a?style=flat-square&logo=grpc&logoColor=white)
![Protobuf](https://img.shields.io/badge/Protobuf-E24B26?style=flat-square&logo=googlecloud&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Vert.x](https://img.shields.io/badge/Vert.x-782A90?style=flat-square&logo=eclipseide&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-008ECF?style=flat-square&logo=go&logoColor=white)
![Netty](https://img.shields.io/badge/Netty-4A90D9?style=flat-square&logo=java&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![NATS](https://img.shields.io/badge/NATS-27AAE1?style=flat-square&logo=natsdotio&logoColor=white)
![ISO 8583](https://img.shields.io/badge/ISO_8583-5B5B5B?style=flat-square&logoColor=white)

**Data**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![ScyllaDB](https://img.shields.io/badge/ScyllaDB-6DB33F?style=flat-square&logo=apachecassandra&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white)
![MinIO](https://img.shields.io/badge/MinIO-C72E49?style=flat-square&logo=minio&logoColor=white)

**Platform &amp; delivery**

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Consul](https://img.shields.io/badge/Consul-F24C53?style=flat-square&logo=consul&logoColor=white)
![Vault](https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7?style=flat-square&logo=opentelemetry&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)

---

## A closer look

<details>
<summary><b>How I keep a transfer correct under failure</b></summary>

<br>

Money is held before it moves. Idempotency keys are derived deterministically from the transaction itself, so a retried request lands on the same ledger row instead of creating a second one. Escrow is not released and then re-collected — it is sealed and split inside a single settlement transaction, so there is no window where the money exists twice or not at all.

Storage choice follows the access pattern, not fashion: the hottest balance rows sit in MySQL because InnoDB updates them in place, without leaving dead tuples behind.

</details>

<details>
<summary><b>How I orchestrate work across services</b></summary>

<br>

Multi-service transactions run through a saga engine with durable instance state. A workflow can park on something the system cannot hurry — a driver accepting a trip, a KYC check clearing, an approval landing — and sit in `WAITING` for as long as it takes. Any process can pick it up and resume from the exact step it stopped at.

When a step fails, completed steps are compensated in reverse order. A restart mid-flight loses nothing, because the engine owns the state rather than the request.

</details>

<details>
<summary><b>How I hold a payment switch upright</b></summary>

<br>

ISO 8583 rides on long-lived TCP links to bank hosts, so throughput is bounded by syscalls and wakeups rather than bytes. The transport runs on Netty with custom length-prefixed and network-byte-order frame codecs, and a selectable epoll / kqueue / io_uring multiplexer with JDK NIO as the portable fallback.

Links stay up through drops with echo keep-alive, automatic reconnect and health-checked failover. Rate and concurrency limiters shed load rather than let the switch tip over. Messages dispatch through a routing trie instead of linear matching, so new message types are declared, not hand-wired.

</details>

<details>
<summary><b>How I pick a database</b></summary>

<br>

| Engine | Where it earns its place |
|---|---|
| PostgreSQL | transactional core — pgx behind PgBouncer, PITR for recovery |
| MySQL | balance rows — GTID replication, ProxySQL routing, binlog pipelines |
| ScyllaDB | timelines and feeds at write-heavy scale |
| ClickHouse | audit trails and risk events, queried analytically |
| Redis | GEO, pub/sub, cache and streams — split by workload, not one node for all |
| OpenSearch | catalog and message search |
| MinIO | object storage |

One service, one database. No cross-service joins.

</details>

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
