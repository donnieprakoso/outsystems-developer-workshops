---
title: Getting Started with MCP (Model Context Protocol)
description: Extend agents with custom tools using Model Context Protocol
weight: 20
type: docs
layout: single
authors: [donnie]
---

# Getting Started with MCP

Model Context Protocol (MCP) enables you to extend OutSystems agents with custom tools and integrations. This workshop shows you how to build and deploy MCP servers.

## What is MCP?

MCP is a standard protocol for:
- Adding custom tools to agents
- Connecting to any API or service
- Creating domain-specific capabilities
- Building reusable integrations

## Learning Objectives

By the end of this workshop, you'll be able to:

✅ Understand how MCP works  
✅ Build a simple MCP server  
✅ Connect it to an OutSystems agent  
✅ Deploy safely to production  

## Part 1: MCP Basics

### When to Use MCP

Use MCP when:
- Your agent needs a custom tool (not in pre-built connectors)
- You're integrating with a proprietary system
- You need real-time data (not available via connector)
- You want to encapsulate business logic

### MCP Architecture

```
Agent → MCP Protocol → Your Server → External System/API
```

### Example: Custom Pricing Engine

Your agent needs access to a custom pricing engine that:
- Calculates discounts based on customer tier
- Applies seasonal pricing
- Reserves inventory

Build an MCP server as a bridge.

## Part 2: Building an MCP Server

### Prerequisites

- Node.js 16+ or Python 3.8+
- Understanding of REST APIs
- 1 hour

### Step 1: Create Project Structure

```bash
mkdir pricing-mcp
cd pricing-mcp
npm init -y
npm install @modelcontextprotocol/sdk
```

### Step 2: Implement Tools

Define what your agent can do:

```javascript
const server = new MCPServer({
  name: "pricing-service",
  version: "1.0.0"
});

server.tool("get_price", 
  {
    product_id: "string",
    customer_tier: "gold|silver|bronze",
    quantity: "number"
  },
  async (args) => {
    // Your business logic here
    return { price: 99.99, discount: 10 };
  }
);

server.tool("check_inventory",
  { product_id: "string" },
  async (args) => {
    return { available: 50, reserved: 5 };
  }
);
```

### Step 3: Connect to Agent

In OutSystems Agent Workbench:

1. Click **Add Tool**
2. Select **MCP Server**
3. Enter endpoint: `http://your-server:3000`
4. Select tools: `get_price`, `check_inventory`
5. Test with sample data
6. Deploy

## Part 3: Real-World Examples

### Example 1: Legacy System Bridge

Connect to a 20-year-old mainframe system:

```
Agent → MCP Server → REST wrapper → COBOL API
```

The MCP server translates modern queries to legacy protocols.

### Example 2: Real-Time Data

Get live data not available elsewhere:

```
Agent → MCP → Redis cache → Third-party API
```

Agent queries cache through MCP, cache updates every 5 mins.

### Example 3: Complex Calculations

Outsource business logic to specialized service:

```
Agent → MCP → Advanced ML model → Predictions
```

Agent gets predictions without understanding the model.

## Part 4: Best Practices

### Design Principles

1. **Single Responsibility** — one tool = one job
2. **Idempotent** — calling twice = same result as once
3. **Fast** — respond in <1 second
4. **Documented** — describe what each tool does
5. **Testable** — can test without the agent

### Error Handling

Always return structured errors:

```javascript
throw new MCPError({
  code: "INVALID_PRODUCT",
  message: "Product #XYZ not found",
  details: { product_id: "XYZ" }
});
```

Agent can handle specific errors gracefully.

### Security

- Never expose credentials in tools
- Use environment variables for secrets
- Validate all inputs
- Rate limit if needed
- Log tool calls for audit

### Testing MCP Servers

```bash
# Test locally before connecting to agent
curl -X POST http://localhost:3000/tool/get_price \
  -H "Content-Type: application/json" \
  -d '{"product_id": "SKU123", "customer_tier": "gold", "quantity": 5}'

# Expected response:
# {"price": 89.99, "discount": 15}
```

## Part 5: Deployment

### Deploy Your MCP Server

Options:

**Option 1: Docker (Recommended)**
```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "server.js"]
```

Deploy to: AWS ECS, Google Cloud Run, Azure Container Instances

**Option 2: Serverless**
- AWS Lambda
- Google Cloud Functions
- Azure Functions

**Option 3: On-Premises**
- Your data center
- Kubernetes cluster
- Heroku/Render

### Connect to Agent in Production

In OutSystems:

1. Update MCP endpoint to production URL
2. Add authentication (API key, OAuth)
3. Test against sample requests
4. Canary deploy (10% agents use MCP first)
5. Monitor error rates
6. Full rollout if stable

## Part 6: Monitoring & Troubleshooting

### Monitor MCP Health

Track:
- Response time (p50/p95/p99)
- Error rate
- Request volume
- Uptime

### Common Issues

| Problem | Cause | Fix |
|---------|-------|-----|
| Timeout (>5s) | Slow backend | Optimize query, add caching |
| Connection refused | Server down | Check logs, restart |
| Invalid response | Bad formatting | Return valid JSON |
| Auth failure | Wrong credentials | Check env vars |

## Quick Reference

### MCP Tool Template

```javascript
server.tool("tool_name",
  {
    param1: "string",
    param2: "number"
  },
  async (args) => {
    // Validate inputs
    if (!args.param1) throw new Error("param1 required");
    
    // Do work
    const result = await someFunction(args);
    
    // Return structured result
    return { success: true, data: result };
  }
);
```

### Deploy Checklist

- [ ] Code tested locally
- [ ] Environment variables set
- [ ] Secrets in vault (not in code)
- [ ] Error handling implemented
- [ ] Logging configured
- [ ] Rate limiting set
- [ ] Monitoring configured
- [ ] Documentation complete
- [ ] Backup plan in case of failure

---

**Next:** Build your first MCP server in 30 minutes and connect it to an agent.

[View MCP Documentation](https://spec.modelcontextprotocol.io/)
