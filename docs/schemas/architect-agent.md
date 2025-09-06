# Architect Agent Schema

## Overview

Specialized agent for system design and technical architecture decisions.

## Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Architect Agent Schema",
  "type": "object",
  "required": ["agent_config", "request", "context"],
  
  "properties": {
    "agent_config": {
      "type": "object",
      "required": ["agent_id", "agent_type", "version"],
      "properties": {
        "agent_id": {
          "type": "string",
          "pattern": "^architect_[0-9]{3}$"
        },
        "agent_type": {
          "type": "string",
          "const": "architect"
        },
        "version": {
          "type": "string",
          "pattern": "^1\\.0\\.[0-9]+$"
        },
        "expertise": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["microservices", "serverless", "monolithic", "event-driven", "cloud-native", "distributed"]
          }
        }
      }
    },
    
    "request": {
      "type": "object",
      "required": ["requirements", "constraints"],
      "properties": {
        "requirements": {
          "type": "object",
          "properties": {
            "functional": {
              "type": "array",
              "items": {"type": "string"},
              "minItems": 1
            },
            "non_functional": {
              "type": "array",
              "items": {"type": "string"}
            },
            "user_stories": {
              "type": "array",
              "items": {"type": "string"}
            }
          }
        },
        "constraints": {
          "type": "object",
          "properties": {
            "budget": {
              "type": "object",
              "properties": {
                "amount": {"type": "number"},
                "currency": {"type": "string", "default": "USD"}
              }
            },
            "timeline": {
              "type": "object",
              "properties": {
                "start_date": {"type": "string", "format": "date"},
                "end_date": {"type": "string", "format": "date"},
                "milestones": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "name": {"type": "string"},
                      "date": {"type": "string", "format": "date"}
                    }
                  }
                }
              }
            },
            "technology_stack": {
              "type": "object",
              "properties": {
                "preferred": {"type": "array", "items": {"type": "string"}},
                "avoided": {"type": "array", "items": {"type": "string"}}
              }
            },
            "scalability": {
              "type": "object",
              "properties": {
                "users": {"type": "integer"},
                "requests_per_second": {"type": "integer"},
                "data_volume_gb": {"type": "number"}
              }
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
      "required": ["architecture", "recommendations"],
      "properties": {
        "architecture": {
          "type": "object",
          "properties": {
            "type": {
              "type": "string",
              "enum": ["microservices", "serverless", "monolithic", "hybrid"]
            },
            "components": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {"type": "string"},
                  "type": {"type": "string"},
                  "technology": {"type": "string"},
                  "responsibilities": {"type": "array", "items": {"type": "string"}},
                  "interfaces": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "data_flow": {
              "type": "object",
              "properties": {
                "diagrams": {"type": "array", "items": {"type": "string"}},
                "description": {"type": "string"}
              }
            },
            "infrastructure": {
              "type": "object",
              "properties": {
                "cloud_provider": {"type": "string"},
                "services": {"type": "array", "items": {"type": "string"}},
                "deployment_strategy": {"type": "string"}
              }
            }
          }
        },
        "technology_decisions": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "category": {"type": "string"},
              "chosen": {"type": "string"},
              "alternatives": {"type": "array", "items": {"type": "string"}},
              "rationale": {"type": "string"}
            }
          }
        },
        "recommendations": {
          "type": "array",
          "items": {"type": "string"}
        },
        "risks": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "description": {"type": "string"},
              "impact": {"type": "string", "enum": ["low", "medium", "high"]},
              "mitigation": {"type": "string"}
            }
          }
        }
      }
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "alternatives_considered": {"type": "integer"},
        "confidence_level": {"type": "number"}
      }
    }
  }
}
```