# Installing the Cerberus Skill

## For Claude Code

### Option 1: Automatic Installation

The skill has already been deployed to:
- `~/.claude/skills/cerberus/`
- `~/.claude-code/skills/cerberus/`

### Option 2: Manual Installation

If you need to reinstall or deploy to a different location:

```bash
# From the claude-code-skills repository
cp -r cerberus ~/.claude/skills/

# Verify installation
ls -la ~/.claude/skills/cerberus/
```

### Testing the Installation

**Important**: You may need to restart your Claude Code session for the skill to be recognized.

After restarting, invoke the skill:

```bash
/cerberus
```

Or use one of the aliases:
```bash
/plan-review
/prompting-analysis
```

## Verifying Installation

1. Check the skill is available:
```bash
/help
# Should list /cerberus in available skills
```

2. Test invocation with the files in this repo:
```bash
# Navigate to a project with an execution plan
/cerberus
```

## Skill Structure

```
cerberus/
├── skill.json              # Skill metadata and configuration
├── system-prompt.md        # Complete Cerberus instructions
├── examples.md             # Example interactions
├── README.md               # User-facing documentation
├── QUICKSTART.md          # Quick reference guide
├── SUMMARY.md             # Development summary
└── INSTALL.md             # This file
```

## Testing with Sample Data

The repository includes sample plan review data in the `files/` directory:

```bash
# The files/ directory contains:
# - DEMO.md - Example of three-strategy comparison
# - plan_reviewer.py - Python proof-of-concept
# - SKILL.md - Strategy descriptions
# - raw_comparisons.json - Sample output structure

# You can test Cerberus with this content
/cerberus
# When prompted, reference or paste content from DEMO.md
```

## Troubleshooting

### Skill Not Recognized

**Problem**: `/cerberus` says "Unknown skill"

**Solutions**:
1. Verify skill.json is valid JSON: `cat ~/.claude/skills/cerberus/skill.json | jq .`
2. Check file permissions: `ls -la ~/.claude/skills/cerberus/`
3. **Restart your Claude Code session** (most common fix)
4. Verify you're in the correct directory
5. Try the full path: Check both `~/.claude/skills/` and `~/.claude-code/skills/`

### No Plans Found

**Problem**: Cerberus says "No execution plans found in codebase"

**Solutions**:
1. Create a plan file (e.g., `docs/deployment-plan.md`)
2. Use the manual input option when prompted
3. Test with the sample DEMO.md in the files/ directory

### Strategy Selection Unclear

**Problem**: Unsure which strategies to select

**Solutions**:
1. For first-time use: Choose "All three strategies" to see differences
2. For high-risk plans: All three (maximum coverage)
3. For medium-risk: Contrastive + Positive
4. For low-risk: Positive only
5. See QUICKSTART.md for recommendations by plan type

## Configuration

No configuration needed! Cerberus works out of the box.

### Optional: Test with Custom Plans

Create a test plan file:

```markdown
# Test Deployment Plan

## Step 1: Database Migration
- Create new table: user_preferences
- Migrate data from users.settings (2.3M rows)
- DROP COLUMN users.settings
- Estimated time: 2 hours

## Step 2: Deploy API Changes
- Update user service to read from new table
- Backwards compatible
```

Save as `test-plan.md` and invoke:
```bash
/cerberus
```

## Updating the Skill

To update Cerberus with new features:

```bash
# Pull latest changes
git pull origin main

# Copy to skills directory
cp -r cerberus ~/.claude/skills/

# Restart Claude Code session
```

## Uninstalling

```bash
# Remove from skills directory
rm -rf ~/.claude/skills/cerberus
rm -rf ~/.claude-code/skills/cerberus
```

## Usage Syntax

### Basic Invocation
```bash
/cerberus
```

### With Aliases
```bash
/plan-review
/prompting-analysis
```

### Interactive Flow
```
You: /cerberus

Cerberus: Searching for execution plans in your codebase...
          Found: docs/migration-plan.md
          Risk Level: HIGH
          Recommended: All three strategies
          Proceed? (yes/no)

You: yes

Cerberus: [Executes reviews and meta-analysis]
          Results saved to: cerberus-review-migration-20260111.md
```

## Getting Started

1. **Install**: Already done! ✅
2. **Test**: Restart Claude Code and type `/cerberus`
3. **Learn**: Use all three strategies on your first plan
4. **Optimize**: Choose specific strategies based on what you learned

## Support

For issues or questions:
- Check [README.md](README.md) for usage documentation
- Review [QUICKSTART.md](QUICKSTART.md) for quick reference
- See [examples.md](examples.md) for interaction patterns
- Check [SUMMARY.md](SUMMARY.md) for development details

## Advanced Usage

### Create Plan Type Templates

Based on Cerberus reviews, you can create standardized templates:

```bash
# After running multiple database migration reviews
# Extract common patterns and create templates
```

### Integration with CI/CD

You could integrate Cerberus reviews into your pipeline:

```bash
# In CI/CD, provide plan file and capture output
/cerberus < deployment-plan.md > review-results.md
```

### Custom Risk Profiles

Adapt strategy recommendations for your organization:
- Edit system-prompt.md section on "Strategy Selection"
- Customize risk level thresholds
- Add domain-specific patterns

## What's Next?

After installation:
1. Try it on a real execution plan
2. Compare how the three strategies differ
3. Identify which approach works best for your use cases
4. Build organizational knowledge of effective review patterns

## License

Part of claude-code-skills repository by David Proctor - AI CoE
