# Contributing to Unnati Chatbot

First off, thanks for taking the time to contribute! 🎉

## Code of Conduct

This project adheres to the Contributor Covenant code of conduct. By participating, you are expected to uphold this code.

---

## How Can I Contribute?

### 🐛 Reporting Bugs

Before creating a bug report, check if it's already reported. When creating a bug report, include:

- **Title**: Clear, descriptive title
- **Description**: What you expected vs. what happened
- **Steps to Reproduce**: Exact steps to reproduce the issue
- **Environment**:
  - n8n version
  - Node.js version
  - Browser/OS
  - Any relevant API versions

**Example:**
```markdown
**Title**: Gemini LLM timeout on long conversations

**Description**: When conversation history exceeds 50 messages, Gemini times out

**Steps**:
1. Start new conversation
2. Send 50+ messages
3. Notice timeout error

**Environment**: n8n 1.x, Node 18, MongoDB 6.0
```

---

### 💡 Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion:

- Use a clear, descriptive title
- Provide a step-by-step description
- Provide specific examples
- Describe the current behavior and expected behavior
- Explain why this enhancement would be useful

---

### 🔧 Pull Requests

1. **Fork the Repository**
   ```bash
   git clone https://github.com/yourusername/unnati-chatbot.git
   cd unnati-chatbot
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/add-sentiment-analysis
   ```

3. **Make Your Changes**
   - Follow existing code style
   - Comment complex logic
   - Update README if needed
   - Test thoroughly

4. **Commit with Clear Messages**
   ```bash
   git commit -m "Add sentiment analysis to responses"
   ```

5. **Push to Your Fork**
   ```bash
   git push origin feature/add-sentiment-analysis
   ```

6. **Open a Pull Request**
   - Reference any related issues (#123)
   - Describe changes clearly
   - Include screenshots for UI changes

---

## Development Setup

### Prerequisites
- Node.js 18+
- MongoDB instance
- n8n (self-hosted or cloud)
- Git

### Local Development

```bash
# Clone repository
git clone https://github.com/yourusername/unnati-chatbot.git
cd unnati-chatbot

# Copy environment file
cp .env.example .env

# Fill in your API keys
nano .env

# Start n8n (if self-hosted)
docker run -it --rm -p 5678:5678 n8nio/n8n

# Import workflow
# 1. Open http://localhost:5678
# 2. Create > Workflow from JSON
# 3. Upload Unnati_Chatbot.json
```

---

## Workflow Modification Guidelines

### Adding a New Tool

1. **Create HTTP Request Node**
   ```
   Type: n8n-nodes-base.httpRequestTool
   Method: POST/GET
   URL: Your API endpoint
   Headers: Include auth tokens
   ```

2. **Update AI Agent System Prompt**
   ```
   Add: "X. [Tool Name]\nUse this tool to..."
   ```

3. **Test Thoroughly**
   - Mock requests
   - Error handling
   - Response validation

4. **Document**
   - Add to README Tools section
   - Include example usage
   - Describe when tool is triggered

### Modifying LLM Behavior

Edit the AI Agent node's system prompt:
- Keep it concise and clear
- Use examples for complex rules
- Test response format consistency

### Optimizing Performance

- Monitor token usage in API calls
- Reduce unnecessary API calls
- Cache common responses
- Batch requests where possible

---

## Testing Checklist

Before submitting a PR, ensure:

- [ ] Workflow activates without errors
- [ ] All credential connections verified
- [ ] Test messages processed correctly
- [ ] Memory persists across sessions
- [ ] Tools respond with correct format
- [ ] Error handling works as expected
- [ ] Response time is acceptable
- [ ] No sensitive data in logs

---

## Style Guidelines

### Node Naming
- Use clear, descriptive names
- Follow pattern: `[Action] [Subject]`
- Examples: `Send Email`, `Get FAQ`, `Parse Response`

### System Prompts
- Use markdown formatting
- Keep instructions concise
- Number tool descriptions
- Include response format rules

### Comments
- Explain WHY, not WHAT
- Use clear language
- Update when changing logic

---

## Commit Message Format

```
[Type]: Brief description

Detailed explanation of changes (if needed)

Fixes #123
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `refactor:` Code restructuring
- `perf:` Performance improvement
- `test:` Test addition/modification

**Examples:**
```
feat: Add Slack tool for notifications

fix: MongoDB memory not persisting on restart

docs: Update deployment section in README

perf: Reduce Perplexity API calls by 30%
```

---

## Documentation Updates

When updating documentation:

- [ ] Spell-checked
- [ ] Links verified
- [ ] Code examples tested
- [ ] Formatting consistent
- [ ] Images included (if needed)

---

## Questions?

- 📧 Ask in GitHub Discussions
- 💬 Comment on related issues
- 📚 Check existing documentation

---

## Recognition

Contributors will be recognized in:
- README contributors section
- Release notes
- GitHub contributors page

Thank you for contributing! 🚀
