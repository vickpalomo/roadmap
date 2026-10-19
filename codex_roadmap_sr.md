# Codex Roadmap Senior Engineer

Duracion: 22 semanas (~5.5 meses)
Dedicacion: 1.5-2h diarias
Metodo: Codear -> Romper -> Medir -> Leer -> Refactorizar

---

# Objetivo

Este roadmap busca llevarte a un nivel de **Senior Software Engineer fuerte**:

- Tomas features ambiguas y las conviertes en diseno, codigo, tests y entrega.
- Escribes codigo mantenible que otros pueden extender sin preguntarte todo.
- Entiendes el sistema completo, no solo tu ticket.
- Disenas APIs, modelos de datos y boundaries con criterio.
- Sabes diagnosticar problemas de performance, queries lentas, locks, errores y fallas en produccion.
- Haces code reviews utiles y elevas el estandar del equipo.
- Operas con fluidez en dos lenguajes con filosofias distintas (C# y Go) y sabes cuando usar cada uno.

El objetivo no es "saber muchas tecnologias". El objetivo es ser confiable entregando software listo para produccion.

---

# Stack

| Stack | Uso | Proyecto |
|-------|-----|----------|
| C# + ASP.NET Core | Domain-rich APIs, DDD, CQRS, modular monolith | Orders, Products, Users, Promotions |
| .NET tooling | xUnit, FluentAssertions, Moq/NSubstitute, WebApplicationFactory, EF Core | Testing e integracion del monolito |
| Go | High-performance services, concurrencia, workers, gRPC | Payment Service, Inventory Worker |
| Go tooling | testing nativo, table-driven tests, benchmarks, `go test -race` | Testing del servicio Go |
| PostgreSQL | Base de datos compartida (schemas separados por servicio) | Ambos servicios |
| Redis | Cache, rate limiting, pub/sub entre servicios | Ambos servicios |
| gRPC + Protocol Buffers | Comunicacion entre el monolito C# y el servicio Go | Contrato compartido |
| Docker + GitHub Actions | Entorno reproducible y pipeline | Ambos servicios |

Reglas:
- C# lleva el dominio rico (DDD, hexagonal, CQRS) — donde las clases y el type system brillan.
- Go lleva lo que haria en produccion: alto rendimiento, concurrencia pesada, workers, gRPC server.
- Los servicios se comunican via gRPC (sync) y message queue (async).
- No duplicar: cada concepto se implementa en el lenguaje donde tiene mas sentido. Se comparan cuando vale la pena contrastar.

---

# Proyecto Integrador

Un e-commerce con dos piezas que se comunican:

```text
┌─────────────────────────────────────┐     gRPC      ┌──────────────────────────┐
│  C# Modular Monolith (ASP.NET Core) │ ◄───────────► │  Go Payment Service      │
│                                     │               │                          │
│  orders/                            │               │  cmd/server/             │
│  products/                          │     async     │  internal/payment/       │
│  users/                             │ ◄──── queue ──│  internal/inventory/     │
│  promotions/                        │               │  internal/fraud/         │
└─────────────────────────────────────┘               └──────────────────────────┘
```

**C# (monolito modular)**:
- Orders: aggregate root, DDD tactico, CQRS.
- Products: CRUD + cache + search.
- Users: auth basica, JWT.
- Promotions/Reviews: modulo final end-to-end.

**Go (payment + inventory service)**:
- Payment: gRPC server, worker pool para procesamiento, idempotency.
- Inventory: reservas de stock con concurrencia, race condition handling.
- Fraud check: fan-out a N providers en paralelo.

Estructura C# por modulo:
```text
domain/
application/
infrastructure/
api/
```

Estructura Go:
```text
cmd/server/          (entry point)
internal/payment/    (domain + handlers)
internal/inventory/  (domain + workers)
internal/fraud/      (fan-out checker)
pkg/grpc/            (proto-generated + server)
```

Meta final:
- Dos servicios comunicandose via gRPC.
- Domain model rico en C# con invariants.
- Concurrencia real en Go con workers, channels, race detection.
- PostgreSQL con migrations, indexes y query analysis en ambos.
- Tests unitarios e integracion en ambos lenguajes.
- Docker Compose levantando todo.
- CI para ambos.
- Logs estructurados y correlation IDs cross-service.

---

# Biblioteca Base

Lectura principal:

| Tema | Recurso |
|------|---------|
| Diseno de codigo | A Philosophy of Software Design - John Ousterhout |
| Clean code / SOLID / Architecture | Clean Code Fundamentals (2025) - Robert C. Martin |
| Refactoring | Refactoring - Martin Fowler |
| Patterns | Head First Design Patterns + Refactoring.Guru |
| Testing | Test Driven Development: By Example - Kent Beck |
| Arquitectura | Fundamentals of Software Architecture - Richards & Ford |
| DDD | Learning Domain-Driven Design - Vlad Khononov |
| Bases de datos | DDIA + PostgreSQL docs + Use The Index, Luke |
| Produccion | Release It! - Michael Nygard |
| Observabilidad | Observability Engineering - Majors et al. |
| System design | System Design Interview Vol. 1 - Alex Xu |
| Go | Learning Go (2nd ed) - Jon Bodner |
| Go concurrencia | Concurrency in Go - Katherine Cox-Buday |

Lecturas de referencia, no lineales:
- Microsoft Learn: ASP.NET Core Web API, Dependency Injection, EF Core
- Microsoft Learn: Minimal APIs, middleware, filters, health checks, logging
- .NET Microservices Architecture for Containerized .NET Applications
- PostgreSQL: Up and Running
- Database Internals
- API Design Patterns
- gRPC: Up and Running

---

# FASE 1 - Foundations: Codigo, APIs y Testing (Semanas 1-4)

Go ramp-up: leer Learning Go caps 1-9 en paralelo durante estas 4 semanas (1 cap cada 2-3 dias). Al final de la fase debes poder escribir funciones, structs, interfaces, manejar errores y crear un HTTP server basico.

## Semana 0 - Fundamentos de C# (prerequisito)

Este roadmap asume que ya escribes C# sin ayuda de IA. Si no es asi, empieza aqui. Mientras no puedas escribir una clase `Order` con una lista de items sin asistencia, la Semana 1 no se puede aplicar.

Go queda en pausa hasta terminar esta semana: no leas Learning Go caps 1-3 todavia. Se retoma en la Semana 1.

Practica (es lo principal):
- Exercism, track de C# (https://exercism.org/tracks/csharp): ejercicios cortos con tests automaticos. Sin IA ni Copilot.

Leer (solo como apoyo cuando un ejercicio te atore):
- Mark J. Price, C# 14 and .NET 10 – Modern Cross-Platform Development Fundamentals, 10a ed. (O'Reilly), caps 1-5. Despues: cap 6 (interfaces y herencia), cap 8 (tipos comunes de .NET: colecciones, `List`/`Dictionary`) y cap 11 (LINQ) en las semanas siguientes. Cap 15 (web services) cuando llegues al proyecto Orders de la Semana 1. Usar SDK .NET 10 (LTS).

| Dia | Tema | Price | Exercism (conceptos) |
|-----|------|-------|----------------------|
| 1 | `dotnet new console`, variables, tipos, strings | caps 1-2 | Basics, Strings, Numbers |
| 2 | `if`, `switch`, loops, conversion de tipos, excepciones | cap 3 | Booleans, Conditionals, For loops |
| 3 | Metodos, parametros, `null` | cap 4 | Methods, Nullability |
| 4 | Clases, constructores, properties, `private`/`public` | cap 5 | Classes, Properties |

Dedicacion: 30-45 min, 4 dias. Mas chico que el resto del roadmap a proposito.

Reglas:
- Practicando, nada de IA. Si te atoras: 20 min intentando, luego Price o docs.microsoft.com, y solo al final pedirle a Claude que *explique* (no que escriba).
- En el trabajo, no aceptar codigo generado sin poder explicar linea por linea por que esta asi.

Proyecto:
- `dotnet new console -n Practica` y el primer ejercicio de Exercism ("Lucian's Luscious Lasagna").

Criterio de salida (para pasar a la Semana 1):
- Escribir sin ayuda una clase `Order` con `List<OrderItem>`, un metodo `AddItem` y una property `Total`.
- Si hace falta extender la Semana 0 con `List`/`Dictionary` (Price cap 8), LINQ basico (cap 11), interfaces y herencia (cap 6), hacerlo antes de avanzar.

Entregable:
- Ejercicios de Exercism completados (commits en un repo propio) y la clase `Order` del criterio de salida.

---

## Semana 1 - OOP, Encapsulacion y API Basica

Leer:
- A Philosophy of Software Design, caps 1-4
- Clean Code Fundamentals (2025), cap 3: First Principles
- Clean Code Fundamentals (2025), cap 4: Meaningful Names
- Clean Code Fundamentals (2025), cap 12: Objects and Data Structures
- Clean Code Fundamentals (2025), cap 13: Clean Classes (adelantado de la semana 2 — es donde se nombra cohesion)
- Google API Design Guide, secciones de recursos, metodos y errores
- Learning Go, caps 1-3 (Setup, tipos primitivos, composite types)

Aprender esta semana — cada item esta en la lectura de arriba:
- Encapsulation — Clean Code cap 12: data/object anti-symmetry, Tell-Don't-Ask, Law of Demeter.
- Abstraction — APoSD cap 4: interface vs implementation, modulos profundos vs superficiales.
- Cohesion — Clean Code cap 13.
- Complejidad y dependencias — APoSD cap 2.
- [C#] Records, classes, interfaces, access modifiers e immutability.
- [Go] Structs, exported/unexported.
- REST naming: `/orders`, `/products`, subresources.
- Status codes, error format, validation y pagination.

Aviso de vocabulario: Ousterhout **no** usa las palabras "cohesion" ni "coupling" en APoSD. Llama al mismo tema complexity, dependencies y obscurity. Sus tres sintomas — change amplification, cognitive load, unknown unknowns — son consecuencias de acoplamiento alto. Si buscas esos dos terminos en APoSD no los vas a encontrar: no falta el tema, falta el diccionario.

Llega despues — no lo busques ahora:
- Composition over inheritance — Head First Design Patterns cap 1 (semana 5). En Go, embedding: Learning Go cap 7 (semana 3).
- Coupling por nombre + principios de componentes — Clean Code cap 20 (sin semana asignada; consultarlo en semana 8, con modular monolith).
- Information hiding a fondo — APoSD cap 5 (semana 2).

Regla para el resto del roadmap: si un concepto de la lista "Aprender" no aparece en la lectura de esa semana, es (a) que se nombra en una semana posterior, o (b) que ese autor lo llama distinto. En los dos casos: anotalo y sigue con el proyecto. Releer capitulos buscando un termino que no esta es la forma mas comun de perder una semana. La lista "Aprender" es el resultado esperado al final de la fase, no un indice de la lectura semanal.

Proyecto:
- [C#] Crear `Orders` en ASP.NET Core Web API.
  - Endpoints: `POST /orders`, `GET /orders`, `GET /orders/:id`
  - Persistencia in-memory.
  - Error format consistente, pagination.
- [Go] Crear un HTTP server minimo con `net/http` o chi:
  - `GET /health` que retorne status.
  - Familiarizarse con el tooling: `go run`, `go build`, `go fmt`.

Entregable:
- Codigo C# de Orders funcionando.
- HTTP server Go minimo corriendo.
- Documento: "3 decisiones de diseno en C# y como Go me forzaria a pensar distinto".

---

## Semana 2 - Funciones, Responsabilidad y Modulos Profundos

Leer:
- A Philosophy of Software Design, caps 5-8
- Clean Code Fundamentals (2025), cap 5: Comments
- Clean Code Fundamentals (2025), cap 7: Clean Functions
- Clean Code Fundamentals (2025), cap 13: Clean Classes
- Learning Go, caps 4-5 (Blocks/shadows, Functions)

Aprender:
- Deep modules vs shallow modules.
- Information hiding.
- [C#] Controller -> application service -> repository.
- [Go] Handler -> service -> repository. Packages como unidad de modularidad.
- DTOs/request models vs domain objects.

Proyecto:
- [C#] Separar Orders en controller, application service y repository.
  - Agregar modulo `Products` con filtering/sorting.
- [Go] Crear la estructura basica del Payment Service:
  - `cmd/server/main.go`
  - `internal/payment/service.go` (in-memory, solo firma de funciones)
  - `internal/payment/handler.go` (HTTP handlers)
  - Un endpoint: `POST /payments` (stub que retorna 201).

Entregable:
- PR/diff del refactor C#.
- Estructura de packages Go lista con endpoint stub.

---

## Semana 3 - SOLID Aplicado

Leer:
- Clean Code Fundamentals (2025), cap 19: The SOLID Principles
- A Philosophy of Software Design, caps 9-11
- Learning Go, caps 6-7 (Pointers, Types/Methods/Interfaces)

Aprender:
- SRP, OCP, LSP, ISP, DIP.
- [C#] DI en ASP.NET Core: lifetimes (singleton, scoped, transient).
- [Go] Interfaces implicitas: ISP y DIP salen naturales. DI manual (constructor injection).
- Interfaces utiles vs abstracciones prematuras en ambos lenguajes.

Proyecto:
- [C#] Agregar descuentos (cupon, tipo de cliente, cantidad).
  - `DiscountCalculator` separado del `OrderService`.
  - Interfaces para repositorios.
- [Go] Definir interfaces en el Payment Service:
  - `PaymentRepository` interface (in-memory implementation).
  - `FraudChecker` interface (stub que siempre aprueba).
  - Comparar: como DI en Go es explicitamente manual vs el container de ASP.NET Core.

Entregable:
- Auditoria SOLID del proyecto C#.
- Payment Service Go con interfaces definidas y stubs.
- Nota: "DI en Go vs C# — que gano y que pierdo con cada enfoque".

---

## Semana 4 - Testing como Diseno

Leer:
- Test Driven Development: By Example, Part I, caps 1-17
- Clean Code Fundamentals (2025), cap 14: Testing Disciplines (TDD)
- Clean Code Fundamentals (2025), cap 15: Clean Tests
- Learning Go, caps 8-9 (Generics, Errors)
- Learning Go, cap 15 (Testing en Go)

Aprender:
- Test pyramid: unit -> integration -> e2e.
- Mocks, stubs y fakes.
- Arrange / Act / Assert.
- TDD: Red -> Green -> Refactor.
- [C#] xUnit + FluentAssertions + WebApplicationFactory.
- [Go] Table-driven tests, testing package nativo, testify opcional.

Proyecto:
- [C#] Tests unitarios: OrderService, DiscountCalculator, ProductService.
  - Tests de integracion con WebApplicationFactory.
  - Validacion: orden no puede exceder stock.
- [Go] Table-driven tests para PaymentService:
  - Happy path: crear payment, obtener payment.
  - Edge cases: payment duplicado, monto invalido.
  - Correr con `go test -race` desde el inicio (habito).

Entregable:
- Suite de tests C#: 70-80% coverage en dominio/aplicacion.
- Suite de tests Go: table-driven, con `-race` flag.
- Reflexion: "Que diferencia noto entre testear con DI container (C#) vs DI manual (Go)".

---

# FASE 2 - Refactoring, Patterns y Modularidad (Semanas 5-8)

Go learning: caps 10-12 (Modules/Packages, Standard Library, Concurrency intro). El Payment Service empieza a tomar forma real.

## Semana 5 - Patterns que Si Usarias

Leer:
- Head First Design Patterns, caps 1-4
- Refactoring.Guru como referencia
- Learning Go, cap 10 (Modules, Packages, Imports)

Aprender:
- Strategy, Factory, Adapter, Facade, Decorator.
- [C#] Decorator como middleware/filters, Options pattern.
- [Go] Strategy con interfaces + funciones first-class. Factory como funcion que retorna interface.

Proyecto:
- [C#] Strategy para shipping calculation. Adapter para payment gateway (que llama al servicio Go via HTTP por ahora).
- [Go] Strategy para fraud check: multiple implementaciones de `FraudChecker` interface.
  - `AlwaysApproveFraudChecker` (test/dev)
  - `RuleBasedFraudChecker` (produccion)
  - Factory function: `NewFraudChecker(config) FraudChecker`

Entregable:
- Tests antes/despues en ambos lenguajes.
- Nota: "Strategy en Go con funciones vs Strategy en C# con clases — cuando cada uno".

---

## Semana 6 - Refactoring Disciplinado

Leer:
- Refactoring - Fowler, caps 1-6
- Learning Go, cap 11 (Standard Library: io, net/http, encoding/json, time)

Aprender:
- Extract function/class, Move function, Introduce parameter object.
- Replace conditional with polymorphism.
- Refactor manteniendo tests verdes.

Proyecto:
- [C#] Elegir modulo mas complejo, aplicar 5 refactors en commits separados.
- [Go] Refactorizar Payment Service:
  - Extraer validacion a funciones puras.
  - Introducir `PaymentRequest` como parameter object (en vez de multiples args).
  - Mover logica de HTTP handler a service (handler solo parsea/serializa).

Entregable:
- Serie de commits atomicos en ambos repos.
- Self-review de cada refactor.

---

## Semana 7 - Anti-patterns, Code Review y gRPC Setup

Leer:
- Fowler, code smells
- Articulos de Martin Fowler sobre technical debt
- gRPC: Up and Running, caps 1-2 (conceptos + protobuf)

Aprender:
- Anti-patterns: God service, anemic domain model, circular deps, interface pollution.
- Reviews que ensenan sin bloquear por gusto.
- gRPC basico: definir `.proto`, generar codigo, client/server.

Proyecto:
- [C#] Auditar y corregir 2 anti-patterns. Documentar API con Swagger. ProblemDetails.
- [Go] Convertir Payment Service de HTTP a gRPC:
  - Definir `payment.proto` con `CreatePayment` y `GetPayment` RPCs.
  - Generar codigo Go con `protoc`.
  - Server gRPC basico sirviendo las mismas operaciones.
- [C#] Crear gRPC client en el monolito que llama al Payment Service Go.

Entregable:
- Comunicacion gRPC funcionando: C# client -> Go server.
- Documento: "Anti-patterns encontrados y como los corregi".

---

## Semana 8 - Modular Monolith + Service Boundary

Leer:
- Fundamentals of Software Architecture, caps 1-3
- Learning Go, cap 12 (Concurrency: goroutines, channels, select) — lectura inicial

Aprender:
- Modularity: coupling, cohesion, connascence.
- Boundaries entre modulos (C#) y entre packages (Go).
- Monolito modular + servicio externo: el patron hibrido real.

Proyecto:
- [C#] Reorganizar e-commerce como monolito modular:
  - Cada modulo con boundary claro. No acceso directo a internals de otros modulos.
  - Orders llama a Payments via gRPC client (no directamente al repo de pagos).
- [Go] Reorganizar Payment Service con boundaries internos:
  - `internal/payment/` (core domain)
  - `internal/inventory/` (placeholder para semana 15)
  - `pkg/grpc/` (transport layer)

Entregable:
- Diagrama de dependencias del sistema completo (monolito + servicio Go).
- Regla escrita: "Que puede importar cada modulo/package y que no".
- Milestone: sistema con 2 procesos comunicandose via gRPC.

---

# FASE 3 - Arquitectura Practica y DDD Tactico (Semanas 9-12)

## Semana 9 - Hexagonal Architecture

Leer:
- Clean Code Fundamentals (2025), caps 25-27 (Architectural Boundaries, Clean Boundaries, Clean Architecture)
- Fundamentals of Software Architecture, caps 9-12

Aprender:
- Domain, Application/use cases, Infrastructure/adapters, Ports.
- Controllers/endpoints/gRPC handlers como adapters, no dominio.
- Hexagonal se aplica en ambos lenguajes con diferente mecanismo.

Proyecto:
- [C#] Reestructurar Orders como hexagonal:
  ```
  orders/domain/        (entities, VOs, ports interfaces)
  orders/application/   (use cases, services)
  orders/infrastructure/(EF Core repo, HTTP controllers)
  ```
  - Test: verificar que `domain/` no referencia `infrastructure/`.
- [Go] Reestructurar Payment Service como hexagonal:
  ```
  internal/payment/domain/     (types, interfaces/ports)
  internal/payment/app/        (use cases)
  internal/payment/infra/      (postgres repo, grpc handler)
  ```
  - Test: verificar con `go vet` o import analysis que domain no importa infra.

Entregable:
- Ambos servicios en arquitectura hexagonal.
- Tests de dependency rule en ambos.
- Nota: "Hexagonal en Go vs C# — donde el lenguaje ayuda y donde estorba".

---

## Semana 10 - DDD Tactico

Leer:
- Learning Domain-Driven Design, caps 1-7

Aprender:
- Ubiquitous language, Entities, Value Objects, Aggregates, Invariants.
- Domain services vs application services.
- [C#] Modelo rico con clases, private setters, domain methods.
- [Go] Modelo rico con structs, constructors (`NewOrder()`), unexported fields, methods que validan.

Proyecto:
- [C#] Order Aggregate: Order (root), OrderItem (entity), Money (VO), Address (VO).
  - Invariants: no agregar items a orden cancelada, total no negativo, no confirmar sin items.
- [Go] Payment Aggregate: Payment (root), Amount (VO), PaymentStatus.
  - Invariants: no procesar payment ya completado, monto > 0, no refund mayor al monto original.
  - Constructor `NewPayment()` que garantiza estado valido.

Entregable:
- Modelos de dominio ricos en ambos lenguajes.
- Tests de invariants en ambos.
- Insight: "Private setters (C#) vs unexported fields (Go) — mismo efecto, diferente mecanismo".

---

## Semana 11 - Boundaries, Events y ACL

Leer:
- Learning Domain-Driven Design, caps 8-11

Aprender:
- Bounded contexts, Context map, Domain events, Anti-Corruption Layer.

Proyecto:
- Dibujar context map: Orders (C#), Payments (Go), Inventory (Go), Products (C#).
- [C#] Implementar eventos internos:
  - `OrderCreatedEvent` -> publica hacia cola (para que Go lo consuma).
  - ACL: cuando C# recibe respuesta de Payment (gRPC), traduce al lenguaje del dominio Orders.
- [Go] Consumir evento `OrderCreated` desde una queue (in-memory o NATS/RabbitMQ basico):
  - Payment Service inicia el cobro cuando recibe el evento.
  - Publicar `PaymentCompletedEvent` de vuelta.

Entregable:
- Context map del sistema.
- Flujo async funcionando: Order created (C#) -> Payment processed (Go) -> Order confirmed (C#).
- Tests de integracion del flujo.

---

## Semana 12 - C4, ADRs y Documentacion Tecnica

Leer:
- The C4 Model, niveles Context, Container, Component
- Fundamentals of Software Architecture, caps 19-21

Aprender:
- C4 diagrams, ADRs, Tradeoffs.
- Como explicar decisiones a alguien que no vio el codigo.

Proyecto:
- Diagrama C4:
  - Context: usuario -> sistema e-commerce.
  - Container: monolito C# + Payment Service Go + PostgreSQL + Redis + Queue.
  - Component: Orders module internals.
- ADR: "Por que C# para el monolito y Go para payments".
- ADR: "Por que gRPC entre servicios y no REST".

Entregable:
- C4 (3 niveles) + 2 ADRs.
- Mini system design: URL shortener en 30 minutos y comparacion con Alex Xu.

---

# FASE 4 - Databases, Internals y Performance (Semanas 13-16)

Esta fase es deliberadamente fuerte. Para Senior, bases de datos separan a quien solo implementa de quien entiende produccion.

## Semana 13 - SQL, Modelado e Indexes

Leer:
- DDIA, data models y storage basics
- Use The Index, Luke, secciones de indexes y composite indexes
- PostgreSQL docs: indexes

Aprender:
- Normalizacion vs denormalizacion.
- B-Tree indexes, composite indexes, covering indexes.
- Selectivity y cardinality.
- Indexes aceleran reads pero cuestan writes y espacio.

Proyecto:
- [C#] Migrar Orders y Products a PostgreSQL con EF Core migrations.
  - Disenar 3 queries importantes + indexes justificados.
  - Usar Dapper para una query read-heavy y comparar.
- [Go] Conectar Payment Service a PostgreSQL con pgx:
  - Schema: `payments` table con indexes.
  - Disenar 2 queries importantes + indexes justificados.
  - Repository real reemplaza el in-memory.

Entregable:
- Schemas de ambos servicios.
- Tabla: query -> index -> razon -> tradeoff (para ambos).

---

## Semana 14 - EXPLAIN ANALYZE y Query Performance

Leer:
- PostgreSQL docs: `EXPLAIN`
- PostgreSQL docs: planner statistics

Aprender:
- `EXPLAIN` vs `EXPLAIN ANALYZE`.
- Seq scan, index scan, bitmap index scan.
- Nested loop, hash join, merge join.
- N+1 queries, cursor pagination.

Proyecto:
- [C#] Cargar datos de prueba. Analizar 3 queries con EXPLAIN ANALYZE. Optimizar 2.
  - Cursor pagination en `GET /orders`.
  - Provocar N+1 con EF Core y corregirlo (Include/eager loading).
- [Go] Cargar datos de prueba en payments. Analizar 2 queries.
  - Pagination en `ListPayments` gRPC method.
  - pgx no tiene N+1 por defecto (queries explicitas), pero analizar batch vs individual.

Entregable:
- Reporte: antes/despues de query plans en ambos servicios.
- Explicacion de por que el planner eligio cada plan.

---

## Semana 15 - Transacciones, MVCC, Locks y Concurrencia de Inventario

Leer:
- DDIA, transactions
- PostgreSQL docs: transaction isolation, MVCC, explicit locking

Aprender:
- ACID, MVCC, isolation levels (read committed, repeatable read, serializable).
- Row locks, deadlocks, optimistic vs pessimistic locking.
- Connection pooling, migraciones expand/contract.

Proyecto:
- [C#] Crear order + reservar stock en una transaccion.
  - Simular race condition de inventario y corregirla.
  - EF Core concurrency tokens.
- [Go] Implementar Inventory Worker en `internal/inventory/`:
  - `ReserveStock` con transaction + row lock (`SELECT ... FOR UPDATE`).
  - Simular 100 goroutines intentando reservar el mismo stock.
  - Detectar race con `go test -race`, corregir con locking correcto.
  - Simular deadlock y explicar por que ocurrio.

Entregable:
- Documento: "Concurrencia y consistencia en Inventory" (cubre ambos lenguajes).
- Tests de concurrencia: C# con Parallel + Go con goroutines.

---

## Semana 16 - Redis, Caching y Read Performance

Leer:
- Redis docs: data types, expiration, cache patterns
- DDIA, caching/replication secciones relevantes

Aprender:
- Cache-aside, TTL, cache invalidation, stampede.
- Rate limiting basico.

Proyecto:
- [C#] Cache-aside para Products con `IDistributedCache` o StackExchange.Redis.
  - Invalidacion al actualizar producto.
  - Rate limiting simple en endpoint publico.
- [Go] Redis para idempotency en Payment Service:
  - Guardar idempotency key en Redis con TTL.
  - Si el payment ya existe (key hit), retornar resultado previo sin re-procesar.
  - Rate limiting en gRPC interceptor.
- Medir latencia antes/despues en ambos.

Entregable:
- Cache y rate limiting implementados en ambos servicios.
- Nota: "Que se gana, que riesgo se introduce, como invalido".

---

# FASE 5 - Production Readiness (Semanas 17-18)

## Semana 17 - Docker, CI/CD y Entornos

Leer:
- 12factor.net
- Docker docs, getting started

Aprender:
- Dockerfile multi-stage (C# y Go).
- Docker Compose para multi-servicio.
- Variables de entorno, health checks.
- CI pipeline: format/lint -> test -> build.

Proyecto:
- Dockerfile para ASP.NET Core (multi-stage).
- Dockerfile para Go (multi-stage — build con golang, run con scratch/distroless).
- Docker Compose: monolito C# + Payment Service Go + PostgreSQL + Redis + NATS/RabbitMQ.
- GitHub Actions (2 pipelines):
  - C#: `dotnet format --verify-no-changes` -> test -> build.
  - Go: `go vet` + `staticcheck` -> `go test -race ./...` -> build.
- Health endpoints en ambos servicios.

Entregable:
- Sistema completo levantando con `docker compose up`.
- Pipelines CI funcionando para ambos lenguajes.

---

## Semana 18 - Resiliencia Basica

Leer:
- Release It!, stability antipatterns y stability patterns

Aprender:
- Timeouts, retries con exponential backoff, circuit breaker.
- Bulkheads conceptuales, idempotency.
- Error handling en boundaries (gRPC status codes).

Proyecto:
- [C#] Circuit breaker con Polly/Microsoft.Extensions.Http.Resilience en el gRPC client que llama a Go.
  - Timeout configurado. Retry solo para errores transient.
  - Fallback: si Payment Service esta caido, encolar y reintentar despues.
- [Go] Payment Service con fallos controlados:
  - gRPC interceptor que simula latencia/errores (para probar el circuit breaker del client).
  - Idempotency key en `CreatePayment` (Redis-backed).
  - Graceful shutdown: cerrar listeners, drenar goroutines, timeout de gracia.

Entregable:
- Flujo de pago resiliente end-to-end.
- ADR corto: "Donde usamos retry y donde no, y por que".

---

# FASE 6 - Concurrencia Deep Dive (Semanas 19-21)

## Semana 19 - Concurrencia en C#: async/await, Threads y Primitivas

Leer:
- CLR via C# — Jeffrey Richter — Cap 27-28 (o equivalente en Microsoft Learn)
- Stephen Cleary: "There Is No Thread" y "Async/Await Best Practices"

Aprender:

Modelo mental:
- Thread pool del CLR: OS threads managed, ~1MB stack cada uno.
- async/await NO crea threads — libera el thread al pool durante I/O.
- Concurrency vs parallelism: concurrencia es estructura, paralelismo es ejecucion simultanea.
- Preemptive scheduling: el OS puede interrumpir un thread en cualquier punto.

Primitivas de sincronizacion:
- `lock` / `Monitor`: mutual exclusion. Nunca usar en codigo async.
- `SemaphoreSlim`: limitar N accesos concurrentes. Async-friendly (`WaitAsync`).
- `Interlocked.*`: operaciones atomicas. El mas barato.
- `ReaderWriterLockSlim`: multiple readers, single writer.
- `ConcurrentDictionary`, `ConcurrentQueue`: colecciones thread-safe.
- `Channel<T>`: producer/consumer moderno (equivalente a Go channels).

Race conditions:
- Read-modify-write no es atomico.
- No hay detector nativo (vs `go run -race`). Usar stress tests + assertions.
- Fix: `Interlocked` para contadores, `lock` para secciones criticas, `Channel<T>` para serializar.

Deadlocks:
- Classic lock ordering.
- **Thread pool starvation**: `.Result` o `.Wait()` bloquea el thread. Si el pool se agota, deadlock.
- Regla: **async all the way down**.

Patterns:
- `Task.WhenAll`: N tareas I/O en paralelo.
- `Channel<T>` producer/consumer con backpressure.
- `SemaphoreSlim` como throttle.
- `CancellationToken` propagado end-to-end.
- `Parallel.ForEachAsync` (.NET 6+).

Trampas:
- `Task.Run` en ASP.NET Core: no mejora nada, mismo pool.
- `async void`: excepciones se pierden.
- Thread pool starvation: latencia crece, thread count sube, CPU baja.

Proyecto:
- Ejercicio 1: Race condition con `Parallel.For`. Corregir con `Interlocked` y con `lock`. Medir.
- Ejercicio 2: Provocar thread pool starvation con `.Result` bajo carga (`bombardier`). Corregir.
- Ejercicio 3: `Channel<T>` + `BackgroundService`: endpoint encola ordenes, background las procesa.
- Ejercicio 4: Throttle a API externa con `SemaphoreSlim` (max 5 concurrentes).
- Ejercicio 5: `CancellationToken` end-to-end (client cancela -> API -> DB query se cancela).

Entregable:
- Race condition provocada y corregida con evidencia.
- `Channel<T>` + `BackgroundService` procesando ordenes.
- Documento: "Thread pool starvation: como lo provoque, detecte y corregi".

---

## Semana 20 - Concurrencia en Go: Goroutines, Channels y Patterns

Leer:
- Concurrency in Go — Katherine Cox-Buday — Cap 1-4
- Repasar Learning Go cap 12 (ya leido en semana 8)

Aprender:

Modelo mental:
- Goroutines: green threads M:N, ~2KB stack.
- "Don't communicate by sharing memory; share memory by communicating."
- Go scheduler: cooperative + preemptive (Go 1.14+).
- `go test -race`: detector de races built-in.

Primitivas:
- `sync.Mutex` / `sync.RWMutex`.
- `sync/atomic`.
- `sync.WaitGroup`.
- `sync.Once`.
- Channels: unbuffered y buffered.
- `context.Context`: cancelacion y timeouts.

Patterns:
- Fan-out/fan-in.
- Worker pool (ya implementado parcialmente).
- `select`: multiplexar channels + timeout + cancelacion.
- Pipeline: stages conectados por channels.
- Context cancellation propagada.

Deadlocks en Go:
- Channel unbuffered sin receptor.
- Go detecta deadlocks triviales (todas goroutines dormidas).
- Solucion: receptor antes de enviar, buffered channels, `select` + timeout.

Comparativa C# vs Go:

| Concepto | C# | Go |
|----------|----|----|
| Mutual exclusion | `lock` / `Monitor` | `sync.Mutex` |
| Read-write lock | `ReaderWriterLockSlim` | `sync.RWMutex` |
| Atomicos | `Interlocked.*` | `sync/atomic` |
| Semaforo | `SemaphoreSlim` | `make(chan struct{}, n)` |
| Esperar N tareas | `Task.WhenAll` | `sync.WaitGroup` |
| One-time init | `Lazy<T>` | `sync.Once` |
| Thread-safe map | `ConcurrentDictionary` | `sync.Map` o mutex+map |
| Cancelacion | `CancellationToken` | `context.Context` |
| Producer/consumer | `Channel<T>` | channels |
| Race detection | No nativo | `go test -race` |

Proyecto:
- Expandir Payment Service Go con concurrencia real:
  - Worker pool: N goroutines consumiendo payments de un channel.
  - Fan-out fraud check: consultar 3 providers en paralelo, tomar la primera respuesta.
  - Provocar race condition intencionalmente -> `go test -race` -> corregir.
  - Context cancellation: si el client cancela, propagar hasta la goroutine mas profunda.
  - `select` con timeout: si fraud check tarda >2s, cancelar y aprobar con flag.

Entregable:
- Worker pool produccion-ready en Go.
- Fan-out fraud check con `select` + timeout.
- Race condition detectada y corregida (evidencia de `-race`).
- Documento: "Concurrencia C# vs Go — que me cuesta mas, tradeoffs, cuando cada uno".

---

## Semana 21 - Distributed Systems Conceptual

Leer:
- Building Microservices (2nd ed) — Sam Newman — Cap 1-2
- Microservices Patterns — Chris Richardson — Cap 1
- Microservices Patterns — Cap 4, seccion "Saga" (lectura conceptual)
- DDIA 2nd ed — Cap 6 (Replication) + Cap 7 (Sharding) — lectura ligera

Aprender:
- Microservices: que son, cuando NO usarlos.
  - Monolito -> Modular Monolith -> Microservices (evolucion, no big bang).
  - Un Senior opera dentro de microservices — no los disena.
- CQRS conceptual: separar writes de reads.
- Sagas conceptual: orchestration vs choreography, compensacion.
- Async messaging: queues, idempotency, Dead Letter Queue.
- Database per service, eventual consistency.
- CAP theorem simplificado.

Proyecto:
- Analizar tu sistema actual (C# monolito + Go service):
  - Ya tienes 2 servicios comunicandose. Eso es un "micro-front" de microservices.
  - Disenar (en papel): que pasaria si agregas Inventory como tercer servicio.
  - Dibujar la saga: Order -> Reserve Stock -> Charge Payment -> Confirm (con compensaciones).
- [Go] Implementar consumer de Dead Letter Queue:
  - Payments que fallan 3 veces van a DLQ.
  - Worker que loggea/alerta sobre mensajes en DLQ.
- [C#] Publicar evento `OrderCreated` via MassTransit/queue real (no in-memory).

Entregable:
- Diagrama: saga del flujo de compra con compensaciones.
- DLQ consumer funcionando en Go.
- Documento: "Cuando microservices SI y cuando NO para este proyecto".

---

# FASE 7 - Observability y Senior Integration (Semana 22)

## Semana 22 - Modulo Final End-to-End

Leer:
- Observability Engineering, caps 1-2, 5-7
- Repasar notas de todo el roadmap

Aprender:
- Structured logging, Correlation IDs, Metrics RED.
- Tracing basico con OpenTelemetry.
- [C#] Serilog o logging nativo de .NET.
- [Go] slog (structured logging nativo desde Go 1.21).
- Senior ownership: codigo, tests, deploy, monitoreo y review.

Proyecto final — elegir UNO:

Opcion A (C#): Agregar bounded context `Promotions` o `Reviews` al monolito.
Opcion B (Go): Agregar `Inventory Service` completo como servicio Go independiente.

Debe incluir (sin importar el lenguaje elegido):
- Domain model con invariants.
- Arquitectura hexagonal.
- PostgreSQL con migrations e indexes.
- Query analysis de al menos 2 queries.
- Tests unitarios e integracion.
- API documentada (Swagger en C#, proto docs en Go).
- Logs estructurados con correlation ID.
- Correlation ID propagado entre servicios (OpenTelemetry o header manual).
- Al menos una decision documentada en ADR.
- C4 Component diagram.
- Self-review del PR.

Entregable:
- PR final listo para merge.
- Documento: "Que revisaria si este PR fuera de otra persona".
- Trace end-to-end: un request que cruza ambos servicios con correlation ID visible.

---

# Rutina Semanal

| Dia | Actividad | Tiempo |
|-----|-----------|--------|
| Lunes | Lectura principal + notas | 90 min |
| Martes | Implementacion (alternar C#/Go por semana) | 90 min |
| Miercoles | Implementacion + tests | 90 min |
| Jueves | Medicion/refactor/debug | 90 min |
| Viernes | Entregable + self-review | 90 min |
| Sabado | System design o practica DB | 60 min |
| Domingo | Repaso ligero | 30 min |

---

# Autoevaluacion Mensual

Puntua del 1 al 5:

| Area | Mes 1 | Mes 2 | Mes 3 | Mes 4 | Mes 5 |
|------|-------|-------|-------|-------|-------|
| Clean Code y OOP | | | | | |
| SOLID y refactoring | | | | | |
| Testing unit/integration | | | | | |
| API design (REST + gRPC) | | | | | |
| Go fluency | | | | | |
| Modular monolith + service boundaries | | | | | |
| Hexagonal architecture | | | | | |
| DDD tactico | | | | | |
| PostgreSQL modeling | | | | | |
| Indexes y query plans | | | | | |
| Transactions/MVCC/locks | | | | | |
| Redis/caching | | | | | |
| Docker/CI (multi-servicio) | | | | | |
| Resilience (circuit breaker, retry) | | | | | |
| Concurrencia C# (async, Channel, starvation) | | | | | |
| Concurrencia Go (goroutines, channels, race) | | | | | |
| Distributed systems conceptual | | | | | |
| Observability | | | | | |
| Code review y mentoring | | | | | |

---

# Entregables Clave

| Fase | Semanas | Entregables |
|------|---------|-------------|
| 1 - Foundations | 1-4 | Orders C# + Payment Service Go (stub), tests en ambos, gRPC en semana 7 |
| 2 - Patterns/Refactoring | 5-8 | Patterns en ambos, gRPC conectado, modular monolith + service |
| 3 - Architecture/DDD | 9-12 | Hexagonal en ambos, DDD en ambos, events cross-service, C4, ADRs |
| 4 - Databases | 13-16 | PostgreSQL en ambos servicios, EXPLAIN, locks, Redis, idempotency |
| 5 - Production | 17-18 | Docker multi-servicio, CI dual, resilience end-to-end |
| 6 - Concurrencia | 19-21 | Deep dive C# y Go, worker pool, fan-out, distributed systems |
| 7 - Integration | 22 | Modulo final end-to-end con observability cross-service |

Total:
- 14+ entregables fuertes.
- 2 servicios reales comunicandose (C# + Go).
- 1 fase fuerte de bases de datos.
- 1 fase fuerte de concurrencia en ambos lenguajes.
- 1 PR final que demuestre nivel Senior.

---

# Preguntas que Debes Poder Responder al Final

- Por que elegiste ese boundary de modulo?
- Que invariants protege tu aggregate?
- Que pasa si dos usuarios compran el ultimo item al mismo tiempo?
- Que es thread pool starvation y como lo provocas con `.Result`?
- Por que `lock` no sirve en codigo async y que usas en su lugar?
- En Go, por que channels son preferibles a mutex para comunicacion entre goroutines?
- Cuando usas gRPC vs REST vs async messaging?
- Por que este index ayuda a esta query?
- Por que esta query hizo sequential scan?
- Que isolation level estas usando y que anomalias permite?
- Como evitas N+1?
- Como harias esta migracion sin downtime?
- Que pasa si Redis cae?
- Esta operacion es idempotente? Como lo garantizas?
- Si el Payment Service se cae, que pasa con las ordenes pendientes?
- Que log necesitas para debuggear un bug que cruza dos servicios?
- Que revisarias antes de aprobar este PR?
- Cuando pondrias algo en Go vs C#? Dame un ejemplo concreto.

---

# Guia Rapida: Cuando Go vs C#

| Criterio | Go | C# |
|----------|----|----|
| Concurrencia pesada (miles de goroutines) | ✓ | |
| Worker pools, consumers de queues | ✓ | |
| gRPC server de alto throughput | ✓ | |
| CLI tools, infra, devtools | ✓ | |
| Domain model rico (DDD, aggregates) | | ✓ |
| CQRS con command/query buses | | ✓ |
| API REST con logica de negocio | | ✓ |
| Middleware/filters/interceptors complejos | | ✓ |
| Prototipado rapido de APIs | | ✓ |
| Idempotency/retry workers | ✓ | |
| Performance critica, baja latencia | ✓ | |
| Event-driven consumers | ✓ | Posible |
| Background processing simple | Posible | ✓ (BackgroundService) |

Regla: Go cuando necesitas rendimiento, concurrencia y simplicidad. C# cuando necesitas estructura, DDD y velocidad de desarrollo. Se conectan via gRPC o queues.

---

# Criterio de Exito

Terminas este roadmap cuando puedes tomar una feature ambigua y entregar:

- Diseno claro (elige el lenguaje correcto para el problema).
- Codigo mantenible en C# Y en Go.
- Tests utiles en ambos.
- Modelo de datos justificado.
- Performance medida.
- Concurrencia correcta (sin races, sin starvation).
- Servicios resilientes y comunicandose.
- Logs/traces suficientes para debuggear cross-service.
- Deploy reproducible.
- PR entendible.
- Tradeoffs documentados.

Eso es Senior fuerte.
