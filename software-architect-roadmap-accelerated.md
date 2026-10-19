# software-architect-roadmap-accelerated.md

Duración: 16 semanas
Meta: Architectural Thinking + System Design Real

---

# 🧠 PRINCIPIO CLAVE

Un architect NO sabe más tecnologías.
Un architect:
- reduce complejidad
- toma tradeoffs
- diseña límites correctos
- piensa en evolución del sistema

---

# 📅 FASE 1 — ARCHITECTURE MINDSET (Semanas 1–4)

## Semana 1 — Qué es Arquitectura REALMENTE
Leer:
- Fundamentals of Software Architecture
  - Cap 1: What is Architecture
  - Cap 2: Architectural Thinking
  - Cap 3: Modularity

Ejercicio:
- Analizar tu proyecto actual:
  - coupling
  - cohesion
  - dependencies

Output:
Documento de problemas arquitectónicos.

---

## Semana 2 — Tradeoffs (Skill #1 del Architect)
Leer:
- Fundamentals of Software Architecture
  - Cap 4–6

Aprender:
- Architecture characteristics
- Tradeoff analysis

Ejercicio:
Diseñar:
Monolith vs Microservices (pros/cons).

---

## Semana 3 — Clean Architecture aplicado
Leer:
- Clean Architecture
  - Cap 15–22

Practicar:
- Dependency rule
- Ports & Adapters

Ejercicio:
Redibujar arquitectura hexagonal.

---

## Semana 4 — Design Patterns (solo los que importan)
Estudiar:
- Strategy
- Adapter
- Factory
- Observer
- Dependency Injection

Fuente:
Refactoring.Guru

Objetivo:
Reconocer patrones en código real.

---

# 📅 FASE 2 — DOMAIN DRIVEN DESIGN (Semanas 5–8)

## Semana 5 — DDD Foundations
Leer:
- Learning Domain-Driven Design
  - Cap 1–3

Conceptos:
- Domain model
- Ubiquitous language

Ejercicio:
Modelar dominio de:
Sistema de órdenes.

---

## Semana 6 — Tactical DDD
Leer:
- Learning DDD
  - Cap 4–7

Aprender:
- Entities
- Value Objects
- Aggregates
- Repositories

Ejercicio:
Refactor modelo anémico → rico.

---

## Semana 7 — Strategic DDD
Leer:
- Learning DDD
  - Cap 8–10

Conceptos:
- Bounded Context
- Context Mapping

Ejercicio:
Separar dominios:
Payments / Users / Orders.

---

## Semana 8 — Domain Events
Leer:
- Learning DDD
  - Cap 11

Construir:
Event publishing interno.

---

# 📅 FASE 3 — CQRS + DISTRIBUTED THINKING (Semanas 9–12)

## Semana 9 — CQRS
Leer:
- Martin Fowler CQRS article

Aprender:
- Commands vs Queries
- Read models

Ejercicio:
Separar endpoints read/write.

---

## Semana 10 — Event Driven Architecture
Leer:
- Building Microservices
  - Event chapters

Construir:
Event bus simple.

---

## Semana 11 — Consistency & Reality
Estudiar:
- Eventual consistency
- Idempotency
- Retries
- DLQ

Ejercicio:
Diseñar flujo resiliente.

---

## Semana 12 — Saga Pattern
Aprender:
- Distributed transactions
- Compensation logic

Ejercicio:
Order → Payment → Notification saga.

---

# 📅 FASE 4 — SYSTEM DESIGN MASTER (Semanas 13–16)

## Semana 13 — Data Systems
Leer:
Designing Data-Intensive Applications
  - Cap 1–3

Conceptos:
- Storage engines
- Indexes
- Logs

---

## Semana 14 — Scaling
Leer:
DDIA
  - Cap 5–6

Aprender:
- Replication
- Partitioning

Ejercicio:
Escalar URL shortener.

---

## Semana 15 — Reliability
Leer:
Release It!
  - Stability patterns

Conceptos:
- Circuit breaker
- Bulkhead
- Backpressure

---

## Semana 16 — Architect Simulation
Diseñar desde cero:

1. Ride sharing system
2. Chat system
3. Payment platform

Debe incluir:
- bounded contexts
- events
- CQRS
- scaling strategy
- observability

Output:
Architecture Decision Records (ADRs)

---

# 🧠 Rutina diaria

90 min → lectura + notas  
45 min → diagramas  
45 min → implementación pequeña

---

# ✅ Resultado esperado

Después de 16 semanas:

✔ Pensás en sistemas, no endpoints  
✔ Explicás tradeoffs claramente  
✔ Diseñás bounded contexts naturales  
✔ Entendés sistemas distribuidos  
✔ Nivel Staff/Senior+ mindset

---

🧠 Algo importante (esto acelera x3)

El error común:

leer arquitectura → entender → aplicar
___

El orden correcto:

diseñar algo

↓

fallar

↓

leer capítulo

↓

rediseñar

END