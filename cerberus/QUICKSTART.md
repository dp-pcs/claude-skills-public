# Cerberus Quick Start Guide

## Installation

```bash
cp -r cerberus ~/.claude-code/skills/
```

## Basic Usage

```bash
/cerberus
```

That's it! Cerberus will guide you through the rest.

## What Happens Next

1. **Discovery**: Cerberus searches for execution plans in your repo
2. **Selection**: Choose which prompting strategies to use (or accept recommendation)
3. **Analysis**: Cerberus executes selected strategies
4. **Comparison**: Meta-analysis shows which strategy worked best
5. **Report**: Full results saved to markdown file

## Strategy Quick Reference

| Strategy | When to Use | Best For |
|----------|-------------|----------|
| 🐕 Contrastive | HIGH risk | Finding non-obvious edge cases |
| 🐕 Positive | Any risk | Actionable checklists |
| 🐕 Negative | HIGH risk | Hard safety boundaries |

## Recommended Combinations

- **Database migrations**: All three
- **API changes**: Contrastive + Positive
- **Deployments**: Positive + Negative
- **Config updates**: Positive only
- **Learning exercise**: All three (even on simple plans)

## Common Commands

```bash
# Auto-discover plan in repo
/cerberus

# Review specific file
# (provide file path when prompted)
/cerberus
```

## Reading the Output

### Risk Levels
- **CRITICAL**: Blocker - do not proceed
- **HIGH**: Must address before execution
- **MEDIUM**: Should address, may proceed with mitigation
- **LOW**: Good to address, not blocking

### Strategy Comparison Symbols
- ✓✓✓ = Comprehensive coverage
- ✓✓ = Good coverage
- ✓ = Basic coverage
- ✗ = Missed this risk

## Quick Tips

1. For first-time use: Choose "All three strategies" to see differences
2. For high-risk plans: Don't skip Negative (catches hard blockers)
3. For execution: Positive provides the best checklist format
4. For learning: Compare how strategies differ on same plan

## Example Session

```
You: /cerberus

Cerberus: Found plan: docs/migration.md (HIGH risk)
          Recommend: All three strategies
          Proceed? yes/no

You: yes

Cerberus: [Executes reviews...]
          Winner: Negative (caught 3 blockers)
          Report: cerberus-review-migration-20260111.md

You: Generate remediation checklist

Cerberus: [Creates prioritized action items...]
```

## Need Help?

- Full details: See [README.md](README.md)
- Examples: See [examples.md](examples.md)
- Theory: See system-prompt.md section on "The Three Strategies"
