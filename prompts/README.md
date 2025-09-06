# Agent Prompts Library

## Overview

This directory contains all prompts for the multi-agent system. Each agent has specific prompts designed for optimal performance.

## Prompt Structure

All prompts follow this structure:

1. **System Context** - Agent role and capabilities
2. **Task Description** - What the agent should accomplish
3. **Constraints** - Limitations and rules
4. **Output Format** - Expected response structure
5. **Examples** - Sample inputs and outputs

## Agent Prompts

### Lead Agent (Orchestrator)
- [lead-agent.md](lead-agent.md)
- Task decomposition and delegation

### Research Agent
- [research-agent.md](research-agent.md)
- Information gathering and analysis

### Architect Agent
- [architect-agent.md](architect-agent.md)
- System design and technical decisions

### UX/UI Agent
- [ux-ui-agent.md](ux-ui-agent.md)
- Interface design and user experience

### Test Agent
- [test-agent.md](test-agent.md)
- Quality assurance and validation

### Assembly Agent
- [assembly-agent.md](assembly-agent.md)
- Result aggregation and reporting

## Best Practices

1. **Be Specific:** Clear, detailed instructions
2. **Use Examples:** Provide input/output samples
3. **Define Boundaries:** Clear task limitations
4. **Enforce Format:** Strict output structure
5. **Include Fallbacks:** Error handling instructions

## Prompt Engineering Tips

### DO's
- ✅ Use structured JSON for responses
- ✅ Include confidence scores
- ✅ Provide citation requirements
- ✅ Set iteration limits
- ✅ Define quality thresholds

### DON'Ts
- ❌ Vague objectives
- ❌ Unlimited iterations
- ❌ Unstructured outputs
- ❌ Missing error handling
- ❌ No validation rules

## Testing Prompts

Use the `/tests` folder to validate prompt effectiveness:

```bash
# Test individual agent
node tests/test-prompt.js research-agent

# Test all agents
node tests/test-all-prompts.js
```

## Version Control

All prompts are versioned:
- Major changes: Update version number
- Minor tweaks: Update patch number
- Document changes in CHANGELOG.md