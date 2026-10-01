DevPilot

AI-powered coding assistant for GitHub repositories, built with
RAG.

DevPilot is a GitHub-connected AI coding assistant that lets developers
authenticate with GitHub, index their repositories, and chat with their
codebase using retrieval-augmented generation (RAG).

It combines a Spring Boot backend, Next.js frontend,
PostgreSQL + pgvector, and AI-powered code retrieval to provide
repository-aware answers grounded in the developer's own source code.

✨ Features

🔐 GitHub OAuth Login --- Authenticate securely with your GitHub
account.

📂 Repository Integration --- Connect and work with GitHub
repositories.

🔎 Codebase Indexing --- Index repository code for semantic
retrieval.

🧠 RAG-Powered Q&A --- Ask questions about your codebase and
retrieve relevant source context.

💬 AI Chat Sessions --- Maintain repository-aware conversations.

⚡ Streaming Responses --- Stream AI responses using Server-Sent
Events (SSE).

🗄️ Vector Search --- Store and retrieve code embeddings using
PostgreSQL and pgvector.

🎨 Modern Dashboard --- Next.js, React, TypeScript, and Tailwind
CSS frontend.

🔒 Secure Backend --- Spring Security and OAuth2-based
authentication.

🏗️ Architecture

                    ┌──────────────────────┐
                    │       Developer      │
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
                    │  Security + REST     │
                    └───────┬───────┬──────┘
                            │       │
                 ┌──────────┘       └───────────┐
                 ▼                              ▼
        ┌─────────────────┐            ┌─────────────────┐
        │     GitHub      │            │   AI / RAG      │
        │ OAuth + Repos   │            │ Code Retrieval  │
        └─────────────────┘            └────────┬────────┘
                                                │
                                                ▼
                                      ┌──────────────────┐
                                      │ PostgreSQL +     │
                                      │     pgvector     │
                                      └──────────────────┘

🛠️ Tech Stack

Backend

Java 21

Spring Boot

Spring Security

OAuth2

Spring Data JPA

PostgreSQL

pgvector

Spring AI / OpenAI-compatible AI integration

Server-Sent Events (SSE)

Frontend

Next.js

React

TypeScript

Tailwind CSS

shadcn-style UI components

Infrastructure

Docker

Docker Compose

PostgreSQL

pgvector (pgvector/pgvector:pg16)

📁 Project Structure

devpilot/
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── devPilot/backend/
│   │   │   │       ├── config/
│   │   │   │       ├── controllers/
│   │   │   │       ├── dto/
│   │   │   │       ├── entity/
│   │   │   │       ├── exceptions/
│   │   │   │       ├── repository/
│   │   │   │       ├── security/
│   │   │   │       └── services/
│   │   │   └── resources/
│   │   └── test/
│   ├── pom.xml
│   ├── mvnw
│   ├── mvnw.cmd
│   └── .mvn/
│
├── client/
│   ├── app/
│   ├── components/
│   ├── hooks/
│   ├── lib/
│   ├── public/
│   ├── package.json
│   ├── next.config.ts
│   └── tsconfig.json
│
├── docker/
│   └── postgres/
│
├── docker-compose.yml
├── .gitignore
└── README.md

🚀 Getting Started

Prerequisites

Make sure you have the following installed:

Java 21+

Node.js 20+

npm

Docker

Docker Compose

Maven is optional because the backend includes the Maven Wrapper.

1. Clone the repository

git clone https://github.com/<your-username>/<your-repository>.git
cd devpilot

2. Start PostgreSQL + pgvector

From the project root:

docker compose up -d

The development database is configured with:

Host:     localhost
Port:     5433
Database: devpilot
Username: postgres

Keep database credentials and API keys out of Git. Use environment
variables or local configuration files.

3. Configure the backend

Configure the required GitHub OAuth and AI provider settings in:

backend/src/main/resources/application.properties

or provide them through environment variables.

Typical configuration includes:

GitHub OAuth Client ID
GitHub OAuth Client Secret
Frontend URL
AI provider/API configuration
Database configuration

4. Start the backend

From the project root:

cd backend
./mvnw spring-boot:run

On Windows:

cd backend
.\mvnw.cmd spring-boot:run

5. Start the frontend

Open another terminal:

cd client
npm install
npm run dev

Open:

http://localhost:3000

🔄 How DevPilot Works

The application follows a repository-aware RAG workflow:

GitHub Login
     ↓
Connect Repository
     ↓
Fetch Repository Content
     ↓
Process & Index Source Code
     ↓
Generate / Store Embeddings
     ↓
PostgreSQL + pgvector
     ↓
User Asks a Question
     ↓
Semantic Retrieval
     ↓
Relevant Code Context
     ↓
AI Response
     ↓
Stream Response to Client

This allows the AI assistant to answer questions using relevant code
from the connected repository rather than relying only on the model's
general knowledge.

🔌 API Overview

The backend exposes APIs under the /api namespace.

Authentication

/api/auth/login-url
/api/auth/me

Chat

/api/chat/sessions
/api/chat/sessions/{id}
/api/chat/sessions/{id}/messages

Additional repository-related endpoints are available for repository
integration and indexing.

🧪 Development

Backend

Run the backend:

cd backend
./mvnw spring-boot:run

Frontend

Run the frontend:

cd client
npm run dev

Database

Start the database:

docker compose up -d

Stop the database:

docker compose down

🔐 Security Notes

Do not commit sensitive credentials to the repository.

Keep the following outside Git:

GitHub OAuth client secrets

AI API keys

Database passwords

Session or application secrets

Other private credentials

Use environment variables or local configuration for development.

📌 Current Scope

DevPilot is focused on repository-aware AI assistance for software
development. The core workflow combines GitHub authentication,
repository access, source-code indexing, vector retrieval, and
AI-powered chat.

🤝 Contributing

Contributions are welcome.

Fork the repository.

Create a feature branch.

git checkout -b feature/your-feature

Make your changes.

Run the relevant backend/frontend checks.

Commit your changes.

git commit -m "Add your feature"

Push your branch and open a pull request.

📄 License

No license has been specified yet.

If you plan to make the project open source, add an appropriate
LICENSE file.

DevPilot --- chat with your codebase, grounded in your repository.
