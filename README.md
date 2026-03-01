<h1 align="center">🚀 OpenAnalyst Web</h1>
<h3 align="center">Enterprise-Grade AI Search & Knowledge Intelligence Platform</h3>

<p align="center">
  AI-powered enterprise search platform with Advanced RAG, MCP integrations, and intelligent workflow orchestration.
</p>

<hr/>

<h2>🔍 Overview</h2>

<p>
OpenAnalyst Web is a scalable AI-powered enterprise search and knowledge intelligence platform 
designed to unify fragmented workplace data and transform it into actionable insights.
</p>

<p>It enables organizations to:</p>

<ul>
  <li>🔎 Search across multiple data sources using natural language</li>
  <li>📚 Retrieve context-aware answers with citations</li>
  <li>🤖 Build AI-powered workflows</li>
  <li>🧠 Create intelligent assistants on top of internal knowledge</li>
</ul>

<hr/>

<h2>🧠 Core Capabilities</h2>

<h3>🔎 Intelligent Enterprise Search</h3>
<ul>
  <li>Natural language querying</li>
  <li>Semantic search over structured & unstructured data</li>
  <li>Context-aware ranking</li>
  <li>Citation-backed responses</li>
</ul>

<h3>📚 Advanced RAG Pipeline</h3>
<ul>
  <li>Document ingestion & parsing</li>
  <li>Smart chunking strategies</li>
  <li>Vector embedding & similarity search</li>
  <li>Knowledge graph-backed retrieval</li>
  <li>Optimized context selection (token efficient)</li>
  <li>Multi-step reasoning workflows</li>
</ul>

<h3>🔗 MCP Integrations</h3>
<ul>
  <li>Model Context Protocol integrations</li>
  <li>Tool-aware agent workflows</li>
  <li>Structured tool execution</li>
  <li>Extensible AI capability layer</li>
</ul>

<h3>🔐 Secure Access-Control Retrieval</h3>
<ul>
  <li>Source-level permissions</li>
  <li>Role-based visibility filtering</li>
  <li>Secure document filtering before generation</li>
</ul>

<hr/>

<h2>🏗 High-Level Architecture</h2>

<pre>
Data Sources 
     ↓
Ingestion Layer
     ↓
Processing & Chunking
     ↓
Vector Store (Qdrant)
     ↓
Knowledge Graph (ArangoDB)
     ↓
RAG Orchestrator (LangGraph)
     ↓
LLM Inference Layer
     ↓
Web Interface
</pre>

<p><strong>Architecture Principles:</strong></p>

<ul>
  <li>Modular microservices</li>
  <li>Event-driven indexing</li>
  <li>Asynchronous processing</li>
  <li>Scalable retrieval</li>
  <li>Model-agnostic design</li>
</ul>

<hr/>

<h2>🧩 Supported Data Sources</h2>

<ul>
  <li>Google Drive, Docs, Sheets</li>
  <li>Microsoft OneDrive, SharePoint</li>
  <li>Slack</li>
  <li>Jira</li>
  <li>Confluence</li>
  <li>GitHub</li>
  <li>S3 / Azure Blob Storage</li>
  <li>PDFs (including scanned)</li>
  <li>DOCX, XLSX, PPTX</li>
  <li>Markdown</li>
  <li>Images (with OCR)</li>
  <li>Audio & Video transcripts</li>
</ul>

<hr/>

<h2>🛠 Tech Stack</h2>

<h3>Frontend</h3>
<ul>
  <li>React</li>
  <li>TypeScript</li>
  <li>Material UI</li>
  <li>Zod</li>
  <li>React Hook Form</li>
</ul>

<h3>Backend</h3>
<ul>
  <li>FastAPI</li>
  <li>LangChain</li>
  <li>LangGraph</li>
  <li>Qdrant (Vector Database)</li>
  <li>ArangoDB (Graph Database)</li>
  <li>Kafka</li>
  <li>Redis</li>
  <li>Celery</li>
  <li>Docling</li>
  <li>PyMuPDF</li>
  <li>OCRmyPDF</li>
  <li>Pandas</li>
  <li>etcd3</li>
</ul>

<hr/>

<h2>🚀 Deployment</h2>

<h3>Production (Docker)</h3>

<pre>
git clone https://github.com/AnantBisht07/OpenAnalyst-web.git
cd OpenAnalyst-web/deployment/docker-compose
docker compose -f docker-compose.prod.yml up -d
</pre>

<h3>Development</h3>

<pre>
docker compose -f docker-compose.dev.yml up --build -d
</pre>

<hr/>

<h2>🔐 Security</h2>

<ul>
  <li>HTTPS required for production</li>
  <li>Access filtering before generation</li>
  <li>Isolated service containers</li>
  <li>Environment-based secrets configuration</li>
</ul>

<hr/>

<h2>📈 Roadmap</h2>

<ul>
  <li>Code Search Intelligence</li>
  <li>Advanced MCP Tooling</li>
  <li>AI Agents Marketplace</li>
  <li>Personalized Search Ranking</li>
  <li>Kubernetes HA Deployment</li>
  <li>PageRank-based scoring</li>
</ul>

<hr/>

<h2 align="center">⭐ Support</h2>

<p align="center">
If this project helps you, consider starring the repository.
</p>
