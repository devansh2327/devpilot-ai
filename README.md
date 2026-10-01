# DevPilot

> AI-powered coding assistant for GitHub repositories, built with Retrieval-Augmented Generation (RAG).

DevPilot is a GitHub-connected AI coding assistant that allows developers to authenticate with GitHub, connect repositories, index source code, and chat with their codebase.

The project combines a **Spring Boot backend**, **Next.js frontend**, **OpenAI**, and **PostgreSQL with pgvector** to retrieve relevant code context and generate repository-aware AI responses.

---

## ✨ Features

- 🔐 **GitHub OAuth Authentication**
- 📂 **GitHub Repository Integration**
- 📑 **Repository Source-Code Indexing**
- ✂️ **Code Chunking** for efficient retrieval
- 🧠 **Retrieval-Augmented Generation (RAG)**
- 🔎 **Semantic Code Retrieval** using vector similarity
- 🗄️ **PostgreSQL + pgvector** for vector storage
- 🤖 **OpenAI-powered responses**
- 💬 **Repository-aware AI Chat**
- ⚡ **Streaming AI Responses** using Server-Sent Events (SSE)
- 📚 **Source Citation Mapping**
- 🎨 **Next.js Dashboard UI**

---

## 🏗️ Architecture

```text
                         ┌──────────────────────┐
                         │      Developer       │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    Next.js Client    │
                         │ React + TypeScript   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   Spring Boot API    │
                         │ Security + REST APIs │
                         └───────┬───────┬──────┘
                                 │       │
                    ┌────────────┘       └──────────────┐
                    ▼                                   ▼
          ┌─────────────────┐                 ┌──────────────────┐
          │     GitHub      │                 │    AI / RAG      │
          │ OAuth + Repos   │                 │    Pipeline      │
          └────────┬────────┘                 └────────┬─────────┘
                   │                                   │
                   ▼                                   ▼
          ┌─────────────────┐                 ┌──────────────────┐
          │ Repository      │                 │ Code Retrieval   │
          │ Indexing        │                 │ + Prompt Context │
          └────────┬────────┘                 └────────┬─────────┘
                   │                                   │
                   ▼                                   ▼
          ┌─────────────────┐                 ┌──────────────────┐
          │ Code Chunking   │                 │     OpenAI       │
          └────────┬────────┘                 └────────┬─────────┘
                   │                                   │
                   ▼                                   │
          ┌────────────────────────────────────────────┐
          │            PostgreSQL + pgvector            │
          │              Vector Embeddings              │
          └────────────────────────────────────────────┘
```

---

## 🧠 How DevPilot Works

DevPilot uses a **Retrieval-Augmented Generation (RAG)** pipeline to provide answers grounded in the connected GitHub repository.

```text
GitHub Repository
        ↓
Repository Indexing
        ↓
Code Chunking
        ↓
Vector Embeddings
        ↓
PostgreSQL + pgvector
        ↓
User Question
        ↓
Semantic Code Retrieval
        ↓
Relevant Code Context
        ↓
RAG Prompt Construction
        ↓
OpenAI
        ↓
Streaming AI Response
        ↓
Next.js Chat Interface
```

### RAG Pipeline

1. **Repository Indexing** — Source files from a connected GitHub repository are processed for indexing.
2. **Code Chunking** — Source files are divided into smaller code chunks for efficient retrieval.
3. **Embedding Generation** — Code chunks are converted into vector embeddings.
4. **Vector Storage** — Embeddings are stored using PostgreSQL with the pgvector extension.
5. **Semantic Retrieval** — Relevant code is retrieved using vector similarity.
6. **Context Construction** — Retrieved code is assembled into contextual information for the AI prompt.
7. **AI Response** — OpenAI generates a response using the retrieved repository context.
8. **Streaming** — The response is streamed back to the Next.js frontend using SSE.
9. **Citation Mapping** — Retrieved context can be mapped back to relevant source information.

---

## 🛠️ Tech Stack

### Backend

- Java 21
- Spring Boot
- Spring Security
- Spring Data JPA
- Spring AI
- OpenAI
- PostgreSQL
- pgvector

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

### AI / RAG

- Retrieval-Augmented Generation (RAG)
- Code chunking
- Vector embeddings
- Semantic code retrieval
- pgvector vector store
- Context-aware prompt construction
- Streaming AI responses

### Infrastructure

- Docker
- Docker Compose
- PostgreSQL
- pgvector

---

## 📁 Project Structure

