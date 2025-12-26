# Personal AI Agent with Quality Control

An intelligent personal assistant that represents you on your website or portfolio. Uses your LinkedIn profile and personal summary to answer questions about your background, skills, and experience - with built-in quality control to ensure professional responses.

## 🎯 What This Does

- **Reads your LinkedIn PDF** and personal summary
- **Answers questions** about your background professionally
- **Quality control system** evaluates responses before sending
- **Self-correcting** - regenerates responses that fail evaluation
- **Interactive UI** with Gradio for easy testing
- **Structured outputs** using Pydantic for reliable evaluation

## ✨ Key Features

- 📄 PDF processing for LinkedIn profiles
- 💬 Natural conversation interface
- ✅ Automated quality evaluation
- 🔄 Self-correction with feedback
- 🎨 Clean Gradio web interface
- 🛡️ Professional representation guaranteed

## 📋 Prerequisites

- Python 3.8+
- OpenAI API key (required)
- Google API key (optional, for evaluator)
- Your LinkedIn profile as PDF
- A personal summary text file

## 🚀 Quick Start

### 1. Clone and Install

```bash
git clone https://github.com/csg09/personal-ai-agent.git
cd personal-ai-agent
pip install -r requirements.txt
```

### 2. Set Up Your Personal Data

Create a `me` folder with two files:

**linkedin.pdf**: Export from LinkedIn
1. Go to your LinkedIn profile
2. Click "More" → "Save to PDF"
3. Save as `me/linkedin.pdf`

**summary.txt**: Your personal summary
```text
Example content:
I'm a software engineer with 5 years of experience in AI/ML.
Specialized in natural language processing and computer vision.
Led development of X product that achieved Y results.
Passionate about building AI tools that help people.
```

### 3. Configure API Keys

Create `.env` file:
```bash
# Required
OPENAI_API_KEY=your_openai_key_here

# Optional (for evaluator - can use OpenAI as fallback)
GOOGLE_API_KEY=your_google_key_here
```

### 4. Update Your Name

Edit `personal_ai_agent.py` or the notebook:
```python
name = "Your Actual Name"  # Change this!
```

### 5. Run the Agent

```bash
jupyter notebook personal_ai_agent.ipynb
```

Or run directly:
```bash
python personal_ai_agent.py
```

The Gradio interface will open in your browser!

## 📂 Project Structure

```
personal-ai-agent/
├── personal_ai_agent.ipynb  # Main notebook
├── me/
│   ├── linkedin.pdf         # Your LinkedIn profile (you create this)
│   └── summary.txt          # Your summary (you create this)
├── requirements.txt         # Python dependencies
├── .env.example            # API key template
├── .gitignore              # Protects your data
├── LICENSE                 # MIT License
└── README.md               # This file
```

## 💡 How It Works

### Architecture Flow

```
User Question
    ↓
Agent Generates Response
    ↓
Evaluator Checks Quality
    ↓
Pass? → Send to User
    ↓
Fail? → Regenerate with Feedback
    ↓
Send Improved Response
```

### Components

1. **PDF Reader**: Extracts text from your LinkedIn profile
2. **System Prompt**: Configures agent to represent you professionally
3. **Chat Function**: Handles conversation with context
4. **Evaluator**: LLM judge that checks response quality
5. **Self-Correction**: Regenerates responses with feedback
6. **Gradio UI**: Clean web interface for interaction

## 🎓 Use Cases

- **Portfolio Website**: Add an AI chatbot to your personal site
- **Job Applications**: Help recruiters learn about you 24/7
- **Networking**: Provide quick answers about your background
- **Personal Branding**: Consistent professional representation
- **Learning Tool**: Study conversation AI and quality control

## 🛠️ Customization

### Adjust Agent Personality

Edit the system prompt:
```python
system_prompt = f"You are {name}, a friendly and approachable [role]. \
Your style is [casual/professional/technical]..."
```

### Change Evaluation Criteria

Modify the evaluator prompt to check for:
- Technical accuracy
- Appropriate tone
- Length constraints
- Specific topics to avoid
- Citation requirements

### Use Different Models

```python
# For agent
response = openai.chat.completions.create(
    model="gpt-4o",  # More capable but slower
    messages=messages
)

# For evaluator
response = gemini.chat.completions.create(
    model="gemini-1.5-pro",  # Different perspective
    messages=messages
)
```

### Add Multiple Evaluators

