# Test Suite

## Overview

Comprehensive test suite for the multi-agent system.

## Test Categories

### 1. Schema Validation
- JSON schema format
- Required fields
- Type validation
- Constraint checking

### 2. Agent Tests
- Individual agent responses
- Task completion
- Error handling
- Timeout behavior

### 3. Integration Tests
- Full workflow execution
- Agent coordination
- Context passing
- Memory persistence

### 4. Performance Tests
- Response time
- Token usage
- Parallel execution
- Load handling

## Running Tests

### All Tests
```bash
npm test
```

### Specific Category
```bash
npm test:schemas
npm test:agents
npm test:integration
npm test:performance
```

## Test Data

Sample requests in `/test-data`:
- `simple-query.json`
- `complex-research.json`
- `parallel-agents.json`
- `error-scenarios.json`

## Validation Tools

- JSON Schema Validator
- Postman Collection
- n8n Test Workflows
- Performance Profiler

## CI/CD Integration

Tests run automatically on:
- Pull requests
- Main branch commits
- Release tags
- Scheduled daily

## Coverage Report

Current coverage:
- Schemas: 100%
- Agents: 85%
- Integration: 75%
- Performance: 60%

Target: >90% overall coverage