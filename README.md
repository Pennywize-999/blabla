# Minimal Exploit Server (Burp-style workflow)

This repository contains a lightweight Python exploit-server-like utility for **authorized security testing labs**.

## Features

- Serves a configurable exploit response at `/`
- Stores request captures for inspection at `/admin/logs`
- Serves payload files from `payloads/` at `/payload/<filename>`
- Lets you update the root exploit body via `POST /admin/set-exploit` with an API token

## Run

```bash
python3 exploit_server.py --host 0.0.0.0 --port 8000
```

Optional flags:

- `--payload-dir payloads`
- `--api-token <token>` (or env var `EXPLOIT_SERVER_TOKEN`)

## Example usage

1. Start server.
2. Visit `http://localhost:8000/` (victim/test browser in your lab).
3. Update exploit body:

```bash
curl -X POST http://localhost:8000/admin/set-exploit \
  -H 'Content-Type: application/json' \
  -H 'X-API-Token: <TOKEN>' \
  -d '{"body":"<script src=\"/payload/hello.js\"></script>"}'
```

4. Review captures at:

```bash
curl http://localhost:8000/admin/logs
```

## Notes

Use only on systems you own or are explicitly authorized to test.
