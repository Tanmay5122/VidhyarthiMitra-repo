# Unnati Chatbot 🤖

> **AI-Powered Website Support Assistant** using n8n, LangChain, and Advanced LLMs

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![n8n](https://img.shields.io/badge/built%20with-n8n-red.svg)](https://n8n.io)
[![Status](https://img.shields.io/badge/status-active-brightgreen.svg)]()

## Overview

Unnati is a sophisticated, multi-tool AI chatbot built on **n8n** that handles educational website support queries with intelligence and professionalism. It combines multiple LLMs (Google Gemini, Groq), vector databases (Pinecone), and intelligent routing to deliver accurate, context-aware responses.

### Key Features ✨

- **Dual LLM Architecture**: Google Gemini + Groq for redundancy and optimal performance
- **RAG Integration**: Pinecone vector database for FAQ knowledge retrieval
- **Smart Tool Routing**: 3 intelligent tools that auto-select based on user intent
- **Persistent Memory**: MongoDB-backed conversation history
- **Email Integration**: Direct Gmail integration for escalation workflows
- **Website Intelligence**: Deep website knowledge via Perplexity API
- **Production Ready**: Webhook-based, stateless architecture

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│       Chat Message Received (Webhook)            │
└────────────────┬────────────────────────────────┘
                 │
        ┌────────▼────────┐
        │   AI Agent      │
        │  (LangChain)    │
        └─┬──────────┬────┘
          │          │
    ┌─────▼───┐  ┌───▼──────────┐
    │ LLM     │  │ Tool Router  │
    ├─────────┤  ├──────────────┤
    │Gemini   │  │ RAG Tool     │
    │Groq     │  │ Gmail Tool   │
    └─────────┘  │ Web Tool     │
          │      └──────┬───────┘
    ┌─────▼──────────────────────┐
    │    Memory & Persistence    │
    ├────────────────────────────┤
    │   MongoDB Chat History     │
    └────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

- **n8n** (self-hosted or cloud)
- **Node.js** 18+
- **MongoDB** instance
- **API Keys** (see below)

### Installation

1. **Clone this repository**
   ```bash
   git clone https://github.com/yourusername/unnati-chatbot.git
   cd unnati-chatbot
   ```

2. **Import workflow into n8n**
   - Open n8n dashboard
   - Click **Create** → **Workflow from JSON**
   - Upload `Unnati_Chatbot.json`
   - Configure credentials (see below)

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```

4. **Start workflow**
   - Activate the workflow
   - Copy webhook URL
   - Deploy to your endpoint

---

## 🔐 Required API Keys & Credentials

| Service | Purpose | Setup Link |
|---------|---------|-----------|
| **Google Gemini** | Primary LLM | [Google AI Studio](https://makersuite.google.com/app/apikey) |
| **Groq** | Secondary LLM (fast inference) | [Groq Console](https://console.groq.com) |
| **Pinecone** | Vector DB for RAG | [Pinecone Cloud](https://www.pinecone.io) |
| **Perplexity API** | Web search & context | [Perplexity API](https://docs.perplexity.ai) |
| **MongoDB** | Conversation memory | [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) |
| **Gmail OAuth2** | Email escalation | [Google Cloud Console](https://console.cloud.google.com) |

### Configuration Steps

```yaml
Node: Google Gemini Chat Model
  └─ Connect "Google Gemini(PaLM) VM2026 Api account"

Node: Groq Chat Model
  └─ Connect "Groq account"

Node: MongoDB Chat Memory
  └─ Database: AIChatbot
  └─ Collection: Memory
  └─ Session Key: chatId

Node: Website Questions
  └─ Perplexity API Bearer Token
  └─ Search domains: vidyarthimitra.org, cetcell.mahacet.org, shiksha.com

Node: Send a message in Gmail
  └─ Connect Gmail OAuth2 account
  └─ Recipient: contact@vidhyarthimitra.org
```

---

## 📋 Available Tools

### 1️⃣ RAG Questions Tool
**Purpose**: Answer FAQs from training knowledge base

- **Endpoint**: `https://prod-1-data.ke.pinecone.io/assistant/chat/unnati`
- **Use Case**: General education FAQs, quick reference answers
- **Response Type**: Markdown formatted

### 2️⃣ Send Gmail Tool
**Purpose**: Escalate queries or send customer communications

- **Recipient**: contact@vidhyarthimitra.org (configurable)
- **Includes**: Dynamic subject & message generation
- **Use Case**: Complex requests, feedback, complaints

### 3️⃣ Website Questions Tool
**Purpose**: Deep website knowledge retrieval

- **Provider**: Perplexity API (sonar-pro model)
- **Coverage**: Courses, cut-offs, exam dates, fees, eligibility
- **Response**: JSON (table or text format)
- **Sources**: Verified from vidyarthimitra.org, CET Cell, Shiksha

---

## 💬 Example Interactions

### Example 1: FAQ Query
```
User: What are the eligibility criteria?

→ RAG Tool activates
→ Fetches from Pinecone
→ Returns formatted FAQ answer
```

### Example 2: Website Information
```
User: What's the cut-off for Engineering?

→ Website Questions Tool activates
→ Queries Perplexity API
→ Returns JSON table with cut-offs
```

### Example 3: Escalation
```
User: I need to speak with someone

→ Triggers Gmail Tool
→ Sends inquiry to support team
→ Responds with confirmation
```

---

## 🔧 Customization

### Change LLM Models
In `AI Agent` node → Edit system prompt to switch between Gemini/Groq

### Modify Response Format
Edit `Website Questions` tool JSON schema for different response structures

### Add New Tools
1. Create HTTP request node
2. Add to AI Agent as tool
3. Update system prompt with tool description

### Adjust Memory Settings
MongoDB Chat Memory node:
- Change `collectionName` for different conversation contexts
- Modify `sessionIdType` for user/chat grouping

---

## 📊 Performance Metrics

| Metric | Value |
|--------|-------|
| **LLM Response Time** | 800-1500ms (Groq) / 1-2s (Gemini) |
| **Tool Invocation Latency** | 200-500ms |
| **Memory Lookup** | 100-300ms |
| **Typical End-to-End** | 2-4 seconds |

---

## 🛡️ Security Best Practices

✅ **Implemented**
- OAuth2 for Gmail integration
- API key isolation (separate credentials)
- MongoDB session-based memory
- Input validation via system prompt

⚠️ **Recommendations**
```bash
# Store API keys in n8n Credentials (never in code)
# Use environment variables for sensitive data
# Enable API rate limiting on webhook
# Monitor MongoDB for unauthorized access
# Rotate Perplexity API keys quarterly
# Use VPN/firewall for MongoDB access
```

---

## 🚢 Deployment Options

### Option 1: n8n Cloud
- No infrastructure management
- Built-in scaling
- [Start here](https://n8n.cloud)

### Option 2: Self-Hosted (Docker)
```bash
docker run -it --rm \
  -p 5678:5678 \
  -e DB_TYPE=postgresdb \
  n8nio/n8n
```

### Option 3: n8n on AWS/GCP/Azure
- Full control
- Custom domain
- Advanced scaling

---

## 📝 Workflow Nodes Breakdown

| Node | Type | Purpose |
|------|------|---------|
| When chat message received | Trigger | Webhook listener |
| AI Agent | LangChain | Core decision engine |
| Google Gemini Chat Model | LLM | Primary language model |
| Groq Chat Model | LLM | Backup/fast LLM |
| MongoDB Chat Memory | Memory | Persistent conversation store |
| Rag Questions | Tool | FAQ retrieval |
| Website Questions | Tool | Web search & structured data |
| Send a message in Gmail | Tool | Email escalation |

---

## 🐛 Troubleshooting

### Issue: "Tool not responding"
```
Solution:
1. Check API key validity
2. Verify firewall/proxy settings
3. Check rate limits on external APIs
4. Review n8n logs: docker logs <container_id>
```

### Issue: "Memory not persisting"
```
Solution:
1. Verify MongoDB connection string
2. Check collection name matches (AIChatbot.Memory)
3. Ensure sessionKey field is being passed
```

### Issue: "Slow responses"
```
Solution:
1. Switch to Groq LLM (faster)
2. Reduce max_tokens in API calls
3. Cache common FAQs in system prompt
4. Use smaller vector embeddings in Pinecone
```

---

## 📚 Documentation Links

- [n8n LangChain Docs](https://docs.n8n.io/nodes/n8n-nodes-langchain/)
- [Pinecone Vector DB](https://docs.pinecone.io)
- [Perplexity API](https://docs.perplexity.ai)
- [Google Gemini API](https://ai.google.dev)
- [Groq API](https://groq.com/api)

---

## 🤝 Contributing

Found a bug? Have an improvement idea?

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Unnati Chatbot Project**  
Built with ❤️ using n8n, LangChain, and AI APIs

---

## ⭐ Show Your Support

If this project helped you, please give it a ⭐!

---

## 📞 Support & Questions

- 📧 Email: contact@vidhyarthimitra.org
- 💬 Discussions: [GitHub Discussions](https://github.com/yourusername/unnati-chatbot/discussions)
- 🐛 Issues: [Report a Bug](https://github.com/yourusername/unnati-chatbot/issues)

---

**Last Updated**: April 2026  
**Workflow Version**: 1.0.0  
**n8n Version**: Latest
