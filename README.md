# ChittyCorp Organization `.github` Repository

This repository contains default community health files and workflow templates for all ChittyCorp repositories.

## Files in This Repository

### Community Health Files
These files automatically apply to all repositories without their own copies:

- **[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)** - Code of Conduct reflecting ChittyFoundation principles
- **[SECURITY.md](SECURITY.md)** - Security policy and vulnerability reporting
- **[SUPPORT.md](SUPPORT.md)** - How to get help
- **[FUNDING.yml](FUNDING.yml)** - Sponsor/funding links

### Profile
- **[profile/README.md](profile/README.md)** - Organization profile visible at https://github.com/chittycorp

### Workflow Templates
- **[workflow-templates/](workflow-templates/)** - Reusable GitHub Actions workflows

## How This Works

GitHub automatically uses files from this repository as defaults for all organization repositories that don't have their own versions.

For example:
- If `chittycorp/chittycan` has its own `CODE_OF_CONDUCT.md`, it uses that
- If `chittycorp/newproject` doesn't have one, it inherits from this repository

## Updating Organization Defaults

To update default files for all repositories:

1. Clone this repository
2. Make your changes
3. Submit a PR
4. Get approval from ChittyCorp maintainers
5. Merge to `main`

Changes take effect immediately across all repositories without their own versions.

## Local Override

Individual repositories can override any of these files by creating their own version in their root directory.

**Best Practice:** Only override if you have a good reason (e.g., project-specific security requirements).

## Contributing

See [SUPPORT.md](SUPPORT.md) for how to suggest changes.

For major policy changes (Code of Conduct, Security Policy), discuss in [GitHub Discussions](https://github.com/orgs/chittycorp/discussions) first.

---

**ChittyCorp**
Building tools for proof, fairness, and human-first AI

https://chittycorp.com
