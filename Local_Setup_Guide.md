# 💻 Local Development Setup - VS Code Guide

This guide will walk you through setting up the ADGM Corporate Agent on your local machine using VS Code. Perfect for developers or anyone who wants to run this locally.

## 🎯 Before You Start

**What you'll need:**
- A computer with at least 4GB free RAM
- Python 3.8 or newer (check with `python --version`)
- VS Code installed
- About 30 minutes of setup time
- Internet connection (for downloading dependencies)

**What you'll get:**
- A fully functional legal document analysis system
- AI-powered compliance checking
- Web interface for easy document upload
- Detailed analysis reports and reviewed documents

## 📁 Step 1: Project Structure Setup

After downloading/cloning the project, your folder should look like this:

```
📁 ADGM_CORP_AGENT1/                    ← Main project folder
├── 📁 .venv/                           ← Virtual environment (you'll create this)
├── 📁 app/                             ← Main application code
│   ├── 📁 models/
│   │   └── 📄 llm_client.py            ← AI client for Gemini
│   ├── 📄 checklist.py                 ← Document requirement lists
│   ├── 📄 comments.py                  ← Word document comment insertion
│   ├── 📄 parser.py                    ← Document type detection
│   ├── 📄 rag.py                       ← Legal knowledge retrieval
│   ├── 📄 rules.py                     ← Compliance checking rules
│   ├── 📄 summary.py                   ← Document summarization
│   └── 📄 ui.py                        ← Streamlit web interface
├── 📁 data/                            ← Your legal reference documents
│   └── 📁 adgm_laws/                   ← Put PDF/DOCX legal files here
├── 📁 chroma_db/                       ← Vector database (auto-created)
├── 📄 ingest.py                        ← Script to build knowledge base
├── 📄 requirements.txt                 ← Python packages needed
├── 📄 .env                             ← Your API keys (you create this)
├── 📄 README.md                        ← Documentation
└── 📄 LOCAL_SETUP_GUIDE.md            ← This file
```

## 🚀 Step 2: VS Code Setup

### Open Project in VS Code
1. **Open VS Code**
2. **File → Open Folder** 
3. **Select your ADGM_CORP_AGENT1 folder**

### Install Python Extension
1. **Go to Extensions** (Ctrl/Cmd + Shift + X)
2. **Search for "Python"** 
3. **Install the official Microsoft Python extension**

