<h1 align="center">Achmad Saifuddin</h1>

<p align="center">
  <b>Senior Backend Engineer</b> · Jakarta, Indonesia<br>
  <sub>Payment switching · distributed systems · Go &amp; Java</sub>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/achmad-saifuddin-434a748b/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
  <a href="mailto:saifuddinahmad12@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white"></a>
  <a href="https://ahmadss.github.io/yaudah/arsitektur/zentara-arsitektur.html#ringkasan"><img alt="Architecture" src="https://img.shields.io/badge/Architecture_Guide-14615E?style=flat-square&logo=readthedocs&logoColor=white"></a>
</p>

---

I build transaction systems that cannot afford to be wrong.

Ten years in, most of that time has gone into the parts users never see — a QRIS MPM switching platform talking ISO 8583 to bank hosts, mobile banking and brokerage APIs, and wallet ledgers where a half-completed transfer is not an option. These days I work mainly in **Go**, with **Java** still in reach when a system asks for it.

```
Currently  ·  building Zentara, a super-app platform I architect and run end to end
Focus      ·  event-driven services, polyglot persistence, Kubernetes on bare metal
Open to    ·  senior backend roles — Go, Java, fintech, high-throughput systems
```

---

### Stack

**Languages**

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Java](https://img.shields.io/badge/Java-E76F00?style=for-the-badge&logo=openjdk&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

**Services &amp; messaging**

![gRPC](https://img.shields.io/badge/gRPC-244c5a?style=flat-square&logo=grpc&logoColor=white)
![Protobuf](https://img.shields.io/badge/Protobuf-E24B26?style=flat-square&logo=googlecloud&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-008ECF?style=flat-square&logo=go&logoColor=white)
![Netty](https://img.shields.io/badge/Netty-4A90D9?style=flat-square&logo=java&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![NATS](https://img.shields.io/badge/NATS-27AAE1?style=flat-square&logo=natsdotio&logoColor=white)

**Data**

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![ScyllaDB](https://img.shields.io/badge/ScyllaDB-6DB33F?style=flat-square&logo=apachecassandra&logoColor=white)
![ClickHouse](https://img.shields.io/badge/ClickHouse-FFCC01?style=flat-square&logo=clickhouse&logoColor=black)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white)
![MinIO](https://img.shields.io/badge/MinIO-C72E49?style=flat-square&logo=minio&logoColor=white)

**Platform**

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7?style=flat-square&logo=opentelemetry&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)

---

### What I'm building

**Zentara** — a super-app platform covering wallet, ride-hailing, commerce, chat and social, which I architect and operate on my own.

<table>
<tr>
<td align="center"><b>65</b><br><sub>Go services</sub></td>
<td align="center"><b>103</b><br><sub>protobuf contracts</sub></td>
<td align="center"><b>175</b><br><sub>K8s manifests</sub></td>
<td align="center"><b>16</b><br><sub>Flutter modules</sub></td>
</tr>
</table>

📐 **[Read the full architecture guide →](https://ahmadss.github.io/yaudah/arsitektur/zentara-arsitektur.html#ringkasan)**
_Flow maps, service catalog, data layer, encryption schemes. Written in Bahasa Indonesia._

<details>
<summary><b>The money path</b> — how a transaction survives partial failure</summary>

<br>

Every transfer is held before it is moved. Idempotency keys are derived deterministically from the transaction itself, so a retried request lands on the same ledger row rather than creating a second one. Escrow is never released and then re-collected — it is sealed and split inside a single settlement transaction, so there is no window in which the money exists in two places or neither.

Balances live in MySQL rather than PostgreSQL on purpose: the hottest rows are updated in place, and InnoDB updates them without leaving a trail of dead tuples behind.

</details>

<details>
<summary><b>Durable saga orchestration</b> — workflows that outlive the process running them</summary>

<br>

Multi-service transactions run through a saga engine of my own, spanning nine domains with 80+ step executors. A workflow can park on something the system cannot hurry — a driver accepting a trip, a KYC check clearing, an approval landing — and sit in `WAITING` for as long as it takes. Another process picks it up and resumes from the exact step it stopped at.

When a step fails, completed steps are compensated in reverse order. The engine keeps the instance state itself, so a restart mid-flight loses nothing.

</details>

<details>
<summary><b>Polyglot persistence</b> — eight storage engines, each where it earns its place</summary>

<br>

| Engine | Carries |
|---|---|
| PostgreSQL | transactional core, via pgx behind PgBouncer |
| MySQL | wallet balances — GTID replication, ProxySQL routing |
| ScyllaDB | timelines and feeds |
| ClickHouse | audit trail and risk events |
| Redis | GEO queries, pub/sub, cache, streams — split by workload |
| OpenSearch | catalog and chat search |
| MinIO | object storage |
| NATS | service-to-service events |

One service, one database. No cross-service joins.

</details>

<details>
<summary><b>Payment switching</b> — ISO 8583 over TCP</summary>

<br>

On the switching side I've worked on QRIS MPM for a national payment switching network: MPAN inquiry, payment credit, check status, refund and reversal, carried over a service bus that speaks ISO 8583, gRPC and HTTP from one core.

The transport runs on Netty with custom frame codecs and selectable epoll / io_uring transports, holding host links open through drops with echo keep-alive and health-checked failover. Messages dispatch through a routing trie rather than linear matching, so new message types are declared instead of hand-wired.

</details>

---

### GitHub

<p align="center">
  <img height="165" alt="stats" src="https://github-readme-stats.vercel.app/api?username=ahmadss&show_icons=true&hide_border=true&include_all_commits=true&theme=graywhite&title_color=14615E&icon_color=14615E">
  <img height="165" alt="languages" src="https://github-readme-stats.vercel.app/api/top-langs/?username=ahmadss&layout=compact&hide_border=true&langs_count=8&theme=graywhite&title_color=14615E">
</p>

<sub>Most of my recent work lives in private repositories — the public ones here are older. The architecture guide above is the best window into what I build today.</sub>

---

<p align="center">
  <sub>Open to senior backend engineering roles · <a href="mailto:saifuddinahmad12@gmail.com">saifuddinahmad12@gmail.com</a></sub>
</p>
