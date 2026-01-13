# Cerberus Usage Examples

## Example 1: Database Migration Review

```
User: /cerberus

Cerberus: I'm Cerberus, your multi-strategy plan reviewer. Let me search for execution plans...

Found: docs/db-migration.md
Type: Database Migration - Add user_preferences table
Risk Level: HIGH (2.3M rows, DROP COLUMN operation)

For this high-risk migration, I recommend all three strategies:
🐕 Contrastive - Surface hidden risks through comparison
🐕 Positive - Build actionable verification checklist
🐕 Negative - Establish hard safety boundaries

Proceed with full Cerberus analysis?

User: yes

[Cerberus executes all three strategies and provides meta-analysis]

Result: Identified 3 critical blockers, recommended hybrid approach
Best strategy for database migrations: Negative (for blockers) + Contrastive (for scale issues)
```

## Example 2: API Deployment Review

```
User: /cerberus

Cerberus: Searching for execution plans...

Found: .github/deployment-plan.md
Type: API Deployment - New authentication endpoints
Risk Level: MEDIUM (backwards compatibility concerns)

Recommended strategies for API changes:
🐕 Contrastive - Check for breaking changes
🐕 Positive - Verify backwards compatibility checklist

Skip Negative strategy for medium-risk? (yes/no)

User: yes

[Cerberus executes two strategies]

Result: Contrastive caught subtle breaking change in error response format
Winner: Contrastive (better at surfacing non-obvious incompatibilities)
```

## Example 3: Custom Plan Input

```
User: /cerberus

Cerberus: No execution plans found in codebase.

Please provide the plan you'd like me to review (paste markdown, YAML, or text)

User: [pastes plan]

We're deploying a new feature flag system:
1. Add feature_flags table
2. Deploy feature flag service
3. Migrate existing config-based flags
4. Update client SDKs

Cerberus: Analyzing plan...

Identified 4 steps:
1. [MEDIUM] Database change
2. [MEDIUM] Service deployment
3. [HIGH] Data migration
4. [LOW] Client updates

Step 3 is highest risk. Focus review there? (yes/review all)

User: yes

[Reviews step 3 with selected strategies]
```

## Example 4: Technique Comparison Learning

```
User: I want to see how the three prompting strategies compare on a simple deployment plan

Cerberus: Great! This is perfect for learning strategy differences.

Please provide the plan, and I'll run all three strategies even though it may be overkill. We'll focus on comparing how each approach handles the same content.

User: [provides simple deployment plan]

[Cerberus runs all three]

Meta-Analysis Results:

Contrastive: Identified 2 risks through reasoning
Positive: Created 8-item checklist
Negative: Flagged 1 hard blocker

For simple deployments:
- Positive is most actionable (clear checklist)
- Contrastive adds value for edge cases
- Negative may be too restrictive for low-risk changes

Learning: Use Positive for routine deployments, add Contrastive for novel patterns
```

## Example 5: Partial Strategy Selection

```
User: /cerberus

Cerberus: Found: infra/terraform-rollout.md
Type: Infrastructure Change
Risk Level: HIGH (production VPC modification)

Recommended: All three strategies

Which strategies to use?
[ ] All three (full analysis)
[ ] Contrastive + Positive
[ ] Contrastive + Negative
[ ] Custom selection

User: Contrastive + Negative

Cerberus: Good choice - Contrastive for reasoning, Negative for hard stops.
Skipping Positive (operational checklist).

[Runs two strategies]

Result:
- Contrastive identified VPC peering routing edge case
- Negative blocked on untested rollback

Skipped Positive means no operational checklist, but critical risks caught.
Recommend adding Positive for execution readiness.
```

## Common Usage Patterns

### Pattern 1: High-Risk Plan (Use All Three)
- Database migrations with data loss risk
- Production infrastructure changes
- Security-related deployments
- Large-scale data transformations

### Pattern 2: Medium-Risk Plan (Use Contrastive + Positive)
- API changes with backwards compatibility needs
- Feature deployments with gradual rollout
- Service updates with zero-downtime requirements
- Schema additions (non-destructive)

### Pattern 3: Low-Risk Plan (Use Positive Only)
- Documentation updates with process changes
- Configuration updates
- Routine deployments of tested code
- Standard operational procedures

### Pattern 4: Learning/Comparison (Use All Three on Simple Plans)
- When you want to understand strategy differences
- Training team on prompting techniques
- Building institutional knowledge
- Evaluating which approach fits your org best
