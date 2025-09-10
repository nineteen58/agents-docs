# Custom Tools

Custom tools allow you to create HTTP-based integrations that connect your AI agents to external APIs, databases, and services. These tools enable your agents to perform actions, retrieve data, and interact with your business systems.

## Overview

Custom tools are HTTP-based integrations that:
- **Make API Calls**: Send requests to external services
- **Process Data**: Transform and validate information
- **Handle Authentication**: Manage API keys and tokens
- **Provide Error Handling**: Graceful failure management
- **Enable Actions**: Perform operations on external systems

## Creating Custom Tools

### Step 1: Define Tool Purpose

Before creating a tool, clearly define:
- **What it does**: Specific functionality and purpose
- **When to use**: Triggers and use cases
- **Input required**: Parameters and data needed
- **Output expected**: Response format and data
- **Error scenarios**: How to handle failures

### Step 2: Configure Tool Settings

1. Navigate to **Resources** → **Tools**
2. Click **Create Tool**
3. Fill in the basic information:

```json
{
  "name": "Customer Lookup",
  "description": "Retrieve customer information from CRM",
  "method": "GET",
  "endpoint": "https://api.crm.com/customers/{customer_id}",
  "headers": {
    "Authorization": "Bearer {api_key}",
    "Content-Type": "application/json"
  }
}
```

### Step 3: Define Parameters

Configure input parameters for your tool:

```json
{
  "parameters": {
    "customer_id": {
      "type": "string",
      "description": "Customer ID to lookup",
      "required": true
    },
    "include_history": {
      "type": "boolean",
      "description": "Include customer history",
      "required": false,
      "default": false
    }
  }
}
```

### Step 4: Configure Response Handling

Define how to process the API response:

```json
{
  "response_handling": {
    "success_format": "json",
    "error_handling": "graceful",
    "timeout": 30,
    "retry_attempts": 3
  }
}
```

## Tool Configuration Options

### HTTP Methods

**GET**: Retrieve data from external systems
```json
{
  "method": "GET",
  "endpoint": "https://api.example.com/data/{id}",
  "description": "Retrieve information by ID"
}
```

**POST**: Create new records or send data
```json
{
  "method": "POST",
  "endpoint": "https://api.example.com/create",
  "body": {
    "name": "{customer_name}",
    "email": "{customer_email}"
  }
}
```

**PUT**: Update existing records
```json
{
  "method": "PUT",
  "endpoint": "https://api.example.com/update/{id}",
  "body": {
    "status": "{new_status}",
    "notes": "{update_notes}"
  }
}
```

**DELETE**: Remove records or data
```json
{
  "method": "DELETE",
  "endpoint": "https://api.example.com/delete/{id}",
  "description": "Remove record by ID"
}
```

### Authentication Methods

**API Key Authentication**:
```json
{
  "headers": {
    "Authorization": "Bearer {api_key}",
    "X-API-Key": "{api_key}"
  }
}
```

**Basic Authentication**:
```json
{
  "headers": {
    "Authorization": "Basic {base64_credentials}"
  }
}
```

**Custom Headers**:
```json
{
  "headers": {
    "X-Custom-Header": "{custom_value}",
    "Content-Type": "application/json"
  }
}
```

### Parameter Types

**String Parameters**:
```json
{
  "customer_name": {
    "type": "string",
    "description": "Customer's full name",
    "required": true,
    "validation": {
      "min_length": 2,
      "max_length": 100
    }
  }
}
```

**Number Parameters**:
```json
{
  "order_amount": {
    "type": "number",
    "description": "Order total amount",
    "required": true,
    "validation": {
      "min": 0,
      "max": 10000
    }
  }
}
```

**Boolean Parameters**:
```json
{
  "include_details": {
    "type": "boolean",
    "description": "Include detailed information",
    "required": false,
    "default": false
  }
}
```

**Array Parameters**:
```json
{
  "product_ids": {
    "type": "array",
    "description": "List of product IDs",
    "required": true,
    "item_type": "string"
  }
}
```

## Common Tool Examples

### Customer Management Tools

**Customer Lookup**:
```json
{
  "name": "Customer Lookup",
  "description": "Retrieve customer information by ID or email",
  "method": "GET",
  "endpoint": "https://api.crm.com/customers",
  "parameters": {
    "customer_id": {
      "type": "string",
      "description": "Customer ID",
      "required": false
    },
    "email": {
      "type": "string",
      "description": "Customer email",
      "required": false
    }
  },
  "headers": {
    "Authorization": "Bearer {crm_api_key}"
  }
}
```

**Create Customer**:
```json
{
  "name": "Create Customer",
  "description": "Create a new customer record",
  "method": "POST",
  "endpoint": "https://api.crm.com/customers",
  "body": {
    "name": "{customer_name}",
    "email": "{customer_email}",
    "phone": "{customer_phone}",
    "company": "{company_name}"
  },
  "headers": {
    "Authorization": "Bearer {crm_api_key}",
    "Content-Type": "application/json"
  }
}
```

### Order Management Tools

