# 🚀 LangChain Learning Series

A comprehensive, step-by-step guide to building AI applications with **LangChain** and **Google Generative AI**. This repository demonstrates the complete workflow from language models to retrieval-augmented applications.

---

## 📚 Notebook Overview

### Learning Path: From Basics to Advanced RAG

#### **Phase 1: Language Models & Prompting**

**1. Language Models** [`1_llm.ipynb`]
- Initialize Google Generative AI models
- Load environment variables with `.env`
- Basic LLM invocation using Gemini
- Understanding temperature and response generation

**2. Prompt Templates** [`2_promottemplate.ipynb`]
- Simple `PromptTemplate` for parameterized prompts
- `ChatPromptTemplate` for multi-turn conversations
- `MessagesPlaceholder` for conversation history
- Building dynamic prompts with context

**3. Structured Output** [`3_Structured_output.ipynb`]
- Extract structured data from LLMs using `TypedDict`
- Define data models with `Pydantic`
- JSON Schema validation
- Movie details extraction example

**4. Output Parsers** [`4_Output_parser.ipynb`]
- `StrOutputParser` for text extraction
- `JsonOutputParser` for JSON responses
- Building chains with output parsing
- Product information extraction

#### **Phase 2: Chains & Workflows**

**5. Chains** [`5_Chain.ipynb`]
- Simple chains with `|` operator
- Sequential chains for multi-step workflows
- Parallel chains using `RunnableParallel`
- Chain visualization with `get_graph().print_ascii()`
- Real-world examples:
  - Summary generation
  - Key points extraction
  - Combining multiple outputs

#### **Phase 3: Document Processing**

**6. Document Loaders** [`6_Document_loader.ipynb`]
- `TextLoader` - Plain text files
- `PyPDFLoader` - Single PDF documents
- `PyPDFDirectoryLoader` - Multiple PDFs
- `CSVLoader` - CSV files
- `JSONLoader` - JSON documents
- `UnstructuredLoader` - Multiple file types
- Batch loading documents from directories

**7. Text Splitters** [`7_Text_spilter.ipynb`]
- `CharacterTextSplitter` - Simple character-based splitting
- `RecursiveCharacterTextSplitter` - Intelligent recursive splitting
- `MarkdownHeaderTextSplitter` - Split by markdown headers
- Configurable chunk size and overlap
- Preserving metadata during splitting

#### **Phase 4: Embeddings & Vector Storage**

**8. Embeddings** [`8_Embeddings.ipynb`]
- Google Generative AI embeddings (`gemini-embedding-001`)
- Converting text to vector representations
- Embedding queries and documents
- Foundation for semantic search

**9. Vector Stores** [`9_Vector_Store.ipynb`]
- Chroma vector database setup
- Adding raw texts with `from_texts()`
- Adding documents with metadata
- Multiple collections
- Persistent storage
- Batch document management

**10. Retrievers** [`10_retriever.ipynb`]
- Creating retrievers from vector stores
- FAISS vector store integration
- **Search types:**
  - Similarity search (default)
  - MMR (Maximal Marginal Relevance) for diversity
  - Similarity score threshold
- Query-document matching
- Retrieving top-K most relevant documents

---

## 🏗️ Complete Workflow Example

```
User Input
    ↓
[Prompt Template] → Formatted Query
    ↓
[LLM] → Generate/Process
    ↓
[Output Parser] → Structured Response
    ↓
[Document Loader] → Load Documents
    ↓
[Text Splitter] → Chunks
    ↓
[Embeddings] → Vectors
    ↓
[Vector Store] → Store
    ↓
[Retriever] → Get Context
    ↓
[Chain] → Final Output
```

---

## 🛠️ Prerequisites

### Environment Setup
```bash
# Create virtual environment
python -m venv langvenv

# Activate (Windows PowerShell)
.\langvenv\Scripts\Activate.ps1

# Activate (macOS/Linux)
source langvenv/bin/activate
```

### Installation
```bash
# Install all dependencies
pip install -r requirements.txt

# Or upgrade existing packages
pip install -U langchain langchain-community langchain-core
```

### Configuration
Create a `.env` file in the project root:
```env
GOOGLE_API_KEY=your_api_key_here
```

Get your API key from [Google AI Studio](https://aistudio.google.com/app/apikey)

---

## 📦 Key Dependencies

| Package | Purpose |
|---------|---------|
| `langchain` | Core LangChain framework |
| `langchain-core` | Core abstractions |
| `langchain-community` | Community integrations |
| `langchain-google-genai` | Google Generative AI integration |
| `langchain_text_splitters` | Text splitting utilities |
| `chromadb` | Vector database |
| `faiss-cpu` | Vector similarity search |
| `pydantic` | Data validation |
| `python-dotenv` | Environment variables |

---

## 🎯 Use Cases

### 1. Q&A System
Load documents → Split → Embed → Store → Retrieve → Answer
(See notebooks: 6, 7, 8, 9, 10)

### 2. Structured Data Extraction
Prompt → LLM → Pydantic Output → Structured Data
(See notebooks: 2, 3, 4)

### 3. Multi-Step Workflows
Sequential chains for complex tasks
(See notebook: 5)

### 4. Conversational AI
Chat templates with message history
(See notebook: 2 - MessagesPlaceholder)

---

## 🚀 Quick Start Examples

### Example 1: Simple LLM Query
```python
from langchain_google_genai import ChatGoogleGenerativeAI
from dotenv import load_dotenv

load_dotenv()
llm = ChatGoogleGenerativeAI(model="gemini-3-flash-preview", temperature=0.6)
response = llm.invoke("What is AI?")
print(response.content)
```

### Example 2: Prompt Template Chain
```python
from langchain_core.prompts import PromptTemplate
from langchain_core.output_parsers import StrOutputParser

template = PromptTemplate.from_template("What is the capital of {country}?")
chain = template | llm | StrOutputParser()
result = chain.invoke({"country": "France"})
```

### Example 3: Document Retrieval
```python
from langchain_community.vectorstores import Chroma
from langchain_google_genai import GoogleGenerativeAIEmbeddings

embeddings = GoogleGenerativeAIEmbeddings(model="gemini-embedding-001")
db = Chroma.from_texts(texts, embeddings, persist_directory="db")
retriever = db.as_retriever(search_type="similarity", search_kwargs={"k": 3})
results = retriever.invoke("Your query")
```

---

## 📖 Learning Tips

1. **Start Sequential**: Follow notebooks 1→10 in order
2. **Experiment**: Modify prompts and parameters
3. **Combine Techniques**: Mix multiple notebooks for real projects
4. **Check Metadata**: Pay attention to document metadata in loaders
5. **Test Locally**: Run each notebook independently first
6. **Monitor Costs**: Google Generative AI has usage limits

---

## 🔗 Related Resources

- [LangChain Documentation](https://python.langchain.com/)
- [Google Generative AI](https://ai.google.dev/)
- [Chroma Documentation](https://docs.trychroma.com/)
- [FAISS Wiki](https://github.com/facebookresearch/faiss/wiki)

---

## 📝 License

This project is provided as educational material.

---

## 💡 Notes

- All notebooks use **Google Generative AI** (Gemini models)
- Some notebooks include **Arabic comments** for clarity
- Environment variables are required for API access
- Be mindful of token usage and rate limits
