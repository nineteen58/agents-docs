# Sub-Agents and Routing

Learn how to create specialised sub-agents and configure intelligent routing to ensure customers always get the right expert for their needs.

## Understanding Sub-Agents

Sub-agents are specialised AI experts that handle specific types of customer inquiries. They work alongside your main agent to provide more targeted and knowledgeable responses.

### Benefits of Sub-Agents

- **Specialised Knowledge**: Each expert focuses on specific domains
- **Better Accuracy**: More targeted responses for complex topics
- **Improved Efficiency**: Faster resolution of specialised queries
- **Scalable Expertise**: Add new experts as your business grows

## Creating Sub-Agents

### Step 1: Identify Specialisation Areas

Common sub-agent specialisations:

- **Technical Support**: Platform features, integrations, troubleshooting
- **Billing & Accounts**: Payments, subscriptions, invoices
- **Sales**: Product information, pricing, demos
- **Onboarding**: Setup, training, best practices
- **Compliance**: Security, privacy, regulatory questions

### Step 2: Define the Sub-Agent

1. **Navigate to your agent**
2. **Click "Add Sub-Agent"**
3. **Configure basic information**:
   - **Name**: Descriptive name (e.g., "Technical Support Expert")
   - **Description**: Brief description of expertise
   - **When to Use**: Clear criteria for when this expert should be activated

### Step 3: Create Specialised Prompts

Each sub-agent needs a focused prompt that builds on the main agent's foundation:

```markdown
# Personality
You are Alex, a senior technical support specialist with 5 years of 
experience helping customers with WorkflowPro's advanced features.

# Expertise
You specialise in:
- API integrations and webhook configuration
- Data migration and import processes
- Performance optimisation and troubleshooting
- Advanced workflow automation
- Third-party app connections

# When to Use
Handle technical questions about:
- "How do I integrate with..."
- "My data import is failing..."
- "The system is running slowly..."
- "I need to automate..."
- "Can I connect to [third-party app]?"

# Goal
Provide detailed technical solutions and step-by-step guidance for 
complex technical challenges.

# Approach
- Ask clarifying questions to understand the technical context
- Provide specific, actionable solutions
- Include relevant documentation links
- Escalate to engineering team for bugs or feature requests
```

## Routing Configuration

### Automatic Routing

The system uses AI to analyse incoming messages and route them to the most appropriate expert:

1. **Message Analysis**: The system examines the content and context
2. **Expert Matching**: Compares against available experts and their specialisations
3. **Confidence Scoring**: Determines the best match based on confidence levels
4. **Fallback Handling**: Routes to main agent if no expert is appropriate

### Routing Criteria

Define clear criteria for when each sub-agent should be used:

#### Technical Support Expert
```markdown
# When to Use
Route to Technical Support when customers ask about:
- API documentation and integration
- Data import/export processes
- Performance issues or system errors
- Advanced feature configuration
- Third-party integrations
- Webhook setup and troubleshooting

Keywords: API, integration, import, export, error, slow, webhook, 
automation, script, technical, developer
```

#### Billing Specialist
```markdown
# When to Use
Route to Billing when customers ask about:
- Subscription plans and pricing
- Payment methods and billing
- Invoice generation and history
- Refund requests
- Account upgrades or downgrades
- Payment processing issues

Keywords: billing, payment, invoice, subscription, plan, pricing, 
refund, upgrade, downgrade, credit card, payment method
```

#### Sales Expert
```markdown
# When to Use
Route to Sales when customers ask about:
- Product features and capabilities
- Pricing and plan comparisons
- Demo requests
- Enterprise features
- Competitive comparisons
- Implementation timelines

Keywords: demo, pricing, features, enterprise, comparison, 
implementation, timeline, ROI, benefits, capabilities
```

### Routing Examples

Here are examples of how messages get routed:

**Message**: "I'm getting an error when trying to import my CSV file"
**Route**: Technical Support Expert
**Reason**: Technical issue with data import

**Message**: "What's the difference between the Pro and Enterprise plans?"
**Route**: Sales Expert
**Reason**: Product comparison and pricing inquiry

**Message**: "I need to update my payment method"
**Route**: Billing Specialist
**Reason**: Account and payment management

