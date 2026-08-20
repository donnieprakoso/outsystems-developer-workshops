---
title: Getting Started with OutSystems Mentor
description: Learn how to use OutSystems Mentor to build and deploy enterprise-grade agentic workflows
weight: 10
type: docs
layout: single
---

OutSystems Mentor is your AI-powered guide to building enterprise-ready agentic systems. This workshop will walk you through the fundamentals and get you building agents in hours, not weeks.

## What is OutSystems Mentor?

OutSystems Mentor combines:
- **Visual Agent Builder** — drag-and-drop UI, no prompt engineering required
- **Enterprise Context Graph** — grounding AI with your actual systems
- **Agent Evaluations** — automated testing for agent reliability
- **Human-in-the-Loop** — approval workflows built-in
- **Multi-Model Orchestration** — choose the right model for each task

It's designed for teams with no AI expertise to ship production agents in weeks.

---

## Prerequisites

Before starting, you'll need:

- **OutSystems Account** — [Sign up for free](https://www.outsystems.com/Platform/Signup?uc=startfree)
- **Personal Edition or Cloud** — recommended for learning
- **Basic understanding of workflows** — OutSystems low-code experience helpful but not required
- **30 minutes** — for this workshop

---

## Learning Objectives

By the end of this workshop, you'll be able to:

✅ Create your first agent using the visual canvas  
✅ Connect an agent to data and systems  
✅ Write test cases and evaluate agent accuracy  
✅ Implement human-in-the-loop approval workflows  
✅ Deploy an agent to production safely  

---

## Part 1: Agent Basics

### What is an Agent?

An agent is an AI system that:
1. **Observes** — understands a situation (user request, system state)
2. **Reasons** — decides what to do (using your data and context)
3. **Acts** — takes action (reads/writes to systems, calls APIs)
4. **Learns** — improves over time (via your feedback and evaluations)

**Example:** A support ticket agent that:
- Reads: Customer ticket, past interactions, knowledge base
- Reasons: "This is a billing issue, escalate to finance team"
- Acts: Creates task in ITSM system, notifies finance
- Learns: Evaluations show 95% accuracy on billing issues

### Agent vs. Chatbot

| Aspect | Chatbot | Agent |
|--------|---------|-------|
| **Interaction** | Conversation only | Conversation + action |
| **Systems** | Reads info only | Reads and writes |
| **Decision** | Responds to user | Makes decisions independently |
| **Example** | "Here's the status..." | "Your status: X. Escalating now." |

---

## Part 2: Building Your First Agent

### Step 1: Create a New Agent

1. Log into OutSystems Personal Edition or Cloud
2. Navigate to **Agent Workbench**
3. Click **+ New Agent**
4. Name it: **"Support Ticket Triage"**
5. Description: *"Auto-categorize support tickets by severity and route to appropriate team"*

### Step 2: Define Agent Capabilities

Tell your agent what it can do:

```
Agent Name: Support Ticket Triage
Capabilities:
  - Read support tickets
  - Read ticket history
  - Query knowledge base
  - Determine severity (low/medium/high/critical)
  - Route to team (support, billing, engineering)
  - Create task in ITSM system
```

### Step 3: Connect to Data

Use **Enterprise Context Graph** to give your agent visibility:

1. Click **Add Data Source**
2. Select **Support Tickets** (pre-built connector)
3. Configure: *"Read-only access to tickets created in last 30 days"*
4. Click **Add Knowledge Base**
5. Upload: **Support team handbook** (PDF)
6. Agent will query: *"What's the SLA for critical issues?"*

### Step 4: Write the Agent Logic

In the visual canvas:

```
1. INPUT: Receive support ticket
2. REASON: "What's the severity?"
   - Read ticket description
   - Query knowledge base for patterns
   - Assess impact (1 user vs. 1000 users)
3. DECIDE: Route based on severity
   - Critical → Engineering team + VP escalation
   - High → Support manager review
   - Medium → Support team queue
   - Low → Self-service + FAQ recommendation
4. ACT: Create task in ITSM
5. OUTPUT: Confirmation to user
```

**In OutSystems:**
- Drag nodes for each step
- Configure AI prompts (visual editor)
- Define routing rules
- Set escalation conditions

---

## Part 3: Testing & Evaluation

### Why Test Agents?

Agents can be wrong. Test cases help you:
- Verify accuracy before production
- Catch edge cases (angry customer, vague ticket)
- Ensure SLA compliance
- Monitor drift over time

### Create Test Cases

For your Support Ticket Triage agent:

| Input | Expected Output | Importance |
|-------|-----------------|-----------|
| *"System completely down for 500 users"* | Critical → Engineering | High |
| *"Can't remember password"* | Low → FAQ link | High |
| *"Billing charged twice this month"* | High → Billing team | Medium |
| *"Feature request: dark mode"* | Low → Roadmap link | Low |
| *"App crashes when I click Settings"* | High → Engineering | Medium |

### Run Evaluation

1. Click **Evaluate**
2. Run agent against all test cases
3. See results: **4/5 pass (80% accuracy)**
4. Debug failure: *"Password reset"* routed to Engineering instead of FAQ
5. Adjust prompt and re-run

**Target:** 95%+ accuracy before production

---

## Part 4: Human-in-the-Loop

### When to Escalate to Humans?

Not all decisions should be automatic. Define approval rules:

```
Auto-Approve:
  - Low severity tickets → immediate routing
  - Standard routing → no review needed
  
Require Approval:
  - Critical tickets → Engineering VP reviews
  - New ticket categories → human first
  - Unusual routing patterns → security review

Escalate to Specialist:
  - Ambiguous severity → support manager decides
  - Customer angry/urgent → human takes over
  - SLA about to breach → escalate for priority handling
```

### Configure Approval Workflow

In Agent Workbench:

1. Click **Workflow**
2. Define approval routes:
   - **Tier 1 (Low Risk):** Auto-approve
   - **Tier 2 (Medium Risk):** Manager review (SLA: 30 min)
   - **Tier 3 (High Risk):** Director review (SLA: 15 min)
3. Set notifications (Slack, email, Teams)
4. Configure escalation (auto-escalate if SLA breached)

### Human Review UI

When a ticket needs approval, humans see:

```
📋 Ticket: #1024 - "System down"
🤖 Agent Decision: CRITICAL → Engineering Team
📊 Confidence: 92%

Agent Reasoning:
- Keywords detected: "system down", "critical", "500 users"
- SLA: Critical = 1 hour response
- Recommended action: Create P1 incident + VP notification

✅ Approve  |  ❌ Reject  |  🔄 Reassign to: [Dropdown]
```

---

## Part 5: Deployment & Monitoring

### Pre-Production Checklist

Before going live:

- [ ] Test cases pass (95%+ accuracy)
- [ ] Human approval workflows configured
- [ ] Knowledge base up-to-date
- [ ] Escalation paths tested
- [ ] Cost estimates reviewed ($X/month)
- [ ] Compliance audit completed (GDPR, SOC2)
- [ ] Team training completed

### Deploy Safely

Deployment options:

**Option 1: Shadow Mode** (Recommended for new agents)
- Agent runs but doesn't take action
- Humans see recommendations
- Compare agent vs. human decisions
- Run for 1-2 weeks

**Option 2: Canary Deployment**
- Send 10% of tickets to agent
- Monitor accuracy for 1 week
- Increase to 50% if metrics good
- Full rollout if 95%+ accurate

**Option 3: Full Rollout**
- Only for proven agents (weeks of data)
- Keep human override available
- Monitor SLAs closely

### Monitor Agent Health

Dashboard shows:

```
📊 Accuracy: 96.2% (trend: ↑)
⏱️  Avg response: 1.2s (SLA: <2s) ✅
💰 Cost: $120/month (on budget)
👤 Human escalation rate: 4.1% (target: <5%) ✅
📈 Processed: 2,340 tickets this week
⚠️  Failures: 2 (both edge cases)
```

### Alerts

Get notified if:
- Accuracy drops below 90%
- Average response time exceeds SLA
- Cost spikes unexpectedly
- Escalation rate jumps above threshold
- Agent crashes or hangs

---

## Part 6: Real-World Use Cases

### Banking: Loan Origination

**What it does:**
- Customer applies for loan
- Agent gathers documents (income proof, credit check)
- Agent evaluates creditworthiness
- Routes to loan officer if marginal
- Approves automatically if clear

**Time saved:** 5 hours → 15 minutes per application

**Compliance:** Full audit trail for regulatory review

### Insurance: Claims Processing

**What it does:**
- Customer files claim
- Agent auto-categorizes (auto vs. collision vs. theft)
- Agent gathers evidence (photos, police reports)
- Determines if clear approval vs. investigation
- Escalates fraud risks to adjuster

**Time saved:** 3 days → same day for clear cases

**Quality:** Consistent decisions, fewer appeals

### Manufacturing: Supplier Portal

**What it does:**
- Supplier submits PO/invoice
- Agent validates against purchase order
- Agent checks delivery status
- Routes exceptions to procurement
- Updates supplier automatically

**Time saved:** Manual data entry eliminated

**Accuracy:** 99.8% (vs. 94% manual)

---

## Part 7: Best Practices

### Design Principles

1. **Start simple** — one decision, not everything
2. **Test thoroughly** — more test cases = better agent
3. **Escalate early** — when in doubt, ask human
4. **Monitor always** — drift happens, catch it
5. **Iterate fast** — update prompts based on feedback

### Common Mistakes

❌ **Don't:**
- Build agent for 10 different tasks at once (scope creep)
- Skip test cases ("it'll work fine")
- Deploy without human approval workflows
- Ignore escalation patterns (same issues recurring)
- Set and forget (no monitoring)

✅ **Do:**
- Start with 1 decision (severity, category, priority)
- Write 20+ test cases covering edge cases
- Build approval workflow from day one
- Check accuracy weekly, adjust promptly
- Monitor metrics religiously

### Cost Optimization

Save money on inference:

| Approach | Benefit | Trade-off |
|----------|---------|-----------|
| Use Haiku for simple decisions | 80% cheaper | Slightly lower accuracy |
| Batch process non-urgent tickets | 50% savings | Delayed processing |
| Cache knowledge base lookups | 30% savings | Stale data risk |
| Spike to cheaper model during peaks | 20% savings | Quality variance |

### Scaling to 100+ Agents

- Centralize team workspace
- Share connectors and knowledge bases
- Monitor total cost and accuracy trends
- Create approval workflows that handle volume
- Route escalations efficiently

---

## Part 8: Next Steps

### What to Build First?

Pick a workflow that's:
1. **High volume** — 100+ per week (impact)
2. **Repetitive** — same decisions over and over (easy to test)
3. **Low risk** — won't harm customer if wrong (safe to iterate)
4. **Low technical debt** — not tied to legacy systems

**Good first projects:**
- Support ticket triage
- Lead routing in sales
- Invoice validation in finance
- Order routing in ops
- Password reset automation in IT

**Not good first projects:**
- Medical diagnosis (high-risk)
- Fraud detection (complex business rules)
- Hiring decisions (regulatory, bias risk)
- Complete ERP replacement (too broad)

### Training & Resources

- **Interactive tutorial:** 30 min in Agent Workbench
- **Video series:** Building your first agent (YouTube)
- **Partner documentation:** https://partner.outsystems.com/agents
- **Community:** Slack #agents channel
- **Support:** 4-hour SLA for critical issues

### Get Help

- **Technical questions:** partner-support@outsystems.com
- **Implementation help:** Schedule consulting (14 hours free)
- **Co-marketing:** Partner GTM programs available
- **Certification:** OutSystems Agentic Systems Architect

---

## Recap

You now know:

✅ What agents are and why they matter  
✅ How to build one with OutSystems Mentor  
✅ How to test for reliability  
✅ How to keep humans in control  
✅ How to deploy safely and monitor success  
✅ Real-world examples and best practices  

**Next:** Start building! Pick one use case and ship in 2 weeks.

---

## Appendix: Quick Reference

### Common AI Models

| Model | Best For | Cost | Speed |
|-------|----------|------|-------|
| Claude Opus | Complex reasoning, nuance | $$ | Slow |
| Claude Sonnet | Balanced (90% of use cases) | $ | Medium |
| Claude Haiku | Simple decisions, volume | $ | Fast |
| Llama 70B | Open-source, cost-sensitive | $$ | Medium |
| Mistral | European deployments | $ | Fast |

### Key Metrics

- **Accuracy:** % of correct decisions (target: 95%+)
- **Latency:** Response time (target: <2s)
- **Cost:** $ per transaction (monitor for creep)
- **Escalation rate:** % sent to human (target: <5%)
- **SLA compliance:** % within response time (target: 99%+)

### Troubleshooting

| Problem | Cause | Fix |
|---------|-------|-----|
| Low accuracy | Unclear prompt, bad test cases | Rewrite prompt, add examples |
| High cost | Using expensive model | Switch to Haiku for simple tasks |
| Slow responses | Model overloaded, bad query | Add caching, batch non-urgent |
| Frequent escalations | Poor context or ambiguous cases | Add data source, clarify rules |
| Hallucinations | Agent making up facts | Add output validation, fact-check |

---

**Ready to build?** [Sign up for OutSystems Personal Edition](https://www.outsystems.com/personaledition/) and start your first agent in 30 minutes.