```text
devpilot/
│
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── devPilot/
│   │   │   │       └── backend/
│   │   │   │           ├── config/
│   │   │   │           ├── controllers/
│   │   │   │           ├── dto/
│   │   │   │           ├── entity/
│   │   │   │           ├── exceptions/
│   │   │   │           ├── repository/
│   │   │   │           ├── security/
│   │   │   │           └── services/
│   │   │   │               ├── ai/
│   │   │   │               ├── github/
│   │   │   │               └── indexing/
│   │   │   └── resources/
│   │   └── test/
│   ├── pom.xml
│   ├── mvnw
│   ├── mvnw.cmd
│   └── .mvn/
│
├── client/
│   ├── app/
│   │   ├── auth/
│   │   ├── chat/
│   │   ├── dashboard/
│   │   └── login/
│   ├── components/
│   ├── hooks/
│   ├── lib/
│   ├── public/
│   ├── package.json
│   └── tsconfig.json
│
├── docker/
│   └── postgres/
│
├── docker-compose.yml
├── .gitignore
└── README.md
```

### Important Backend Components

```text
services/
├── ai/
│   ├── ChatPromptBuilder.java
│   ├── ChatStreamHandler.java
│   ├── CitationMapper.java
│   ├── CodeContextRetriever.java
│   ├── RagSettings.java
│   └── RetrievedContext.java
│
├── github/
│
└── indexing/
    ├── CodeChunker.java
    ├── CodeFileFilter.java
    └── IndexingService.java
```

---

## 🚀 Getting Started

### Prerequisites

- Java 21+
- Node.js 20+
- npm
- Docker
- Docker Compose

Maven is optional because the backend includes the Maven Wrapper.

### 1. Clone the repository

```bash
git clone https://github.com/devansh2327/devpilot-ai.git
cd devpilot-ai
```

### 2. Start PostgreSQL + pgvector

```bash
docker compose up -d
```

The development database uses:

```text
Host:     localhost
Port:     5433
Database: devpilot
Username: postgres
```

Check the database container:

```bash
docker compose ps
```

### 3. Configure the backend

Configure the required settings in:

```text
backend/src/main/resources/application.properties
```

or through environment variables.

Typical configuration includes:

```text
GitHub OAuth Client ID
GitHub OAuth Client Secret
Frontend URL
OpenAI API configuration
Database configuration
```

> **Never commit API keys, OAuth secrets, database passwords, or other credentials to GitHub.**

### 4. Start the backend

Linux/macOS:

```bash
cd backend
./mvnw spring-boot:run
```

Windows PowerShell:

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

### 5. Start the frontend

Open another terminal:

```bash
cd client
npm install
npm run dev
```

Then open:

```text
http://localhost:3000
```

---

## 🔌 API Overview

The backend exposes APIs under the `/api` namespace.

### Authentication

```text
/api/auth/login-url
/api/auth/me
```

### Chat

```text
/api/chat/sessions
/api/chat/sessions/{id}
/api/chat/sessions/{id}/messages
```

The backend also provides repository-related functionality for connecting repositories and indexing source code.

---

## 🔐 Security

DevPilot integrates with GitHub OAuth and external AI services, so sensitive configuration should never be committed to the repository.

Keep the following outside Git:

- GitHub OAuth client secrets
- OpenAI API keys
- Database passwords
- Application secrets
- Session secrets
- Other private credentials

Use environment variables or local configuration files instead.

A local `.env` file can be used for development, but it should remain in `.gitignore`.

---

## 🧪 Development

Start the database:

```bash
docker compose up -d
```

Stop the database:

```bash
docker compose down
```

Run the backend:

```bash
cd backend
./mvnw spring-boot:run
```

Run the frontend:

```bash
cd client
npm run dev
```

---

## 📌 Current Scope

DevPilot focuses on repository-aware AI assistance for software development.

The core workflow combines:

- GitHub authentication
- Repository access
- Source-code indexing
- Code chunking
- Vector embeddings
- pgvector storage
- Semantic retrieval
- RAG-based prompt construction
- OpenAI-powered responses
- Streaming chat responses
- Source-aware citation mapping

---

## 🤝 Contributing

Contributions and improvements are welcome.

1. Fork the repository.
2. Create a feature branch:

```bash
git checkout -b feature/your-feature
```

3. Make your changes.
4. Test the relevant backend and frontend functionality.
5. Commit your changes:

```bash
git commit -m "Add your feature"
```

6. Push your branch and open a pull request.

---

## 📄 License

No license has been specified yet.

If you plan to make DevPilot open source, add an appropriate `LICENSE` file.

---

## 💡 Project Summary

**DevPilot** is an AI-powered coding assistant that lets developers chat with their GitHub repositories using Retrieval-Augmented Generation.

Instead of sending an entire codebase to an AI model, DevPilot indexes and chunks repository source code, stores vector embeddings in PostgreSQL with pgvector, retrieves relevant code for each question, and uses that context to generate a repository-aware response.

**GitHub → Indexing → Chunking → Embeddings → pgvector → Retrieval → RAG → OpenAI → Streaming Response**

⭐ If you find the project useful, consider starring the repository.
