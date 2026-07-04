# Security Policy

## Reporting a vulnerability

**Do not open a public issue for security problems.**

Use GitHub's private vulnerability reporting on the affected repository (Security tab → "Report a vulnerability"). If that's unavailable, email security@skylence.be.

You can expect an acknowledgement within 72 hours. Please include reproduction steps and the version (`skyway --version`) where applicable.

## Scope notes

- skyway executes workflows that drive an AI agent with real tool access. Reports about **prompt-injection paths, sandbox/boundary escapes, secret leakage into logs or events, and lint bypasses** (`SKY-WF-*` safety rules) are explicitly in scope and appreciated.
- The daemon binds to loopback and is single-user by design unless multi-user mode is enabled; reports assuming a hostile local network should state that assumption.
- Only the latest released version is supported with fixes.

## Disclosure

We'll work with you on a coordinated disclosure timeline; credit is given unless you prefer otherwise.
