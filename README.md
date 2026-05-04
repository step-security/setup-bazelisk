[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# setup-bazelisk v3
Set up your GitHub Actions workflow with a specific version of Bazelisk

Note that GitHub Actions includes Bazelisk by default as of <https://github.com/actions/virtual-environments/pull/490> so this setup is not necessary unless you want to customize the Bazelisk version, or are running Bazel inside a container.

This action sets up Bazelisk for use in actions by:

- optionally downloading and caching a version of Bazelisk by version and adding to PATH
- setting up cache for downloaded Bazel versions

# Usage

See [action.yml](action.yml)

Basic:
```yaml
steps:
- uses: actions/checkout@v6
- uses: step-security/setup-bazelisk@v3
- name: Mount bazel cache  # Optional
  uses: actions/cache@v5
  with:
    path: "~/.cache/bazel"
    key: bazel
- run: bazel build //...
```

# Known issues on Windows
* This action doesn't work with PowerShell. Make sure to have `shell: bash` in your `run:` steps.
* Windows removes one of the slashes (`/`) when two are present (`bazel test //tests/...` becomes `bazel test /tests/...` and fails). 
  As a workaround, don't have any prefix `//`. Since all runs start at WORKSPACE dir, it should work all the same.

Full workaround example on windows:
```yaml
- name: Run tests
  run: bazel test tests/...
  shell: bash
```

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
