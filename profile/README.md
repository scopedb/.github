<p align="center">
  <a href="https://www.scopedb.io">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="/profile/banner-dark.png">
      <source media="(prefers-color-scheme: light)" srcset="/profile/banner-light.png">
      <img alt="ScopeDB — Turn live events into real-time insights." src="/profile/banner-light.png" width="100%">
    </picture>
  </a>
</p>

<p align="center">
  <a href="https://www.scopedb.io"><strong>Website</strong></a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://console.scopedb.cloud/?signup"><strong>Start Free</strong></a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://www.scopedb.io/agent"><strong>Start with Your Agent</strong></a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://www.scopedb.io/docs"><strong>Docs</strong></a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://www.scopedb.io/blog"><strong>Blog</strong></a>
</p>

---

Write structured columns alongside evolving `object` payloads directly from your application, OpenTelemetry collector, or AI agent — without an intermediate ETL pipeline — and investigate live events in real time with **[ScopeQL](https://www.scopedb.io/docs/reference)**:

```sql
FROM payment_requests
WHERE time >= NOW() - 'PT15m'::interval
GROUP BY release, attributes['gateway']::string AS gateway
  AGGREGATE count() AS requests, sum(if(status >= 500, 1, 0)) AS failures
SELECT release, gateway, requests, failures,
  round(10000.0 * failures / requests) / 100.0 AS failure_pct
ORDER BY failure_pct DESC
```

We maintain the following open-source projects around ScopeDB:

- **[scopedb-skills](https://github.com/scopedb/scopedb-skills)** & **[scopedb-cli](https://github.com/scopedb/scopedb-cli)** — Connect your AI agent ([Claude Code, Codex, Cursor](https://www.scopedb.io/agent)) or terminal (`scope`) to inspect schemas, run ScopeQL queries, and generate portable HTML reports.
- **[scopedb-js](https://github.com/scopedb/scopedb-js)** · **[goscopedb](https://github.com/scopedb/goscopedb)** · **[scopedb-client](https://github.com/scopedb/scopedb-client)** — Official TypeScript/JavaScript, Go, and Rust SDKs for high-concurrency event ingestion and querying.
- **[Telescope](https://github.com/scopedb/telescope)** — OpenTelemetry Collector distribution that sinks OTLP logs, traces, and metrics directly into ScopeDB tables.
- **[ScopeView](https://github.com/scopedb/scopeview)** — Zero-dependency Canvas chart library and CLI for time-series metrics, trace waterfalls, and offline interactive charts.
