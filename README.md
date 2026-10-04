# go-cli-template

A minimal template for building Go command-line applications with Cobra and structured logging via `slog` + `tint`.

## Features

- Cobra-based CLI entrypoint
- Global `--verbose` / `-v` flag
- Semantic-versioned releases with GoReleaser and GitHub Actions
- Structured logging with `log/slog`
- Colorized terminal log output with `tint`
- Small, easy-to-extend project layout

## Project Structure

```text
.
├── .github/workflows/
│   └── release.yaml
├── cmd/
│   └── root.go
├── scripts/
│   └── tag.sh
├── .goreleaser.yaml
├── main.go
├── mise.toml
├── go.mod
└── go.sum
```

## Requirements

- Go 1.27 or later
- [mise](https://mise.jdx.dev) (optional, for the `build` and `tag` tasks)

## Getting Started

Clone the repository and run the CLI:

```bash
go run .
```

Run with verbose logging enabled:

```bash
go run . --verbose
```

Build a binary:

```bash
mise run build
./dist/go-cli-template --verbose
```

## Release

Versions follow [Semantic Versioning](https://semver.org) as `vX.Y.Z` tags.
Pushing a tag runs `.github/workflows/release.yaml`, which tests and builds
with [GoReleaser](https://goreleaser.com) and publishes archives for Linux,
macOS and Windows (amd64/arm64) with checksums and build provenance
attestations to GitHub Releases. Tag the next version from an up-to-date,
clean `main`:

```bash
mise run tag patch --dry-run   # preview: v1.2.3 -> v1.2.4
mise run tag minor             # tag and push after confirmation (M|m|p also work)
```

Verify a downloaded archive with `gh attestation verify <file> -R yz4230/go-cli-template`.

## What This Template Sets Up

The root command configures a default logger in `PersistentPreRun`:

- standard log level by default
- debug-level logging with `--verbose`
- source locations in log output
- time-only timestamps for readable terminal logs

## Extending the Template

Typical next steps:

1. Add subcommands under `cmd/`
2. Define application-specific flags
3. Replace the module path in `go.mod`, and the binary name in `mise.toml` and this README
4. Add business logic and tests

## Dependencies

- [`github.com/spf13/cobra`](https://github.com/spf13/cobra)
- [`github.com/lmittmann/tint`](https://github.com/lmittmann/tint)

## License

Add a license that matches how you want to share this template.
