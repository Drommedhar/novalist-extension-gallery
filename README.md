# Novalist Extension Gallery

This repository contains the official index of community extensions for [Novalist](https://github.com/Drommedhar/novalist-official).

Novalist fetches [`gallery.json`](gallery.json) to populate the in-app extension store. Each entry points to a GitHub repository where the extension is developed and released.

## For Users

Browse and install extensions directly from the **Extensions → Browse Store** tab inside Novalist. No manual setup required.

## For Extension Authors

Want to publish your extension? See [CONTRIBUTING.md](CONTRIBUTING.md) for the submission process and release requirements.

### Quick Overview

1. Develop your extension using the [Novalist SDK](https://github.com/Drommedhar/novalist-official/tree/main/Novalist.Sdk).
2. Publish releases on your GitHub repo as ZIP assets (see release convention below).
3. Submit a PR adding your extension to `gallery.json`.

### `gallery.json` Entry Format

```jsonc
{
  "id": "com.example.myextension",        // Must match extension.json "id"
  "name": "My Extension",                 // Display name
  "description": "Short description.",     // Shown in the browse list
  "author": "Your Name",                  // Author name
  "repo": "youruser/novalist-myext",      // GitHub repo (owner/repo)
  "tags": ["productivity", "writing"]     // Free-form tags for search/filter
}
```

### Release Convention

Each GitHub release on your extension repo must:

- **Tag** — Use semantic versioning: `v1.0.0`, `v1.2.3`, etc.
- **Asset** — Attach a ZIP file named `{extension-id}.zip` (e.g. `com.example.myextension.zip`).
- **ZIP contents** — Flat structure (no wrapper folder):
  ```
  com.example.myextension.zip
  ├── extension.json       # Required
  ├── MyExtension.dll      # Required (entry assembly)
  ├── Locales/             # Optional
  └── ...
  ```
- **extension.json** — Must include `version`, `minHostVersion`, and optionally `maxHostVersion` for compatibility checking. Can include an optional `icon` URL for the store listing.
- **Pre-releases** — GitHub releases marked as pre-release are ignored by the store.

For full documentation, see the [Extension Developer Guide](https://github.com/Drommedhar/novalist-official/blob/main/docs/extension-guide.md).