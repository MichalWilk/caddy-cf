# caddy-cf

[Caddy](https://caddyserver.com/) with the [Cloudflare DNS](https://github.com/caddy-dns/cloudflare) plugin, built automatically via GitHub Actions.

## Image

```
ghcr.io/michalwilk/caddy-cf:latest
```

Tags:
- `latest` - most recent build
- `<version>-alpine` (e.g. `2.11.2-alpine`) - pinned to a specific Caddy version

## Usage

```yaml
services:
  caddy:
    image: ghcr.io/michalwilk/caddy-cf:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config

volumes:
  caddy_data:
  caddy_config:
```

Caddyfile example with Cloudflare DNS challenge:

```
example.com {
  tls {
    dns cloudflare {env.CF_API_TOKEN}
  }
  respond "Hello"
}
```

## Auto-updates

The GitHub Actions workflow checks daily for new upstream Caddy releases and rebuilds the image only when a new version is detected.