**Order Status Check**:
```json
{
  "name": "Order Status Check",
  "description": "Check the status of an order",
  "method": "GET",
  "endpoint": "https://api.orders.com/orders/{order_id}",
  "parameters": {
    "order_id": {
      "type": "string",
      "description": "Order ID to check",
      "required": true
    }
  },
  "headers": {
    "Authorization": "Bearer {orders_api_key}"
  }
}
```

**Update Order Status**:
```json
{
  "name": "Update Order Status",
  "description": "Update the status of an order",
  "method": "PUT",
  "endpoint": "https://api.orders.com/orders/{order_id}",
  "parameters": {
    "order_id": {
      "type": "string",
      "description": "Order ID to update",
      "required": true
    },
    "status": {
      "type": "string",
      "description": "New order status",
      "required": true,
      "enum": ["pending", "processing", "shipped", "delivered", "cancelled"]
    }
  },
  "body": {
    "status": "{status}",
    "notes": "{update_notes}"
  },
  "headers": {
    "Authorization": "Bearer {orders_api_key}",
    "Content-Type": "application/json"
  }
}
```

### Communication Tools

**Send Email**:
```json
{
  "name": "Send Email",
  "description": "Send an email to a customer",
  "method": "POST",
  "endpoint": "https://api.email.com/send",
  "body": {
    "to": "{recipient_email}",
    "subject": "{email_subject}",
    "body": "{email_body}",
    "template": "{email_template}"
  },
  "headers": {
    "Authorization": "Bearer {email_api_key}",
    "Content-Type": "application/json"
  }
}
```

**Send SMS**:
```json
{
  "name": "Send SMS",
  "description": "Send an SMS message",
  "method": "POST",
  "endpoint": "https://api.sms.com/send",
  "body": {
    "to": "{phone_number}",
    "message": "{sms_message}",
    "from": "{sender_id}"
  },
  "headers": {
    "Authorization": "Bearer {sms_api_key}",
    "Content-Type": "application/json"
  }
}
```

## Error Handling

### Response Validation

**Success Response**:
```json
{
  "status": "success",
  "data": {
    "customer_id": "12345",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

**Error Response**:
```json
{
  "status": "error",
  "error": {
    "code": "CUSTOMER_NOT_FOUND",
    "message": "Customer with ID 12345 not found"
  }
}
```

### Error Handling Configuration

```json
{
  "error_handling": {
    "timeout": 30,
    "retry_attempts": 3,
    "retry_delay": 1000,
    "fallback_response": "I'm sorry, I'm having trouble accessing that information right now. Please try again later or contact support."
  }
}
```

### Common Error Scenarios

**Network Timeout**:
- Implement retry logic
- Provide fallback responses
- Log timeout occurrences
- Monitor network performance

**Authentication Failure**:
- Verify API credentials
- Check token expiration
- Implement token renewal
- Provide clear error messages

**Data Validation Errors**:
- Validate input parameters
- Provide helpful error messages
- Suggest corrections
- Log validation failures

## Testing and Validation

### Tool Testing

1. **Parameter Validation**: Test with valid and invalid parameters
2. **Authentication**: Verify API credentials and permissions
3. **Response Handling**: Test success and error scenarios
4. **Performance**: Monitor response times and timeouts
5. **Error Scenarios**: Test failure conditions and fallbacks

### Test Scenarios

**Valid Request**:
```json
{
  "customer_id": "12345",
  "include_history": true
}
```

**Invalid Request**:
```json
{
  "customer_id": "invalid_id",
  "include_history": "not_boolean"
}
```

**Missing Parameters**:
```json
{
  "include_history": true
}
```

### Validation Checklist

- [ ] Tool responds correctly to valid requests
- [ ] Error handling works for invalid requests
- [ ] Authentication is properly configured
- [ ] Response format matches expectations
- [ ] Performance meets requirements
- [ ] Error messages are helpful and clear

## Best Practices

### Tool Design

- **Single Purpose**: Each tool should have one clear purpose
- **Clear Documentation**: Provide detailed descriptions and examples
- **Robust Error Handling**: Handle all possible error scenarios
- **Performance Optimisation**: Minimise response times and timeouts

### Security

- **Secure Credentials**: Store API keys securely
- **Input Validation**: Validate all input parameters
- **Output Sanitisation**: Sanitise response data
- **Access Controls**: Limit tool access to necessary agents

### Maintenance

- **Regular Testing**: Test tools regularly for functionality
- **Monitor Performance**: Track response times and success rates
- **Update Documentation**: Keep documentation current
- **Version Control**: Track changes and updates

## Troubleshooting

### Common Issues

**Tool Not Responding**:
- Check endpoint URL and method
- Verify authentication credentials
- Test with API testing tools
- Review error logs

**Authentication Failures**:
- Verify API key validity
- Check token expiration
- Review authentication method
- Test with different credentials

**Data Format Issues**:
- Validate request/response formats
- Check parameter types and validation
- Review API documentation
- Test with sample data

### Debugging Steps

1. **Check Tool Configuration**: Verify all settings are correct
2. **Test Manually**: Use API testing tools to test endpoints
3. **Review Logs**: Check tool execution logs for errors
4. **Validate Parameters**: Ensure input parameters are correct
5. **Monitor Performance**: Track response times and success rates
