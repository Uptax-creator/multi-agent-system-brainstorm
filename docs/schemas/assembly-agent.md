# Assembly Agent Schema

## Overview

Specialized agent for aggregating results from multiple agents and generating final reports.

## Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Assembly Agent Schema",
  "type": "object",
  "required": ["agent_config", "request", "context"],
  
  "properties": {
    "agent_config": {
      "type": "object",
      "required": ["agent_id", "agent_type", "version"],
      "properties": {
        "agent_id": {
          "type": "string",
          "pattern": "^assembly_[0-9]{3}$"
        },
        "agent_type": {
          "type": "string",
          "const": "assembly"
        },
        "version": {
          "type": "string",
          "pattern": "^1\\.0\\.[0-9]+$"
        },
        "output_formats": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["markdown", "json", "html", "pdf", "executive_summary"]
          }
        }
      }
    },
    
    "request": {
      "type": "object",
      "required": ["agent_outputs", "output_format"],
      "properties": {
        "agent_outputs": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "agent_id": {"type": "string"},
              "agent_type": {"type": "string"},
              "timestamp": {"type": "string", "format": "date-time"},
              "status": {"type": "string"},
              "data": {"type": "object"},
              "confidence_score": {"type": "number"}
            }
          }
        },
        "output_format": {
          "type": "string",
          "enum": ["markdown", "json", "html", "pdf", "executive_summary"]
        },
        "synthesis_rules": {
          "type": "object",
          "properties": {
            "prioritization": {
              "type": "string",
              "enum": ["confidence_based", "timestamp_based", "agent_hierarchy", "custom"]
            },
            "conflict_resolution": {
              "type": "string",
              "enum": ["highest_confidence", "most_recent", "consensus", "all_perspectives"]
            },
            "sections_required": {
              "type": "array",
              "items": {"type": "string"}
            },
            "max_length": {"type": "integer"},
            "include_metadata": {"type": "boolean"}
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
      "required": ["final_report", "summary"],
      "properties": {
        "final_report": {
          "type": "object",
          "properties": {
            "executive_summary": {"type": "string"},
            "sections": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "title": {"type": "string"},
                  "content": {"type": "string"},
                  "source_agents": {"type": "array", "items": {"type": "string"}},
                  "confidence": {"type": "number"}
                }
              }
            },
            "findings": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "finding": {"type": "string"},
                  "evidence": {"type": "array", "items": {"type": "string"}},
                  "confidence": {"type": "number"},
                  "source_agents": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "recommendations": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "recommendation": {"type": "string"},
                  "priority": {"type": "string", "enum": ["critical", "high", "medium", "low"]},
                  "rationale": {"type": "string"},
                  "source_agents": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "next_steps": {
              "type": "array",
              "items": {"type": "string"}
            },
            "appendices": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "title": {"type": "string"},
                  "content": {"type": "string"},
                  "type": {"type": "string"}
                }
              }
            }
          }
        },
        "summary": {
          "type": "string",
          "minLength": 100,
          "maxLength": 500
        },
        "conflicts_resolved": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "issue": {"type": "string"},
              "resolution": {"type": "string"},
              "agents_involved": {"type": "array", "items": {"type": "string"}}
            }
          }
        },
        "metadata": {
          "type": "object",
          "properties": {
            "total_agents": {"type": "integer"},
            "successful_agents": {"type": "integer"},
            "failed_agents": {"type": "integer"},
            "total_processing_time_ms": {"type": "integer"},
            "total_tokens_consumed": {"type": "integer"},
            "overall_confidence": {"type": "number"}
          }
        }
      }
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "synthesis_method": {"type": "string"},
        "confidence_level": {"type": "number"}
      }
    }
  }
}
```

## Example Usage

### Request

```json
{
  "agent_config": {
    "agent_id": "assembly_001",
    "agent_type": "assembly",
    "version": "1.0.0",
    "output_formats": ["markdown", "json"]
  },
  "request": {
    "agent_outputs": [
      {
        "agent_id": "research_001",
        "agent_type": "research",
        "timestamp": "2025-09-06T10:00:00Z",
        "status": "completed",
        "data": { ... },
        "confidence_score": 0.87
      },
      {
        "agent_id": "architect_001",
        "agent_type": "architect",
        "timestamp": "2025-09-06T10:05:00Z",
        "status": "completed",
        "data": { ... },
        "confidence_score": 0.92
      }
    ],
    "output_format": "markdown",
    "synthesis_rules": {
      "prioritization": "confidence_based",
      "conflict_resolution": "highest_confidence",
      "sections_required": ["executive_summary", "findings", "recommendations"],
      "max_length": 5000,
      "include_metadata": true
    }
  },
  "context": {
    "session_id": "550e8400-e29b-41d4-a716-446655440000",
    "user_query": "Original user query"
  }
}
```