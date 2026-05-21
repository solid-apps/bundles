# solid-apps/bundles

Curated bundles of Solid apps, served as JSON-LD docs. Consumed by:

- **`jss install --bundle <name>`** — installs every app in the bundle into your running pod
- **`jspod install --bundle <name>`** *(once jspod delegates to JSS)* — same
- **`nosdav-server install --bundle <name>`** *(once nosdav delegates to JSS)* — same

The bundle URL resolves `jss install --bundle <name>` → `https://raw.githubusercontent.com/solid-apps/bundles/main/<name>.jsonld`.

## Bundles

| Name | Apps | Use |
|---|---|---|
| **`default`** | home, store, explorer, git, vellum, plume, chat, plaza, timeline, charlie, chrome | Auto-installed on first run of `jspod`. Initially identical to `jspod`; kept separate so it can drift (e.g. shrink for faster first-run latency) without changing what `jspod` recommends |
| **`starter`** | home, store, explorer, chrome, vellum, plume, pdf, alarm, chat, plaza | Minimal pleasant first-run |
| **`jspod`** | home, store, explorer, git, vellum, plume, chat, plaza, timeline, charlie, chrome | The canonical jspod set — what jspod recommends every Solid pod should have on top of pilot |
| **`all`** | home, store, explorer, chrome, vellum, plume, chat, plaza, timeline, win98, pdf, hub, alarm, playlist | Everything in solid-apps (except pilot, which jspod bundles by default) |
| **`media`** | explorer, playlist, pdf | File browser + media stack — audio + PDF |
| **`productivity`** | home, store, explorer, vellum, plume, hub, win98, chat, plaza, mindstr, transcribe | File browser + docs + blog + workspace + retro shell + team chat + group chat + mind mapping + speech-to-text |
| **`agentic`** | home, store, charlie, chat, plaza, taskify, vellum, forum, explorer, chrome | Run agents on your pod — DM + group chat, dashboard, SKILL.md editor, record-of-work, file browser, windowing. Pairs with `jss start --idp --mcp`. |
| **`teams`** | home, store, plaza, chat, vellum, plume, taskify, explorer, hub, chrome | Run a team on your own pods — Slack-shaped group chat, DMs, shared docs, team blog, task tracking, files. Federated by default, no central platform. |

## Bundle format

JSON-LD `schema:ItemList`:

```json
{
  "@context": { "schema": "https://schema.org/", "app": "urn:jss:app:" },
  "@id": "#bundle",
  "@type": "schema:ItemList",
  "schema:name": "Display name",
  "schema:description": "One-line summary",
  "schema:itemListElement": [
    "chrome",
    "vellum",
    { "app:spec": "litecut/litecut.github.io=litecut", "app:label": "Litecut" }
  ]
}
```

Each item is either:

- A bare string — any spec `jss install` accepts (`chrome`, `org/repo`, `org/repo#ref`, `org/repo=rename`, full URL)
- An object — required `app:spec`, optional `app:label` / `app:description` for UI tooling that displays bundles before installing

## Adding a bundle

PR with a new `<name>.jsonld` here. Keep bundles focused (3–7 apps); broad "everything" bundles work but are less useful than themed sets.

## Custom bundles

You can host your own bundles anywhere — a pod, a GitHub repo, a static host — and point `jss install` at the URL:

```bash
jss install --bundle https://my.pod/bundles/dev.jsonld
jss install --bundle ./my-stack.jsonld
```

Personal bundles live in your own pod. Curated cross-app collections live here.

## License

CC0-1.0 (bundles are just lists of names; no creative content to copyright).
