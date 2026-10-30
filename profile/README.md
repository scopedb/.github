# ScopeDB

**ScopeDB** is a fully managed, serverless columnar database for event analytics, built in Rust on top of commodity object storage. Applications, OpenTelemetry collectors, and AI agents append business events, operational logs, and high-concurrency traces directly to ScopeDB without an intermediate ETL pipeline, and query them with **ScopeQL**, a composable pipelined query language.

[Website](https://www.scopedb.io/) · [ScopeDB Cloud Console](https://console.scopedb.cloud/) · [Start with your agent](https://www.scopedb.io/agent) · [Documentation](https://www.scopedb.io/docs) · [ScopeQL Reference](https://www.scopedb.io/docs/reference) · [Blog](https://www.scopedb.io/blog) · [llms.txt](https://www.scopedb.io/llms.txt)

## Key Capabilities

- **Direct ingestion without ETL**: Append structured and semi-structured rows directly from application backends or OpenTelemetry pipelines and query committed data immediately.
- **Schema on the fly**: Combine typed columns (`timestamp`, `string`, `int`, `float`, `boolean`) for stable keys with flexible `object` and `array` columns for evolving nested payloads, backed by point, range, search, and materialized expression indexes.
- **Pipelined ScopeQL**: Express filtering, derived columns, deduplication (`DISTINCT ON`), grouping (`GROUP BY ... AGGREGATE`), window calculations (`WINDOW ... AGGREGATE`), and joins in a linear top-to-bottom data-flow pipeline.
- **Elastic serverless architecture**: Keep durable event history in shared object storage while isolated, stateless ingestion and query compute groups scale up with demand and release resources after bursts.
- **Agent-native investigation**: Connect Claude Code, Codex, or any terminal-capable AI agent via the official [ScopeDB Agent Skill](https://github.com/scopedb/scopedb-skills) and CLI (`scope`) to inspect tables, run read-only ScopeQL queries, maintain reusable analysis context, and export offline interactive charts.

## ScopeQL at a Glance

```scopeql
CREATE TABLE app.events (
    event_time timestamp,
    service_version string,
    trace_id string,
    span_id string,
    payload object
);

FROM app.events
WHERE event_time >= NOW() - 'PT1h'::interval
  AND try(payload["http"]["status"]::int) >= 500
DISTINCT ON trace_id, span_id BY event_time DESC
SELECT service_version, try(payload["error"]["code"]::string) AS error_code
GROUP BY service_version, error_code
  AGGREGATE count() AS failed_requests
ORDER BY failed_requests DESC
```

## Official SDKs, CLI, and Ecosystem

| Repository                                                           | Role                   | Description                                                                                                                       |
| -------------------------------------------------------------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [`scopedb/scopedb-skills`](https://github.com/scopedb/scopedb-skills) | Agent Skill            | Official Agent Skill (`agentskills.io`) to connect workspaces, write ScopeQL, retain domain context, and export offline charts.   |
| [`scopedb/scopedb-cli`](https://github.com/scopedb/scopedb-cli)       | Command-Line Interface | `scope` CLI for interactive and scripted ScopeQL queries, declarative Catalog workflows, and workspace authentication.            |
| [`scopedb/scopedb-js`](https://github.com/scopedb/scopedb-js)         | JavaScript / TS SDK    | Official client (`npm install scopedb`) for Node.js, Bun, and Cloudflare Workers.                                                 |
| [`scopedb/goscopedb`](https://github.com/scopedb/goscopedb)           | Go SDK                 | Official Go client (`github.com/scopedb/goscopedb`) supporting `AppendStream`, statements, and REST Catalog operations.           |
| [`scopedb/scopedb-client`](https://github.com/scopedb/scopedb-client) | Rust SDK               | Official async Rust client (`scopedb-client` on crates.io) for querying and streaming row appends.                                |
| [`scopedb/telescope`](https://github.com/scopedb/telescope)           | OpenTelemetry          | OpenTelemetry Collector distribution that maps OTLP logs, traces, and metrics directly into ScopeDB tables.                       |
| [`scopedb/scopeview`](https://github.com/scopedb/scopeview)           | Visualization          | Zero-dependency Canvas chart library and CLI (`@scopedb/scopeview`) for metrics, traces, and portable offline HTML reports.       |
| [`scopedb/scopedb-site`](https://github.com/scopedb/scopedb-site)     | Website & Docs         | Source for [scopedb.io](https://www.scopedb.io/) and [`/docs`](https://www.scopedb.io/docs), including `.md` documentation routes. |
