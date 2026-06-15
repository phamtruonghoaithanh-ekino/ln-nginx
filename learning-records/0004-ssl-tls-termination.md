# Learning Record 0004: SSL/TLS termination with nginx

## Date
2026-06-13

## What was learned
- SSL/TLS termination means nginx handles HTTPS and proxies plain HTTP to the backend
- `listen 443 ssl;` enables TLS on a port (the `ssl` parameter on `listen` is the modern way)
- `ssl_certificate` + `ssl_certificate_key` point to PEM files for the certificate chain and private key
- `ssl_protocols` and `ssl_ciphers` control which TLS versions/ciphers are accepted
- `ssl_session_cache shared:SSL:10m` stores ~40,000 TLS sessions in shared memory across workers
- HTTP → HTTPS redirect: `return 301 https://$host$request_uri;`
- Self-signed certs work for local dev; Let's Encrypt (certbot) for production
- When proxying, set `X-Forwarded-Proto: https` so the backend knows the scheme

## Skills acquired
- Generating a self-signed cert with `openssl req -x509 ...`
- Configuring an HTTPS server block with TLS termination
- Setting up HTTP → HTTPS redirect
- Testing with `curl -k` (skip verification) and `curl -v` (inspect TLS handshake)
- Combining SSL termination with reverse proxy to a backend

## Questions / confusion
- What is OCSP stapling? (nails down: it lets nginx cache the CA's certificate revocation check — improves performance and privacy)
- How does certbot auto-renewal work with nginx? (covers in a later lesson or as a reference)

## Next steps
- Multiple server blocks (name-based virtual hosting)
- nginx built-in variables and `map`/`geo` modules
- gzip compression, caching, and logging

## Related resources
- https://nginx.org/en/docs/http/configuring_https_servers.html
- https://nginx.org/en/docs/http/ngx_http_ssl_module.html
- Let's Encrypt: https://letsencrypt.org
