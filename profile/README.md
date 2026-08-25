<div align="center">

# Drumee

### The sovereign workspace built to be yours

Files, folder-native chat, video meetings and fine-grained permissions —
self-hosted on infrastructure **you** control, under AGPL-3.0.

[Website](https://drumee.com) ·
[Documentation](https://docs.drumee.com/introduction/) ·
[Self-host with Docker](https://github.com/drumee/docker-hosted) ·
[Discussions](https://github.com/orgs/drumee/discussions) ·
[X](https://x.com/drumeeOS)

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Docker Pulls](https://img.shields.io/docker/pulls/drumee/stable)](https://hub.docker.com/r/drumee/stable)
[![Self-hosted](https://img.shields.io/badge/self--hosted-yes-success)](https://github.com/drumee/docker-hosted)

</div>

---

## What is Drumee

Drumee is a complete team workspace — files, chat that lives inside the folder
it is about, video meetings, and POSIX-style permissions — that runs on your own
server. No per-seat lock-in, no third party holding your data.

It installs on a single machine with Docker, on bare-metal Debian, or on a
Synology NAS.

## Get started

| Path | Best for | Start here |
|---|---|---|
| **Docker** | Most self-hosters | [drumee/docker-hosted](https://github.com/drumee/docker-hosted) |
| **Debian / bare metal** | Production installs | [drumee/debian-hosted](https://github.com/drumee/debian-hosted) |
| **Synology NAS** | Home and small-office NAS | [drumee/synology-hosted](https://github.com/drumee/synology-hosted) |
| **Build on Drumee** | Developers extending the platform | [drumee/starter-kit](https://github.com/drumee/starter-kit) |

Full documentation: **[docs.drumee.com](https://docs.drumee.com/introduction/)**

## How the code is organised

Drumee is not a single binary — it is a set of services that install together.
The repositories worth knowing:

| Repository | What it is |
|---|---|
| [server-team](https://github.com/drumee/server-team) | The workspace back-end: desk content, sharing, chat and meeting APIs |
| [ui-team](https://github.com/drumee/ui-team) | The workspace front-end — the desk you actually see |
| [server-core](https://github.com/drumee/server-core) · [server-essentials](https://github.com/drumee/server-essentials) | Shared back-end runtime every Drumee service is built on |
| [ui-core](https://github.com/drumee/ui-core) · [ui-essentials](https://github.com/drumee/ui-essentials) | The client-side rendering engine and its shared library |
| [schemas](https://github.com/drumee/schemas) | Database schema and stored procedures |
| [static](https://github.com/drumee/static) | Fonts, icons and other static assets served to the client |

Everything else — installers, setup tooling, per-platform packaging — hangs off
those. [Browse all repositories](https://github.com/orgs/drumee/repositories).

## For developers

Under the workspace sits an application platform: a built-in identity and access
layer, a permissioned virtual filesystem, and a client-side JSON rendering engine
— so an app built on Drumee ships without rebuilding auth, storage or a UI
framework from scratch.

The [Starter Kit](https://github.com/drumee/starter-kit) is the fastest way in:
it brings up a full local Drumee with Docker and lets you edit the back-end and
front-end sources in place.

## Community

- **[GitHub Discussions](https://github.com/orgs/drumee/discussions)** — questions, self-hosting help, ideas
- **Issues** — file bugs on the repository they belong to
- **X** — [@drumeeOS](https://x.com/drumeeOS)

## Contributing

Contributions are welcome — code, docs, translations, or a good bug report.
Start with [CONTRIBUTING.md](https://github.com/drumee/.github/blob/main/CONTRIBUTING.md)
and our [Code of Conduct](https://github.com/drumee/.github/blob/main/CODE_OF_CONDUCT.md).

## License

Drumee is licensed under the
**[GNU Affero General Public License v3.0](https://www.gnu.org/licenses/agpl-3.0)**.
