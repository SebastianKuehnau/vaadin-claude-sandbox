# vaadin-claude-sandbox

A ready-to-copy [Docker Sandbox](https://docs.docker.com/ai/sandboxes/) kit for Vaadin projects. Copy `.sbx/kit` into your own project and you get a sandbox with:

- JDK 25, installed from Debian when the sandbox is created, with `JAVA_HOME` set
- the Vaadin skills and MCP server for Claude Code (`vaadin-skills` plugin)
- Playwright with Chromium, for browser tests
- a network allowlist for Maven Central, GitHub, and Vaadin's docs, MCP and Javadoc hosts

Adjust the Java version in the "Install JDK" hook of `.sbx/kit/spec.yaml` to match your project.

## Why a sandbox

A Docker Sandbox is a disposable VM built for coding agents: its own kernel behind a hypervisor boundary, its own Docker daemon, a firewall that denies by default, and nothing shared with the host except the project folder. That's what makes --dangerously-skip-permissions a reasonable thing to type.

## Prerequisites
Docker Sandboxes v0.51.0 or newer — brew install docker/tap/sbx, then sbx login. The kit is a schema v3 kit, which older versions cannot combine with the claude agent.

## Usage
Create the sandbox the first time with:

```sh
sbx create claude --kit .sbx/kit --name my-claude-sandbox .
```

and then start the sandbox with:

```sh
sbx run --name my-claude-sandbox
```
