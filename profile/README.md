<div align="center">
  <br />
  <a href="https://www.scopedb.io">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="/profile/scopedb-logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="/profile/scopedb-logo-black.svg">
      <img alt="ScopeDB" src="/profile/scopedb-logo-black.svg" width="260">
    </picture>
  </a>
  <p><strong>Turn live events into real-time insights.</strong></p>
  <p>
    <a href="https://www.scopedb.io">Website</a>
    <span>&nbsp;·&nbsp;</span>
    <a href="https://console.scopedb.cloud">Cloud Console</a>
    <span>&nbsp;·&nbsp;</span>
    <a href="https://www.scopedb.io/agent">Start with Your Agent</a>
    <span>&nbsp;·&nbsp;</span>
    <a href="https://www.scopedb.io/docs">Docs</a>
    <span>&nbsp;·&nbsp;</span>
    <a href="https://www.scopedb.io/blog">Blog</a>
  </p>
  <hr />
</div>

ScopeDB is a serverless database built on object storage to store, search, and analyze live events in real time. Write structured columns and evolving `object` payloads directly from application backends, OpenTelemetry collectors, or AI agents without ETL, and query them with [ScopeQL](https://www.scopedb.io/docs/reference):

```sql
FROM payment_requests
WHERE time >= NOW() - 'PT15m'::interval
GROUP BY release, attributes['gateway']::string AS gateway
  AGGREGATE count() AS requests, sum(if(status >= 500, 1, 0)) AS failures
SELECT release, gateway, requests, failures,
  round(10000.0 * failures / requests) / 100.0 AS failure_pct
ORDER BY failure_pct DESC
```

- **CLI & Agent**: [`scopedb-cli`](https://github.com/scopedb/scopedb-cli) (`scope`) · [`scopedb-skills`](https://github.com/scopedb/scopedb-skills)
- **Client SDKs**: [JavaScript / TypeScript](https://github.com/scopedb/scopedb-js) · [Go](https://github.com/scopedb/goscopedb) · [Rust](https://github.com/scopedb/scopedb-client)
- **Ecosystem**: [Telescope](https://github.com/scopedb/telescope) (OpenTelemetry Collector) · [ScopeView](https://github.com/scopedb/scopeview) (Charts & Traces)
