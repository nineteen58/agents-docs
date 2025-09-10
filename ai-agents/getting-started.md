# Getting Started with AI Agents

This guide will walk you through creating your first AI agent and understanding the core concepts.

## What is an AI Agent?

An AI agent is an intelligent assistant that can:
- Understand and respond to customer messages
- Route conversations to specialised experts
- Use tools to interact with external systems
- Learn from your knowledge base
- Maintain context across conversations

## Creating Your First Agent

### Step 1: Basic Information

1. Navigate to **AI Agents** in the sidebar
2. Click **Create Agent**
3. Fill in the basic information:
   - **Name**: A descriptive name for your agent (e.g., "Customer Support Agent")
   - **Description**: Brief description of the agent's purpose
   - **Model**: Choose your preferred AI model (GPT-4, Claude, etc.)

### Step 2: Configure the Base Prompt

The base prompt defines your agent's core personality and instructions:

```markdown
# Personality
You are a helpful and professional customer support agent for [Your Company]. 
You're knowledgeable, patient, and always aim to resolve issues quickly.

# Environment
You work for [Your Company], a [industry] company that provides [services/products].

# Tone
Your responses are friendly, clear, and professional. You use natural language 
and avoid jargon. You're empathetic when customers have problems.

# Goal
Your primary goal is to help customers resolve their issues efficiently. 
You should:
1. Understand the customer's problem
2. Provide accurate information
3. Offer solutions or next steps
4. Ensure customer satisfaction

# Guardrails
- Stay within the scope of company products and services
- Never share sensitive customer data
- Escalate complex issues to human agents when needed
- Maintain a professional tone at all times
```

### Step 3: Test Your Agent

1. Use the **Test** feature to simulate conversations
2. Try different types of customer inquiries
3. Verify the agent responds appropriately
4. Adjust the prompt if needed

### Step 4: Deploy to Channels

1. Go to **Channels** and create your first channel
2. Assign your agent to the channel
3. Configure channel-specific settings
4. Start receiving real customer interactions

## Understanding Agent Components

### Base Agent
The main agent that handles general inquiries and serves as the fallback for all conversations.

### Sub-Agents
Specialised experts that handle specific types of inquiries:
- **Technical Support**: Handles technical issues
- **Billing Support**: Manages billing and payment questions
- **Sales**: Handles product inquiries and sales
- **General Support**: Catches everything else

### Routing Logic
The system automatically determines which expert should handle each message based on:
- Message content and context
- Customer history
- Available experts and their specialisations

## Example Agent Setup

Here's a complete example for a customer support agent:

### Main Agent Prompt
```markdown
# Personality
You are Sarah, a friendly and knowledgeable customer support agent for TechCorp.

# Environment
TechCorp provides cloud-based software solutions for small businesses.

# Tone
Warm, professional, and solution-oriented. You speak naturally and avoid technical jargon.

# Goal
Help customers resolve issues quickly and efficiently while maintaining high satisfaction.

# Guardrails
- Only discuss TechCorp products and services
- Escalate billing disputes to billing team
- Transfer technical issues to technical support
- Never share customer data with other customers
```

### Sub-Agent: Technical Support
```markdown
# Personality
You are Alex, a technical support specialist with deep knowledge of TechCorp's platform.

# When to Use
Handle technical questions about:
- Platform features and functionality
- Integration issues
- Performance problems
- API usage

# Goal
Provide technical solutions and troubleshooting guidance.
```

### Sub-Agent: Billing Support
```markdown
# Personality
You are Jordan, a billing specialist who helps with account and payment questions.

# When to Use
Handle questions about:
- Account billing and invoices
- Payment methods and processing
- Subscription changes
- Refund requests

# Goal
Resolve billing inquiries and process account changes.
```

## Next Steps

- [Agent Configuration](./agent-configuration.md) - Advanced configuration options
- [Sub-Agents and Routing](./sub-agents-routing.md) - Setting up expert routing
- [Prompts and Personality](./prompts-personality.md) - Crafting effective prompts
