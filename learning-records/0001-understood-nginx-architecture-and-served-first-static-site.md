# Learning Record 0001: Understood nginx architecture and served first static site

## Date
2026-06-13

## What was learned
- nginx uses an event-driven, non-blocking architecture with one master process and multiple worker processes
- This is fundamentally different from Apache's process/thread-per-connection model
- Configuration uses C-style syntax with nested contexts: `main → events/http → server → location`
- Directives end with `;`, block directives use `{ }`
- nginx does not support .htaccess — all config is centralized
- `root` appends the full URI to the filesystem path; `alias` replaces the location prefix
- Location matching order: exact match > prefix with `^~` > regex > plain prefix (longest wins)
- nginx can be controlled with signals: `stop`, `quit`, `reload`, `reopen`
- `reload` validates config syntax first, then does zero-downtime restart

## Skills acquired
- Starting/stopping nginx with `nginx -s quit`, `nginx -s stop`, `nginx -s reload`
- Writing a minimal `nginx.conf` with `events {}`, `http { server { location { root ... } } }`
- Serving static files from a custom directory on a custom port
- Testing with `curl http://localhost:8080/`

## Questions / confusion
- None yet — the core concepts map well to prior knowledge of event loops (Node.js) and web servers

## Next steps
- Reverse proxying: route traffic from nginx to a backend application
- SSL/TLS termination
- Multiple server blocks with `server_name`

## Related resources
- https://nginx.org/en/docs/beginners_guide.html
- https://aosabook.org/en/v2/nginx.html
