# Cerberus Skill - Development Summary

## Project Overview

**Skill Name**: Cerberus
**Version**: 1.0.0
**Created**: January 11, 2026
**Author**: David Proctor - AI CoE

## What is Cerberus?

Cerberus is a Claude Code skill that reviews execution plans using three distinct prompting strategies (contrastive, positive, and negative) and performs meta-analysis to determine which approach produces the best results for different scenarios.

Named after the three-headed guardian dog from mythology, each "head" represents a different cognitive approach to plan review:

- 🐕 **Contrastive Head**: Reasons through correct vs incorrect reviews
- 🐕 **Positive Head**: Builds actionable checklists with evidence requirements
- 🐕 **Negative Head**: Establishes hard safety boundaries and blockers

## Key Features

### Multi-Strategy Review
- Executes up to three different prompting strategies on the same plan
- Each strategy produces a complete, independent review
- Real execution, not just templates

### Meta-Analysis
- Compares effectiveness across strategies
- Identifies which approach caught which risks
- Ranks strategies by actionability and thoroughness
- Recommends best approach for the plan type

### Interactive Workflow
- Auto-discovers execution plans in codebase
- Guides user through strategy selection
- Adapts recommendations to risk level
- Generates comprehensive markdown reports

### Research-Based
Built on prompting research:
- Contrastive prompting leverages LLM reasoning through comparison
- Positive framing creates more actionable guidance
- Negative constraints establish clear safety boundaries

## Files Created

### Core Files
- [skill.json](skill.json) - Skill configuration and metadata
- [system-prompt.md](system-prompt.md) - Complete skill instructions (15.7KB)
- [examples.md](examples.md) - Usage examples and patterns
- [README.md](README.md) - Comprehensive documentation
- [QUICKSTART.md](QUICKSTART.md) - Quick reference guide
- [SUMMARY.md](SUMMARY.md) - This file

### File Purposes

**skill.json**: Defines the skill metadata, invocation commands (`/cerberus`, `/plan-review`, `/prompting-analysis`), and capabilities

**system-prompt.md**: Contains the complete instructions for how Cerberus operates:
- Discovery and plan parsing logic
- Three strategy frameworks (contrastive, positive, negative)
- Meta-analysis methodology
- Interaction guidelines
- Quality checklist

**examples.md**: Real-world usage examples showing:
- Database migration reviews
- API deployment reviews
- Custom plan input
- Technique comparison learning
- Strategy selection patterns

**README.md**: User-facing documentation covering:
- What Cerberus is and when to use it
- The three prompting strategies
- Installation and quick start
- Use cases and advanced usage
- Research background

**QUICKSTART.md**: Condensed reference for quick lookup

## Deployment

The skill has been deployed to: `~/.claude-code/skills/cerberus/`

## How to Use

### Basic Invocation
```bash
/cerberus
```

### What Happens
1. Cerberus searches for execution plans in your codebase
2. Identifies high-risk steps
3. Recommends which strategies to use based on risk level
4. Executes selected strategies
5. Performs meta-analysis comparing effectiveness
6. Saves comprehensive report

### Strategy Recommendations by Risk Level

**HIGH Risk** (database migrations, destructive operations)
- Recommended: All three strategies
- Why: Maximum coverage for critical changes

**MEDIUM Risk** (API changes, deployments)
- Recommended: Contrastive + Positive
- Why: Balance of edge-case detection and actionability

**LOW Risk** (config updates, routine changes)
- Recommended: Positive only
- Why: Efficient checklist without overhead

**Learning Mode**
- Recommended: All three strategies (even on simple plans)
- Why: Compare how different approaches handle the same content

## Technical Implementation

### Architecture
- **Phase 1**: Discovery - Finds execution plans in codebase or accepts user input
- **Phase 2**: Selection - Interactive strategy choice with recommendations
- **Phase 3**: Execution - Performs actual reviews (not just templates)
- **Phase 4**: Meta-Analysis - Compares strategy effectiveness
- **Phase 5**: Output - Generates comprehensive markdown report

### Key Capabilities
- Codebase access for plan discovery
- File creation for reports
- Interactive prompting for user choices
- No external API dependencies

### Plan Types Detected
- Database migrations (highest priority for review)
- Deployments
- API changes
- Infrastructure changes
- Generic execution plans

## Use Cases

### 1. Prevent Production Incidents
Run Cerberus before executing risky changes to catch:
- Untested rollback procedures
- Missing data backups before destructive operations
- Insufficient time windows
- Lock contention issues

### 2. Learn Prompting Techniques
Compare how different prompting strategies handle the same plan:
- Understand which approach works best for your domain
- Train team members on effective review techniques
- Build institutional knowledge

### 3. Build Review Checklists
Extract common patterns from Cerberus reviews:
- Create standardized checklists by plan type
- Identify must-have verification items
- Codify organizational best practices

### 4. Second Opinion
Run Cerberus on already-reviewed plans:
- Catch edge cases human reviewers missed
- Identify normalized anti-patterns
- Validate thoroughness of existing review process

## Strategy Comparison Results (from research)

Based on the analysis in the `files/` directory:

### Contrastive Prompting
**Strengths**:
- Best at surfacing non-obvious risks
- Excellent for reasoning through edge cases
- Forces consideration of failure modes

**Best for**: Database migrations, scale/volume concerns

### Positive Prompting
**Strengths**:
- Most actionable output format
- Clear checklist structure
- Explicit evidence requirements

**Best for**: Operational readiness, execution planning

### Negative Constraint Prompting
**Strengths**:
- Clearest about absolute blockers
- Explicit anti-pattern identification
- Strong safety emphasis

**Best for**: Safety-critical decisions, hard stops

## Next Steps

### For Users
1. Try `/cerberus` in a project with an execution plan
2. Run all three strategies initially to learn differences
3. Save meta-analysis reports to build organizational knowledge
4. Adapt strategy selection based on your findings

### For Development
Potential enhancements:
- Add more plan type templates
- Build library of domain-specific risk patterns
- Export to other formats (JSON, CSV)
- Integration with issue tracking systems

## Project Structure

```
cerberus/
├── skill.json              # Skill metadata and configuration
├── system-prompt.md        # Complete Cerberus instructions
├── examples.md            # Usage examples
├── README.md              # User documentation
├── QUICKSTART.md          # Quick reference
└── SUMMARY.md             # This file
```

## Research References

The skill is based on Python proof-of-concept code in the `files/` directory:
- [plan_reviewer.py](../files/plan_reviewer.py) - Original implementation
- [SKILL.md](../files/SKILL.md) - Strategy descriptions
- [DEMO.md](../files/DEMO.md) - Detailed strategy comparison
- [raw_comparisons.json](../files/raw_comparisons.json) - Sample output structure

## Success Metrics

The skill is successful if:
- Users can invoke `/cerberus` and get meaningful plan reviews
- Meta-analysis clearly shows which strategy worked best
- Output is actionable (users can fix issues before execution)
- Users learn which prompting techniques work for their domain
- Critical risks are caught that single-strategy review might miss

## Conclusion

Cerberus brings research-based prompting techniques into a practical, usable skill for execution plan review. By combining three distinct cognitive approaches and meta-analyzing the results, it provides both comprehensive risk coverage and learning about prompting effectiveness.

The skill is now deployed and ready for use with `/cerberus` in any Claude Code session.
