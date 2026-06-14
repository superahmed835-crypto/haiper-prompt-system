# Haiper Implementation Guide

## 🚀 How to Use Haiper

### Platform-Specific Guides

#### Claude (Claude.ai & API)

**Web Interface:**
1. Go to https://claude.ai
2. Start a new conversation
3. Paste the entire `haiper-prompt.md` content
4. Continue with your questions

**API Integration:**
```python
import anthropic

client = anthropic.Anthropic(api_key="your-api-key")

with open('haiper-prompt.md', 'r') as f:
    system_prompt = f.read()

response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=4096,
    system=system_prompt,
    messages=[
        {
            "role": "user",
            "content": "Your question here"
        }
    ]
)

print(response.content[0].text)
```

---

#### Google Gemini

**Web Interface:**
1. Go to https://gemini.google.com
2. Start a new conversation
3. Paste the `haiper-prompt.md` content
4. Continue with your questions

**API Integration:**
```python
import google.generativeai as genai

genai.configure(api_key="your-api-key")

with open('haiper-prompt.md', 'r') as f:
    system_prompt = f.read()

model = genai.GenerativeModel(
    model_name="gemini-2.0-flash",
    system_instruction=system_prompt
)

response = model.generate_content("Your question here")
print(response.text)
```

---

#### DeepSeek

**Web Interface:**
1. Go to https://chat.deepseek.com
2. Create a new chat
3. Paste the `haiper-prompt.md` content
4. Begin using Haiper

**API Integration:**
```python
from openai import OpenAI

client = OpenAI(
    api_key="your-api-key",
    base_url="https://api.deepseek.com"
)

with open('haiper-prompt.md', 'r') as f:
    system_prompt = f.read()

response = client.chat.completions.create(
    model="deepseek-chat",
    messages=[
        {
            "role": "system",
            "content": system_prompt
        },
        {
            "role": "user",
            "content": "Your question here"
        }
    ],
    max_tokens=4096
)

print(response.choices[0].message.content)
```

---

### 💾 Installation Methods

#### Method 1: Copy & Paste
- Copy entire `haiper-prompt.md` content
- Paste into your AI chat interface
- Start using immediately

#### Method 2: File Integration
```bash
# Clone the repository
git clone https://github.com/superahmed835-crypto/haiper-prompt-system.git
cd haiper-prompt-system

# Use the prompt in your application
cat haiper-prompt.md
```

#### Method 3: Docker Setup
```dockerfile
FROM python:3.11

WORKDIR /app

COPY haiper-prompt.md .
COPY requirements.txt .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

**requirements.txt:**
```
anthropic==0.7.0
google-generativeai==0.3.0
openai==1.0.0
```

---

## 🎯 Best Practices

### 1. **For Research & Analysis**
```
Use Haiper for:
✅ Fact-checking with verification links
✅ Complex problem decomposition
✅ Literature review assistance
✅ Data interpretation

Add custom instructions:
"For this research, I need:
- Academic source links (Google Scholar)
- Recent publications
- Expert perspectives"
```

### 2. **For Code Development**
```
Use Haiper for:
✅ Code architecture planning
✅ Debugging with step-by-step analysis
✅ Learning new frameworks
✅ Security review

Add custom instructions:
"For code tasks, please:
- Always include type hints
- Provide unit test examples
- Link to official documentation"
```

### 3. **For Creative Work**
```
Use Haiper for:
✅ Story ideation with research
✅ Character development
✅ Visual concept creation
✅ Content planning

Add custom instructions:
"For creative work:
- Include reference links
- Suggest similar works
- Break down the creative process"
```

### 4. **For Business/Decision Making**
```
Use Haiper for:
✅ Market research analysis
✅ Risk assessment
✅ Strategy formulation
✅ Competitor analysis

Add custom instructions:
"For business decisions:
- Always cite data sources
- Show confidence levels
- Present multiple scenarios"
```

---

## 🔧 Customization Examples

### Custom Haiper for Data Science

```markdown
## Additional System Requirements for Data Science

### 1. Statistical Verification
- Always show calculation steps
- Provide statistical confidence intervals
- Link to academic papers for complex methods

### 2. Code Verification
- Include pandas/numpy documentation links
- Show data validation steps
- Provide visualization examples

### 3. Common Searches
- https://github.com/search?q=pandas+data+analysis
- https://scikit-learn.org/
- https://stackoverflow.com/questions/tagged/pandas
```

### Custom Haiper for DevOps

```markdown
## Additional System Requirements for DevOps

### 1. Security Checks
- Always review for security best practices
- Link to security standards (OWASP, CIS)
- Show potential vulnerabilities

### 2. Infrastructure as Code
- Always include documentation
- Link to official provider docs
- Show before/after configurations

### 3. Monitoring & Logging
- Always suggest monitoring setup
- Link to observability guides
- Show sample dashboards
```

### Custom Haiper for Education

```markdown
## Additional System Requirements for Education

