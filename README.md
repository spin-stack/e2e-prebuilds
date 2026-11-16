# e2e-prebuilds

Spinbox's end-to-end tests prebuild this repository. Each branch is one outcome of a build:

- `main`: the create task runs and the build is ready. Its workflow sets a remote whose password
  is a reference to a secret (`${FORKS_TOKEN}`), which the credential scan must not refuse.
- `create-fails`: the create task exits 1, and the build fails with what it wrote.
- `credential`: a file holds a password in a URL, and the scan of the build's disk refuses it.
- `spin-yaml-invalid`: the .spin.yaml is of version 2, which the guest refuses before any task runs.

Nothing here is a real credential. Do not change a branch without changing the test that reads it
(spin-stack/spin, `internal/e2e/prebuild_test.go`).
