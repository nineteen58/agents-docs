# Evaluations

Evaluations are a critical component of the platform that enable you to systematically assess and improve your AI agents' performance. They provide structured criteria for measuring conversation outcomes, extracting valuable data, and continuously optimising agent behaviour.

## Table of Contents

- [Overview](#overview)
- [Evaluation Types](#evaluation-types)
- [Creating Evaluations](#creating-evaluations)
- [Evaluation Criteria](#evaluation-criteria)
- [Data Extraction Schemas](#data-extraction-schemas)
- [Managing Evaluations](#managing-evaluations)
- [Using Evaluations with Agents](#using-evaluations-with-agents)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Overview

### What are Evaluations?

Evaluations are structured assessment frameworks that:

- **Measure Performance**: Assess how well agents handle conversations
- **Extract Data**: Capture structured information from interactions
- **Provide Feedback**: Generate insights for continuous improvement
- **Ensure Quality**: Maintain consistent standards across all agents

### Key Benefits

- **Objective Assessment**: Standardised criteria for measuring agent performance
- **Data Extraction**: Structured capture of conversation insights and outcomes
- **Continuous Improvement**: Regular evaluation helps identify areas for enhancement
- **Quality Assurance**: Ensure agents meet your organisation's standards
- **Compliance**: Track adherence to policies and procedures

## Evaluation Types

The platform supports four main evaluation outcomes:

### 🎯 Success
**Definition**: The agent achieved the prompt-defined objective

**Indicators**:
- Aligns with the Goal section and fulfils the objective as specified
- Adheres to Tone and Environment guidance while interacting
- Uses Tools per the Tools section and interprets outputs correctly
- Provides a clear resolution statement consistent with the system prompt's style

### ✅ Complete
**Definition**: The conversation reached a natural conclusion per the system prompt

**Indicators**:
- The prompt-defined objective is satisfied or explicitly declined/redirected as guided
- Closing behaviour matches the system prompt's expectations
- No unresolved follow-ups remain according to the system prompt's flow
- Tone and structure remain consistent with the system prompt

### ⚠️ Incomplete
**Definition**: The conversation was cut off and did not end naturally per the prompt

**Indicators**:
- The exchange ends before meeting the Goal section's completion signals
- Required clarifications or steps are interrupted or missing
- No summary, confirmation, or close-out as described in the prompt
- Final turn leaves outcome ambiguous relative to the prompt's objective

### ❌ Agent Error
**Definition**: The agent strayed outside the system prompt's Guardrails

**Examples**:
- Shares disallowed content or unsafe instructions forbidden by Guardrails
- Makes unsupported claims or hallucinates facts/capabilities
- Ignores constraints/policies defined in the system prompt
- Uses tools in ways not permitted or without required confirmations

## Creating Evaluations

### Step 1: Basic Information

1. Navigate to **Resources** → **Evaluations** → **Create Evaluation**
2. Enter the evaluation name and description
3. Provide context about what this evaluation measures

**Example**:
```
Name: Customer Support Quality Assessment
Description: Evaluates customer support conversations for resolution quality, tone, and compliance
```

### Step 2: Define Evaluation Criteria

For each evaluation type (Success, Complete, Incomplete, Agent Error), specify:

#### Evaluation Description
Define what constitutes each outcome type:

**Success Criteria Example**:
```
Success means the agent achieved the prompt-defined objective.

Checklist (based on the system prompt):
- Aligns with the Goal section and fulfills the objective as specified
- Adheres to Tone and Environment guidance while interacting
- Uses Tools per the Tools section and interprets outputs correctly
- Provides a clear resolution statement consistent with the system prompt's style
```

#### Tools Called (Optional)
Specify which tools should be called for each outcome type:

- **Custom Tools**: Select from your organisation's custom tools
- **MCP Tools**: Choose from available MCP server tools
- **Tool Expectations**: Define which tools should be used for each outcome

### Step 3: Data Extraction Schema

Define a JSON schema for extracting structured data from conversations:

#### Sample Schema
```json
{
  "type": "object",
  "properties": {
    "taskOutcome": {
      "type": "string",
      "description": "One-line summary of the task outcome"
    },
    "confidence": {
      "type": "number",
      "minimum": 0,
      "maximum": 1,
      "description": "Model-assessed confidence in the outcome"
    },
    "usedTools": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Names/IDs of tools used"
    },
    "keyFindings": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Important facts or data extracted"
    },
    "followUps": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Recommended next actions, if any"
    }
  },
  "required": ["taskOutcome", "usedTools"]
}
```

#### Schema Builder
Use the built-in JSON schema builder to:
- Create complex nested schemas
- Define data types and constraints
- Set required and optional fields
- Add descriptions for each field

## Evaluation Criteria

### Success Criteria

Define what constitutes a successful conversation outcome:

**Key Elements**:
- **Objective Achievement**: Did the agent meet the stated goal?
- **Tone Compliance**: Did the agent maintain appropriate tone?
- **Tool Usage**: Were the correct tools used effectively?
- **Resolution Quality**: Was the issue resolved satisfactorily?

**Example Success Criteria**:
```
Success means the customer's issue was resolved and they expressed satisfaction.

Requirements:
- Customer's primary concern was addressed
- Appropriate tools were used to gather information
- Solution was clearly explained
- Customer confirmed understanding and satisfaction
- Conversation ended with appropriate closing
```

### Complete Criteria

Define what constitutes a complete conversation:

**Key Elements**:
- **Natural Conclusion**: Did the conversation end naturally?
- **Closure**: Was proper closure provided?
- **Follow-up**: Were next steps clearly communicated?
- **Consistency**: Did the agent maintain consistent behaviour?

### Incomplete Criteria

Define what constitutes an incomplete conversation:

**Key Elements**:
- **Premature Ending**: Was the conversation cut off?
- **Missing Information**: Were required details not gathered?
- **Unresolved Issues**: Were problems left unaddressed?
- **Ambiguous Outcome**: Was the result unclear?

### Agent Error Criteria

Define what constitutes an agent error:

**Key Elements**:
- **Policy Violation**: Did the agent violate established policies?
- **Inappropriate Content**: Was inappropriate content shared?
- **Tool Misuse**: Were tools used incorrectly?
- **Hallucination**: Did the agent make false claims?

## Data Extraction Schemas

### Purpose

Data extraction schemas enable you to:
- **Capture Insights**: Extract structured data from conversations
- **Track Metrics**: Monitor key performance indicators
- **Generate Reports**: Create automated reporting
- **Improve Agents**: Use data to enhance agent performance

### Schema Design

#### Basic Structure
```json
{
  "type": "object",
  "properties": {
    "fieldName": {
      "type": "string",
      "description": "What this field captures"
    }
  }
}
```

#### Advanced Features
- **Nested Objects**: Create complex data structures
- **Arrays**: Capture lists of items
- **Enums**: Restrict values to specific options
- **Constraints**: Set minimum/maximum values
- **Required Fields**: Specify mandatory data points

#### Common Use Cases

**Customer Support Evaluation**:
```json
{
  "type": "object",
  "properties": {
    "issueType": {
      "type": "string",
      "enum": ["technical", "billing", "account", "product", "other"]
    },
    "resolutionTime": {
      "type": "number",
      "description": "Time to resolution in minutes"
    },
    "customerSatisfaction": {
      "type": "string",
      "enum": ["very_satisfied", "satisfied", "neutral", "dissatisfied", "very_dissatisfied"]
    },
    "escalationRequired": {
      "type": "boolean"
    },
    "toolsUsed": {
      "type": "array",
      "items": { "type": "string" }
    }
  }
}
```

**Sales Evaluation**:
```json
{
  "type": "object",
  "properties": {
    "leadQuality": {
      "type": "string",
      "enum": ["hot", "warm", "cold"]
    },
    "interestLevel": {
      "type": "number",
      "minimum": 1,
      "maximum": 10
    },
    "nextSteps": {
      "type": "array",
      "items": { "type": "string" }
    },
    "objections": {
      "type": "array",
      "items": { "type": "string" }
    },
    "followUpDate": {
      "type": "string",
      "format": "date"
    }
  }
}
```

## Managing Evaluations

### Evaluation List

Access all evaluations from **Resources** → **Evaluations**:

**Features**:
- **Search**: Find evaluations by name or description
- **Sort**: Order by creation date
- **View Details**: Click to see full evaluation configuration
- **Edit**: Modify existing evaluations
- **Delete**: Remove unused evaluations

### Editing Evaluations

1. Navigate to the evaluation details page
2. Click **Edit Evaluation**
3. Modify criteria, schemas, or basic information
4. Save changes

**Note**: Changes to evaluations affect all agents using them.

### Evaluation Details

View comprehensive evaluation information:

**Basic Info Tab**:
- Name and description
- Creation date
- Last modified

**Criteria Tab**:
- Success criteria and tool expectations
- Complete criteria and tool expectations
- Incomplete criteria and tool expectations
- Agent error criteria and tool expectations

**Data Schema Tab**:
- JSON schema definition
- Schema builder interface
- Sample data structure

## Using Evaluations with Agents

### Agent Assignment

1. Navigate to **AI Agents** → Select Agent → **Configuration**
2. Choose an evaluation from the dropdown
3. Save the configuration

### Evaluation Process

When an agent uses an evaluation:

1. **Conversation Completion**: Agent finishes the conversation
2. **Automatic Evaluation**: System runs the evaluation criteria
3. **Data Extraction**: Structured data is extracted using the schema
4. **Outcome Classification**: Conversation is classified as Success/Complete/Incomplete/Agent Error
5. **Results Storage**: Evaluation results are stored for analysis

### Evaluation Results

Access evaluation results through:

- **Interactions Page**: View evaluation outcomes for individual conversations
- **Analytics Dashboard**: See aggregated evaluation metrics
- **Reports**: Generate evaluation performance reports

## Best Practices

### Evaluation Design

#### Clear Criteria
- **Specific**: Define precise, measurable criteria
- **Objective**: Avoid subjective or ambiguous language
- **Comprehensive**: Cover all important aspects of performance
- **Realistic**: Set achievable standards

#### Tool Integration
- **Relevant Tools**: Only specify tools that should actually be used
- **Tool Context**: Consider when and why tools should be called
- **Tool Validation**: Ensure tools are properly configured and available

### Schema Design

#### Structured Data
- **Meaningful Fields**: Capture data that provides actionable insights
- **Appropriate Types**: Use correct data types for each field
- **Clear Descriptions**: Provide helpful descriptions for each field
- **Validation**: Include constraints to ensure data quality

#### Performance Considerations
- **Efficient Extraction**: Design schemas that are easy to process
- **Relevant Data**: Only extract data that will be used
- **Consistent Structure**: Maintain consistent schema across evaluations

### Implementation

#### Gradual Rollout
- **Start Simple**: Begin with basic evaluations and add complexity
- **Test Thoroughly**: Validate evaluations with sample conversations
- **Monitor Results**: Track evaluation outcomes and adjust as needed
- **Iterate**: Continuously improve based on results

#### Team Training
- **Evaluation Purpose**: Ensure team understands evaluation goals
- **Criteria Interpretation**: Train team on how to interpret results
- **Action Planning**: Develop processes for acting on evaluation insights

## Troubleshooting

### Common Issues

#### Evaluation Not Running
**Symptoms**: Conversations not being evaluated
**Solutions**:
- Verify evaluation is assigned to the agent
- Check that the agent is properly configured
- Ensure evaluation criteria are complete
- Review system logs for errors

#### Incorrect Classifications
**Symptoms**: Conversations classified incorrectly
**Solutions**:
- Review and refine evaluation criteria
- Check for ambiguous or conflicting criteria
- Validate tool expectations
- Test with sample conversations

#### Schema Validation Errors
**Symptoms**: Data extraction failing
**Solutions**:
- Validate JSON schema syntax
- Check field types and constraints
- Ensure required fields are properly defined
- Test schema with sample data

#### Performance Issues
**Symptoms**: Slow evaluation processing
**Solutions**:
- Simplify complex schemas
- Reduce number of required fields
- Optimise criteria descriptions
- Monitor system resources

### Debugging Steps

1. **Check Configuration**: Verify evaluation is properly assigned
2. **Review Criteria**: Ensure criteria are clear and complete
3. **Test Schema**: Validate JSON schema syntax and structure
4. **Sample Testing**: Test with known conversation examples
5. **Monitor Logs**: Check system logs for error messages
6. **Iterate**: Make adjustments based on test results

### Getting Help

If you encounter issues:

1. **Review Documentation**: Check this guide for solutions
2. **Test with Samples**: Use sample conversations to validate setup
3. **Check System Status**: Ensure all systems are operational
4. **Contact Support**: Reach out for assistance with complex issues

---

**Next Steps**: Learn how to create your first evaluation with the [Evaluation Creation Guide](#creating-evaluations) or explore [Agent Configuration](../ai-agents/agent-configuration.md) to assign evaluations to your agents.
