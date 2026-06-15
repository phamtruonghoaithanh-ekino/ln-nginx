# Learning Record 0003: Load balancing with upstreams

## Date
2026-06-13

## What was learned
- `upstream` blocks define named groups of backend servers inside `http { }`
- Five load balancing methods: round-robin (default), `least_conn`, `ip_hash`, `hash`, `random`
- Server parameters control behavior: `weight`, `max_fails`, `fail_timeout`, `backup`, `down`
- Passive health checks: nginx tracks failures in a `fail_timeout` window; if `max_fails` is exceeded the server is marked down for `fail_timeout` seconds
- `proxy_pass http://upstream_name` references the upstream group
- Weighted distribution: a server with `weight=3` gets 3x the requests in round-robin

## Skills acquired
- Setting up multiple backend servers and an upstream group
- Switching between load balancing methods
- Testing round-robin behavior with curl
- Using `backup` servers for failover
- Simulating backend failure and observing health check recovery

## Questions / confusion
- How does `ip_hash` interact with clients behind a NAT (all appear as same IP)?
  - Answer: In practice, use cookies or `sticky` for session persistence beyond NAT
- Active health checks (regular probes without real traffic) are only in nginx Plus

## Next steps
- SSL/TLS termination
- Serving multiple sites with server blocks
- nginx variables and advanced config patterns

## Related resources
- https://nginx.org/en/docs/http/load_balancing.html
- https://nginx.org/en/docs/http/ngx_http_upstream_module.html
