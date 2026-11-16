# e2e-prebuilds

Spinbox's end-to-end tests prebuild this repository. Each branch is one outcome of a build:

- `main`: the create task runs and the build is ready. Its workflow sets a remote whose password
  is a reference to a secret (`${FORKS_TOKEN}`), and `docs/settings.example.yaml` commits a password
  in a URL: the credential scan reads only what the build wrote, so neither is refused.
- `create-fails`: the create task exits 1, and the build fails with what it wrote.
- `credential`: the create task writes a password in a URL, and the scan refuses it.
- `spin-yaml-invalid`: the .spin.yaml is of version 2, which the guest refuses before any task runs.

Nothing here is a real credential. Do not change a branch without changing the test that reads it
(spin-stack/spin, `internal/e2e/prebuild_outcomes_test.go`).
