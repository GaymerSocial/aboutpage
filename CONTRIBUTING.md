<p align="center">
  <img src="https://global.media.gaymer.social/logo.png" width="300" alt="Gaymer.Social">
</p>

# Contributing to About.Gaymer.Social

This is [a Stux.Group Service](https://services.stux.group) under the [GaymerSocial](https://github.com/GaymerSocial) organization. Gaymer.Social was discontinued in September 2026; this repo is now a minimal static redirect shell, not a live site. This document exists for anyone with write access to the repo who wants to work on it consistently with how it's actually built.

## Local setup

See the [README](README.md#local-development) for running the site on your own machine with `dev-server.sh` / `dev-server.bat`.

## Project conventions

- Plain static site: `index.html` and `404.html` hold identical redirect/notice content — keep them in sync if you edit either
- `_redirects` is the Netlify catch-all (`/* https://gaymer.social/ 301`) that sends every legacy About.Gaymer.Social URL to the main notice; `404.html` is the fallback for hosts that only support redirects via a custom 404 page
- No build step, no framework, no analytics/tracking scripts
- The dev-mode banner is client-side (inline script in `index.html`/`404.html`), shown automatically on `localhost`/`127.0.0.1`; append `?nodev=1` to preview the real redirect
- This site is a redirect shell, so it has no sitemap; the redirect is a script in `index.html`/`404.html` (skipped on localhost so the dev banner shows) with a `<noscript>` meta refresh as fallback

## Versioning

This project uses [Date Versioning](https://datevers.ing). To release:

1. Add a `## vYY.MM.DD` entry at the top of `CHANGELOG.md`, with its sections in this order: Added, Changed, Fixed, Removed, Security, Deprecated.
2. Set `VERSION.md` to the same bare version (no `v`): today's **UTC** date as `YY.MM.DD`, or `YY.MM.DD-1`, `-2`… for later releases the same UTC day. Never a future date. Use UTC, not local time: just after midnight in the UK it is still the previous day in UTC.
3. Run `bash tests/version.sh`.
4. Run `./commit.sh` (or `commit.bat` on Windows). It checks the version, commits and tags `vYY.MM.DD`, and never pushes.

## Before committing

- Run `dev-server.sh` (or `.bat`) and manually check `index.html`/`404.html` render and the redirect still fires with `?nodev=1`
- This project has no automated test suite — a live check via the local dev server is the only real verification
