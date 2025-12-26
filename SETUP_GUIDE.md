# Setting Up Your Personal Data

This guide will help you set up the `me` folder with your personal information.

## 📁 Folder Structure

Create a `me` folder in your project directory with two files:

```
personal-ai-agent/
├── me/
│   ├── linkedin.pdf      ← Your LinkedIn profile
│   └── summary.txt       ← Your personal summary
└── ... (other files)
```

## 📄 Step 1: Export Your LinkedIn Profile

### Method 1: Direct Export (Recommended)
1. Go to your LinkedIn profile
2. Click the "More" button (three dots)
3. Select "Save to PDF"
4. Save the file as `linkedin.pdf` in the `me` folder

### Method 2: Print to PDF
1. Open your LinkedIn profile
2. Use browser's Print function (Ctrl+P / Cmd+P)
3. Select "Save as PDF"
4. Save as `linkedin.pdf` in the `me` folder

### Important Notes:
- ✅ Ensure the PDF contains selectable text (not a scanned image)
- ✅ Include all relevant sections (Experience, Education, Skills, etc.)
- ✅ Make sure it's up to date
- ⚠️ This file will be added to `.gitignore` for privacy

## ✍️ Step 2: Create Your Summary

Create `summary.txt` in the `me` folder with your personal summary.

### What to Include:

**Opening Statement** (1-2 sentences)
- Your role and years of experience
- Primary field or industry

**Key Skills** (3-5 bullet points)
- Technical skills
- Domain expertise
- Tools and technologies

**Notable Achievements** (2-4 bullet points)
- Specific accomplishments with results
- Projects or products you've built
- Recognition or awards

**Current Focus** (1-2 sentences)
- What you're working on now
- What you're learning
- Your career goals

**Areas of Interest** (1 sentence)
- Topics you're passionate about
- Areas where you want to help others

### Example Summary:

```text
I'm a software engineer with 5 years of experience in AI and machine learning, 
specializing in natural language processing and computer vision applications.

My key areas of expertise include:
- Deep learning with PyTorch and TensorFlow
- Large language model fine-tuning and deployment
- MLOps and production ML systems
- Python, FastAPI, and Docker

Notable achievements:
- Led development of an NLP system that reduced customer support time by 40%
- Published 3 papers on transformer architectures at top-tier ML conferences
- Built and deployed ML pipelines serving 1M+ requests per day
- Mentored 10+ junior engineers in ML best practices

Currently, I'm focused on making AI more accessible and building tools that help 
developers integrate ML into their applications more easily.

I'm passionate about open-source AI and have contributed to several popular ML libraries. 
Feel free to ask me about my experience with LLMs, MLOps, or building AI products.
```

### Tips for a Great Summary:

✅ **Do:**
- Be specific with numbers and results
- Mention concrete technologies and tools
- Highlight unique experiences
- Keep it professional but personable
- Focus on what makes you stand out

❌ **Don't:**
- Be overly modest or generic
- Use clichés like "hard worker" or "team player"
- Include sensitive personal information
- Make unverifiable claims
- Write more than 500 words

## 🔒 Privacy Note

Both files are automatically excluded from Git via `.gitignore`:

```gitignore
# Personal data - NEVER commit your LinkedIn or summary!
me/
linkedin.pdf
summary.txt
```

This means:
- ✅ Your personal data stays on your computer
- ✅ Safe to push code to public GitHub
- ✅ Others can still use your code with their own data

## ✅ Verification

After creating both files, verify the setup:

```bash
# Check files exist
ls me/

# Should show:
# linkedin.pdf
# summary.txt

# Verify PDF is readable
python -c "from pypdf import PdfReader; print(len(PdfReader('me/linkedin.pdf').pages), 'pages')"

# Verify summary
cat me/summary.txt
```

## 🚀 Next Steps

Once you've created both files:

1. Update your name in the code:
   ```python
   name = "Your Actual Name"
   ```

2. Run the notebook and test:
   - Ask about your background
   - Ask about specific skills
   - Ask about your experience

3. Iterate:
   - If agent doesn't know something, add it to summary
   - Refine wording based on responses
   - Adjust tone in system prompt

## 💡 Tips for Best Results

### For LinkedIn PDF:
- Include recommendations section
- Make sure all jobs are listed
- Include skills endorsements
- Add certifications and education

### For Summary:
- Update it regularly (every 3-6 months)
- Tailor to your target audience
- Include keywords for your field
- Highlight recent work prominently

## 🆘 Troubleshooting

**"PDF text extraction failed"**
- Re-export PDF from LinkedIn
- Try print-to-PDF instead
- Check PDF isn't password protected
- Verify text is selectable in PDF reader

**"Summary too generic"**
- Add specific projects and results
- Include concrete technologies
- Mention unique experiences
- Use numbers to quantify impact

**"Agent gives wrong information"**
- Check LinkedIn PDF is up to date
- Add missing info to summary.txt
- Review what's in the system prompt
- Test specific questions

---

Good luck setting up your personal AI agent! 🚀
