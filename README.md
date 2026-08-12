# vaadin-claude-sandbox

A ready-to-copy [Docker Sandbox](https://docs.docker.com/ai/sandboxes/) kit for Vaadin projects. Copy `.sbx/kit` into your own project and you get a sandbox with:

- a Java toolchain installed via SDKMAN
- a network allowlist for Maven Central, GitHub, npm, and `mcp.vaadin.com`
- a `CLAUDE.md` with project conventions for the agent

Adjust the Java version in `.sbx/kit/spec.yaml` to match your project.

## Why a sandbox

A Docker Sandbox is a disposable VM built for coding agents: its own kernel behind a hypervisor boundary, its own Docker daemon, a firewall that denies by default, and nothing shared with the host except the project folder. That's what makes --dangerously-skip-permissions a reasonable thing to type.

## Usage

Create the sandbox the first time with:

```sh
sbx create claude --kit .sbx/kit --name my-claude-sandbox .
```

and then start the sandbox with:

```sh
sbx run --name my-claude-sandbox
```
