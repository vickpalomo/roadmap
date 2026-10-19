# Ruta Completa: Senior (C#) → Staff/Principal (Go + TS)

Duracion total: ~49 semanas (~12 meses)
Dedicacion: 1.5-2h diarias

---

# Vision General

```
FASE A: Senior en C#/.NET (21 semanas)
  → Dominar tu stack actual, ser promovido, entender sistemas en produccion
  → Proyecto: e-commerce modular monolith en C#

FASE B: Transicion a Go + TypeScript (3 semanas)
  → Aprender la sintaxis y patrones basicos de Go y TS/NestJS
  → No repetir conceptos — solo lenguaje

FASE C: Staff/Principal en Go + TS (26 semanas)
  → Aplicar todo lo de Senior a nivel cross-team con stack moderno
  → Proyecto: e-commerce distribuido con Go + NestJS
```

Total: 42-44 semanas (~10-11 meses)

---

# FASE A — Senior Software Engineer en C#/.NET (20 semanas)

Fuente: `codex_roadmap_sr.md`

Este es tu roadmap activo. No lo duplico aqui — sigue ese archivo tal cual.

Resumen de lo que dominas al terminar:

| Area | Nivel |
|------|-------|
| OOP, SOLID, Clean Code | Solido — aplicas sin pensar |
| Design Patterns | Los utiles, no los teoricos |
| Refactoring | Disciplinado, con tests verdes |
| Hexagonal Architecture | Implementado en tu proyecto |
| DDD Tactico | Aggregates, VOs, invariants, events |
| PostgreSQL profundo | Indexes, EXPLAIN ANALYZE, MVCC, locks, deadlocks, migrations |
| Redis / Caching | Cache-aside, invalidation, rate limiting |
| Testing | Unit + integration, TDD, 70-80% coverage |
| API Design | REST, OpenAPI, versionado, ProblemDetails |
| Docker + CI/CD | Multi-stage, compose, GitHub Actions |
| Resilience | Timeouts, retries, circuit breaker, idempotency |
| Observability | Structured logging, correlation IDs, tracing basico |
| Go basico | gRPC service, goroutines, channels |
| Distributed systems conceptual | Microservices, CQRS, Sagas, async messaging — entender, no disenar |

Criterio de exito: puedes tomar una feature ambigua y entregar codigo listo para produccion con tests, performance medida, logs y tradeoffs documentados.

---

# FASE B — Transicion: Go + TypeScript/NestJS (3 semanas)

Esta fase NO repite conceptos. Ya sabes SOLID, DDD, hexagonal, testing, etc. Solo necesitas trasladar ese conocimiento a los nuevos lenguajes.

## Semana 21 — Go: El Lenguaje

Leer:
- Learning Go (2nd ed) — Jon Bodner — Cap 1-9 (tipos, funciones, punteros, methods, interfaces, generics, errors)
- No leer lo que ya sabes conceptualmente — solo la sintaxis y modismos de Go

Lo que cambia vs C#:
- No hay clases — structs + methods
- No hay herencia — composicion by design (embedding)
- Interfaces implicitas — no necesitas `implements`
- Error handling explicito — no exceptions (if err != nil)
- No hay DI container — DI manual via constructores
- Packages como unidad de modularidad (exported/unexported vs public/private)
- No hay generics pesados — los agregaron en 1.18, usarlos con moderacion

Ejercicio:
- Reimplementar tu Order Aggregate del proyecto C# en Go:
  - Structs para Entity/VO
  - Methods para invariants
  - Constructor NewOrder() que valida
  - Interfaces para Repository port
- No necesitas un proyecto nuevo — solo trasladar el modelo de dominio

Entregable:
- Order domain en Go con tests (table-driven)
- Reflexion: que es mas natural en Go y que extranas de C#

---

## Semana 22 — Go: Concurrencia + HTTP

Leer:
- Learning Go — Cap 12 (Concurrency: goroutines, channels, select, mutexes)
- Learning Go — Cap 13 (Standard library: net/http, encoding/json, io)
- Learning Go — Cap 15 (Testing)

Lo que cambia vs C#:
- async/await → goroutines + channels (mas ligero, diferente modelo mental)
- Task → goroutine (no necesitas pool, son baratas)
- CancellationToken → context.Context (lo pasas por todos lados)
- HttpClient → net/http (standard library, no framework)

Ejercicio:
- Crear un HTTP server en Go (chi o gin) con:
  - POST /orders, GET /orders, GET /orders/:id
  - Middleware de logging
  - Error handling consistente
