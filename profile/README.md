<p align="center">
  <a href="https://www.scopedb.io">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="/profile/banner-dark.png">
      <source media="(prefers-color-scheme: light)" srcset="/profile/banner-light.png">
      <img alt="ScopeDB: Turn live events into real-time insights." src="/profile/banner-light.png" width="100%">
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

Send application events, logs, and traces directly to ScopeDB and query them in real time with [ScopeQL](https://www.scopedb.io/docs/reference):

```sql
FROM payment_requests
WHERE time >= NOW() - 'PT15m'::interval
GROUP BY release, attributes['gateway']::string AS gateway
  AGGREGATE count() AS requests, sum(if(status >= 500, 1, 0)) AS failures
SELECT release, gateway, requests, failures,
  round(10000.0 * failures / requests) / 100.0 AS failure_pct
ORDER BY failure_pct DESC
```

Open-source tools and SDKs:

- [ScopeDB Skill](https://github.com/scopedb/scopedb-skills): Let your AI agent query ScopeDB.
- [ScopeDB CLI](https://github.com/scopedb/scopedb-cli): Run ScopeQL from your terminal.
- [Telescope](https://github.com/scopedb/telescope): Ingest OpenTelemetry logs, traces, and metrics.
- [ScopeView](https://github.com/scopedb/scopeview): Render time-series charts and trace waterfalls.
- Client SDKs for [JavaScript](https://github.com/scopedb/scopedb-js), [Go](https://github.com/scopedb/goscopedb), and [Rust](https://github.com/scopedb/scopedb-client).