### Set Up Python Environment
1. **Open Terminal in VS Code** (Ctrl/Cmd + `)
2. **Create virtual environment:**
   ```bash
   python -m venv .venv
   ```
3. **Activate it:**
   - **Mac/Linux:** `source .venv/bin/activate`
   - **Windows:** `.venv\Scripts\activate`

4. **You should see (.venv) in your terminal prompt**

### Install Dependencies
```bash
pip install -r requirements.txt
```

**This will take a few minutes** as it downloads:
- Streamlit (web interface)
- AI models and libraries
- Document processing tools
- Vector database components

## 🔑 Step 3: Get Your API Key

### Why do you need this?
The system uses Google's Gemini AI to analyze documents and provide suggestions. It's free and pretty generous with usage limits.

### Getting the key:
1. **Go to [Google AI Studio](https://makersuite.google.com/app/apikey)**
2. **Sign in with your Google account**
3. **Click "Create API Key"**
4. **Copy the key** (it looks like: `AIzaSyABC123...`)

### Adding the key:
1. **Create a new file called `.env`** in your main project folder
2. **Add this line:** `GEMINI_API_KEY=your_actual_key_here`
3. **Save the file**

**Example .env file:**
```
GEMINI_API_KEY=AIzaSyABCDEFGHIJKLMNOPQRSTUVWXYZ1234567
```

## 📚 Step 4: Add Legal Documents

### What to add:
Put your ADGM legal reference documents in `data/adgm_laws/`. These should be official documents like:
- Companies Regulations 2020
- Employment Regulations
- Licensing requirements
- Standard form templates
- Registration procedures

### Supported formats:
- **PDF files** (.pdf)
- **Word documents** (.docx)

### How to add them:
1. **Navigate to `data/adgm_laws/` folder**
2. **Copy your legal reference documents there**
3. **Make sure they're not password-protected**

**Example:**
```
📁 data/adgm_laws/
├── 📄 ADGM-Companies-Regulations-2020.pdf
├── 📄 Employment-Regulations-2019.pdf
├── 📄 Standard-Articles-Template.docx
└── 📄 UBO-Declaration-Form.docx
```

## 🧠 Step 5: Build the Knowledge Base

This step processes all your legal documents and creates a searchable AI knowledge base.

### Run the ingestion:
```bash
python ingest.py
```

### What you should see:
```
Found 4 files to process...
Processing file 1/4: ADGM-Companies-Regulations-2020.pdf
  Extracted 156 chunks from ADGM-Companies-Regulations-2020.pdf
Processing file 2/4: Employment-Regulations-2019.pdf
  Extracted 89 chunks from Employment-Regulations-2019.pdf
...
✅ Successfully ingested 309 chunks from 4 files into 'adgm_laws'.
Database stored at: ./chroma_db
✅ Database test query successful: Section 1: Interpretation...
```

**This creates a `chroma_db` folder** with your searchable legal knowledge base.

## 🎮 Step 6: Run the Application

### Start the web interface:
```bash
streamlit run app/ui.py
```

### What happens:
1. **Streamlit starts up** (takes ~10-30 seconds)
2. **Your browser opens** to `http://localhost:8501`
3. **You see the ADGM Corporate Agent interface**

### If browser doesn't open:
- **Manually go to:** `http://localhost:8501`
- **Check terminal** for any error messages

## 🧪 Step 7: Test It Out

### Upload a test document:
1. **Click "Browse files" or drag & drop**
2. **Select a .docx file** (start with something simple)
3. **Watch the processing** happen in real-time
4. **Review the results** - summaries, issues, suggestions

### What you should see:
- Document type detection
- Compliance issue identification  
- Severity ratings (High/Medium/Low)
- Suggestions with legal citations
- Process detection (e.g., "Company Incorporation")
- Missing document checklist

## 🔧 VS Code Development Tips

### Recommended Extensions:
- **Python** (Microsoft) - Already installed
- **Python Docstring Generator** - For documentation
- **GitLens** - If using git
- **Bracket Pair Colorizer** - Makes code easier to read

### VS Code Settings:
1. **Ctrl/Cmd + Shift + P** → "Python: Select Interpreter"
2. **Choose the .venv interpreter** (should show the path to your virtual environment)

### Debugging:
1. **Set breakpoints** by clicking left of line numbers
2. **F5 to start debugging**
3. **Configure launch.json** if needed for Streamlit debugging

### Terminal Tips:
- **Keep virtual environment activated** (should see (.venv) in prompt)
- **Use integrated terminal** (Ctrl/Cmd + `) for everything
- **Multiple terminals** available via the + button

## 🐛 Common Issues & Solutions

### "ModuleNotFoundError"
**Problem:** Python can't find installed packages
**Solution:** 
```bash
# Make sure virtual environment is activated
source .venv/bin/activate  # Mac/Linux
.venv\Scripts\activate     # Windows

# Reinstall requirements
pip install -r requirements.txt
```

### "Port already in use"
**Problem:** Streamlit port 8501 is busy
**Solution:**
```bash
# Kill existing Streamlit processes
pkill -f streamlit

# Or use different port
streamlit run app/ui.py --server.port 8502
```

### "RAG database is empty"
**Problem:** Knowledge base wasn't built properly
**Solution:**
```bash
# Run ingestion again
python ingest.py

# Test database
python -c "from app.rag import debug_rag_database; debug_rag_database()"
```

### "SSL/urllib3 warnings"
**Problem:** Harmless SSL warnings on macOS
**Solution:** These don't affect functionality, safe to ignore

### "Rate Limit" or "Quota Exceeded"
**Problem:** Hit Gemini free tier limits
**Solutions:**
```bash
# Option 1: Wait (free tier resets daily)
# Option 2: Upgrade to Gemini Pro (paid)
# Option 3: Switch AI model in app/models/llm_client.py
```

**Free Tier Limits:**
- 15 requests per minute
- 1,500 requests per day  
- 1M requests per month

**For Heavy Usage:** Consider upgrading to Gemini Pro or switching to OpenAI/Claude

## 📊 Understanding the Code Structure

### Key Files to Know:

**🎯 `app/ui.py`** - Main web interface
- Streamlit app that users interact with
- Handles file uploads and displays results
- Coordinates all other components

**🧠 `app/parser.py`** - Document analysis
- Detects document types using patterns and AI
- Extracts text from Word documents
- Core intelligence for document classification

**⚖️ `app/rules.py`** - Compliance checking
- Contains all the legal compliance rules
- Checks for missing clauses, wrong jurisdiction, etc.
- Generates suggestions using AI + legal knowledge

**📚 `app/rag.py`** - Legal knowledge system
- Interfaces with the vector database
- Retrieves relevant legal information
- Powers AI suggestions with real legal context

**🔧 `ingest.py`** - Knowledge base builder
- Processes PDF and Word legal documents
- Creates searchable vector embeddings
- One-time setup (or when adding new legal docs)

## 🚀 Advanced Development

### Adding New Document Types:
1. **Edit `app/parser.py`** 
2. **Add patterns to `TYPE_RULES`**
3. **Test with sample documents**

### Adding Compliance Rules:
1. **Edit `app/rules.py`**
2. **Add new checks to `red_flags()` function**
3. **Include severity and suggestions**

### Custom Legal Knowledge:
1. **Add documents to `data/adgm_laws/`**
2. **Re-run `python ingest.py`**
3. **Knowledge base automatically updates**

## 🎉 You're All Set!

You should now have:
- ✅ **Working development environment**
- ✅ **AI-powered document analysis**
- ✅ **Web interface for easy use**
- ✅ **Legal knowledge base**
- ✅ **VS Code properly configured**

**Next steps:**
- Try uploading different document types
- Experiment with the analysis results
- Customize rules for your specific needs
- Add more legal reference documents

**Need help?** Check the main README.md for troubleshooting tips!

---

*Happy coding! 🚀 You're now ready to analyze ADGM legal documents like a pro.*
