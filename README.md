# pso-protobuf-common

Shared protobuf definitions for PSO Network gRPC services, published to the
Buf Schema Registry as
[`buf.build/psonet/pso-protobuf-common`](https://buf.build/psonet/pso-protobuf-common).

Everything lives in package `net.pso.common.v1`:

| File | Contents |
|------|----------|
| `currency.proto` | `Currency` — ISO 4217 currency codes (numeric values are the ISO numbers) |
| `money.proto` | `Money` — amount as `units` + `atto` (10^-18) in a `Currency` |
| `errors.proto` | `OperationError` metadata, `GrpcStatusCode`, and the `server_error` / `method_errors` options used to annotate typed error details |

## Using it

Add the module to your service's `buf.yaml` and pin a release label:

```yaml
version: v2
modules:
  - path: proto
deps:
  - buf.build/psonet/pso-protobuf-common:v0.1.0
```

Then `buf dep update` and import as usual:

```proto
import "net/pso/common/v1/money.proto";
```

The module is private on the BSR: `buf registry login` (or `BUF_TOKEN`) is
required to resolve it. Generated SDKs for Go, Java, Kotlin and others are
available from the BSR module page.

## Contributing

- Commits follow [Conventional Commits](https://www.conventionalcommits.org);
  `cog check` validates them.
- CI runs `buf format`, `buf lint` (STANDARD) and `buf breaking` (FILE) on
  every PR. Breaking changes require a new package version
  (`net.pso.common.v2`), not edits to `v1`.
- On merge to `main`, [cocogitto](https://github.com/cocogitto/cocogitto)
  bumps the version from the commit history, updates `CHANGELOG.md`, tags
  `vX.Y.Z`, and CI pushes the module to the BSR labelled with both `main`
  and the new tag.

Local checks:

```sh
buf format -d && buf lint && buf breaking --against '.git#branch=main'
cog check
```

## License

GPL-3.0, see [LICENSE](LICENSE).
