# Plugin workflow templates

A collection of copyable GitHub Actions build templates for Minecraft Bedrock
server plugins, maintained by BedrockNexus and community contributors.

| Server software | Builder | PHP | Template |
| --- | --- | --- | --- |
| PocketMine-MP 5 | BedrockNexus Pharynx `0.4.1-bedrocknexus.1` | 8.2 | [pmmp.yml](templates/pmmp.yml) |
| Axolotl-PM 5 | NhanAZ DevTools `2.0.1` | 8.4 | [axolotl.yml](templates/axolotl.yml) |

## Use a template

1. Choose the template for your server software.
2. Replace `{{package_name}}` with your plugin's file basename, such as `MyPlugin`.
3. Copy the file into your plugin repository at
   `.github/workflows/bedrocknexus-publish.yml`.
4. Push and download `plugin-package` from the completed build's Artifacts section.

Each template contains the complete workflow. Builds run in the plugin's own
repository. This repository is the official template list used by Hub.

[templates/index.json](templates/index.json) maps stable template keys to server
software slugs, display names and YAML paths. Hub refreshes this list and its
templates from one Git commit every 15 minutes; administrators can also use
**Refresh catalog**. Template content is maintained here through pull requests.
Convex retains a read-only cache for reactive queries and the last good catalog
if GitHub is unavailable.

Keep `{{package_name}}` intact in this repository: the app replaces it when
installing the selected template. Each installation records its source commit
and path. Updating this list changes future installs and explicit updates;
workflows already installed in plugin repositories keep their recorded version.
Installing or editing a file manually does not automatically make it eligible
for Hub's managed build-selection gate.

## Build and artifact conventions

- Templates expect `plugin.yml` and `src/` at the repository root.
- Upload one artifact named `plugin-package`, containing only the plugin file.
  Keep metadata, logs and additional files in separate artifacts.
- Use read-only repository permissions, hosted runners and pinned build tools.
- Builds produce artifacts; BedrockNexus handles moderation and approved release
  publication separately.

The Axolotl template uses DevTools' default local virion handling. Its optional
Composer preparation is disabled; dependency-heavy projects may need an adapted
template. See the upstream
[dependency guide](https://github.com/NhanAZ/DevTools/blob/5c68bdc7440e962c69f69317d96374315d25d645/docs/dependencies.md).
This Axolotl template does not establish PMMP compatibility.

The initial templates passed workflow linting and Hub's template validator.
The Pharynx release also built a minimal fixture locally with PHP 8.2. Hosted
Axolotl builds and actual server behavior still need verification.

## Contribute

Submit a pull request to improve a template or add support for another server
software. See [CONTRIBUTING.md](CONTRIBUTING.md).

MIT licensed. Referenced tools retain their own licenses.
