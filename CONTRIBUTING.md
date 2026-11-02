# Contributing templates

Edit the YAML files directly in `templates/`. For a new server software, add a
complete copyable template, an entry in `templates/index.json`, and a row in the
README with its builder and runtime requirements. The corresponding server
software slug must already exist in Hub.

Keep each index `key` stable: existing plugin selections refer to it. A key must
not be reassigned to another server software. YAML paths must be direct files
under `templates/`, and labels must contain 3–80 characters. Removing an index
entry retires it from new selection/installation after refresh; previously
installed workflows keep their recorded revision.

Keep templates easy to read and adapt. Pin external actions to full commit SHAs,
annotate their versions, and verify downloaded tools against an expected
checksum. Use read-only repository permissions and hosted runners. Keep release
publication and credentials out of the build template.

Preserve `{{package_name}}` for Hub installation and upload exactly one
`plugin-package` artifact containing only the plugin file. Templates intended for
Hub should keep the workflow name `BedrockNexus Publish` and build on branch
pushes. Pull-request builds can help contributors test but cannot be published
through the current Hub build picker.

Validate changes with actionlint, for example:

```sh
actionlint templates/pmmp.yml templates/axolotl.yml
```

Describe the server/API version, dependency behavior and testing in your pull
request. Distinguish workflow syntax checks, successful packaging and actual
server testing. Hub refreshes the published repository catalog automatically;
invalid content leaves its last good catalog available. A template change does
not overwrite previously installed copies.
