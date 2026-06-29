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
