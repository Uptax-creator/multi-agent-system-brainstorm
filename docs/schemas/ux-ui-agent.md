# UX/UI Agent Schema

## Overview

Specialized agent for user interface design and user experience optimization.

## Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "UX/UI Agent Schema",
  "type": "object",
  "required": ["agent_config", "request", "context"],
  
  "properties": {
    "agent_config": {
      "type": "object",
      "required": ["agent_id", "agent_type", "version"],
      "properties": {
        "agent_id": {
          "type": "string",
          "pattern": "^ux_ui_[0-9]{3}$"
        },
        "agent_type": {
          "type": "string",
          "const": "ux_ui"
        },
        "version": {
          "type": "string",
          "pattern": "^1\\.0\\.[0-9]+$"
        },
        "specializations": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["web", "mobile", "desktop", "responsive", "accessibility", "design_systems"]
          }
        }
      }
    },
    
    "request": {
      "type": "object",
      "required": ["project_type", "requirements"],
      "properties": {
        "project_type": {
          "type": "string",
          "enum": ["website", "mobile_app", "web_app", "dashboard", "landing_page"]
        },
        "requirements": {
          "type": "object",
          "properties": {
            "user_personas": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {"type": "string"},
                  "age_range": {"type": "string"},
                  "tech_savvy": {"type": "string", "enum": ["low", "medium", "high"]},
                  "goals": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "features": {
              "type": "array",
              "items": {"type": "string"}
            },
            "brand_guidelines": {
              "type": "object",
              "properties": {
                "colors": {"type": "array", "items": {"type": "string"}},
                "fonts": {"type": "array", "items": {"type": "string"}},
                "style": {"type": "string"},
                "tone": {"type": "string"}
              }
            },
            "platforms": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": ["ios", "android", "web", "desktop_windows", "desktop_mac", "desktop_linux"]
              }
            },
            "accessibility_level": {
              "type": "string",
              "enum": ["WCAG_A", "WCAG_AA", "WCAG_AAA"]
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
      "required": ["design", "recommendations"],
      "properties": {
        "design": {
          "type": "object",
          "properties": {
            "wireframes": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {"type": "string"},
                  "type": {"type": "string"},
                  "description": {"type": "string"},
                  "url": {"type": "string", "format": "uri"}
                }
              }
            },
            "user_flows": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {"type": "string"},
                  "steps": {"type": "array", "items": {"type": "string"}},
                  "decision_points": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "components": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "name": {"type": "string"},
                  "type": {"type": "string"},
                  "properties": {"type": "object"},
                  "variations": {"type": "array", "items": {"type": "string"}}
                }
              }
            },
            "design_system": {
              "type": "object",
              "properties": {
                "colors": {"type": "object"},
                "typography": {"type": "object"},
                "spacing": {"type": "object"},
                "components": {"type": "array", "items": {"type": "string"}}
              }
            }
          }
        },
        "accessibility": {
          "type": "object",
          "properties": {
            "compliance_level": {"type": "string"},
            "features": {"type": "array", "items": {"type": "string"}},
            "testing_notes": {"type": "string"}
          }
        },
        "recommendations": {
          "type": "array",
          "items": {"type": "string"}
        },
        "usability_notes": {
          "type": "array",
          "items": {"type": "string"}
        }
      }
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "iterations": {"type": "integer"},
        "confidence_level": {"type": "number"}
      }
    }
  }
}
```