# Installation & Setup Guide

Complete guide to get Unnati Chatbot running.

## Table of Contents
- [Quick Start](#quick-start)
- [Detailed Setup](#detailed-setup)
- [API Configuration](#api-configuration)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)

---

## Quick Start

### 5-Minute Setup (Cloud n8n)

```bash
# 1. Go to n8n.cloud and create account
# 2. Create new workflow
# 3. Copy-paste this workflow JSON
# 4. Configure credentials
# 5. Activate and test

# That's it! You're live.
```

---

## Detailed Setup

### Step 1: Create n8n Instance

**Option A: n8n Cloud (Easiest)**
1. Visit [n8n.cloud](https://n8n.cloud)
2. Sign up for free account
3. Click "New Workflow"
4. Ready to import!

**Option B: Self-Hosted (Full Control)**
```bash
# Docker (Recommended)
docker run -it --rm \
  -p 5678:5678 \
  -e DB_TYPE=postgresdb \
  -e DB_POSTGRESDB_HOST=postgres \
  -e DB_POSTGRESDB_PORT=5432 \
  -e DB_POSTGRESDB_DATABASE=n8n \
  -e DB_POSTGRESDB_USER=n8n \
  -e DB_POSTGRESDB_PASSWORD=change_me \
  n8nio/n8n

# Then open http://localhost:5678
```

### Step 2: Import Workflow

1. In n8n dashboard, click **Create**
2. Select **Workflow from JSON**
3. Upload `Unnati_Chatbot.json`
4. Click **Import**

---

## API Configuration

### 1. Google Gemini Setup

```
1. Visit: https://makersuite.google.com/app/apikey
2. Click "Create API Key"
3. Copy API key
4. In n8n:
   - Credentials > Google PaLM API
   - Paste key
   - Save
```

### 2. Groq API Setup

```
1. Visit: https://console.groq.com
2. Sign up for account
3. Create API key
4. In n8n:
   - Credentials > Groq API
   - Paste key
   - Test connection
```

### 3. MongoDB Setup

**Option A: MongoDB Atlas (Cloud)**
```
1. Visit: https://www.mongodb.com/cloud/atlas
2. Create free cluster
3. Get connection string:
   mongodb+srv://user:pass@cluster.mongodb.net/AIChatbot
4. In n8n:
   - Credentials > MongoDB
   - Paste connection string
   - Test connection
```

**Option B: Local MongoDB**
```bash
# Mac (Homebrew)
brew services start mongodb-community

# Ubuntu
sudo systemctl start mongod

# Docker
docker run -d -p 27017:27017 mongo:latest

# Verify
mongo
> db.version()
```

### 4. Pinecone Setup

```
1. Visit: https://www.pinecone.io
2. Create free account
3. Create index (dimension: 1536, metric: cosine)
4. Get API key
5. In HTTP request node "Rag Questions":
   - Add header: Authorization: Bearer <YOUR_KEY>
   - Update URL endpoint
```

### 5. Perplexity API Setup

```
1. Visit: https://docs.perplexity.ai
2. Sign up for API access
3. Get API key
4. In node "Website questions":
   - Header: Authorization: Bearer <YOUR_KEY>
   - Already configured for sonar-pro model
```

### 6. Gmail Setup

```
1. Go to: https://console.cloud.google.com
2. Create new project
3. Enable Gmail API
4. Create OAuth 2.0 credentials (Desktop app)
5. Download JSON file
6. In n8n:
   - Credentials > Gmail OAuth2
   - Upload JSON
   - Authorize
```

---

## Environment Variables

Create `.env` file:

```env
# MongoDB
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/AIChatbot

# API Keys
GOOGLE_GEMINI_API_KEY=your_key
GROQ_API_KEY=your_key
PERPLEXITY_API_KEY=your_key
PINECONE_API_KEY=your_key

# Gmail
GMAIL_RECIPIENT=contact@vidhyarthimitra.org

# n8n
N8N_WEBHOOK_URL=https://your-domain.com/webhook/unnati
```

---

## Testing

### Test 1: Basic Connectivity

```bash
# Test webhook is live
curl -X POST https://your-n8n-instance/webhook/unnati \
  -H "Content-Type: application/json" \
  -d '{
    "chatId": "test-123",
    "message": "Hello"
  }'
```

### Test 2: LLM Response

In n8n:
1. Open "AI Agent" node
2. Click "Test"
3. Should see response from Gemini/Groq

### Test 3: MongoDB Connection

```bash
# Connect to MongoDB
mongo "mongodb+srv://user:pass@cluster.mongodb.net/AIChatbot"

# Check collection
> use AIChatbot
> db.Memory.find()
```

### Test 4: Full Integration

Message bot:
```
User: What is the website?
Expected: Bot should use Website Questions tool
Should see structured response
```

---

## Common Issues & Fixes

### ❌ "Credentials not found"
```
Fix:
1. Open each node (Gemini, Groq, MongoDB, etc.)
2. Click "Select Credentials"
3. If empty, create new credentials
4. Test connection
5. Save node
```

### ❌ "MongoDB connection timeout"
```
Fix:
1. Check internet connection
2. Whitelist IP in MongoDB Atlas:
   - MongoDB > Network Access > Add IP
   - Add 0.0.0.0/0 for testing (restrict in production)
3. Verify connection string format
4. Check username/password
```

### ❌ "API key invalid"
```
Fix:
1. Regenerate API key on provider website
2. Copy EXACT key (no spaces)
3. Test in n8n credentials
4. Restart workflow
```

### ❌ "Webhook not receiving messages"
```
Fix:
1. Check webhook URL is correct
2. Test with curl (see above)
3. Check n8n logs: 
   - Settings > Execution logs
4. Ensure workflow is active (toggle on)
```

### ❌ "Tools not responding"
```
Fix:
1. Test each tool individually
2. Check rate limits on external APIs
3. Verify request format (JSON schema)
4. Check firewall/proxy settings
5. Review error logs in n8n
```

---

## Performance Optimization

### Reduce Response Time

```
1. Switch to Groq LLM (faster than Gemini)
2. Reduce max_tokens in API calls (2048 → 1024)
3. Cache common FAQs in system prompt
4. Use smaller vector embeddings
5. Enable request caching
```

### Reduce API Costs

```
1. Batch similar requests
2. Increase cache TTL
3. Use Groq for repetitive tasks
4. Limit Perplexity calls to website questions
5. Monitor API usage monthly
```

---

## Deployment Checklist

Before going live:

- [ ] All credentials configured and tested
- [ ] MongoDB backup enabled
- [ ] Error logging configured
- [ ] Rate limiting enabled
- [ ] Gmail recipient verified
- [ ] Webhook URL secured (HTTPS)
- [ ] System prompt reviewed for accuracy
- [ ] Test messages processed correctly
- [ ] Response format consistent
- [ ] Team trained on how it works

---

## Next Steps

1. ✅ Import workflow
2. ✅ Configure credentials
3. ✅ Run tests
4. ✅ Deploy
5. ✅ Monitor performance
6. ✅ Gather user feedback
7. ✅ Iterate & improve

---

## Need Help?

- 📖 Check README.md
- 🔍 Search GitHub issues
- 💬 Ask in Discussions
- 📧 Contact: contact@vidhyarthimitra.org
