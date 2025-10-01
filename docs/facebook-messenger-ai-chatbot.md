# Facebook Messenger AI Chatbot

## 📝 Description

A production-ready, AI-powered chatbot for Facebook Messenger that provides intelligent, context-aware responses to customer inquiries. This workflow integrates OpenAI's GPT-4o Mini model with Facebook Messenger API to create an automated customer service solution that maintains conversation context and handles messages gracefully.

Perfect for businesses looking to automate customer support, lead generation, and engagement on their Facebook pages.

## ✨ Features

- 🤖 **AI-Powered Responses**: Uses OpenAI GPT-4o Mini for intelligent, natural conversations
- 💬 **Context-Aware**: Maintains conversation history per user for coherent dialogues
- 🔒 **Secure**: Uses environment variables and credential management
- 🛡️ **Error Handling**: Robust error handling with graceful fallbacks
- ⚡ **Optimized**: Efficient data processing and minimal API calls
- 📊 **Production Ready**: Includes validation, logging, and proper response handling
- 🔄 **Latest n8n**: Compatible with the latest n8n version and best practices

## 🎯 Use Cases

- **Customer Support**: Answer frequently asked questions automatically
- **Lead Generation**: Qualify leads and collect requirements
- **Business Hours Coverage**: Provide 24/7 responses when team is unavailable
- **Information Distribution**: Share product/service information instantly
- **Appointment Booking**: Help customers schedule appointments or demos
- **Requirement Gathering**: Collect customer needs and preferences

## 📋 Prerequisites

### Required Services

