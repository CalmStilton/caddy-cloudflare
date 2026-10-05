# caddy-cloudflare

Stock [Caddy 2](https://caddyserver.com) with one extra module,
[`caddy-dns/cloudflare`](https://github.com/caddy-dns/cloudflare), so Caddy
can get certificates via the ACME DNS-01 challenge on Cloudflare-hosted
domains. This is needed for wildcard certificates and for hosts that aren't
reachable from the internet.

```
ghcr.io/calmstilton/caddy-cloudflare:latest
ghcr.io/calmstilton/caddy-cloudflare:<caddy version>   # e.g. 2.11.2
```

## How it stays current

The image is built by GitHub Actions:

- **Daily:** rebuilds only if the official `caddy:2` image digest has changed.
- **Mondays:** a forced rebuild, which picks up new versions of the
  Cloudflare module.
- **On push to `main`** and on manual dispatch.

It only tracks Caddy **2.x**. A future major version needs a deliberate
Dockerfile change.

## Usage

```caddyfile
*.example.com {
    tls {
        dns cloudflare {env.CF_API_TOKEN}
    }
}
```

Use a Cloudflare API token scoped to **Zone → DNS → Edit** on the one zone
only.
