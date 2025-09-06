# Base Communication Schema

## Overview

The base schema defines the standard communication protocol for all agents in the multi-agent system.

## Master Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Multi-Agent Communication Schema",
  "type": "object",
  "required": ["meta", "request", "context"],
  "properties": {
    "meta": {
      "type": "object",
      "required": ["version", "timestamp", "session_id", "agent_id"],
      "properties": {
        "version": {"type": "string", "pattern": "^\\d+\\.\\d+\\.\\d+$"},
        "timestamp": {"type": "string", "format": "date-time"},
        "session_id": {"type": "string", "format": "uuid"},
        "agent_id": {"type": "string"},
        "parent_agent_id": {"type": "string"},
        "execution_mode": {
          "type": "string",
          "enum": ["sync", "async", "parallel"]
        }
      }
    },
    "request": {
      "type": "object",
      "required": ["task", "parameters"],
      "properties": {
        "task": {
          "type": "object",
          "required": ["type", "objective", "constraints"],
          "properties": {
            "type": {
              "type": "string",
              "enum": ["research", "architect", "ux_design", "test", "assembly"]
            },
            "objective": {"type": "string", "minLength": 10},
            "constraints": {
              "type": "object",
              "properties": {
                "max_iterations": {"type": "integer", "minimum": 1, "maximum": 10},
                "time_limit_seconds": {"type": "integer", "minimum": 30, "maximum": 300},
                "output_format": {
                  "type": "string",
                  "enum": ["json", "markdown", "structured_data"]
                }
              }
            }
          }
        },
        "parameters": {
          "type": "object",
          "additionalProperties": true
        }
      }
    },
    "context": {
      "type": "object",
      "required": ["user_query", "previous_results"],
      "properties": {
        "user_query": {"type": "string"},
        "previous_results": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "agent_id": {"type": "string"},
              "timestamp": {"type": "string", "format": "date-time"},
              "result": {"type": "object"}
            }
          }
        },
        "shared_memory": {
          "type": "object",
          "additionalProperties": true
        }
      }
    }
  }
}
```

## Response Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Agent Response Schema",
  "type": "object",
  "required": ["status", "data", "meta"],
  "properties": {
    "status": {
      "type": "string",
      "enum": ["pending", "processing", "completed", "failed", "partial"]
    },
    "data": {
      "type": "object",
      "properties": {
        "findings": {"type": "array"},
        "confidence_score": {"type": "number", "minimum": 0, "maximum": 1},
        "citations": {"type": "array"},
        "summary": {"type": "string"}
      }
    },
    "errors": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "code": {"type": "string"},
          "message": {"type": "string"},
          "details": {"type": "object"}
        }
      }
    },
    "next_context": {
      "type": "object",
      "description": "Context to pass to next agent"
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "tokens_used": {"type": "integer"},
        "tools_called": {"type": "array"}
      }
    }
  }
}
```

## Usage Examples

### Request Example

```json
{
  "meta": {
    "version": "1.0.0",
    "timestamp": "2025-09-06T10:00:00Z",
    "session_id": "550e8400-e29b-41d4-a716-446655440000",
    "agent_id": "research_001",
    "parent_agent_id": "lead_001",
    "execution_mode": "parallel"
  },
  "request": {
    "task": {
      "type": "research",
      "objective": "Find and analyze top 10 AI agent companies",
      "constraints": {
        "max_iterations": 3,
        "time_limit_seconds": 180,
        "output_format": "json"
      }
    },
    "parameters": {
      "include_financial_data": true
    }
  },
  "context": {
    "user_query": "Find AI companies",
    "previous_results": [],
    "shared_memory": {}
  }
}
```

## Validation

Use [JSON Schema Validator](https://jsonschemavalidator.net/) to validate your schemas.