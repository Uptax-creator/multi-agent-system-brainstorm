# Architect Agent Schema Documentation

## Overview
The Architect Agent is responsible for designing system architecture based on requirements and constraints. It follows the Anthropic multi-agent pattern for comprehensive architectural decisions.

## Schema Version: 1.0.0

## Request Structure

### Requirements Section
- **Functional Requirements**: List of features with priority levels (critical/high/medium/low)
- **Non-Functional Requirements**: Performance, security, scalability metrics
- **Constraints**: Technical, business, regulatory, and resource limitations

### Context Section
- **Tech Stack**: Preferred, avoided, and existing technologies
- **Team**: Size, expertise level, and skills available
- **Timeline**: Project dates and milestones
- **Budget**: Total budget and breakdown by category
- **Existing Systems**: Current systems that need integration

## Response Structure

### Architecture Section
The agent provides:
- **Pattern Selection**: Microservices, monolithic, serverless, etc.
- **Layer Definition**: Clear separation of concerns
- **Technology Mapping**: Specific tech for each layer

### Components Section
Detailed component specifications including:
- **Service Types**: Services, databases, caches, queues, gateways
- **Interfaces**: REST, GraphQL, gRPC, WebSocket definitions
- **Dependencies**: Sync/async relationships between components
- **Scaling Strategy**: Horizontal/vertical scaling rules

### Rationale Section
Architectural decision records containing:
- **Key Decisions**: What was decided and why
- **Alternatives Considered**: Other options evaluated
- **Trade-offs**: What was gained vs sacrificed
- **Risk Assessment**: Probability, impact, and mitigation strategies

### Implementation Plan
- **Phased Approach**: Incremental delivery phases
- **Critical Path**: Essential tasks sequence
- **Resource Allocation**: Team distribution

### Quality Attributes
- **Performance**: Response time, throughput targets
- **Security**: Authentication, authorization, encryption
- **Scalability**: Horizontal, vertical, geographic scaling
- **Maintainability**: Modularity, testability, documentation

## Usage Example

```json
{
  "request": {
    "requirements": {
      "functional": [
        {
          "id": "FR-001",
          "description": "User authentication system",
          "priority": "critical",
          "acceptance_criteria": [
            "Support OAuth 2.0",
            "2FA authentication",
            "Session management"
          ]
        }
      ],
      "non_functional": [
        {
          "category": "performance",
          "requirement": "API response time",
          "metric": "95th percentile",
          "target_value": "< 200ms"
        }
      ]
    },
    "context": {
      "tech_stack": {
        "preferred": ["Node.js", "PostgreSQL", "Redis"],
        "avoided": ["PHP", "MySQL"],
        "existing": ["AWS", "Docker"]
      },
      "team": {
        "size": 5,
        "expertise_level": "intermediate",
        "skills": ["JavaScript", "DevOps", "React"]
      }
    }
  }
}
```

## Integration with n8n

This schema is designed to work seamlessly with n8n's Structured Output Parser node:

1. **Input Validation**: Ensures all required fields are present
2. **Type Safety**: Enforces correct data types
3. **Enum Constraints**: Limits values to predefined options
4. **Output Structure**: Guarantees consistent response format

## Best Practices

1. **Always provide clear functional requirements** with acceptance criteria
2. **Include measurable non-functional requirements** with specific metrics
3. **Document all constraints** that might impact architecture decisions
4. **Specify team capabilities** to ensure realistic architecture
5. **Define integration points** with existing systems upfront

## Common Patterns

### Microservices Architecture
Best when:
- Team size > 10
- Multiple deployment schedules needed
- Technology diversity required
- Independent scaling necessary

### Monolithic Architecture
Best when:
- Small team (< 5)
- Rapid prototyping needed
- Simple deployment preferred
- Shared database acceptable

### Serverless Architecture
Best when:
- Variable/unpredictable load
- Pay-per-use model desired
- Minimal operations overhead
- Event-driven workflows

## Validation Rules

The schema enforces:
- Required fields must be present
- Enums must match predefined values
- Arrays must have minimum items where specified
- Strings must meet length requirements
- Numbers must be within defined ranges

## Error Handling

Common validation errors:
- Missing required fields
- Invalid enum values
- Exceeded array limits
- Invalid date formats
- Malformed URIs

## Next Steps

After receiving the architecture design:
1. Review with stakeholders
2. Validate against requirements
3. Assess risk mitigation strategies
4. Create detailed implementation tasks
5. Setup monitoring and metrics

---

*This schema is part of the Multi-Agent System Brainstorm project*