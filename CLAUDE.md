# CLAUDE.md

Conventions for working on this repository with Claude Code.

## Project context

`claude-sandboxed` is a template repository for Vaadin projects that use
Docker Sandboxes (`sbx` CLI) as the execution environment for agentic
programming with Claude Code.

The sandbox environment is defined in `.sbx/kit/spec.yaml`:

- a Java toolchain suited for Vaadin development
- network access limited to the hosts needed for Maven, Vaadin, and GitHub
- automatic installation of the `vaadin-skills` Claude Code plugin from the
  `vaadin/agent-marketplace`

## Working conventions

- Keep `.sbx/kit/spec.yaml` as the single source of truth for the sandbox
  environment (toolchain, setup commands, network permissions).
- Only add network permissions that are actually required by the toolchain
  or by a plugin/setup command; remove entries once they are no longer
  needed.
- When adding a setup step, prefer a single idempotent command over multiple
  steps, and comment out example/reference commands rather than deleting
  them if they document an alternative setup path.

## Testing

- After changing `.sbx/kit/spec.yaml`, start a sandbox from this spec and
  confirm the setup commands succeed and the expected network hosts are
  reachable before considering the change done.
