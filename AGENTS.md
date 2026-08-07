# AGENTS.md — ESP32-S3 Matrix 8x8 LED Configuration

Tool-agnostic project brief for AI coding agents (Claude Code, Codex, Cursor,
Copilot, and anything else that reads `AGENTS.md`) working in this repository.

## Project overview

An [ESPHome](https://esphome.io/) configuration for an ESP32-S3 development
board with an onboard 8×8 WS2812B addressable RGB LED matrix. It exposes a
set of light effects (rainbow, color wipe, scan, twinkle, flicker, fireworks,
plus status icons) controlled over Wi-Fi, and supports Wi-Fi provisioning via
Improv Serial, a captive portal, or Bluetooth LE. There is no application
code to build — `esp32_s3_matrix.yml` **is** the deliverable, compiled and
flashed by the ESPHome toolchain.

## Repo structure

```
.
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   ├── dependabot.yml         # GitHub Actions updates only, monthly, grouped
│   └── workflows/
│       ├── auto-merge.yml     # auto-merges Dependabot PRs (squash) once checks pass
│       ├── auto-stale.yml     # weekly: labels stale issues/PRs, prunes stale branches
│       ├── release.yml        # on vX.Y.Z tag push: validates semver, publishes a release with esp32_s3_matrix.yml + README attached
│       ├── smoke-test.yml     # on every PR: validates the config via `esphome config` in the esphome/esphome Docker image
│       └── welcome.yml        # greets first-time issue/PR authors, congratulates first merged PR
├── CONTRIBUTING.md
├── LICENSE                    # Unlicense (public domain)
├── README.md
├── esp32-s3-matrix-5.jpg      # photo used in README
└── esp32_s3_matrix.yml        # the ESPHome device configuration (the deliverable)
```

## Non-negotiables

- **`esp32_s3_matrix.yml` is the single source of truth.** Validate changes
  the same way CI does before opening a PR:
  ```bash
  docker run --rm -v "$PWD:/config" -w /config esphome/esphome:2024.6.0 config esp32_s3_matrix.yml
  ```
  `smoke-test.yml` runs this on every PR and blocks merge on invalid config.
- **Never commit a real `secrets.yaml`.** `smoke-test.yml` stubs one with
  fake values at CI time; there's no `secrets.example.yaml` in this repo
  (see README's Wi-Fi/API-encryption instructions instead) — if you add a
  new `!secret` key, update those instructions in the same change.
- **Releases are tag-driven, not merge-driven.** Pushing a tag matching
  `v[0-9]*.[0-9]*.[0-9]*` runs `release.yml`, which re-validates the tag
  against strict [SemVer](https://semver.org/) in-job and fails the run if it
  doesn't actually conform (no leading zeros, valid prerelease/build
  metadata) — the workflow's trigger glob is looser than the validation it
  runs, so don't assume any tag matching the glob will succeed.
- **`esphome: min_version: 2024.6.0`** in `esp32_s3_matrix.yml` must stay in
  sync with the ESPHome Docker image tag pinned in `smoke-test.yml` — bump
  both together, not just one.
- Dependabot PRs against `github-actions` auto-merge via squash once checks
  pass (`auto-merge.yml`); it requires an `ACCESS_TOKEN` secret with repo
  permissions to be set, distinct from the default `GITHUB_TOKEN`.

## Commit conventions

**Every commit must follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).**

```
<type>(<optional scope>): <imperative description>

<optional body explaining why>

<optional footers>
```

- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`,
  `ci`, `chore`, `revert`.
- Scopes used here: `matrix`, `effects`, `wifi`, `release`, `ci`, `docs`.
- Imperative mood, no trailing period, subject ≤ 72 chars.
- Breaking = a substitution name changed, an effect renamed/removed, or a
  config option that would require an existing user's `secrets.yaml` or
  entities to change. Use `type(scope)!:` and/or a `BREAKING CHANGE:` footer.
- One logical change per commit; PR titles use the same format.

```
feat(effects): add fireworks light effect
fix(wifi): correct improv_serial provisioning fallback
ci(release): pin esphome image to 2024.6.0
docs: note 5GHz Wi-Fi is unsupported
```

- **Cutting a release is a separate, deliberate step from committing:**
  after merging conventional commits to `main`, tag with
  `git tag vX.Y.Z && git push origin vX.Y.Z` per [`CONTRIBUTING.md`](CONTRIBUTING.md)
  to trigger `release.yml`.

## CI / automation

- **Dependabot** (`.github/dependabot.yml`): `github-actions` ecosystem only,
  monthly, grouped, commit prefix `ci`.
- **`auto-merge.yml`**: squash-merges Dependabot PRs automatically once
  checks pass (requires the `ACCESS_TOKEN` secret above).
- **`auto-stale.yml`**: weekly — labels issues/PRs stale via `actions/stale`,
  and separately prunes branches inactive 120+ days (deleted at 180) via
  `crs-k/stale-branches`, excluding `dependabot/*` branches.
- **`smoke-test.yml`**: validates `esp32_s3_matrix.yml` on every PR against
  a stubbed `secrets.yaml`.
- **`release.yml`**: on a `vX.Y.Z` tag push, validates SemVer and publishes a
  GitHub release with `esp32_s3_matrix.yml` and `README.md` attached.
- **`welcome.yml`**: comments a greeting on a contributor's first issue/PR
  and congratulates their first merged PR — not a functional gate, just
  friendliness.

## License

[Unlicense](LICENSE) — public domain. By contributing you agree your
contributions are released under the same terms.
