# Felipe Suarez AI Assistant - Complete Documentation

## 🤖 Overview

The Felipe Suarez AI Assistant is a sophisticated sales automation system that combines a messenger-style web interface with powerful AI capabilities. It's designed to handle customer interactions, automate appointments, process payments, and manage communications through an integrated n8n workflow system.

## 🎯 Key Features

### Core Capabilities
- **Intelligent Conversational AI**: GPT-4o-mini powered sales agent with natural language processing
- **Multi-language Support**: Automatically adapts to user's language preference
- **Real-time Chat Interface**: Professional Instagram/Messenger-style UI with animations
- **Automated Sales Process**: Complete funnel from lead capture to payment processing
- **Smart Tool Integration**: Calendar, Gmail, and Stripe automation through MCP (Model Context Protocol)

### Advanced Features
- **Session Management**: Persistent conversation history with PostgreSQL
- **Vector Search**: Supabase-powered service documentation retrieval
- **Payment Processing**: Integrated Stripe payment link generation
- **Email Automation**: Gmail integration for confirmations and follow-ups
- **Calendar Management**: Google Calendar integration for appointment scheduling
- **Mobile Responsive**: Optimized for all device types

## 🏗️ System Architecture

### Frontend Components
- **HTML Interface** (`index1.html`): Modern messenger-style chat interface
- **Automatic Chat Flow**: Pre-programmed conversation sequences
- **Webhook Integration**: Real-time communication with n8n backend
- **Session Tracking**: Unique session IDs for conversation continuity

### Backend Workflow (n8n)
- **Main Messenger Workflow**: Core AI agent orchestration
- **Calendar Agent**: Google Calendar integration
- **Gmail Agent**: Email automation and management
- **MCP Tools**: Model Context Protocol for tool integration

### AI Components
- **Language Model**: OpenAI GPT-4o-mini for natural conversations
- **Vector Store**: Supabase for service documentation retrieval
- **Memory System**: PostgreSQL chat memory for context retention
- **Embeddings**: OpenAI embeddings for semantic search

## 🛠️ Setup Instructions

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google Cloud Console account
- OpenAI API account
- Supabase account
- Stripe account
- PostgreSQL database
- ngrok or similar tunneling service

### Step 1: Environment Setup

#### Google Services Configuration
1. **Google Cloud Console Setup**:
   - Create a new project or select existing
   - Enable Google Calendar API
   - Enable Gmail API
   - Enable Google Drive API
   - Create OAuth 2.0 credentials
   - Configure OAuth consent screen

2. **Google Drive Setup**:
   - Create service documentation in Google Docs
   - Note the document ID for n8n integration
   - Ensure proper sharing permissions

#### API Keys and Credentials
1. **OpenAI API**:
   - Sign up at platform.openai.com
   - Generate API key
   - Note the key for n8n configuration

2. **Supabase Setup**:
   - Create new project
   - Set up vector store table:
   ```sql
   CREATE TABLE documents (
     id SERIAL PRIMARY KEY,
     content TEXT,
     metadata JSONB,
     embedding VECTOR(1536)
   );
   ```
   - Generate API keys (anon and service role)

3. **Stripe Configuration**:
   - Create Stripe account
   - Get publishable and secret keys
   - Set up webhook endpoints

### Step 2: n8n Workflow Import

#### Import Workflows
1. **Main Messenger Workflow**:
   - Import `Messenger (38).json`
   - Configure webhook endpoint
   - Set up all credential connections

2. **Calendar Agent**:
   - Import `Calendar Agent (1).json`
   - Configure Google Calendar credentials
   - Set up MCP trigger endpoint

3. **Gmail Agent**:
   - Import `Gmail Agent (1).json`
   - Configure Gmail OAuth credentials
   - Set up MCP trigger endpoint

#### Configure Credentials in n8n
1. **OpenAI API**: Add API key to OpenAI Chat Model nodes
2. **Google Services**: Configure OAuth2 for Calendar and Gmail
3. **Supabase**: Add project URL and API keys
4. **PostgreSQL**: Configure database connection for chat memory
5. **Stripe**: Add secret key for payment processing

### Step 3: MCP (Model Context Protocol) Setup

#### Configure MCP Endpoints
The system uses MCP for tool integration. Each agent needs an endpoint:

1. **Calendar Agent MCP**: `https://your-ngrok-url/mcp/e501a93c-a5b6-4483-b6b5-2cfa26dad807`
2. **Gmail Agent MCP**: `https://your-ngrok-url/mcp/a34e27e7-ee1e-4796-9826-c9b0203e881b`
3. **Stripe MCP**: `https://your-ngrok-url/mcp/b3cfbb40-8a85-4216-86d1-0fdaae28a44e`

#### Update MCP Client Tools
In the main Messenger workflow, update the MCP Client Tool nodes with your ngrok URLs.

