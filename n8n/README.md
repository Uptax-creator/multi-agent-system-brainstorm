# n8n Workflows

## Overview

This directory contains all n8n workflow files for the multi-agent system.

## Workflow Structure

```
/n8n
├── main-workflow.json       # Main orchestrator workflow
├── agents/
│   ├── lead-agent.json
│   ├── research-agent.json
│   ├── architect-agent.json
│   ├── ux-ui-agent.json
│   ├── test-agent.json
│   └── assembly-agent.json
├── utils/
│   ├── context-handler.json
│   ├── error-handler.json
│   └── memory-manager.json
└── tests/
    ├── test-single-agent.json
    └── test-full-flow.json
```

## Setup Instructions

### 1. Prerequisites

- n8n v1.0+ installed
- LLM API credentials
- Redis (optional for production)

### 2. Import Workflows

1. Open n8n interface
2. Go to Workflows > Import
3. Upload JSON files in this order:
   - utils/*.json
   - agents/*.json
   - main-workflow.json

### 3. Configure Credentials

1. Go to Credentials
2. Add LLM provider (Claude/OpenAI)
3. Configure Redis (if using)
4. Set webhook URLs

### 4. Environment Variables

```env
LLM_API_KEY=your_api_key
REDIS_URL=redis://localhost:6379
WEBHOOK_BASE_URL=https://your-domain.com
MAX_PARALLEL_AGENTS=5
AGENT_TIMEOUT_SECONDS=180
```

## Key Nodes Configuration

### Webhook Trigger
```json
{
  "path": "multi-agent",
  "method": "POST",
  "responseMode": "onReceived"
}
```

### Structured Output Parser
```json
{
  "schema": "{{$json.schema}}",
  "mode": "strict"
}
```

### LLM Chain
```json
{
  "model": "claude-3-opus",
  "temperature": 0.7,
  "maxTokens": 4000
}
```

## Testing

### Test Single Agent
```bash
curl -X POST http://localhost:5678/webhook/multi-agent/test \
  -H "Content-Type: application/json" \
  -d @tests/single-agent-request.json
```

### Test Full Flow
```bash
curl -X POST http://localhost:5678/webhook/multi-agent \
  -H "Content-Type: application/json" \
  -d @tests/full-flow-request.json
```

## Monitoring

- Check execution history in n8n UI
- Monitor Redis for memory usage
- Track API token consumption
- Review error logs

## Troubleshooting

### Common Issues

1. **Schema Validation Errors**
   - Check JSON schema format
   - Validate with online tool
   - Review error logs

2. **Agent Timeout**
   - Increase timeout setting
   - Optimize prompt
   - Check API limits

3. **Memory Issues**
   - Clear Redis cache
   - Reduce context size
   - Implement cleanup

## Production Deployment

1. Use environment variables
2. Enable Redis persistence
3. Set up monitoring
4. Configure rate limiting
5. Implement error recovery

## Support

For issues or questions:
- Check documentation
- Review test cases
- Open GitHub issue