- Worker pool: procesar N orders en paralelo con goroutines + channels
- Provocar race condition → detectar con `go run -race` → corregir

Entregable:
- API REST basica en Go con tests
- Worker pool con race condition corregida

---

## Semana 23 — TypeScript + NestJS

Leer:
- TypeScript docs: tipos basicos, interfaces, generics, utility types (30 min)
- NestJS docs: overview, controllers, providers, modules (docs.nestjs.com)
- NestJS docs: testing, guards, interceptors, pipes

Lo que cambia vs C#:
- C# → TypeScript es muy natural — ambos tienen tipos, clases, interfaces, decorators/attributes
- ASP.NET Core DI → NestJS DI (casi identico: @Injectable = [Service], Module = Program.cs/Startup)
- Controllers → Controllers (mismo concepto)
- Middleware/Filters → Guards/Interceptors/Pipes (mismo concepto, diferentes nombres)
- EF Core → TypeORM o Prisma
- xUnit → Jest
- El tipado de TS es estructural, no nominal — se parece mas a Go en ese sentido

Ejercicio:
- Reimplementar Orders API en NestJS:
  - Module, Controller, Service, Repository
  - Misma estructura hexagonal que ya conoces
  - Jest tests
- Comparar: cuantas lineas te tomo lo mismo en C# vs NestJS vs Go

Entregable:
- Orders API en NestJS con tests
- Tabla comparativa: C# vs Go vs NestJS para la misma feature

---

# FASE C — Staff/Principal Engineer en Go + TS (26 semanas)

Fuente: `software-architect-roadmap-v2.md`

Este es tu segundo roadmap activo. No lo duplico aqui — sigue ese archivo.

Pero hay un cambio importante: **ya no necesitas las fases 1-4 completas**. Ya las dominaste en C#. Lo que necesitas es aplicarlas en el nuevo stack y avanzar a lo que no cubriste.

## Que puedes acelerar (ya lo sabes, solo aplica en Go/TS):

| Semana Staff | Tema | Tu situacion |
|---|---|---|
| 1-4 | OOP, SOLID, Testing, Concurrencia | Ya dominas — solo aplica al proyecto e-commerce en Go+NestJS |
| 5-8 | Patterns, Refactoring | Ya dominas — aplica rapido al proyecto |
| 9-12 | Hexagonal, C4, ADRs | Ya lo hiciste en C# — reestructura en Go+NestJS |
| 13-16 | DDD | Ya lo implementaste — aplica al e-commerce nuevo |

Estimacion realista: semanas 1-16 del Staff las puedes hacer en 8-10 semanas si no repites lectura.

## Que es nuevo y necesita tiempo completo:

| Semana Staff | Tema | Por que es nuevo |
|---|---|---|
| 17-18 | Databases + DevOps (escala) | Ya sabes DBs — pero ahora es database-per-service, no monolito |
| 19-22 | Microservices, CQRS, Sagas, Async | Ya tienes la intro conceptual — ahora implementas en Go+NestJS |
| 23-24 | Resilience + Observability (escala) | Ya sabes lo basico — ahora es multi-servicio con OpenTelemetry |
| 25-26 | Staff Mindset, Team Topologies | Completamente nuevo — liderazgo tecnico sin autoridad |

## Plan ajustado para FASE C:

| Periodo | Que haces | Semanas |
|---------|-----------|---------|
| Bloque 1 | Semanas 1-16 aceleradas: proyecto e-commerce en Go+NestJS aplicando lo que ya sabes | 8-10 semanas |
| Bloque 2 | Semanas 17-22: Distributed systems, microservices, CQRS, sagas (nuevo) | 6 semanas |
| Bloque 3 | Semanas 23-26: Resilience, observability, Staff mindset (nuevo) | 4 semanas |

Total FASE C ajustada: ~18-20 semanas en vez de 26.

---

# Timeline Realista

| Fase | Duracion | Stack | Resultado |
|------|----------|-------|-----------|
| A: Senior | 21 semanas | C#/.NET | Senior solido, promovible |
| B: Transicion | 3 semanas | Go + TS | Lenguajes listos |
| C: Staff (acelerado) | 18-20 semanas | Go + NestJS | Staff/Principal ready |
| **Total** | **42-44 semanas** | | **~10-11 meses** |

Si mantienes el ritmo de 1.5-2h diarias, en 10 meses pasas de donde estas hoy a Staff/Principal con stack moderno.

---

