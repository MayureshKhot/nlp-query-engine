# NLP Query Engine for Employee Data

A full-stack application that provides a natural language query interface for an employee database. It dynamically adapts to the database schema and can query both structured (SQL) and unstructured (documents) data without hard-coding table or column names.

## 🚀 Core Features

- **Dynamic Schema Discovery**: Automatically discovers and visualizes the database schema upon connection
- **Natural Language Queries**: Translates natural language questions into SQL queries or semantic document searches using LLMs
- **Hybrid Search**: Capable of fetching data from both the SQL database and uploaded documents to answer a single query
- **Document Ingestion**: Supports uploading various document formats (PDF, DOCX, TXT, CSV) for semantic search
- **Performance Optimized**: Features query caching, connection pooling, and asynchronous operations

## 🛠 Tech Stack

- **Backend**: FastAPI (Python)
- **Frontend**: React (Vite)
- **Database**: PostgreSQL (can be adapted for MySQL)
- **LLM Integration**: Groq for fast NL-to-SQL translation
- **Embeddings**: Sentence-Transformers for document embeddings
- **Vector Store**: FAISS for efficient similarity search
- **Containerization**: Docker & Docker Compose

## 📁 Project Structure

```
project/
├── backend/
│   ├── api/
│   │   ├── routes/
│   │   │   ├── ingestion.py
│   │   │   └── query.py
│   │   └── main.py
│   ├── services/
│   │   ├── schema_discovery.py
│   │   ├── document_processor.py
│   │   ├── query_engine.py
│   │   └── cache.py
│   ├── core/
│   │   └── config.py
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── App.jsx
│   │   └── index.css
│   ├── public/
│   ├── package.json
│   └── vite.config.js
├── docker-compose.yml
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+ installed on your local machine
- Node.js 18+ installed on your local machine
- A Groq API key for natural language processing

### Setup

1. **Clone the repository:**
   ```bash
   git clone <your-repo-url>
   cd nlp-query-engine
   ```

2. **Create Environment File:**
   Create a `.env` file in the root directory and add your Groq API key:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   ```

3. **Quick Start (Windows):**
   ```bash
   start-all.bat
   ```

4. **Quick Start (Linux/Mac):**
   ```bash
   chmod +x start-all.sh
   ./start-all.sh
   ```

5. **Manual Start:**
   
   **Backend:**
   ```bash
   cd backend
   pip install -r requirements-simple.txt
   python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```
   
   **Frontend:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

6. **Access the Application:**
   - **Frontend**: Open your browser and go to http://localhost:5173
   - **Backend API Docs**: Go to http://localhost:8000/docs

## 🔧 How It Works

### Data Ingestion

1. **Database**: On the UI, provide a PostgreSQL connection string. The backend will connect, automatically discover the schema (tables, columns, relationships), and display it.

2. **Documents**: Drag and drop documents (PDF, DOCX, etc.). The backend processes them, creates text embeddings, and stores them in a FAISS vector store for searching.

### Querying

1. Type a question in plain English (e.g., "Show me engineers hired last year with python skills")
2. The backend classifies the query:
   - **SQL queries**: Uses Groq's LLM to convert your question into a SQL query based on the discovered schema
   - **Document queries**: Performs a semantic search on the ingested document vectors
   - **Hybrid queries**: Combines both SQL and document search results
3. Results from both sources are combined and displayed

## 🎯 Query Types

### SQL Queries
- "Show me all employees in the Engineering department"
- "What's the average salary by department?"
- "List employees hired in the last 6 months"

### Document Queries
- "Find resumes with Python experience"
- "Search for performance reviews mentioning leadership"
- "Look for documents containing machine learning skills"

### Hybrid Queries
- "Show me all engineers and their skills from resumes"
- "Find employees with Python experience and their salary data"
- "Combine database info with document search results"

## 🔧 API Endpoints

### Database Connection
- `POST /api/connect-database` - Connect to database and discover schema

### Document Management
- `POST /api/upload-documents` - Upload and process documents
- `GET /api/documents` - List all uploaded documents
- `DELETE /api/documents/{filename}` - Delete a specific document

### Query Processing
- `POST /api/query` - Process natural language queries
- `GET /api/query/history` - Get query history
- `DELETE /api/query/cache` - Clear query cache

### Health & Status
- `GET /health` - Health check endpoint
- `GET /` - API information

## 🐳 Docker Services

- **postgres**: PostgreSQL database
- **backend**: FastAPI application
- **redis**: Caching service
- **frontend**: React development server

## 🔑 Environment Variables

```env
# Required
GROQ_API_KEY=your_groq_api_key_here

# Database
DATABASE_URL=postgresql://postgres:postgres@postgres:5432/nlp_query_engine

# Redis
REDIS_URL=redis://redis:6379

# Application Settings
CACHE_TTL=3600
MAX_FILE_SIZE=10485760
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2
VECTOR_DIMENSION=384
MAX_RESULTS=100

# CORS
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173,http://127.0.0.1:5173
```

## 🚀 Development

### Backend Development
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### Frontend Development
```bash
cd frontend
npm install
npm run dev
```

## 📊 Performance Features

- **Connection Pooling**: Efficient database connection management
- **Query Caching**: Redis-based caching for frequently asked queries
- **Asynchronous Processing**: Non-blocking document processing
- **Vector Search**: FAISS-optimized semantic search
- **Chunked Processing**: Efficient handling of large documents

## 🔍 Advanced Features

- **Schema Visualization**: Interactive database schema display
- **Query Classification**: Intelligent routing between SQL and document search
- **Hybrid Results**: Combined results from multiple data sources
- **Execution Metrics**: Query performance tracking
- **Error Handling**: Comprehensive error reporting and recovery

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions, please open an issue in the repository or contact the development team.