```python
def multi_evaluate(reply, message, history):
    evaluators = [openai, gemini, claude]
    votes = [eval.evaluate(reply, message, history) for eval in evaluators]
    return majority_vote(votes)
```

## 📊 Example Conversation

```
User: What's your background in AI?

Agent: [Generates response based on LinkedIn/summary]
Evaluator: ✓ Acceptable - professional, accurate, engaging

Agent: "I have 5 years of experience in AI/ML, specializing in 
natural language processing. I've led projects involving..."

---

User: Can you code in Python?

Agent: [Generates overly brief response]
Evaluator: ✗ Rejected - too short, lacks detail

Agent: [Regenerates with feedback]
Agent: "Yes! Python is my primary language. I use it daily for 
ML work with libraries like PyTorch, Transformers, and Pandas. 
I've built [specific projects from LinkedIn]..."
```

## 🔧 Advanced Features

### Add Source Citations

```python
system_prompt += "\n\nWhen answering, reference specific experiences \
from the LinkedIn profile or summary. Example: 'As mentioned in my \
LinkedIn, I worked on...'"
```

### Track Rejections

```python
rejections = []

def chat(message, history):
    # ... existing code ...
    if not evaluation.is_acceptable:
        rejections.append({
            'question': message,
            'response': reply,
            'feedback': evaluation.feedback
        })
    # ... rest of code ...
```

### Add Response Caching

```python
from functools import lru_cache

@lru_cache(maxsize=100)
def cached_response(message_hash):
    # Generate and return response
    pass
```

## 💰 Cost Estimation

| Component | Model | Cost per 1M tokens | Typical Query |
|-----------|-------|-------------------|---------------|
| Agent | GPT-4o-mini | $0.15-$0.60 | ~$0.001 |
| Evaluator | Gemini 2.0 Flash | $0.075 | ~$0.0005 |
| **Total per query** | | | **~$0.0015** |

For 1,000 queries: approximately **$1.50**

## 🐛 Troubleshooting

### PDF Not Loading
```
Error: FileNotFoundError: me/linkedin.pdf
```
**Solution**: 
- Create `me` folder in project directory
- Download LinkedIn profile as PDF
- Save as `me/linkedin.pdf`
- Ensure PDF is text-based (not scanned image)

### Gradio Won't Launch
```
Error: Port 7860 already in use
```
**Solution**:
```python
gr.ChatInterface(chat, type="messages").launch(server_port=7861)
```

### Evaluator Always Accepts/Rejects
**Solution**:
- Review evaluator criteria
- Add specific examples
- Test with different questions
- Adjust feedback prompt

### History Format Errors (Groq, etc.)
**Solution**: Add this line at start of `chat()`:
```python
history = [{"role": h["role"], "content": h["content"]} for h in history]
```

### PDF Text Extraction Issues
**Solution**:
- Ensure PDF has selectable text
- Try re-exporting from LinkedIn
- Check PDF isn't password protected
- Use Adobe Reader to verify text

## 🔒 Security & Privacy

- ✅ Never commit `.env` files
- ✅ Add `me/` folder to `.gitignore` 
- ✅ Don't share your LinkedIn PDF publicly
- ✅ Review API logs for sensitive data
- ✅ Consider using environment-specific configs

## 📚 Extension Ideas

1. **Multi-Language Support**: Detect and respond in user's language
2. **Voice Interface**: Add speech-to-text / text-to-speech
3. **Analytics Dashboard**: Track popular questions
4. **A/B Testing**: Compare different system prompts
5. **Context Memory**: Remember previous conversations
6. **Source Attribution**: Cite specific LinkedIn sections
7. **Feedback Loop**: Users rate responses, improve over time
8. **Integration**: Embed in actual website
9. **Scheduling**: "When are you available for calls?"
10. **Portfolio Links**: Reference projects with URLs

## 🤝 Contributing

Ideas for contributions:
- Support for other resume formats (Word, JSON)
- Multiple evaluator voting system
- Response quality metrics and logging
- UI improvements and themes
- Integration guides for popular website platforms

## 📝 License

MIT License - see LICENSE file

## 🙏 Acknowledgments

- Built for showcasing personal brands professionally
- Uses Gradio for easy UI development
- Inspired by the need for 24/7 personal representation

## 📧 Questions?

Open an issue or contribute improvements!

---

**Represent yourself professionally, 24/7! 🚀**