# Reglas de la Ruta

1. **No saltes la Fase A.** La tentacion es ir directo a Go+TS. Resiste. La profundidad de Senior (especialmente DBs, concurrencia, produccion) es lo que separa a un Staff real de alguien que solo leyo libros de arquitectura.

2. **No repitas conceptos en Fase C.** Si ya implementaste hexagonal en C#, no leas de nuevo que es hexagonal — solo implementalo en el nuevo stack. La lectura es para conceptos nuevos.

3. **El proyecto Senior en C# es tan importante como el Staff en Go+TS.** Ambos van a tu portfolio. El primero demuestra profundidad, el segundo demuestra amplitud.

4. **Go se aprende rapido si ya eres Senior.** La sintaxis es simple — lo dificil (diseño de sistemas, testing, concurrencia) ya lo dominas de C#. Solo cambia la herramienta.

5. **NestJS es casi identico a ASP.NET Core.** Si dominas DI, controllers, middleware y modules en .NET, NestJS es cuestion de dias.

6. **Mide tu progreso con los entregables, no con las horas.** Si una semana la terminas en 3 dias porque ya sabias el tema, avanza.

---

# Libros: Orden de Lectura Total

## Fase A (Senior C#):
1. A Philosophy of Software Design — Ousterhout (completo)
2. Clean Code Fundamentals (2025) — Martin (Part I: Code, los caps relevantes)
3. Head First Design Patterns — Freeman & Robson (caps 1-8)
4. Refactoring — Fowler (caps 1-6 + catalogo como referencia)
5. Clean Code Fundamentals (2025) — Part II-III (SOLID, Components, Architecture)
6. Fundamentals of Software Architecture — Richards & Ford (caps 1-3, 9-12, 19-21)
7. Learning Domain-Driven Design — Khononov (caps 1-11)
8. DDIA 2nd ed — Kleppmann (caps 3-4, 8)
9. The C4 Model — Simon Brown (caps 1-6)
10. Test Driven Development: By Example — Kent Beck (Part I-II)
11. Release It! — Nygard (caps 4-5)
12. Observability Engineering — Majors et al. (caps 1-2, 5-7)
13. System Design Interview Vol. 1 — Alex Xu (caps 1, 3, 8)

## Fase B (Transicion):
14. Learning Go (2nd ed) — Jon Bodner (caps 1-15)

## Fase C (Staff):
15. Building Microservices (2nd ed) — Sam Newman (caps 1-8, 11-12)
16. Microservices Patterns — Chris Richardson (caps 1-4, 6-8)
17. DDIA 2nd ed — Kleppmann (caps 1-2, 6-7, 9-10) — lo que no leiste en Fase A
18. System Design Interview Vol. 1 + Vol. 2 — Alex Xu (resto de capitulos)
19. Software Architecture: The Hard Parts — Richards et al. (caps 1-6)
20. gRPC: Up and Running — Kasun Indrasiri (caps 1-4)
21. Team Topologies — Skelton & Pais (caps 1-5)
22. The Staff Engineer's Path — Tanya Reilly (caps 1-5)
23. Staff Engineer — Will Larson (caps 1-3)
24. Think Distributed Systems — Tornow (complemento)

---

# Que Archivo Seguir en Cada Fase

| Fase | Archivo | Notas |
|------|---------|-------|
| A | `codex_roadmap_sr.md` | Seguir tal cual, semana por semana |
| B | Este archivo (semanas 21-23) | La transicion esta aqui |
| C | `software-architect-roadmap-v2.md` | Acelerar semanas 1-16, tiempo completo 17-26 |

---

# FAQ

**¿Y si me promueven a Senior antes de terminar la Fase A?**
Perfecto. Termina la Fase A de todas formas — la profundidad en DBs y produccion es lo que te sostiene en el rol. No es solo el titulo.

**¿Puedo empezar Go antes de terminar la Fase A?**
Si. La semana 19 del codex roadmap ya incluye Go basico. Esa es tu introduccion. No hagas mas hasta terminar Fase A.

**¿Que pasa si quiero quedarme en C# y no ir a Go+TS?**
Entonces haz el codex roadmap de Senior y despues arma un Staff roadmap en C#. Es valido. Pero dijiste que quieres Go+TS como stack moderno — esta ruta respeta esa decision.

**¿Puedo saltar la Fase B si ya se algo de Go/TS?**
Si ya escribiste Go o TS en produccion, si. Si solo hiciste tutorials, no — dedica las 3 semanas.

---

END.
