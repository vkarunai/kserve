# KServe Fork (vkarunai/kserve)

This is a fork of `kserve/kserve`.
The Go module path is `github.com/kserve/kserve` (same as upstream).

## Build & Test

```bash
# Build all Go binaries
go build ./...

# Build the qpext submodule (separate go.mod)
cd qpext && go build ./...

# Run Go tests (Ginkgo + Gomega)
make test

# Lint
make go-lint

# Generate CRDs and RBAC manifests
make manifests

# Format code
make fmt
```

## Project Structure

```
cmd/             # Go binary entrypoints: manager, agent, router
pkg/             # Core packages: API types, controllers, constants
  constants/     # Shared constants
  controller/    # Kubernetes controllers (InferenceService, InferenceGraph, etc.)
python/          # Python model servers (huggingface, xgb, etc.)
qpext/           # Queue proxy extension (separate Go module)
config/          # Kustomize manifests
  default/       # Base kustomize config
```

## Merge Conflict Resolution Guidelines

When resolving conflicts between upstream and this fork:

1. Accept upstream changes by default — minimize drift from upstream.
2. If this fork has specific customizations (identified by comments, unique functions,
   or non-upstream code paths), preserve them and integrate upstream refactors on top.
3. For `go.mod`: accept upstream versions; keep any fork-specific `replace` directives
   that have explanatory comments.
4. After resolving, verify: `go build ./...`, `cd qpext && go build ./...`, and `grep`
   for leftover conflict markers.
