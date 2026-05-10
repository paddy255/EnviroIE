EnviroIE 🌿
Project Scope & Architecture Document
Natural language querying of Irish environmental data, powered by Spring AI and local LLMs
1. Project Overview
Field
Detail
Project Name
EnviroIE (Environment Ireland)
Repository
github.com/paddy255/EnviroIE
Author
Patrick
Status
Scoping — May 2026


EnviroIE is a Spring AI powered RAG chatbot that answers natural language questions about Irish environmental data, running on a local Ollama model to minimise carbon footprint. It represents a unique intersection of enterprise Java architecture, agentic AI, and environmental data science.

Example Queries
What is the air quality in Dublin today compared to last month?
Which Dublin postcodes have the worst building energy ratings?
What are current water quality risks on the Liffey?
What was the rainfall in Phoenix Park last week?
How does Dublin's NO2 compare to WHO guidelines?

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


Frontend
Technology
Choice & Rationale
Framework
React 19
Styling
Tailwind CSS 4
Components
shadcn/ui (accessible, Tailwind-based)
Deployment
Azure Static Web Apps (free tier, global CDN)
Platform
PWA — installable on web, mobile and desktop from one codebase
Data Fetching
GraphQL client + SSE consumer (useOptimistic / Suspense)


Java 25/26 Features to Showcase
Virtual Threads — replaces reactive overhead, clean imperative code
Structured Concurrency — coordinate multiple Irish data API fetches simultaneously
Scoped Values — pass request context instead of ThreadLocal
Sealed Classes — model Irish environmental data domain
Pattern Matching — process different EPA/Met Eireann response types
Records — immutable data transfer objects

3. System Architecture
Deployment — Azure JAMstack
EnviroIE follows a clean JAMstack architecture deployed entirely on Azure:

Component
Azure Service
React 19 Frontend (PWA)
Azure Static Web Apps
Spring Boot 4 Modulith
Azure Container Apps (ACA) — scales to zero
Container Images
Azure Container Registry (ACR)
PostgreSQL + pgvector
Azure Database for PostgreSQL Flexible Server
Semantic Cache
Azure Cache for Redis
Secrets
Azure Key Vault
Observability
Azure Monitor + OpenTelemetry (OTel-AI)


Spring Boot 4 Modulith — Bounded Contexts
A single deployable Modulith with internal modules, each owning its own PostgreSQL schema and pgvector embeddings:
Weather Module — Met Eireann API connector, schema: weather, geolocation-queryable forecasts
Air Quality Module — AirQuality.ie / EPA connector, schema: air_quality, 115 monitoring stations, hourly AQIH data
Water Module — data.gov.ie WFD river/lake/groundwater datasets, schema: water
Energy Module — SEAI BER Research Tool, building energy ratings by postcode, schema: energy
EnviroIE RAG Module — Spring AI + MCP over SSE, Ollama local LLM, Structured Concurrency for parallel data source fetching, Redis semantic caching layer, EPA PDF reports ingested as RAG documents

Communication Protocols
Layer
Protocol
React 19 to Backend (data queries)
GraphQL
React 19 to Backend (AI streaming)
SSE — LLM token streaming
Internal interservice
REST with Virtual Threads
MCP Tool Communication
MCP over SSE (Spring AI)


4. Irish Environmental Data Sources
Data Source
What It Provides
Met Eireann API
Live weather forecasts by geolocation, 1hr/3hr/6hr intervals out to 240 hours
AirQuality.ie (EPA)
Hourly AQIH from 115 stations nationwide incl. Dublin
data.gov.ie
River, lake, groundwater quality risk datasets (WFD)
SEAI BER Tool
Building energy ratings by Dublin postcode
EPA GeoPortal
Geospatial environmental datasets
EPA PDF Reports
Annual air quality, state of environment reports — ingested as RAG docs
Copernicus / Sentinel-2
Satellite land cover and environmental data


5. Proposed Repository Structure
enviroi/
├── enviroi-backend/          # Spring Boot 4 Modulith (ACA)
│   ├── weather/             # Met Eireann module
│   ├── airquality/          # EPA / AirQuality.ie module
│   ├── water/               # data.gov.ie water module
│   ├── energy/              # SEAI BER module
│   └── ragsai/              # Spring AI RAG + MCP module
├── enviroi-frontend/         # React 19 PWA (Azure Static Web Apps)
│   ├── src/components/      # shadcn/ui + Tailwind 4
│   ├── src/app/             # React 19 Server Components
│   └── src/hooks/           # SSE consumer hooks
├── enviroi-infra/            # Azure Bicep IaC
├── docker-compose.yml       # Local dev (Ollama + PostgreSQL + Redis)
└── README.md

6. Immediate Next Steps
This Week (Phone / GitHub Mobile)
Create the EnviroIE repository on GitHub
Add README.md with project description and architecture diagram
Star and follow: spring-projects/spring-ai, langchain4j/langchain4j, ollama/ollama, mlco2/codecarbon
Browse spring-ai-community/awesome-spring-ai for patterns
Open Issues on EnviroIE as a TODO backlog

When Laptop Replaced
Scaffold Spring Boot 4 Modulith with Spring Initializr
Set up local dev: Docker Compose with Ollama + PostgreSQL/pgvector + Redis
Implement Met Eireann connector first (simplest API, JSON endpoints)
Wire up first Spring AI RAG query against weather data
Scaffold React 19 PWA with Tailwind 4 + shadcn/ui
Deploy skeleton to Azure (ACA + Static Web Apps)

GitHub Community
Submit to spring-ai-community organisation once MVP is working
Write a dev.to / medium post announcing the project
LinkedIn post positioning EnviroIE as evidence of sabbatical work

7. Key Links & Resources
Resource
URL
Spring AI
github.com/spring-projects/spring-ai
Spring AI Community
github.com/spring-ai-community
Awesome Spring AI
github.com/spring-ai-community/awesome-spring-ai
Met Eireann Open Data
data.gov.ie (search: Met Eireann)
AirQuality.ie API
airquality.ie
EPA GeoPortal
epa.ie/our-services/monitoring--assessment
data.gov.ie
data.gov.ie
SEAI BER Tool
seai.ie/tools-resources/ber-research-tool
CodeCarbon
github.com/mlco2/codecarbon
Ollama
github.com/ollama/ollama
shadcn/ui
ui.shadcn.com
Azure Static Web Apps
docs.microsoft.com/azure/static-web-apps
Azure Container Apps
docs.microsoft.com/azure/container-apps


EnviroIE — Environment + Ireland  |  May 2026
