# 🧠 Software Architect — Mapa Mental Completo

Este documento describe el modelo mental necesario para evolucionar desde Backend Developer hasta Software Architect / Staff Engineer.

---

# 🧭 Visión General

Un arquitecto no domina tecnologías.

Domina **capas de pensamiento**.

┌────────────────────────────────┐
│ 6. Organizational Architecture │
├────────────────────────────────┤
│ 5. Evolution & Trade-offs      │
├────────────────────────────────┤
│ 4. Distributed Systems         │
├────────────────────────────────┤
│ 3. System Architecture         │
├────────────────────────────────┤
│ 2. Domain Modeling (DDD)       │
├────────────────────────────────┤
│ 1. Engineering Fundamentals    │
└────────────────────────────────┘

Cada nivel cambia las preguntas que haces.

---

# 🧱 1. Engineering Fundamentals (Junior → Mid)

## Objetivo
Controlar el código y producir software mantenible.

## Dominar

- Clean code
- Testing (unit, integration)
- API design
- Debugging
- Error handling
- Logging
- Refactoring
- Performance básico

## Pregunta mental dominante

> ¿Cómo implemento esto correctamente?

## Habilidades clave

- modularidad
- legibilidad
- bajo acoplamiento
- tests confiables

## Libros recomendados

- Clean Architecture — Robert C. Martin
- A Philosophy of Software Design — John Ousterhout ⭐⭐⭐

## Resultado esperado

Código mantenible y entendible por otros.

---

# 🧩 2. Domain Modeling (DDD) (Mid → Senior)

## Objetivo
Modelar software según el negocio, no según la base de datos.

## Conceptos clave

- Ubiquitous Language
- Entities
- Value Objects
- Aggregates
- Invariants
- Domain Events
- Repositories (DDD)
- Application Services
- Bounded Contexts (introducción)

## Cambio mental

Antes:


tabla orders


Después:


Order Aggregate protege reglas del negocio


## Pregunta mental dominante

> ¿Qué modelo representa correctamente la realidad del negocio?

## Libros recomendados

- Learning Domain-Driven Design — Vlad Khononov ⭐⭐⭐
- Domain-Driven Design Distilled — Vaughn Vernon

## Resultado esperado

Software alineado con reglas reales del negocio.

---

# 🏗️ 3. System Architecture (Senior)

## Objetivo
Diseñar sistemas completos, no solo features.

## Conceptos clave

- Clean Architecture
- Hexagonal Architecture
- Dependency inversion
- CQRS
- Event-driven architecture
- API boundaries
- Separation of concerns
- Cohesion vs Coupling

## Pregunta mental dominante

> ¿Dónde debe vivir cada responsabilidad?

## Decisiones comunes

- Sync vs Async
- Monolith vs Modular Monolith
- Service boundaries

## Libros recomendados

- Architecture Patterns with Python ⭐⭐⭐
- Building Microservices — Sam Newman

## Resultado esperado

Sistemas extensibles y modificables sin caos.

---

# 🌐 4. Distributed Systems Thinking (Senior++ → Architect)

## Objetivo
Diseñar sistemas que sobrevivan fallas reales.

## Conceptos clave

- Replication
- Partitioning
- Consistency models
- CAP theorem trade-offs
- Idempotency
- Retries
- Timeouts
- Backpressure
- Observability
- Failure modes

## Pregunta mental dominante

> ¿Qué pasa cuando esto falla a las 3 AM?

## Mentalidad nueva

Aceptar:


Las redes fallan.
Los mensajes se duplican.
Los servicios caen.
El tiempo no es confiable.


## Libros recomendados

- Designing Data-Intensive Applications — Martin Kleppmann ⭐⭐⭐⭐
- Release It! — Michael Nygard ⭐⭐⭐

## Resultado esperado

Sistemas resilientes.

---

# ⚖️ 5. Evolution & Trade-Off Thinking (Architect)

## Objetivo
Tomar decisiones que envejezcan bien.

## Conceptos clave

- Trade-off analysis
- Evolutionary architecture
- Fitness functions
- Technical debt strategy
- Incremental design
- Cost vs complexity
- YAGNI aplicado correctamente

## Pregunta mental dominante

> ¿Qué decisión seguirá siendo buena dentro de 2 años?

## Libros recomendados

- Software Architecture: The Hard Parts ⭐⭐⭐
- Building Evolutionary Architectures ⭐⭐⭐
- Fundamentals of Software Architecture ⭐⭐⭐

## Resultado esperado

Arquitectura sostenible.

---

# 👥 6. Organizational Architecture (Staff / Principal)

## Objetivo
Diseñar arquitectura alineada con equipos humanos.

## Conceptos clave

- Conway’s Law
- Team Topologies
- Cognitive Load
- Service ownership
- Communication paths
- Socio-technical systems

## Insight clave

La arquitectura sigue la estructura del equipo.

## Pregunta mental dominante

> ¿Puede este equipo operar y evolucionar este sistema?

## Libro esencial

- Team Topologies — Matthew Skelton & Manuel Pais ⭐⭐⭐⭐

## Resultado esperado

Arquitecturas mantenibles por organizaciones reales.

---

# 🔥 Evolución de Preguntas Mentales

| Nivel | Pregunta |
|------|---------|
| Junior | ¿Cómo funciona? |
| Mid | ¿Cómo lo implemento bien? |
| Senior | ¿Cómo escala? |
| Senior+ | ¿Cómo falla? |
| Architect | ¿Qué trade-off acepto? |
| Principal | ¿Cómo afecta al equipo? |

---

# 🧠 Habilidades Invisibles del Software Architect

## 1. Architectural Decision Records (ADR)

Formato estándar:


Contexto
Opciones consideradas
Decisión tomada
Consecuencias positivas
Consecuencias negativas


Un arquitecto escribe decisiones, no solo código.

---

## 2. Constraint Thinking

Arquitectura = optimizar bajo restricciones:

- tiempo
- personas
- presupuesto
- conocimiento del equipo

---

## 3. Abstraction Control

Saber cuándo:

- abstraer
- NO abstraer

Evitar sobreingeniería.

---

## 4. Failure Imagination

Ejercicio diario:


¿Cómo podría romperse esto?


---

# 📊 Autoevaluación Mensual

Puntúa del 1 al 5:

| Área | Score |
|------|------|
| Engineering fundamentals | |
| Domain modeling | |
| System architecture | |
| Distributed systems | |
| Trade-offs thinking | |
| Organizational thinking | |

Revisar progreso cada mes.

---

# 🚀 Evolución Completa del Arquitecto


Code
↓
Domain Model
↓
System Architecture
↓
Distributed Thinking
↓
Trade-offs
↓
Organization Design


Cuando llegas arriba:

No diseñas solo software.

Diseñas **sistemas socio-técnicos**.

---

# ✅ Cómo usar este documento

Leer:

- semanalmente
- antes de diseñar sistemas
- al escribir ADRs
- cuando te sientas bloqueado técnicamente

Este documento funciona como brújula profesional hacia Software Architect.