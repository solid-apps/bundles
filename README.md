# solid-apps/bundles

Curated bundles of Solid apps, served as JSON-LD docs. Consumed by:

- **`jss install --bundle <name>`** — installs every app in the bundle into your running pod
- **`jspod install --bundle <name>`** *(once jspod delegates to JSS)* — same
- **`nosdav-server install --bundle <name>`** *(once nosdav delegates to JSS)* — same

The bundle URL resolves `jss install --bundle <name>` → `https://raw.githubusercontent.com/solid-apps/bundles/main/<name>.jsonld`.

## Bundles

| Name | Apps | Use |
|---|---|---|
| **`starter`** | chrome, vellum, pdf, alarm | Minimal pleasant first-run |
| **`all`** | chrome, vellum, win98, pdf, hub, alarm, playlist | Everything in solid-apps (except pilot, which jspod bundles by default) |
| **`media`** | playlist, pdf | Media stack — audio + PDF |
| **`productivity`** | vellum, hub, win98 | Docs + workspace + retro shell |
| **`agentic`** | charlie, taskify, vellum, forum, chrome | Run agents on your pod — chat UI, dashboard, SKILL.md editor, record-of-work, windowing. Pairs with `jss start --idp --mcp`. |

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
