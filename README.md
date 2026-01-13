# Claude Skills Public

A collection of public Claude Code skills for enhancing Claude's capabilities.

## Available Skills

### Cerberus - Multi-Strategy Plan Review

Multi-strategy plan review using three prompting approaches (contrastive, positive, negative) to analyze execution plans and identify which technique works best for different scenarios. Best for database migrations, deployments, and high-risk changes.

**Installation:**

```bash
cp -r cerberus ~/.claude/skills/
```

**Usage:**

```bash
/cerberus
```

[Read more about Cerberus](cerberus/README.md)

---

### Maestro - Parallel Multi-Agent Deployment Orchestrator

Orchestrates complex multi-phase deployments by spawning parallel sub-agents for database migrations, services, APIs, and testing. Transforms large implementation plans into coordinated parallel execution.

**Installation:**

```bash
cp -r maestro ~/.claude/skills/
```

**Usage:**

```bash
/maestro
# Then provide your deployment plan path
```

[Read more about Maestro](maestro/README.md)

## Installation

To install a skill:

1. Copy the skill directory to your Claude skills folder:

   ```bash
   cp -r <skill-name> ~/.claude/skills/
   ```

2. The skill will be automatically available in Claude Code

## Usage

Once installed, skills can be invoked using the slash command format:

```bash
/<skill-name>
```

For example:

```bash
/cerberus
```

## Contributing

Feel free to contribute your own skills or improvements to existing ones. Submit a PR with:

- The complete skill directory
- Documentation including README.md
- Examples of usage

## License

MIT