1. **n8n Instance** - [n8n.io](https://n8n.io) (Self-hosted or Cloud)
2. **Facebook Page** - [Create a Facebook Page](https://www.facebook.com/pages/create)
3. **Meta Developer Account** - [developers.facebook.com](https://developers.facebook.com)
4. **OpenAI Account** - [platform.openai.com](https://platform.openai.com)

### Required Credentials

1. **OpenAI API Key**
   - Sign up at [OpenAI Platform](https://platform.openai.com)
   - Generate an API key
   - Ensure you have credits or billing set up

2. **Facebook Page Access Token**
   - Create a Facebook App in Meta Developer Console
   - Add Messenger product to your app
   - Generate a Page Access Token (should never expire)
   - Get your Page ID

3. **Facebook Verify Token**
   - Create a custom verification token (random string)
   - Used to verify webhook setup with Facebook

## 🚀 Setup Instructions

### Step 1: Import the Workflow

1. Download `facebook-chatbot.json` from the repository
2. In n8n, navigate to **Workflows** → **Import from File**
3. Select the downloaded JSON file
4. Click **Import**

### Step 2: Set Up Environment Variables

Add these environment variables to your n8n instance:

```bash
# Facebook Verify Token (create your own random string)
FACEBOOK_VERIFY_TOKEN=your_custom_verify_token_here

# Example: FACEBOOK_VERIFY_TOKEN=my_secure_token_12345
```

**How to set environment variables:**

- **Docker**: Add to your `docker-compose.yml` or use `-e` flag
- **Self-hosted**: Add to `.env` file or system environment
- **n8n Cloud**: Add in Settings → Environment Variables

### Step 3: Configure OpenAI Credentials

1. In the workflow, click on **"OpenAI GPT-4o Mini"** node
2. Click **"Create New Credential"** if you haven't set up OpenAI yet
3. Enter your OpenAI API key
4. Click **"Save"**
5. Test the connection

### Step 4: Configure Facebook Page Token

1. In the workflow, click on **"Send to Facebook"** node
2. Click on **Credentials** → **"Create New Credential"**
3. Select **HTTP Header Auth**
4. Configure:
   - **Name**: `Authorization`
   - **Value**: `Bearer YOUR_PAGE_ACCESS_TOKEN`
5. Click **"Save"**

### Step 5: Activate the Workflow

1. Toggle the workflow to **Active** status
2. Copy the webhook URLs from both webhook nodes:
   - **GET**: `https://your-n8n-instance.com/webhook/facebook-messenger-webhook`
   - **POST**: `https://your-n8n-instance.com/webhook/facebook-messenger-webhook`

### Step 6: Configure Facebook Webhook

1. Go to [Meta Developer Console](https://developers.facebook.com)
2. Select your app → **Messenger** → **Settings**
3. In **Webhooks** section, click **"Add Callback URL"**
4. Enter:
   - **Callback URL**: Your webhook URL from n8n
   - **Verify Token**: The same token you set in environment variables
5. Click **"Verify and Save"**
6. Subscribe to webhook fields:
   - ✅ `messages`
   - ✅ `messaging_postbacks`
   - ✅ `messaging_optins`

### Step 7: Subscribe to Page Events

1. In the **Webhooks** section, click **"Add Subscriptions"**
2. Select your Facebook Page
3. Enable the same webhook fields as above
4. Click **"Subscribe"**

### Step 8: Test Your Chatbot

1. Go to your Facebook Page
2. Send a test message: "Hello, I need help with chatbot setup"
3. The bot should respond with an AI-generated message
4. Check n8n execution history to verify workflow ran successfully

## 🔄 Workflow Description

### Workflow Architecture

The workflow is split into two main paths:

#### 1. **Verification Path** (GET Webhook)
Handles Facebook's webhook verification when you set up the integration.

#### 2. **Message Processing Path** (POST Webhook)
Processes incoming messages and generates AI responses.

### Detailed Flow

#### Verification Flow

1. **Webhook Verify** → Receives GET request from Facebook
2. **Verify Token** → Validates the verify token matches
3. **Respond Challenge** → Returns challenge to Facebook

#### Message Processing Flow

1. **Facebook Webhook** → Receives POST request with message
2. **Validate Message** → Checks if message contains text
3. **Extract Message Data** → Safely extracts sender, recipient, and message
4. **Set Variables** → Prepares data for AI processing
5. **AI Agent** → Processes message with OpenAI GPT-4o Mini
   - Uses conversation memory for context
   - Applies output parser for clean responses
6. **Send to Facebook** → Sends AI response back to user
7. **Respond Success** → Acknowledges receipt to Facebook

#### Error Handling

- **Validate Message**: Returns 200 OK for non-text messages (reactions, images, etc.)
- **Error Handler**: Logs errors and provides graceful fallback
- **Respond Success**: Always acknowledges to Facebook to prevent retries

## ⚙️ Configuration Options

### AI Agent Settings

| Parameter | Description | Default Value | Recommendation |
|-----------|-------------|---------------|----------------|
| Temperature | Creativity of responses | 0.7 | 0.5-0.9 for conversational |
| Max Tokens | Maximum response length | 500 | 300-800 based on use case |
| System Message | AI personality & instructions | Custom prompt | Customize for your brand |

### Memory Settings

| Parameter | Description | Default Value | Recommendation |
|-----------|-------------|---------------|----------------|
| Context Window | Number of messages to remember | 10 | 5-20 based on conversation complexity |
| Session Key | User identification | Sender ID | Keep as sender ID |

### Facebook API Settings

| Parameter | Description | Notes |
|-----------|-------------|-------|
| API Version | Facebook Graph API version | v21.0 (update as needed) |
| Messaging Type | Response type | RESPONSE (for replies) |

## 🔧 Customization

### Customize AI Personality

Edit the **System Message** in the **AI Agent** node:

```javascript
You are a professional AI assistant for [YOUR COMPANY NAME], a company that [YOUR SERVICES].

**Your Role:**
- [Define the role]
- [Key responsibilities]

**Key Services:**
- [Service 1]
- [Service 2]

**Guidelines:**
- [Tone and style guidelines]
- [Response format preferences]
```

### Add Quick Replies

Modify the **Send to Facebook** node to include quick replies:

```json
{
  "recipient": {
    "id": "{{ $('Set Variables').item.json.senderId }}"
  },
  "messaging_type": "RESPONSE",
  "message": {
    "text": {{ JSON.stringify($json.output) }},
    "quick_replies": [
      {
        "content_type": "text",
        "title": "Talk to Sales",
        "payload": "SALES_INQUIRY"
      },
      {
        "content_type": "text",
        "title": "Get Support",
        "payload": "SUPPORT_REQUEST"
      }
    ]
  }
}
```

### Add Typing Indicator

Insert a new HTTP Request node before **Send to Facebook**:

```json
{
  "recipient": {
    "id": "{{ $('Set Variables').item.json.senderId }}"
  },
  "sender_action": "typing_on"
}
```

### Change AI Model

In the **OpenAI GPT-4o Mini** node, change the model:

- **GPT-4o**: More powerful, higher cost
- **GPT-4o-mini**: Balanced (current)
- **GPT-3.5-turbo**: Faster, lower cost

### Store Conversations

Add a database node after **AI Agent** to log conversations:

1. Add **Postgres/MySQL/MongoDB** node
2. Store: sender ID, message, response, timestamp
3. Use for analytics and training

## 🐛 Troubleshooting

### Common Issues

#### 1. Webhook Verification Fails

**Symptoms**: Facebook shows "The URL couldn't be validated"

**Solutions**:
- ✅ Ensure workflow is **Active**
- ✅ Check `FACEBOOK_VERIFY_TOKEN` environment variable matches
- ✅ Verify n8n instance is publicly accessible (use ngrok for local testing)
- ✅ Check n8n logs for incoming requests
- ✅ Ensure webhook path is correct

#### 2. Bot Doesn't Respond to Messages

**Symptoms**: Messages sent but no response

**Solutions**:
- ✅ Check workflow execution history in n8n
- ✅ Verify Facebook Page Access Token is valid
- ✅ Ensure page is subscribed to webhook events
- ✅ Check OpenAI API key has credits
- ✅ Review error logs in n8n

#### 3. AI Responses Are Generic

**Symptoms**: Bot gives irrelevant or generic answers

**Solutions**:
- ✅ Improve system message with more context
- ✅ Increase context window in memory settings
- ✅ Add example conversations in system message
- ✅ Use GPT-4o instead of GPT-4o-mini
- ✅ Fine-tune temperature settings

#### 4. Timeout Errors

**Symptoms**: Workflow times out or takes too long

**Solutions**:
- ✅ Reduce max tokens in AI settings
- ✅ Increase n8n execution timeout settings
- ✅ Optimize system message length
- ✅ Consider using faster AI model
- ✅ Check internet connectivity

#### 5. Facebook API Errors

**Symptoms**: Error messages from Facebook API

**Solutions**:
- ✅ Verify Page Access Token permissions
- ✅ Check if token has expired (use never-expire token)
- ✅ Ensure page is published and active
- ✅ Review Facebook API version compatibility
- ✅ Check rate limits

#### 6. Conversation Context Lost

**Symptoms**: Bot doesn't remember previous messages

**Solutions**:
- ✅ Verify sender ID is correctly extracted
- ✅ Check memory node configuration
- ✅ Ensure session key is set to sender ID
- ✅ Increase context window length
- ✅ Check if memory node is properly connected

### Debug Mode

Enable debug mode to troubleshoot issues:

1. In each node, click **Settings**
2. Enable **"Always Output Data"**
3. Check execution data to see what's being passed
4. Review n8n execution logs

### Testing Locally

Use **ngrok** to test locally:

```bash
# Install ngrok
npm install -g ngrok

# Expose n8n port
ngrok http 5678

# Use ngrok URL as webhook in Facebook
```

## 📊 Performance Optimization

### Best Practices

1. **Reduce Token Usage**:
   - Keep system message concise
   - Set appropriate max tokens (300-500)
   - Use GPT-4o-mini for cost efficiency

2. **Optimize Memory**:
   - Set context window to 5-10 for most use cases
   - Clear old conversations periodically
   - Use session-based memory (current implementation)

3. **Handle High Traffic**:
   - Use n8n queue mode for scaling
   - Set up multiple n8n instances with load balancer
   - Implement rate limiting if needed

4. **Reduce Latency**:
   - Host n8n close to users geographically
   - Use faster AI models for simple queries
   - Cache common responses

5. **Monitor Performance**:
   - Track execution times in n8n
   - Monitor OpenAI API usage
   - Set up alerts for failures

## 📈 Analytics & Monitoring

### What to Track

1. **Message Volume**: Number of messages received
2. **Response Time**: Time from message to response
3. **Error Rate**: Failed executions
4. **Popular Topics**: Common user queries
5. **AI Costs**: OpenAI API usage and costs

### Monitoring Setup

Add a **Webhook** or **HTTP Request** node to send data to analytics platforms:

- **Google Analytics**: Track conversation events
- **Mixpanel**: User behavior analytics
- **Custom Dashboard**: Build with Grafana/Metabase

## 🔗 Related Resources

### Facebook Messenger API
- [Messenger Platform Documentation](https://developers.facebook.com/docs/messenger-platform)
- [Send API Reference](https://developers.facebook.com/docs/messenger-platform/reference/send-api)
- [Webhook Reference](https://developers.facebook.com/docs/messenger-platform/webhooks)

### OpenAI API
- [OpenAI API Documentation](https://platform.openai.com/docs)
- [GPT-4o Models](https://platform.openai.com/docs/models/gpt-4o)
- [Best Practices](https://platform.openai.com/docs/guides/prompt-engineering)

### n8n Resources
- [n8n Webhook Node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)
- [n8n AI Nodes](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)
- [n8n Error Handling](https://docs.n8n.io/workflows/error-handling/)

## 💡 Advanced Features

### Add Intent Recognition

Create a **Switch** node to route to different AI agents based on intent:

```javascript
// In Code node before AI Agent
const message = $json.userMessage.toLowerCase();

if (message.includes('pricing') || message.includes('cost')) {
  return { json: { intent: 'pricing' } };
} else if (message.includes('support') || message.includes('help')) {
  return { json: { intent: 'support' } };
} else {
  return { json: { intent: 'general' } };
}
```

### Implement Handoff to Human

Add a condition to transfer to human agent:

```javascript
// Check for keywords that require human
const requiresHuman = [
  'speak to human', 'talk to person', 'real person', 
  'representative', 'agent'
];

if (requiresHuman.some(kw => message.toLowerCase().includes(kw))) {
  // Send notification to team
  // Update CRM status
  // Provide human contact info
}
```

### Multi-Language Support

Add language detection and translation:

1. Use **Google Translate** node to detect language
2. Translate to English for AI processing
3. Translate response back to user's language

### Integration with CRM

Connect to your CRM system:

1. Add **Salesforce/HubSpot** node
2. Create or update contact when new user messages
3. Log conversation history
4. Track lead status

## 👤 Author

- **Workflow**: Optimized for latest n8n version
- **Original**: Expedite Formation Chatbot
- **Documentation**: Comprehensive setup and customization guide

## 📄 License

This workflow is available under the MIT License. Free to use and modify for your projects.

## 🆘 Support

Need help with this workflow?

- **GitHub Issues**: [Report issues](https://github.com/tarikmanoar/n8n-hacktober-workflow/issues)
- **n8n Community**: [Ask questions](https://community.n8n.io)
- **Documentation**: Review this guide thoroughly

## 📝 Changelog

### Version 2.0 (Optimized)
- ✅ Updated to latest n8n node versions
- ✅ Separated GET and POST webhooks for clarity
- ✅ Added comprehensive error handling
- ✅ Implemented safe data extraction with Code node
- ✅ Added Set node for better variable management
- ✅ Updated to GPT-4o-mini model
- ✅ Reduced context window for efficiency (50 → 10)
- ✅ Added output parser for clean responses
- ✅ Implemented environment variables for security
- ✅ Added detailed node descriptions
- ✅ Improved system message for better responses
- ✅ Added proper response acknowledgment
- ✅ Updated Facebook API to v21.0
- ✅ Improved credential management
- ✅ Added workflow tags

### Version 1.0 (Original)
- Initial chatbot implementation

---

<div align="center">

**Built with ❤️ for the n8n community**

⭐ If this workflow helped you, consider starring the repository!

</div>
