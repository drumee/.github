# Contributing to Drumee

Welcome. Whether you're fixing a bug, adding a feature, improving the docs or
just reporting something that broke — every contribution counts.

## Before you start

- **Understand the shape of the project.** Drumee is not one repository. The
  back-end lives in [server-team](https://github.com/drumee/server-team), the
  front-end in [ui-team](https://github.com/drumee/ui-team), the database schema
  in [schemas](https://github.com/drumee/schemas), and installers in
  `docker-hosted` / `debian-hosted` / `synology-hosted`. Start from
  [the documentation](https://docs.drumee.com/introduction/).
- **Check open issues** before opening a new one, and file the issue on the
  repository it actually belongs to.
- **Ask first for anything large.** Open a
  [Discussion](https://github.com/orgs/drumee/discussions) before writing a big
  feature, so we can agree on the approach before you spend the time.

## Prerequisites

- Docker and Docker Compose
- Node.js 22 or newer, and npm
- Git and a GitHub account

The fastest way to a working development environment is the
[Starter Kit](https://github.com/drumee/starter-kit): it brings up a full local
Drumee in Docker and lets you edit the back-end and front-end sources in place.

## Making a change

- **Bug fixes** — link the issue and describe the fix in the pull request.
- **Features** — make sure the change fits Drumee's direction; for anything
  substantial, open a proposal first.
- **Code style** — match the file you are editing. Two-space indentation.
  Proposals for a shared linter setup are welcome.
- **Documentation** — corrections to READMEs and docs are real contributions and
  are reviewed like code.

## Submitting a pull request

1. Fork the repository and create a branch for your change.
2. Keep the pull request focused — one concern per PR reviews far faster.
3. Describe what changed and why, and link any related issue.
4. Wait for review and CI. A maintainer will get back to you.

## Security

Please do **not** open a public issue for a security vulnerability. Report it
privately to the maintainers instead, and give us a chance to ship a fix before
any public disclosure.

## Code of Conduct

All contributors are expected to follow our
[Code of Conduct](https://github.com/drumee/.github/blob/main/CODE_OF_CONDUCT.md).
Be respectful, be inclusive, assume good faith.

## Need help?

- Open a [Discussion](https://github.com/orgs/drumee/discussions)
- Open an issue on the relevant repository
- Mention a maintainer in your pull request

Thank you for helping build a workspace people can actually own.