**Message**: "How do I get started with the platform?"
**Route**: Main Agent or Onboarding Expert
**Reason**: General onboarding question

## Advanced Routing Strategies

### Multi-Criteria Routing

Use multiple factors for routing decisions:

```markdown
# Routing Logic
Route to Technical Support if:
- Message contains technical keywords AND
- Customer has technical support access AND
- Issue is not billing-related

Route to Billing if:
- Message is about payments, subscriptions, or invoices OR
- Customer explicitly mentions billing issues

Route to Sales if:
- Customer is not a current subscriber AND
- Message is about features or pricing
```

### Context-Aware Routing

Consider customer context in routing:

```markdown
# Context Considerations
- Customer's subscription level
- Previous conversation history
- Account status and permissions
- Geographic location
- Time of day and business hours
```

### Fallback Strategies

Always have fallback plans:

1. **Main Agent Fallback**: Route to main agent if no expert is appropriate
2. **Human Escalation**: Transfer to human agents for complex issues
3. **Queue Management**: Handle overflow when experts are unavailable

## Testing Routing Logic

### Test Scenarios

Create comprehensive test scenarios:

1. **Clear Routing**: Messages that should clearly go to specific experts
2. **Ambiguous Cases**: Messages that could go to multiple experts
3. **Edge Cases**: Unusual or complex routing scenarios
4. **Fallback Cases**: Messages that should go to main agent

### Routing Validation

Test your routing with these message types:

**Technical Support Test Messages**:
- "My API calls are returning 500 errors"
- "How do I set up webhooks for my integration?"
- "The data import process is failing"

**Billing Test Messages**:
- "I need to change my payment method"
- "Can you explain the charges on my invoice?"
- "I want to upgrade to the Enterprise plan"

**Sales Test Messages**:
- "What features are included in the Pro plan?"
- "Can I schedule a demo for next week?"
- "How does your platform compare to [competitor]?"

**Ambiguous Test Messages**:
- "I'm having trouble with my account" (could be technical or billing)
- "I need help with the platform" (could be any expert)
- "Something isn't working" (needs clarification)

## Monitoring and Optimisation

### Routing Analytics

Monitor routing performance:

- **Routing Accuracy**: Percentage of messages routed correctly
- **Expert Utilisation**: How often each expert is used
- **Fallback Rate**: How often messages fall back to main agent
- **Customer Satisfaction**: Satisfaction scores by expert type

### Continuous Improvement

Regularly review and optimise routing:

1. **Analyse Misrouted Messages**: Identify patterns in incorrect routing
2. **Refine Criteria**: Update "when to use" descriptions
3. **Add New Experts**: Create experts for emerging needs
4. **Test Changes**: Validate routing improvements

### Common Routing Issues

**Over-Routing**: Too many messages going to sub-agents
- **Solution**: Tighten routing criteria, improve main agent capabilities

**Under-Routing**: Too many messages going to main agent
- **Solution**: Expand sub-agent specialisations, improve routing criteria

**Misrouting**: Messages going to wrong experts
- **Solution**: Refine criteria, add more specific keywords

## Best Practices

### Expert Design

- **Clear Specialisation**: Each expert should have a distinct, well-defined role
- **Complementary Skills**: Experts should complement rather than overlap
- **Appropriate Scope**: Not too narrow (underused) or too broad (overwhelmed)

### Routing Criteria

- **Specific Keywords**: Use clear, specific terms for routing
- **Context Awareness**: Consider customer history and account status
- **Regular Updates**: Keep routing criteria current with business changes

### Performance Monitoring

- **Track Metrics**: Monitor routing accuracy and expert utilisation
- **Customer Feedback**: Use satisfaction scores to validate routing
- **Regular Reviews**: Schedule periodic routing optimisation sessions

## Troubleshooting

### Common Issues

**Sub-Agent Not Being Used**
- Check routing criteria specificity
- Verify keywords are present in test messages
- Review confidence thresholds

**Incorrect Routing**
- Refine "when to use" descriptions
- Add more specific keywords
- Test with edge cases

**Poor Performance**
- Review expert prompt quality
- Check model configuration
- Validate tool integrations
