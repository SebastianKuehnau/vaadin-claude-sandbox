# CLAUDE.md

Conventions for working on this repository with Claude Code.

## Project context

`vaadin-claude-sandbox` is a template repository for Vaadin projects that use
Docker Sandboxes (`sbx` CLI, v0.51.0 or newer) as the execution environment for
agentic programming with Claude Code.

The sandbox environment is defined in `.sbx/kit/spec.yaml`, a schema v3 kit
composed with the claude workload (`docker.io/sbx/claude`, Debian 13):

- JDK 25 from Debian, with `JAVA_HOME` pointing at `/usr/lib/jvm/default-java`
- automatic installation of the `vaadin-skills` Claude Code plugin from the
  `vaadin/agent-marketplace`
- Node and Playwright with Chromium, for browser tests
- network access limited to the hosts needed for Maven, Vaadin, GitHub and
  Playwright, split into an install-phase and a runtime allowlist

## Working conventions

- Keep `.sbx/kit/spec.yaml` as the single source of truth for the sandbox
  environment (toolchain, install hooks, network policy).
- Keep `# syntax=docker/sandbox-kit:3` as the file's first line; without it sbx
  parses the kit as a Dockerfile.
- Only add network hosts that are actually required by the toolchain or by an
  install hook, and to the right list: hosts reached only while installing go
  under `install.allow`, hosts the agent needs while working under
  `runtime.allow`. Remove entries once they are no longer needed.
- Install hooks see only `PATH`, `HOME` and a few shell basics; list any other
  variable a hook needs in its `env:`. `HOME` is `/home/agent` even for hooks
  running as root, so a root hook that writes into `$HOME` (npm, for one) must
  set `HOME=/root`.
- When adding a setup step, prefer a single idempotent command over multiple
  steps, and comment out example/reference commands rather than deleting
  them if they document an alternative setup path.

## Testing

- After changing `.sbx/kit/spec.yaml`, run `sbx kit validate .sbx/kit`, then
  start a sandbox from this spec and confirm the install hooks succeed and the
  expected network hosts are reachable before considering the change done.
