# Projeto-Java

# 🏦 Financial Ledger Engine (High-Performance)

> Um motor de ledger financeiro de alta confiabilidade, construído para consistência forte, auditabilidade e escala.

## 🚀 O Problema
Sistemas bancários exigem mais que apenas um CRUD. Eles exigem:
- **Zero Double-Spending:** Consistência absoluta.
- **Auditabilidade Imutável:** Capacidade de reconstruir o estado histórico.
- **Alta Performance:** Escala sem gargalos de travamento (deadlocks).

## 🏗️ Arquitetura (High-Level)
Este sistema utiliza *Event Sourcing* para auditoria e *Optimistic Concurrency Control (OCC)* para performance.

```mermaid
graph TD
    Client[Client/API] -->|Auth JWT| Controller[API Layer]
    Controller -->|Service| Engine[Ledger Engine]
    Engine -->|Optimistic Lock| DB[(PostgreSQL)]
    Engine -->|Audit| EventStore[(Event Table)]
    Engine -.->|Anchor| Notary[External Notary]
---

### 2. Docker Compose (Infraestrutura)
Crie um arquivo chamado `docker-compose.yml` na raiz. Isso permite que qualquer pessoa (ou você na banca) rode o sistema com um comando.

```yaml
version: '3.8'
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: ledger
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    ports:
      - "5432:5432"

  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      DB_HOST: db
      DB_USER: user
      DB_PASSWORD: password
      JWT_SECRET: super-secret-key-that-should-be-in-env-vars
    depends_on:
      - db
