2. Technology Stack
Backend
Technology
Choice & Rationale
Language
Java 25 / 26
Framework
Spring Boot 4
Concurrency
Virtual Threads (Project Loom) — replaces WebFlux complexity
AI Framework
Spring AI 1.x
LLM (local)
Ollama — zero cloud inference cost, sustainable
Vector Store
PostgreSQL + pgvector
Semantic Cache
Redis on Azure Cache for Redis
Streaming
SSE (Server-Sent Events) for LLM token streaming
API
GraphQL (data queries) + REST (internal connectors)
MCP
Spring AI MCP over SSE
Carbon Tracking
CodeCarbon

Java 25/26 Features to Showcase
Virtual Threads — replaces reactive overhead, clean imperative code
Structured Concurrency — coordinate multiple Irish data API fetches simultaneously
Scoped Values — pass request context instead of ThreadLocal
Sealed Classes — model Irish environmental data domain
Pattern Matching — process different EPA/Met Eireann response types
Records — immutable data transfer objects