### 1. Learning Progression
- Break down topics by difficulty level
- Suggest prerequisites
- Link to beginner/advanced resources

### 2. Interactive Examples
- Provide code you can run immediately
- Include quizzes/self-assessment questions
- Link to practice problems

### 3. Real-World Applications
- Show how concepts apply in practice
- Link to case studies
- Suggest projects to practice
```

---

## 📊 Monitoring & Evaluation

### Metrics to Track

**1. Accuracy**
```
Track: Percentage of claims with verified sources
Target: 95%+ of claims have verification links
```

**2. User Satisfaction**
```
Track: Did users find verification links helpful?
Monitor: Feedback on response clarity
```

**3. Response Quality**
```
Track: Are responses decomposed logically?
Monitor: User ability to verify claims independently
```

### Evaluation Script

```python
def evaluate_haiper_response(response):
    """Check if response follows Haiper principles"""
    
    checks = {
        "has_verification_links": "https://" in response,
        "shows_reasoning": "step" in response.lower() or "because" in response.lower(),
        "states_uncertainty": any(phrase in response.lower() for phrase in 
                                  ["uncertain", "confident", "likely", "probably"]),
        "structured_format": any(marker in response for marker in 
                                ["##", "1.", "**", "-"]),
        "cites_sources": "search?q=" in response or "https://github.com" in response
    }
    
    score = sum(checks.values()) / len(checks)
    print(f"Haiper Compliance Score: {score:.0%}")
    
    for check, passed in checks.items():
        status = "✅" if passed else "❌"
        print(f"{status} {check}")
    
    return score
```

---

## 🐛 Troubleshooting

### Issue: "Haiper isn't providing verification links"

**Solution:**
- Paste the full prompt again (some links might be missing)
- Explicitly ask: "Please include verification links for each claim"
- Check if you're using the latest version

### Issue: "Responses are too long/detailed"

**Solution:**
Add to your initial prompt:
```
"Please keep responses concise: 
- Maximum 2-3 paragraphs for simple questions
- Numbered lists for complex topics
- Bold key points"
```

### Issue: "Haiper is refusing to help with legitimate requests"

**Solution:**
- Clarify your intent: "This is for educational purposes"
- Provide more context
- Ask why Haiper refused (it should explain)

### Issue: "Getting inconsistent responses across platforms"

**Solution:**
- Ensure you're using the complete prompt (copy-paste carefully)
- Different models may interpret nuance differently
- Try the same question multiple times

---

## 📈 Advanced Usage

### Chaining Haiper with Other Tools

```python
# Combine Haiper with Embeddings for semantic search
from sentence_transformers import SentenceTransformer
import anthropic

model = SentenceTransformer('all-MiniLM-L6-v2')
client = anthropic.Anthropic()

# Get Haiper's response
with open('haiper-prompt.md', 'r') as f:
    system_prompt = f.read()

response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=2000,
    system=system_prompt,
    messages=[{"role": "user", "content": "Your question"}]
)

# Embed response for semantic search
response_text = response.content[0].text
embedding = model.encode(response_text)

# Use for similarity matching with your knowledge base
print(f"Response embedding created: {len(embedding)} dimensions")
```

### Multi-Model Comparison

```python
# Compare same question across Haiper instances
import anthropic
import google.generativeai as genai
from openai import OpenAI

with open('haiper-prompt.md', 'r') as f:
    prompt = f.read()

question = "Your question here"

# Claude
claude_client = anthropic.Anthropic()
claude_response = claude_client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=2000,
    system=prompt,
    messages=[{"role": "user", "content": question}]
)

# Gemini
genai.configure(api_key="...")
gemini_model = genai.GenerativeModel(
    model_name="gemini-2.0-flash",
    system_instruction=prompt
)
gemini_response = gemini_model.generate_content(question)

# DeepSeek
deepseek_client = OpenAI(api_key="...", base_url="https://api.deepseek.com")
deepseek_response = deepseek_client.chat.completions.create(
    model="deepseek-chat",
    messages=[
        {"role": "system", "content": prompt},
        {"role": "user", "content": question}
    ]
)

# Compare
print("=== CLAUDE ===")
print(claude_response.content[0].text[:500])
print("\n=== GEMINI ===")
print(gemini_response.text[:500])
print("\n=== DEEPSEEK ===")
print(deepseek_response.choices[0].message.content[:500])
```

---

## 📚 Resources

- [Claude Documentation](https://claude.ai/docs)
- [Gemini API Docs](https://ai.google.dev)
- [DeepSeek API](https://platform.deepseek.com)
- [Prompt Engineering Guide](https://www.promptingguide.ai/)
- [AI Safety Resources](https://www.aisafetyfundamentals.com/)

---

## 🤝 Getting Help

- Found a bug? Open an issue
- Have improvements? Submit a pull request
- Need clarification? Check EXAMPLES.md
- Want to compare? See COMPARISON.md
