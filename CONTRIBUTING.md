# Contributing to esphome_esp32_s3_matrix

Thanks for your interest in improving this project! This repo contains a simple ESPHome configuration plus a few GitHub workflows. all contributions are welcome.


### How To Contribute

- Open a PR:
  - Fill out the PR template details (what changed, why, and testing notes).
  - Include screenshots/logs when helpful (e.g., ESPHome compile output).
  - Ensure GitHub Actions checks pass.

## Automated workflows you should know about

- **Smoke Test**: Validates ESPHome configuration on every PR to ensure it's valid before merging.
- **Dependabot**: Updates may be auto-approved/merged when safe.
- **Stale**: Issues/PRs are auto‑labeled and may be closed after inactivity.
- **Release**: Creates GitHub releases automatically when tags starting with "v" are pushed.

## Coding/style notes

- Keep YAML clear and commented where it aids users.
- Prefer sensible defaults that work for the target board (ESP32-S3 matrix).
- Avoid committing secrets; use `!secret` and document required keys.

## License

This project uses the Unlicense. By contributing, you agree your contributions are released under the same terms.

## Questions?

Open an issue and describe what you’re trying to do. Thanks for helping make this better!
