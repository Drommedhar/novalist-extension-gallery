# Contributing to the Novalist Extension Gallery

Thank you for contributing an extension to the Novalist community!

## Submission Process

1. **Fork** this repository.
2. **Add** your extension entry to `gallery.json` (see schema below).
3. **Open a pull request** with a brief description of your extension.
4. A maintainer will review your submission — once approved and merged, your extension appears in the in-app store.

## `gallery.json` Entry Schema

Add a single object to the array in `gallery.json`:

```jsonc
{
  "id": "com.yourname.extensionname",
  "name": "Extension Display Name",
  "description": "A short description of what the extension does.",
  "author": "Your Name",
  "repo": "youruser/your-extension-repo",
  "tags": ["tag1", "tag2"]
}
```

| Field         | Required | Description |
|---------------|----------|-------------|
| `id`          | Yes      | Reverse-domain identifier. Must match the `id` in your extension's `extension.json`. Must be unique across all gallery entries. |
| `name`        | Yes      | Human-readable display name. |
| `description` | Yes      | Short description (one or two sentences). |
| `author`      | Yes      | Author or organization name. |
| `repo`        | Yes      | GitHub repository in `owner/repo` format. Must be public. |
| `tags`        | No       | Array of free-form tags for search/filtering. |

> **Note:** Extension icons are defined in the extension's own `extension.json` manifest (via the `icon` field), not in the gallery entry. This lets developers update their icon without a gallery PR.

## Review Checklist

Before submitting, make sure:

- [ ] Your extension's GitHub repository is **public**.
- [ ] Your repo has at least **one GitHub release** with a ZIP asset named `{id}.zip`.
- [ ] The ZIP contains `extension.json` at the root with a valid `id`, `version`, `minHostVersion`, and `entryAssembly`.
- [ ] The `id` in `gallery.json` matches the `id` in your `extension.json`.
- [ ] The `version` in `extension.json` matches the version in the release tag.
- [ ] Your extension does **not** contain malicious code, telemetry without disclosure, or license violations.
- [ ] Your `gallery.json` entry is valid JSON (no trailing commas, proper quoting).

## Release Requirements

Each release on your GitHub repo must follow the [release convention](README.md#release-convention):

- Tag format: `v{major}.{minor}.{patch}` (e.g. `v1.0.0`), or `{slug}-v{version}`
  (e.g. `toolkit-v1.2.0`) when one repository holds several extensions
- Attach a ZIP asset: `{extension-id}.zip`
- ZIP must be flat (no wrapper folder) and contain `extension.json` + the entry assembly DLL
- Set `minHostVersion` (and optionally `maxHostVersion`) for compatibility

## Several Extensions in One Repository

Nothing here assumes one extension per repository. The store matches a release
by an asset named `{id}.zip` and installs into a folder named after the id, so
several can share a repository and a release history.

When they do, name the extension in the tag — `toolkit-v1.2.0` rather than
`v1.2.0` — and attach two more assets beside the ZIP:

- `{id}.extension.json` — the manifest, so compatibility and the icon can be
  checked before anything is downloaded.
- `{id}.README.md` — this extension's store page.

Both are optional. Without them the store falls back to `extension.json` and the
README at the repository root, which is right for a repository with one
extension in it. A repository with four has no manifest at its root, and its
README describes the repository rather than any one of them — so all four
listings would show the same page and none would have its compatibility checked
in advance.

## Updating Your Extension

To publish updates, simply create a new release on your GitHub repo. The Novalist store automatically picks up the latest compatible release — no changes to `gallery.json` are needed.

To update your gallery entry metadata (description, tags, icon), submit a PR with the changes.

## Removing Your Extension

To remove your extension from the gallery, submit a PR removing your entry from `gallery.json`.
