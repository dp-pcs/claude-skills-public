# Cerberus - Multi-Strategy Plan Review

> Named after the three-headed guardian of the underworld, Cerberus uses three distinct prompting strategies to catch risks that any single approach might miss.

## What is Cerberus?

Cerberus is a Claude Code skill that reviews execution plans using three distinct prompting techniques and performs meta-analysis to identify which approach produces the best results for different scenarios.

## The Three Heads

### 🐕 Contrastive Prompting
Generates both a correct and incorrect review, then reasons through the contrast. Excellent at surfacing non-obvious edge cases and hidden assumptions.

**Best for**: Finding risks that traditional reviews miss

### 🐕 Positive Prompting
Frames all guidance as affirmative actions (\"verify X\", \"confirm Y\"). Creates actionable checklists with clear evidence requirements.

**Best for**: Operational readiness and execution planning

### 🐕 Negative Constraint Prompting
Uses prohibitions and hard boundaries (\"DO NOT approve without X\", \"NEVER skip Y\"). Establishes safety rails and absolute blockers.

**Best for**: Safety-critical decisions and known anti-patterns

## When to Use Cerberus

### Perfect For
- Database migrations (especially with data transformations)
- Production infrastructure changes
- API breaking changes
- Security-related deployments
- Learning which prompting technique works best for your team

### Also Useful For
- Feature deployments with gradual rollout
- Service updates requiring zero downtime
- Any plan where the cost of missing a risk is high
- Training exercises to compare prompting strategies

## Installation

Copy the `cerberus` directory to your Claude Code skills folder:

```bash
cp -r cerberus ~/.claude-code/skills/
```

## Quick Start

### Basic Usage

```bash
# In any project with an execution plan
/cerberus
```

Cerberus will:
1. Search for execution plans in your codebase
2. Identify high-risk steps
3. Ask which strategies to use
4. Execute the reviews
5. Provide meta-analysis comparing effectiveness

### With Custom Plan

```bash
/cerberus

# When prompted, paste your plan
```

### Strategy Selection

Cerberus recommends different strategies based on risk level:

- **HIGH risk** (database migrations, destructive operations): All three strategies
- **MEDIUM risk** (API changes, deployments): Contrastive + Positive
- **LOW risk** (config updates, routine deployments): Positive only

You can always override and select custom strategies.

## What You Get

### Individual Strategy Reviews
Each selected strategy produces a complete review with:
- Risk identification
- Specific findings
- Actionable recommendations
- Risk severity levels

### Meta-Analysis Report
Comparison across strategies including:
- Risk identification matrix
- Unique insights per strategy
- Actionability rankings
- Thoroughness rankings
- Recommended best strategy for the plan type

### Saved Output
Complete markdown report saved as:
```
cerberus-review-[plan-name]-[timestamp].md
```

## Example Output

```markdown
## Cerberus Meta-Analysis

### Risk Identification Matrix

| Risk Category    | Contrastive | Positive | Negative | Winner      |
|-----------------|-------------|----------|----------|-------------|
| Data integrity  | ✓✓✓         | ✓✓       | ✓✓✓      | Tie         |
| Performance     | ✓✓✓         | ✓        | ✓✓       | Contrastive |
| Operational     | ✓✓          | ✓✓✓      | ✓✓       | Positive    |

### Best Strategy for Database Migrations

**Primary**: Negative (for hard blockers)
**Secondary**: Contrastive (for scale/volume reasoning)

Negative caught 3 critical blockers that must be resolved before approval.
Contrastive identified the "2-hour window insufficient" issue through scale reasoning.
```

## Use Cases

### Use Case 1: Prevent Production Incidents
Before executing a risky database migration, run Cerberus to catch issues like:
- Untested rollback procedures
- Missing data exports before destructive operations
- Insufficient time windows for large-scale operations
- Lock contention that could cause downtime

### Use Case 2: Learn Prompting Techniques
Run all three strategies on the same plan to learn:
- Which approach your team finds most actionable
- Which strategy catches risks specific to your domain
- How to combine strategies for optimal coverage
- What prompting patterns work best for different plan types

### Use Case 3: Build Review Checklists
Use Cerberus output to create standardized checklists:
- Extract common findings across multiple reviews
- Identify must-have items for specific plan types
- Build institutional knowledge of what matters
- Train new team members on what to look for

### Use Case 4: Second Opinion on Approved Plans
Even if a plan has been reviewed, run Cerberus as a final check:
- Contrastive may surface edge cases humans missed
- Negative may identify anti-patterns that became normalized
- Meta-analysis may reveal gaps in your review process

## Research Background

Cerberus is based on research into prompting strategies:

- **Contrastive Prompting**: LLMs are "decent contrastive reasoners" - explicitly comparing correct vs incorrect approaches improves reasoning quality
- **Positive Framing**: Affirmative guidance (\"do X\") is more actionable than prohibitions (\"don't do Y\")
- **Negative Constraints**: For safety-critical domains, explicit prohibitions create clearer boundaries

By combining all three, Cerberus provides comprehensive coverage across different cognitive approaches.

## Advanced Usage

### Focus on Specific Step

```bash
/cerberus

# When plan is found, select specific step to review
```

### Compare Strategies on Simple Plan

Great for learning - run all three strategies on a low-risk plan to see how they differ without the noise of high complexity.

### Generate Remediation Checklist

After review, ask Cerberus to extract action items into a prioritized checklist.

## Configuration

Cerberus works out of the box, no configuration needed. It:
- Searches your codebase for plans automatically
- Adapts strategy recommendations to risk level
- Generates timestamped reports
- Provides interactive strategy selection

## Tips for Best Results

1. **Start with high-risk plans**: Cerberus shines when stakes are high
2. **Use all three strategies initially**: Learn which works best for your domain
3. **Save the meta-analysis**: Build a library of \"what works\" for different plan types
4. **Don't skip execution**: Cerberus performs actual reviews, not just templates
5. **Act on findings**: The value is in fixing issues before execution, not just identification

## Files

- `skill.json` - Skill configuration
- `system-prompt.md` - Complete Cerberus instructions
- `examples.md` - Usage examples and patterns
- `README.md` - This file
- `QUICKSTART.md` - Quick reference guide

## Author

David Proctor - AI CoE

## Version

1.0.0

## License

Part of claude-code-skills repository
