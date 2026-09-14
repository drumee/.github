# Security Policy

Thank you for taking the time to report a security problem in Drumee. Drumee is
self-hosted software that holds people's files and conversations, so we take
these reports seriously.

## Reporting a vulnerability

**Please do not open a public issue, pull request or discussion for a security
problem.** A public report tells everyone running Drumee about the weakness
before there is a fix available for them to install.

Instead, ask us for a private channel first:

1. Open an issue on the affected repository containing **only** a line such as
   *"I would like to report a security issue privately — please open a private
   channel."* Give no details, no steps and no proof of concept in that issue.
2. A maintainer will open a private GitHub Security Advisory on the repository
   and invite you to it. Everything after that — details, reproduction, patches
   — happens in that private thread, visible only to you and the maintainers.

If the repository's **Security** tab already offers **Report a vulnerability**,
use that instead and skip step 1; it opens the same private thread directly.

### What helps us most

- Which repository and which version, commit or package build you tested.
- How the instance was deployed — Docker, Debian packages, or another way.
- The steps to reproduce it, in as much detail as you can manage.
- What an attacker gets out of it: whose data, and what they can read or change.
- Anything you already know about a fix or a workaround.

A partial report is still worth sending. If you are unsure whether something is
a real issue, report it privately and let us work that out.

## What happens next

We will acknowledge your report in the advisory thread and keep you updated as
we look into it. If we confirm the issue we will work on a fix, tell you when it
ships, and credit you in the advisory unless you would rather stay anonymous.

If we conclude it is not a vulnerability, we will explain why rather than
closing the thread silently.

## Scope

**In scope** — anything in the repositories under
[github.com/drumee](https://github.com/orgs/drumee/repositories) that affects a
Drumee instance: authentication and session handling, the permission and access
control model, the meta filesystem, sharing links, the plugin surface, and the
installation and provisioning tooling.

**Out of scope**

- Vulnerabilities in third-party dependencies — please report those upstream. If
  Drumee's use of a dependency is what makes it exploitable, that is in scope,
  so tell us.
- Volumetric denial of service, spam, and social engineering.
- Missing hardening that has no demonstrated impact.

## Please test responsibly

Test against **an instance you run yourself** — Drumee is designed to be
self-hosted, so standing one up is the intended way to look at it. Please do not
test against the hosted service or against instances belonging to other people,
and please do not run scans that degrade a service others are using.

Do not access, modify or retain anyone else's data. If you come across personal
data while investigating, stop and tell us in the report.

## Disclosure

We ask for a reasonable window to ship a fix before any public write-up, and we
will work with you on the timing rather than leaving you waiting. We are not
going to argue about a date with someone who reported a problem in good faith.
