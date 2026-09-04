# unraid-templates

A personal [Unraid Community Applications](https://forums.unraid.net/topic/38582-plug-in-community-applications/)
Template Repository, shared between a couple of personal Unraid servers so
they install/update the same container definitions from one place instead of
maintaining separate local copies.

Currently covers a small MCP (Model Context Protocol) server stack. More
templates may be added over time as other containers get migrated off ad-hoc
`docker run`/`docker compose` setups.

## Using this repo

**Register it once per server** (Unraid webUI → **Apps** tab → gear icon
→ **Template Repositories** → paste):

```
https://github.com/luck-y13/unraid-templates
```

After that, every template in [`templates/`](templates/) is installable from
the **Apps** tab (search by name) or via **Docker → Add Container → Template**
dropdown, same as any Community Applications template. Updates to a template
here are picked up the next time you install/reinstall it — editing an
already-running container's settings still happens locally on that server
(Docker tab → click the icon → Edit) and does not write back here.

## Notes for anyone (including future me) installing one of these

- Every template leaves `ExtraParams` set to a placeholder
  (`-p YOUR_TAILSCALE_IP:<port>:<port>`) — **edit this to your own Tailscale
  IP** before applying. This is how these containers stay reachable only over
  Tailscale and never get exposed on the LAN or internet interfaces. Don't
  also add a Port mapping in the basic view, or you'll double-map the port.
- Env vars (tokens, passwords, URLs) always ship blank — fill them in at
  install time. Nothing here is a secret.
- `mcp-adguard` is meant to be installed once per AdGuard Home node (rename
  the container and adjust `ADGUARD_HOST` / `ADGUARD_HTTP_PORT` / `ExtraParams`
  for each one) — see the template's own description for details.

## License

MIT — see [LICENSE](LICENSE).