### Step 4: Frontend Deployment

#### Prepare the Web Interface
1. **Upload Assets**:
   - Host `index1.html` on your web server
   - Include required images (`1.jpg`, `3.jpg`, `resume.pdf`)
   - Ensure proper CORS configuration

2. **Configure Webhook URL**:
   - Update the webhook URL in the JavaScript section:
   ```javascript
   return fetch("YOUR_NGROK_URL/webhook/4eb21d65-6dfe-4816-88cf-323664347d0d", {
   ```

#### SSL and Security
- Ensure HTTPS for production deployment
- Configure proper CORS headers
- Set up CSP headers for security

### Step 5: Vector Store Population

#### Upload Service Documentation
1. **Prepare Documentation**:
   - Create comprehensive service descriptions
   - Include pricing information
   - Format in clear, searchable text

2. **Upload to Vector Store**:
   - Use the Google Drive download node
   - Process through the document loader
   - Store in Supabase vector store

### Step 6: Testing and Validation

#### Test Core Functions
1. **Chat Interface**: Verify message flow and UI responsiveness
2. **AI Responses**: Test conversation quality and context retention
3. **Tool Integration**: Validate calendar, email, and payment functions
4. **Error Handling**: Test fallback scenarios

#### Production Checklist
- [ ] All credentials configured and working
- [ ] MCP endpoints responding correctly
- [ ] Vector store populated with current data
- [ ] Payment processing tested in sandbox
- [ ] Email notifications working
- [ ] Calendar integration functional
- [ ] Mobile responsiveness verified
- [ ] SSL certificates installed
- [ ] Error monitoring configured

## 🔧 Configuration Details

### System Prompt Configuration
The AI agent is configured with a detailed system prompt that includes:
- **Identity**: Felipe Suarez, AI Developer persona
- **Sales Process**: Value-first approach with structured workflow
- **Tool Integration**: Specific parameter schemas for MCP tools
- **Communication Style**: Professional, concise, under 80 characters per message
- **Error Handling**: Graceful fallbacks when tools fail

### Memory and Context
- **Session Management**: PostgreSQL-based chat memory
- **Context Retention**: Conversation history preserved across sessions
- **Vector Retrieval**: Semantic search for service information
- **Personalization**: User identification and customized responses

### Payment Integration
- **Stripe Integration**: Automated payment link generation
- **Service Confirmation**: Price confirmation before payment processing
- **Receipt Management**: Automated email confirmations

## 📱 User Experience Flow

### Conversation Progression
1. **Greeting**: Automated welcome message
2. **Information Gathering**: Service inquiry and needs assessment
3. **Value Presentation**: Detailed service explanation with benefits
4. **Price Confirmation**: Clear pricing with service details
5. **Payment Processing**: Stripe payment link generation
6. **Appointment Scheduling**: Calendar integration for consultations
7. **Follow-up**: Email confirmations and next steps

### Automatic vs Interactive Mode
- **Automatic Mode**: Pre-scripted conversation flow
- **Interactive Mode**: Real-time AI responses triggered by user input
- **Seamless Transition**: Automatic detection and mode switching

## 🔄 Maintenance and Updates

### Regular Maintenance Tasks
1. **Vector Store Updates**: Refresh service documentation monthly
2. **Credential Rotation**: Update API keys as needed
3. **Performance Monitoring**: Track response times and error rates
4. **Content Updates**: Modify conversation flows based on feedback

### Scaling Considerations
- **Database Optimization**: Index chat memory tables for performance
- **Rate Limiting**: Implement API rate limiting for high traffic
- **Caching**: Add Redis caching for frequently accessed data
- **Load Balancing**: Scale n8n instances for high availability

## 🚨 Troubleshooting

### Common Issues
1. **MCP Connection Failures**: Check ngrok tunnel status and URLs
2. **Calendar Integration**: Verify Google OAuth scopes and permissions
3. **Payment Processing**: Confirm Stripe webhook configurations
4. **Vector Search**: Ensure embeddings are properly generated

### Error Monitoring
- **n8n Execution Logs**: Monitor workflow execution status
- **Frontend Console**: Check browser console for JavaScript errors
- **API Response Codes**: Monitor webhook response status
- **Database Logs**: Track PostgreSQL connection and query issues

## 📊 Analytics and Insights

### Key Metrics to Track
- **Conversation Completion Rate**: Users who complete the sales funnel
- **Payment Conversion**: Successful payment processing rate
- **Response Quality**: User satisfaction with AI responses
- **Tool Usage**: Frequency of calendar and email integrations

### Data Collection
- **Session Analytics**: Track user engagement and conversation length
- **Error Rates**: Monitor tool failures and system issues
- **Performance Metrics**: Response times and system load

This documentation provides a complete guide for setting up and managing the Felipe Suarez AI Assistant system. The modular architecture allows for easy customization and scaling based on specific business requirements.
