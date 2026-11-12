# Plugin workflow templates

A collection of copyable GitHub Actions build templates for Minecraft Bedrock
server plugins, maintained by BedrockNexus and community contributors.

| Server software | Builder | PHP | Template |
| --- | --- | --- | --- |
| Axolotl-PM 5 | AxolotlBucketLabs DevTools `4.0.3` | 8.4 | [axolotl.yml](templates/axolotl.yml) |

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

The Axolotl template gets libraries from Composer. Declare them in
`composer.json` and commit `composer.lock`, which pins the versions a build
bundles. Plugins without runtime libraries build without a lockfile. Each library
must be a supported Composer virion; see the upstream
[dependency guide](https://github.com/AxolotlBucketLabs/DevTools/blob/106547e8b142a3f6a65a4b3c66d1ace477e56f10/docs/dependencies.md).

The template no longer reads libraries from a committed `virions/` folder. Before
updating an installed workflow, move those libraries to Composer. If `.poggit.yml`
lists them too, set `import-poggit-libraries: false` in `devtools.yml`.

This Axolotl template does not establish PMMP compatibility.

The template passed workflow linting and Hub's template validator. Hosted
Axolotl builds and actual server behavior still need verification.

## Contribute

Submit a pull request to improve a template or add support for another server
software. See [CONTRIBUTING.md](CONTRIBUTING.md).

MIT licensed. Referenced tools retain their own licenses.
