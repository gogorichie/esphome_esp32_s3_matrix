# Contributing to esphome_esp32_s3_matrix

Thanks for your interest in improving this project! This repo contains a simple ESPHome configuration plus a few GitHub workflows. Small contributions are welcome.

## Ways to contribute

- Open an issue for bugs, docs fixes, or feature ideas (please use the provided templates).
- Submit a pull request (PR) with a focused change.


### 1) Install ESPHome CLI

- Python 3.11+ is recommended.
- On Windows (PowerShell):

```powershell
# Option A: pipx (recommended)
pipx install esphome

# Option B: pip (user install)
python -m pip install --user esphome
```

Verify installation:

```powershell
esphome --version
```

### 2) Validate and/or compile the config

From the repository root:

```powershell
# Validate YAML and device config
esphome config .\esp32_s3_matrix.yml

# Optional: compile firmware locally
esphome compile .\esp32_s3_matrix.yml
```

## Branching, commits, and PRs

- Create a feature branch from the latest default branch (main):

```powershell
git checkout -b fix/short-description
```

- Keep commits small and meaningful. Conventional Commits are appreciated:
  - feat: add new matrix effect
  - fix: correct GPIO for LED data pin
  - docs: clarify Wi‑Fi secrets usage

- Open a PR:
  - Fill out the PR template details (what changed, why, and testing notes).
  - Include screenshots/logs when helpful (e.g., ESPHome compile output).
  - Ensure GitHub Actions checks pass.

## Automated workflows you should know about

- Dependabot updates may be auto‑approved/merged when safe.
- Stale issues/PRs are auto‑labeled and may be closed after inactivity.

## Coding/style notes

- Keep YAML clear and commented where it aids users.
- Prefer sensible defaults that work for the target board (ESP32‑S3 matrix).
- Avoid committing secrets; use `!secret` and document required keys.

## License

This project uses the Unlicense. By contributing, you agree your contributions are released under the same terms.

## Questions?

Open an issue and describe what you’re trying to do. Thanks for helping make this better!
