# Test Agent Schema

## Overview

Specialized agent for quality assurance, testing, and validation.

## Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Test Agent Schema",
  "type": "object",
  "required": ["agent_config", "request", "context"],
  
  "properties": {
    "agent_config": {
      "type": "object",
      "required": ["agent_id", "agent_type", "version"],
      "properties": {
        "agent_id": {
          "type": "string",
          "pattern": "^test_[0-9]{3}$"
        },
        "agent_type": {
          "type": "string",
          "const": "test"
        },
        "version": {
          "type": "string",
          "pattern": "^1\\.0\\.[0-9]+$"
        },
        "test_capabilities": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["unit", "integration", "e2e", "performance", "security", "accessibility"]
          }
        }
      }
    },
    
    "request": {
      "type": "object",
      "required": ["test_target", "test_types"],
      "properties": {
        "test_target": {
          "type": "object",
          "properties": {
            "type": {"type": "string", "enum": ["code", "api", "ui", "workflow", "system"]},
            "identifier": {"type": "string"},
            "description": {"type": "string"},
            "technology": {"type": "string"}
          }
        },
        "test_types": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["unit", "integration", "e2e", "performance", "security", "accessibility", "regression"]
          }
        },
        "test_parameters": {
          "type": "object",
          "properties": {
            "coverage_target": {"type": "number", "minimum": 0, "maximum": 100},
            "performance_thresholds": {
              "type": "object",
              "properties": {
                "response_time_ms": {"type": "integer"},
                "throughput_rps": {"type": "integer"},
                "error_rate": {"type": "number"}
              }
            },
            "security_checks": {
              "type": "array",
              "items": {"type": "string"}
            }
          }
        }
      }
    }
  }
}
```

## Response Schema

```json
{
  "type": "object",
  "required": ["status", "data", "meta"],
  "properties": {
    "status": {
      "type": "string",
      "enum": ["completed", "partial", "failed"]
    },
    "data": {
      "type": "object",
      "required": ["test_results", "summary"],
      "properties": {
        "test_results": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "test_type": {"type": "string"},
              "test_name": {"type": "string"},
              "status": {"type": "string", "enum": ["passed", "failed", "skipped", "error"]},
              "duration_ms": {"type": "integer"},
              "details": {"type": "string"},
              "error_message": {"type": "string"}
            }
          }
        },
        "coverage": {
          "type": "object",
          "properties": {
            "line_coverage": {"type": "number"},
            "branch_coverage": {"type": "number"},
            "function_coverage": {"type": "number"}
          }
        },
        "issues_found": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "severity": {"type": "string", "enum": ["critical", "high", "medium", "low"]},
              "type": {"type": "string"},
              "description": {"type": "string"},
              "location": {"type": "string"},
              "suggested_fix": {"type": "string"}
            }
          }
        },
        "performance_metrics": {
          "type": "object",
          "properties": {
            "avg_response_time_ms": {"type": "number"},
            "p95_response_time_ms": {"type": "number"},
            "p99_response_time_ms": {"type": "number"},
            "throughput_rps": {"type": "number"},
            "error_rate": {"type": "number"}
          }
        },
        "summary": {
          "type": "object",
          "properties": {
            "total_tests": {"type": "integer"},
            "passed": {"type": "integer"},
            "failed": {"type": "integer"},
            "skipped": {"type": "integer"},
            "pass_rate": {"type": "number"}
          }
        },
        "recommendations": {
          "type": "array",
          "items": {"type": "string"}
        }
      }
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "test_framework": {"type": "string"},
        "confidence_level": {"type": "number"}
      }
    }
  }
}
```