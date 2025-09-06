# Research Agent Schema

## Overview

Specialized agent for web research and information gathering.

## Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Research Agent Schema",
  "description": "Specialized agent for web research and information gathering",
  "type": "object",
  "required": ["agent_config", "request", "context"],
  
  "properties": {
    "agent_config": {
      "type": "object",
      "required": ["agent_id", "agent_type", "version"],
      "properties": {
        "agent_id": {
          "type": "string",
          "pattern": "^research_[0-9]{3}$",
          "description": "Unique identifier for research agent instance"
        },
        "agent_type": {
          "type": "string",
          "const": "research",
          "description": "Agent specialization type"
        },
        "version": {
          "type": "string",
          "pattern": "^1\\.0\\.[0-9]+$"
        },
        "capabilities": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["web_search", "document_analysis", "data_extraction", "sentiment_analysis", "fact_checking"]
          }
        }
      }
    },
    
    "request": {
      "type": "object",
      "required": ["research_objective", "search_parameters"],
      "properties": {
        "research_objective": {
          "type": "string",
          "minLength": 20,
          "maxLength": 500,
          "description": "Clear description of what to research"
        },
        "search_parameters": {
          "type": "object",
          "properties": {
            "keywords": {
              "type": "array",
              "minItems": 1,
              "maxItems": 10,
              "items": {"type": "string"}
            },
            "sources": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": ["web", "news", "academic", "social_media", "documentation", "forums"]
              }
            },
            "date_range": {
              "type": "object",
              "properties": {
                "from": {"type": "string", "format": "date"},
                "to": {"type": "string", "format": "date"}
              }
            },
            "language": {
              "type": "string",
              "default": "en",
              "enum": ["en", "pt", "es", "fr", "de"]
            },
            "max_results": {
              "type": "integer",
              "minimum": 1,
              "maximum": 100,
              "default": 10
            },
            "quality_threshold": {
              "type": "number",
              "minimum": 0.0,
              "maximum": 1.0,
              "default": 0.7
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
      "enum": ["completed", "partial", "failed", "timeout"]
    },
    "data": {
      "type": "object",
      "required": ["findings", "summary"],
      "properties": {
        "findings": {
          "type": "array",
          "items": {
            "type": "object",
            "required": ["title", "content", "source", "relevance_score"],
            "properties": {
              "title": {"type": "string"},
              "content": {"type": "string", "maxLength": 2000},
              "source": {
                "type": "object",
                "properties": {
                  "url": {"type": "string", "format": "uri"},
                  "domain": {"type": "string"},
                  "type": {"type": "string"},
                  "published_date": {"type": "string", "format": "date-time"},
                  "author": {"type": "string"}
                }
              },
              "relevance_score": {
                "type": "number",
                "minimum": 0.0,
                "maximum": 1.0
              },
              "key_points": {
                "type": "array",
                "items": {"type": "string"}
              },
              "entities": {
                "type": "object",
                "properties": {
                  "companies": {"type": "array", "items": {"type": "string"}},
                  "people": {"type": "array", "items": {"type": "string"}},
                  "technologies": {"type": "array", "items": {"type": "string"}},
                  "locations": {"type": "array", "items": {"type": "string"}}
                }
              }
            }
          }
        },
        "summary": {
          "type": "string",
          "minLength": 100,
          "maxLength": 1000
        },
        "insights": {
          "type": "array",
          "items": {"type": "string"}
        },
        "gaps_identified": {
          "type": "array",
          "items": {"type": "string"},
          "description": "Information gaps that need further research"
        }
      }
    },
    "meta": {
      "type": "object",
      "properties": {
        "processing_time_ms": {"type": "integer"},
        "sources_checked": {"type": "integer"},
        "sources_used": {"type": "integer"},
        "tokens_consumed": {"type": "integer"},
        "search_queries": {
          "type": "array",
          "items": {"type": "string"}
        },
        "confidence_level": {
          "type": "number",
          "minimum": 0.0,
          "maximum": 1.0
        }
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
    "agent_id": "research_001",
    "agent_type": "research",
    "version": "1.0.0",
    "capabilities": ["web_search", "document_analysis"]
  },
  "request": {
    "research_objective": "Find and analyze top AI agent companies in USA for 2025",
    "search_parameters": {
      "keywords": ["AI agents", "automation", "USA", "2025"],
      "sources": ["web", "news", "documentation"],
      "language": "en",
      "max_results": 10,
      "quality_threshold": 0.8
    }
  },
  "context": {
    "session_id": "550e8400-e29b-41d4-a716-446655440000",
    "user_query": "What companies are working on AI agents?",
    "iteration": 1
  }
}
```

### Response

```json
{
  "status": "completed",
  "data": {
    "findings": [
      {
        "title": "Anthropic Leading AI Agent Development",
        "content": "Anthropic continues to innovate...",
        "source": {
          "url": "https://example.com/article",
          "domain": "example.com",
          "type": "article",
          "published_date": "2025-09-01T10:00:00Z"
        },
        "relevance_score": 0.95,
        "key_points": [
          "Multi-agent systems",
          "Claude integration"
        ],
        "entities": {
          "companies": ["Anthropic"],
          "technologies": ["Claude", "LLM"]
        }
      }
    ],
    "summary": "Analysis of top 10 AI agent companies...",
    "insights": [
      "Market dominated by 5 major players",
      "Focus shifting to enterprise solutions"
    ],
    "gaps_identified": [
      "Financial data not publicly available",
      "European market needs research"
    ]
  },
  "meta": {
    "processing_time_ms": 15000,
    "sources_checked": 50,
    "sources_used": 10,
    "tokens_consumed": 4500,
    "search_queries": [
      "AI agents USA 2025",
      "automation companies artificial intelligence"
    ],
    "confidence_level": 0.87
  }
}
```