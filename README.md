# stroppy-io/go-sql-driver-mysql

A fork of [go-sql-driver/mysql](https://github.com/go-sql-driver/mysql), kept
for one purpose: running the driver's own integration tests against MySQL
wire-compatible servers in [stroppy](https://github.com/stroppy-io/stroppy)'s
conformity suites. It is not a separate driver: use upstream for anything
else.

| | |
|---|---|
| Upstream | https://github.com/go-sql-driver/mysql |
| Base | tag `v1.10.1`, commit `7ca26e801d130be8be84c1e265be71784f6f70c1` |
| Fork branch | [`conformity/dsn-params-v1.10.1`](https://github.com/stroppy-io/go-sql-driver-mysql/tree/conformity/dsn-params-v1.10.1) |
| Fork commit | [`4b4595fc81d15956183ae216d2b9257e6238c394`](https://github.com/stroppy-io/go-sql-driver-mysql/commit/4b4595fc81d15956183ae216d2b9257e6238c394) |
| Licence | MPL-2.0, as upstream ([LICENSE](LICENSE)). Changed files keep their MPL-2.0 terms and headers. |

This branch (`stroppy`) holds only this README and the licence. The code is
on the fork branch above, which is the upstream tag plus the commits listed
below and nothing else.

## Our changes

Each change is one commit on top of the base tag. The driver itself
(everything that is not a `_test.go` file) is unchanged.

| Commit | Files | What | Why |
|---|---|---|---|
| `4b4595fc` | `driver_test.go` | Adds `MYSQL_TEST_DSN_PARAMS` (`name=value&...`): extra DSN parameters appended to every DSN the tests connect with. Unset, the tests are upstream's. | Some servers need session settings on every connection (a vendor's MySQL-compatibility switch). The driver sends an unknown DSN parameter as a session system variable, so this lets the unchanged tests run with the switch on. No test body or assertion changes. |

To see the full diff against upstream:
`git diff v1.10.1 conformity/dsn-params-v1.10.1`.

## Rebases

A new upstream release gets a new branch, `conformity/<change>-<tag>`, with
the same commits replayed on the new tag. Old branches are kept, so every
pinned commit stays reachable.

| Date | Base | Fork branch | Fork commit | Notes |
|---|---|---|---|---|
| 2026-10-23 | `v1.10.1` (`7ca26e80`) | `conformity/dsn-params-v1.10.1` | `4b4595fc` | First fork. |
