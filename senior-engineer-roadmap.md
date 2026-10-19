# Senior Software Engineer Roadmap

Duración: 20 semanas (~5 meses)
Dedicación: 2 horas diarias (mínimo 1.5h)
Método: Codear → Romper → Leer → Refactorizar

---

# Principio Fundamental

Un Senior NO es un Mid que sabe más frameworks.
Un Senior:
- Escribe código que otros pueden mantener sin preguntarte
- Es dueño de features end-to-end: diseño, implementación, testing, deploy, monitoreo
- Toma buenas decisiones técnicas dentro de su equipo
- Identifica problemas antes de que se conviertan en incidentes
- Mentora juniors y mids con su código y sus reviews
- **Su código es su mejor documentación**

---

# Evolución: De Mid a Senior

| Mid | Senior |
|-----|--------|
| Implementa lo que le piden | Propone cómo implementar |
| Resuelve bugs | Previene bugs con diseño |
| Escribe tests porque se lo piden | Escribe tests porque mejoran su diseño |
| Conoce su parte del código | Entiende el sistema completo |
| Pregunta "¿cómo?" | Pregunta "¿por qué?" y "¿qué pasa si falla?" |
| Trabaja en su feature | Piensa en cómo su feature afecta al sistema |
| Sigue patterns | Sabe cuándo romper un pattern |

---

# Stack Tecnológico

| Lenguaje | Para qué | Framework / Herramientas |
|----------|----------|--------------------------|
| Go | Microservices de alto rendimiento, CLI tools, infra, concurrencia | Standard library + chi/gin minimal |
| TypeScript | APIs, BFF, dominio de negocio, CQRS, full-stack | NestJS |

Libro adicional para Go:
- Learning Go — Jon Bodner (O'Reilly) — leer en paralelo las primeras 4 semanas

TypeScript / NestJS:
- Documentación oficial de NestJS es suficiente — no necesitas libro aparte

---

# Biblioteca

| # | Libro | Fase | Prioridad | Dónde |
|---|-------|------|-----------|-------|
| 1 | Clean Code Fundamentals (2025) — Robert C. Martin | 1–3 | Alta | O'Reilly |
| 2 | A Philosophy of Software Design — John Ousterhout | 1 | Alta | O'Reilly |
| 3 | Head First Design Patterns — Freeman & Robson | 2 | Alta | O'Reilly |
| 4 | Refactoring — Martin Fowler | 2 | Alta | O'Reilly |
| 5 | (Cubierto por Clean Code Fundamentals 2025 — Part III) | 3 | — | — |
| 6 | Fundamentals of Software Architecture — Richards & Ford | 3 | Media | O'Reilly |
| 7 | The C4 Model — Simon Brown | 3 | Media | O'Reilly |
| 8 | Learning Domain-Driven Design — Vlad Khononov | 4 | Alta | O'Reilly |
| 9 | Designing Data-Intensive Applications (2nd ed, 2026) — Martin Kleppmann | 5–6 | Alta | O'Reilly |
| 10 | Building Microservices (2nd ed) — Sam Newman | 6 | Media | O'Reilly |
| 11 | Microservices Patterns — Chris Richardson | 6 | Media | O'Reilly |
| 12 | Release It! (2nd ed) — Michael Nygard | 6 | Media | O'Reilly |
| 13 | System Design Interview Vol. 1 — Alex Xu | 6–7 | Alta | Comprar aparte (bytebytego.com) |
| 14 | Learning Go (2nd ed) — Jon Bodner | 1–4 | Alta (paralelo) | O'Reilly |

Recursos web (gratis):
- Refactoring.Guru — catálogo visual de design patterns
- c4model.com — guía oficial del modelo C4
- martinfowler.com — artículos de refactoring, patterns, architecture
- NestJS docs (docs.nestjs.com) — referencia oficial del framework
- ByteByteGo newsletter (blog.bytebytego.com) — diagramas de system design
- Google API Design Guide (cloud.google.com/apis/design) — estándar de diseño REST de Google
- Microsoft REST API Guidelines (github.com/microsoft/api-guidelines) — convenciones REST de Microsoft

---

## Arquitectura E-Commerce (hacia donde vas)

| Servicio | Lenguaje | Responsabilidad |
|----------|----------|-----------------|
| Orders Service | NestJS | Orders (DDD + CQRS básico) |
| Payment Service | Go | Payments (gRPC server) |

No empiezas con todo esto. Empiezas con un archivo y vas creciendo.

---

# FASE 1 — OOP, CLEAN CODE & ENGINEERING FOUNDATIONS (Semanas 1–4)

## Semana 1 — OOP Profundo + Clean Code

Stack: Go (aprender sintaxis básica) + TypeScript (refactor en NestJS)

Leer:
- Clean Code Fundamentals (2025) — Cap 1, 3–4 (Clean Code, First Principles, Meaningful Names)
- A Philosophy of Software Design — Cap 1–4
- Learning Go — Cap 1–4 (Setup, tipos, bloques, funciones)

Estudiar OOP a fondo:
- Los 4 pilares: Encapsulation, Abstraction, Inheritance, Polymorphism
- Cuándo usar herencia vs composición (favor composition over inheritance)
- Interfaces vs clases abstractas: cuándo usar cada una
- Cohesión y acoplamiento en clases
- Go perspective: no tiene herencia — composición by design (embedding)

API Design (leer: Google API Design Guide — cloud.google.com/apis/design):
- REST naming: sustantivos plurales (/orders, /products), no verbos
- HTTP methods correctos: GET (leer), POST (crear), PUT (reemplazar), PATCH (actualizar parcial), DELETE
- Status codes: 200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Internal Server Error
- Error format consistente: { "error": { "code": 400, "message": "...", "details": [...] } }
- Pagination desde el inicio: GET /orders?page=1&limit=20 o cursor-based

Ejercicio:
- [TS/NestJS] Tomar un service de tu proyecto actual con más de 200 líneas
- Identificar violaciones de encapsulation y responsabilidad
- Refactorizar aplicando OOP correctamente
- [Go] Crear el mismo concepto usando structs + interfaces (sin clases)

Proyecto E-Commerce:
- [TS/NestJS] Orders module: crear un order (POST /orders), listar orders (GET /orders)
- [Go] Mismo concepto: HTTP server con chi/gin, crear y listar orders
- Base de datos: in-memory (array/map) — no DB real aún
- Aplicar REST best practices desde el día 1: naming, status codes, pagination, error format

Entregable:
- Código refactorizado en ambos lenguajes con antes/después

---

## Semana 2 — Funciones, Responsabilidad y Complejidad

Stack: Go (funciones, packages) + TypeScript (modules NestJS)

Leer:
- Clean Code Fundamentals (2025) — Cap 5, 7–8 (Comments, Clean Functions, Function Heuristics)
- A Philosophy of Software Design — Cap 5–8 (Information Hiding, Deep Modules)
- Learning Go — Cap 5–7 (Funciones, punteros, tipos, métodos, interfaces)

Conceptos:
- Deep modules vs shallow modules (Ousterhout)
- Information hiding como principio de diseño
- Funciones < 20 líneas, un nivel de abstracción por función
- Go: packages como unidad de modularidad (exported vs unexported)

API Design:
- Resource relationships: GET /orders/:id/items (sub-resources)
- Filtering: GET /products?category=electronics&min_price=100
- Sorting: GET /products?sort=price&order=desc
- Referencia: Microsoft REST API Guidelines (github.com/microsoft/api-guidelines)

Ejercicio:
- [TS/NestJS] Elegir un module complejo → aplicar information hiding
- [Go] Crear un package con API pública mínima (exported) y lógica interna (unexported)
- En ambos: convertir shallow modules en deep modules

Proyecto E-Commerce:
- [TS/NestJS] Separar: Controller → Service → Repository (in-memory)
- [Go] Separar: Handler → Service → Repository (in-memory)
- Agregar: Products module/package (CRUD básico con sub-resources, filtering, sorting)

Entregable:
- PR o diff con el refactor aplicado en ambos lenguajes

---

## Semana 3 — SOLID como Mentalidad de Diseño

Stack: Go (interfaces implícitas) + TypeScript (DI en NestJS)

Leer:
- Clean Code Fundamentals (2025) — Cap 12, 19 (Objects and Data Structures, SOLID Principles)
- A Philosophy of Software Design — Cap 9–11
- Learning Go — Cap 8–9 (Generics, Errors)

Estudiar SOLID profundamente:
- S — Single Responsibility: una razón para cambiar
- O — Open/Closed: extensible sin modificar
- L — Liskov Substitution: subtipos deben ser sustituibles
- I — Interface Segregation: interfaces específicas > interfaces gordas
- D — Dependency Inversion: depender de abstracciones, no de concretos
- Go perspective: interfaces implícitas hacen ISP y DIP naturales
- NestJS perspective: el sistema de DI (@Injectable, providers) aplica DIP por defecto

Ejercicio:
- [TS/NestJS] Encontrar al menos 1 violación de cada principio SOLID en tu proyecto
- [Go] Implementar DIP con interfaces implícitas — comparar con el @Injectable de Nest

Proyecto E-Commerce:
- [TS/NestJS] Agregar: descuentos a orders (por tipo de cliente, por cantidad, por cupón)
- [Go] Misma lógica de descuentos
- Interfaces para Repository (ya no depender del in-memory directamente)
- SRP: DiscountCalculator separado del OrderService
- OCP: agregar nuevo tipo de descuento sin modificar código existente
- DIP: Service depende de interface Repository, no de la implementación

Entregable:
- Documento: "Auditoría SOLID de mi proyecto"

---

## Semana 4 — Testing como Diseño + Concurrencia

Stack: Go (testing nativo, concurrencia) + TypeScript (Jest en NestJS)

Leer:
- Clean Code Fundamentals (2025) — Cap 14–15 (Testing Disciplines: TDD, Clean Tests)
- A Philosophy of Software Design — Cap 12–13
- Learning Go — Cap 12 (Concurrency: goroutines, channels, select, mutexes)
- Learning Go — Cap 15 (Testing en Go: table-driven tests, benchmarks)

Concurrencia (conceptos fundamentales):
- Concurrency vs Parallelism: concurrencia es estructura, paralelismo es ejecución
- Threads vs Processes vs Coroutines/Goroutines
- Race conditions: cuando 2 threads/goroutines acceden al mismo dato sin coordinación
- Mutexes / Locks: proteger datos compartidos (sync.Mutex en Go)
- Deadlocks: cuando 2 threads se bloquean mutuamente esperando el lock del otro
- Go: goroutines (lightweight threads), channels (comunicación entre goroutines), select, sync.WaitGroup
- Node/NestJS: event loop, single-threaded por defecto, Worker Threads para CPU-intensive
- Regla de Go: "Don't communicate by sharing memory; share memory by communicating" (channels > mutexes)

Complemento: Concurrency in Go — Katherine Cox-Buday (O'Reilly) — leer Cap 1–4 si quieres profundizar

Leer TDD:
- Test Driven Development: By Example — Kent Beck — Cap 1–17 (Part I: Money Example + Part II: xUnit Example)
- Es corto (~220 páginas) y 100% práctico — se lee en 2-3 días

Aprender testing:
- Test Pyramid: unit → integration → e2e
- Arrange / Act / Assert
- Test doubles: mocks vs stubs vs fakes (cuándo usar cada uno)
- TDD ciclo: Red → Green → Refactor
  - Red: escribir un test que falla
  - Green: escribir el código mínimo para que pase
  - Refactor: limpiar sin romper el test
- TDD como herramienta de diseño: el test te fuerza a pensar en la API antes de implementar
- Tests como documentación viva
- Go: table-driven tests (patrón idiomático), testing package nativo
- NestJS: Jest + @nestjs/testing, TestingModule para DI en tests

Ejercicio:
- [Go] Escribir table-driven tests para el código de semanas anteriores
- [Go] Implementar un worker pool con goroutines + channels: N goroutines procesando tareas de un channel
- [Go] Provocar un race condition intencionalmente, detectarlo con go run -race, y corregirlo con Mutex o channel
- [TS/NestJS] Escribir tests con Jest usando TestingModule para inyectar mocks
- En ambos: practicar test-first → implementación después

Proyecto E-Commerce:
- [TS/NestJS] Tests unitarios: OrderService, DiscountCalculator, ProductService
- [Go] Table-driven tests para lo mismo
- [Go] Agregar concurrencia: inventory check con goroutines (verificar stock de múltiples productos en paralelo)
- [Go] Provocar race condition → detectar con `go run -race` → corregir con mutex
- TDD: Red → Green → Refactor para validar que order no exceda stock

Entregable:
- Suite de tests en Go y NestJS para el código refactorizado
- Worker pool en Go con goroutines + channels
- Race condition detectada con go run -race y corregida
- Mínimo 80% coverage del código de las semanas 1–3

---

# FASE 2 — DESIGN PATTERNS & REFACTORING (Semanas 5–8)

## Semana 5 — Patrones Creacionales y Estructurales

Stack: Go (patrones sin clases) + TypeScript (patrones clásicos OOP)

Leer:
- Head First Design Patterns — Cap 1–4
- Complementar con Refactoring.Guru (web)

Patrones a dominar:
- Factory Method / Abstract Factory — cuándo crear objetos sin exponer lógica
- Builder — construcción compleja paso a paso
- Singleton — por qué es polémico y cuándo es válido
- Adapter — conectar interfaces incompatibles
- Decorator — agregar comportamiento sin modificar clases
- Facade — simplificar subsistemas complejos

Ejercicio:
- [Go] Implementar Factory (función que retorna interface) + Adapter (struct que wrappea otra)
- [TS/NestJS] Implementar Factory como custom provider + Decorator como middleware/interceptor
- NestJS ya usa estos patrones internamente: Guards (Chain of Resp), Interceptors (Decorator), Pipes (Adapter)

Proyecto E-Commerce:
- [TS/NestJS] Factory para crear diferentes tipos de Order (standard, express, subscription)
- [TS/NestJS] Adapter: integrar un payment gateway falso (mock) detrás de un PaymentGatewayPort
- [Go] Factory function que retorna interface Order según tipo
- [Go] Adapter: wrappear un HTTP client externo detrás de una interface

Entregable:
- Código en ambos lenguajes + tests de cada patrón implementado

---

## Semana 6 — Patrones de Comportamiento

Stack: Go (funciones como first-class citizens) + TypeScript (clases + NestJS patterns)

Leer:
- Head First Design Patterns — Cap 5–8
- Refactoring.Guru: sección Behavioral Patterns

Patrones a dominar:
- Strategy — intercambiar algoritmos en runtime
- Observer — notificaciones desacopladas
- Command — encapsular acciones como objetos
- Template Method — definir esqueleto, delegar pasos
- State — comportamiento que cambia según estado
- Chain of Responsibility — pasar requests por una cadena de handlers

Ejercicio:
- [Go] Strategy con interfaces + funciones (en Go, una función puede satisfacer una interface)
- [Go] Observer usando channels (patrón idiomático Go, no callbacks)
- [TS/NestJS] Strategy como providers intercambiables vía DI
- [TS/NestJS] Observer usando EventEmitter2 o @nestjs/cqrs EventBus

Proyecto E-Commerce:
- [TS/NestJS] Strategy: diferentes formas de calcular shipping (flat, by weight, by distance)
- [TS/NestJS] Observer con EventEmitter2: cuando se crea un order → notificar inventory
- [Go] Strategy con interfaces para shipping calculation
- [Go] Observer con channels: order created → channel → inventory listener

Entregable:
- Refactor real de tu código: un switch/if-else convertido a Strategy
- Tests antes y después

---

## Semana 7 — Patrones Avanzados + Anti-patterns

Stack: Go + TypeScript (comparar enfoques)

Leer:
- Head First Design Patterns — Cap 9–12
- Refactoring — Fowler — Cap 1–3 (Intro + Code Smells)

Patrones adicionales:
- Repository (patrón, no DDD aún)
- Dependency Injection: manual (Go) vs container (NestJS)
- Specification pattern
- Mediator — NestJS lo usa internamente con @nestjs/cqrs

Anti-patterns a reconocer:
- God class / God module
- Anemic domain model
- Spaghetti architecture
- Golden hammer ("todo se resuelve con X")
- Premature abstraction
- Go-specific: interface pollution (definir interfaces que nadie más implementa)
- NestJS-specific: circular dependencies entre modules

API Design:
- Documentar tu API con OpenAPI/Swagger:
  - [NestJS] @nestjs/swagger — decorators que generan docs automáticamente
  - [Go] swaggo/swag o escribir openapi.yaml manual
- API contracts: el spec es el contrato entre tu API y los clientes
- Referencia: API Design Patterns — JJ Geewax (O'Reilly) — Cap 1-5 (consulta, no lectura completa)

Ejercicio:
- [TS/NestJS] Auditar tu proyecto buscando anti-patterns
- [Go] Implementar Repository pattern con interface + struct concreto
- Comparar: DI manual en Go vs @Injectable/@Module en NestJS

Proyecto E-Commerce:
- [TS/NestJS] Reemplazar in-memory repository por PostgreSQL (TypeORM o Prisma)
- [Go] Reemplazar in-memory repository por PostgreSQL (pgx o sqlx)
- Agregar Redis para cache de Products
- Documentar API con OpenAPI/Swagger (@nestjs/swagger en NestJS, swaggo/swag en Go)

Entregable:
- Documento: "Anti-patterns encontrados y plan de corrección"
- API documentada con Swagger/OpenAPI

---

## Semana 8 — Refactoring Disciplinado

Stack: Go + TypeScript (refactoring en ambos)

Leer:
- Refactoring — Fowler — Cap 4–6
- A Philosophy of Software Design — Cap 14–17 (repasar)

Técnicas de refactoring:
- Extract Method / Extract Class (TS) / Extract Function + struct (Go)
- Move Method
- Replace Conditional with Polymorphism
- Introduce Parameter Object
- Replace Inheritance with Delegation (TS) / ya es default en Go

Ejercicio:
- [TS/NestJS] Elegir el module más complejo → aplicar 5 técnicas de refactoring
- [Go] Elegir el package más complejo → refactorizar manteniendo tests verdes
- Cada paso debe mantener los tests verdes (en ambos lenguajes)

Proyecto E-Commerce:
- [Ambos] Refactorizar todo el código acumulado:
  - Extract Method donde haya funciones largas
  - Replace Conditional with Polymorphism donde haya if/switch
  - Introduce Parameter Object donde haya muchos parámetros
- Agregar: User module (registro, login básico con JWT)
- Commits atómicos: cada refactoring es un commit separado
- Milestone: tienes un monolito funcional en ambos lenguajes

Entregable:
- Serie de commits atómicos, cada uno con un refactoring específico
- Milestone: al terminar semana 8 debes tener un mini-proyecto en Go y otro en NestJS con tests, patterns aplicados y código limpio

---

# FASE 3 — ARCHITECTURE FUNDAMENTALS (Semanas 9–11)

## Semana 9 — Qué es Arquitectura (para un Senior)

Stack: Agnóstico (conceptual) — aplicar análisis a tus proyectos Go y NestJS

Leer:
- Clean Code Fundamentals (2025) — Cap 23–24 (Two Values of Software, Independence)
- Clean Code Fundamentals (2025) — Cap 25–27 (Architectural Boundaries, Clean Boundaries, Clean Architecture)
- Fundamentals of Software Architecture — Cap 1–3 (Architectural Thinking, Modularity)

Conceptos:
- Arquitectura = las decisiones difíciles de revertir
- Modularity: cohesion, coupling, connascence
- La Dependency Rule: dependencias apuntan hacia adentro
- Un Senior no necesita diseñar la arquitectura entera, pero sí entenderla y respetarla

Ejercicio:
- Analizar tus mini-proyectos Go y NestJS:
  - ¿Cuáles son las decisiones arquitectónicas implícitas?
  - ¿Qué coupling existe entre módulos/packages?
  - Dibujar las dependencias — ¿respetan la dependency rule?

Proyecto E-Commerce:
- Analizar tu monolito e-commerce: ¿qué coupling existe?
- Documentar las decisiones arquitectónicas implícitas que ya tomaste
- Dibujar las dependencias entre módulos/packages
- No construir código nuevo — solo analizar y documentar

Entregable:
- Diagrama de dependencias de tu proyecto con problemas identificados

---

## Semana 10 — Estilos Arquitectónicos + Hexagonal

Stack: NestJS (hexagonal natural) + Go (hexagonal manual)

Leer:
- Clean Code Fundamentals (2025) — Cap 27 (The Clean Architecture: Dependency Rule, Crossing Boundaries)
- Fundamentals of Software Architecture — Cap 9–12 (estilos más comunes)

Estilos a entender:
- Layered architecture — el default (y sus problemas)
- Hexagonal / Ports & Adapters — inversión de dependencias real
- Clean Code Fundamentals (2025) — Cap 27 (la dependency rule aplicada)
- Modular Monolith — el sweet spot para muchos proyectos

API Design:
- Tu API HTTP es un adapter (infrastructure), no parte del domain
- Los controllers/handlers llaman a use cases del application layer
- El domain no sabe si lo llaman por HTTP, gRPC, CLI o un test

Ejercicio:
- [TS/NestJS] Restructurar tu proyecto como hexagonal:
  - domain/ (entities, ports como interfaces)
  - application/ (use cases, services)
  - infrastructure/ (adapters: DB, HTTP, etc.)
  - NestJS modules como bounded modules
- [Go] Misma estructura hexagonal:
  - internal/domain/ (types, interfaces como ports)
  - internal/application/ (use cases)
  - internal/infrastructure/ (adapters)
  - cmd/ (entry point)

Proyecto E-Commerce:
- [TS/NestJS] Reestructurar el e-commerce a hexagonal:
  src/orders/domain/ → entities, value objects, ports
  src/orders/application/ → use cases, services
  src/orders/infrastructure/ → adapters (PostgreSQL repo, HTTP controllers)
- [Go] Misma estructura hexagonal
- Recordar: tu API HTTP es un adapter, no parte del domain

Entregable:
- Código reestructurado como hexagonal en ambos lenguajes
- Tests que prueban que el dominio no depende de infraestructura

---

## Semana 11 — Diagramas C4 y Documentación Técnica

Leer:
- The C4 Model — Simon Brown — Cap 1–6 (los 4 niveles)
- The C4 Model — Cap 7–9 (Dynamic, Deployment, System Landscape)

Aprender:
- Modelo C4: Context, Container, Component, Code
- Cuándo usar cada nivel
- Un Senior debe poder dibujar la arquitectura de su sistema en 5 minutos

Ejercicio:
- Crear diagrama C4 (niveles Context + Container + Component) de tu proyecto
- Nivel Code no siempre es necesario — solo para partes complejas

Proyecto E-Commerce:
- Diagrama C4 completo (3 niveles: Context, Container, Component) del e-commerce
- System Design mini: diseñar un URL shortener (30 min, papel)

Entregable:
- Diagrama C4 (3 niveles) de tu proyecto

Primer System Design mini:
- Leer: System Design Interview Vol. 1 — Cap 1 (Scale From Zero to Millions) + Cap 3 (Framework)
- Diseñar un URL shortener (30 min, papel/whiteboard)
- Después: leer Vol. 1 — Cap 8 (Design a URL Shortener) y comparar

---

# FASE 4 — DOMAIN-DRIVEN DESIGN (Semanas 12–14)

## Semana 12 — DDD Tactical: El Modelo Rico

Stack: NestJS (modelo rico con clases) + Go (modelo rico con structs)

Leer:
- Learning Domain-Driven Design — Cap 1–3 (Domain, Subdomains, Ubiquitous Language)
- Learning DDD — Cap 4–7 (Entities, Value Objects, Aggregates, Repositories)

Conceptos:
- Ubiquitous language — hablar el idioma del negocio en el código
- Entities vs Value Objects
- Aggregates y aggregate roots
- Invariants: reglas que el aggregate protege
- Repositories (patrón DDD)
- Domain Services vs Application Services

Cambio mental:

Antes: tabla orders → ORM → controller
Después: Order Aggregate protege reglas de negocio

Ejercicio:
- [TS/NestJS] Modelar Order Aggregate con clases: Entity base, Value Objects inmutables, invariants en métodos
- [Go] Mismo modelo con structs: NewOrder() constructor, métodos que validan invariants, VOs como tipos custom
- En ambos: refactorizar modelo anémico → modelo rico

Proyecto E-Commerce:
- [TS/NestJS] Order Aggregate: Order (Entity, Aggregate Root), OrderItem (Entity), Money (Value Object), Address (Value Object), OrderStatus con lógica
- Invariants: no puedes agregar items a un order cancelado, total no puede ser negativo
- [Go] Mismo modelo con structs + métodos que protegen invariants
- Refactorizar: modelo anémico → modelo rico

Entregable:
- Código del modelo de dominio en ambos lenguajes + tests de invariants

---

## Semana 13 — Bounded Contexts y Domain Events

Leer:
- Learning DDD — Cap 8–10 (Bounded Contexts, Context Mapping)
- Learning DDD — Cap 11 (Domain Events)

Conceptos:
- Bounded Context: el límite donde un modelo tiene significado
- Context Map: cómo se relacionan los contextos
- Domain Events: hechos que ya ocurrieron en el dominio
- Un Senior no diseña los bounded contexts de toda la empresa, pero debe entenderlos para no violar límites

Ejercicio:
- Dibujar el Context Map de tu sistema — identificar bounded contexts implícitos
- [TS/NestJS] Implementar domain events usando @nestjs/cqrs EventBus
- [Go] Implementar event bus simple con channels

Proyecto E-Commerce:
- Dibujar Context Map: Orders, Payments, Products como bounded contexts
- [TS/NestJS] Domain events con @nestjs/cqrs EventBus:
  - OrderCreatedEvent → Payment module escucha
  - PaymentCompletedEvent → Orders module actualiza status
- [Go] Event bus simple con channels entre packages
- Anti-Corruption Layer entre Orders y Payments

Entregable:
- Context Map diagram
- Código con domain events implementados en ambos lenguajes

System Design mini:
- Diseñar un sistema de notificaciones (30 min)
- Después: leer System Design Interview Vol. 1 — Cap 10 (Design a Notification System) y comparar

---

## Semana 14 — DDD Aplicado: Integración Real

Stack: NestJS (@nestjs/cqrs) + Go

Leer:
- Microservices Patterns — Cap 3 (Inter-process Communication) — sección de Domain Events y Messaging

Conceptos:
- Anti-Corruption Layer: proteger tu dominio de modelos externos
- CQRS básico: separar commands de queries
- Event publishing interno vs externo

Ejercicio:
- [TS/NestJS] Implementar CQRS básico con @nestjs/cqrs:
  - CommandBus para writes
  - QueryBus para reads
- Separar un módulo de tu proyecto usando Anti-Corruption Layer
- Conectar 2 bounded contexts vía domain events

Proyecto E-Commerce:
- [TS/NestJS] CQRS básico con @nestjs/cqrs:
  - CommandBus para writes (CreateOrderCommand, CancelOrderCommand)
  - QueryBus para reads (GetOrderQuery, ListOrdersQuery)
- Conectar 2 bounded contexts vía domain events

Entregable:
- Código con CQRS + Anti-Corruption Layer + domain events
- Diagrama de flujo de eventos entre módulos

---

# FASE 5 — DATABASES & DEVOPS (Semanas 15–16)

## Semana 15 — Databases en la Práctica

Stack: Go (pgx, go-redis) + TypeScript (TypeORM/Prisma en NestJS, ioredis)

Leer:
- DDIA 2nd ed — Cap 3 (Data Models and Query Languages)
- DDIA 2nd ed — Cap 4 (Storage and Retrieval: B-Trees, LSM, indexes)

Bases de datos — cuándo usar cada una:
- PostgreSQL: tu default para casi todo — ACID, JSON support, full-text search
- MongoDB: documentos flexibles, esquema variable — NO es "más escalable que SQL"
- Redis: cache, session store, pub/sub, rate limiting — in-memory, no es DB primaria

Modelado de datos:
- Normalización vs denormalización: tradeoffs reales
- Indexes: cómo funcionan, cuándo crearlos, cuándo son contraproducentes
- Migrations: estrategias para cambios de schema sin downtime
- N+1 queries: el problema más común y cómo resolverlo

Caching:
- Cache-aside pattern (el más común)
- Cache invalidation: TTL, event-based
- Redis como cache: cuándo sí y cuándo es overkill

Ejercicio:
- [TS/NestJS] Modelar el schema de tu proyecto con TypeORM o Prisma — justificar cada index
- [Go] Conectar a PostgreSQL con pgx + implementar cache-aside con Redis
- Analizar query plans de tus 3 queries más pesadas

Proyecto E-Commerce:
- Separar bases de datos por bounded context:
  - Orders: PostgreSQL, Payments: PostgreSQL, Products: PostgreSQL + Redis (cache)
- Modelado de datos: justificar cada index, analizar query plans
- Dockerizar: Dockerfile multi-stage para Go y NestJS
- docker-compose.yml: ambos servicios + PostgreSQL + Redis

Entregable:
- Schema con indexes justificados
- Query plan analysis

---

## Semana 16 — DevOps Fundamentals

Stack: Docker + CI/CD

Leer:
- Building Microservices — Cap 6 (Deployment)
- 12factor.net — The Twelve-Factor App (web, gratis)

Containers:
- Docker mental model: image → container → registry
- Dockerfile: multi-stage builds para Go y Node/NestJS
- Docker Compose: orquestar múltiples servicios localmente

CI/CD:
- Pipeline básico: lint → test → build → deploy
- GitHub Actions: configurar pipeline para tu proyecto Go + NestJS
- Deployment strategies conceptual: rolling update, blue-green, canary

Kubernetes conceptual (no necesitas ser admin):
- Pods, Services, Deployments — qué hace cada uno
- Un Senior debe entender dónde corre su código

Ejercicio:
- Dockerizar tu proyecto Go + NestJS (multi-stage builds)
- Docker Compose: levantar ambos servicios + PostgreSQL + Redis localmente
- Crear pipeline CI/CD básico (GitHub Actions): lint → test → build image

Proyecto E-Commerce:
- GitHub Actions pipeline para Go y NestJS: lint → test → build → docker build
- API versioning: preparar endpoints para evolucionar (/api/v1/orders)

Entregable:
- Dockerfile para Go y NestJS (optimizados con multi-stage)
- docker-compose.yml que levante el sistema completo
- Pipeline CI/CD funcional

---

# FASE 6 — DISTRIBUTED SYSTEMS & MICROSERVICES BASICS (Semanas 17–18)

## Semana 17 — Distributed Systems Fundamentals

Leer:
- DDIA 2nd ed — Cap 1 (Trade-Offs in Data Systems Architecture)
- DDIA 2nd ed — Cap 6 (Replication)
- DDIA 2nd ed — Cap 7 (Sharding)
- DDIA 2nd ed — Cap 8 (Transactions)

Conceptos:
- Por qué los sistemas distribuidos son difíciles (redes fallan, mensajes se duplican, servicios caen)
- Replication: leader-follower, multi-leader
- Sharding: range vs hash
- Transactions: ACID, isolation levels
- Eventual consistency: qué significa en la práctica
- Idempotency: por qué importa

Ejercicio:
- Para tu sistema: ¿necesitas replication? ¿sharding? Justificar
- Diseñar: ¿cómo harías un endpoint idempotente?

Proyecto E-Commerce:
- Extraer Orders y Payments en servicios independientes
- Comunicación sync: gRPC entre Orders y Payments (.proto compartido, Go como server, NestJS como client)
- Implementar endpoint idempotente en Payments

Entregable:
- Documento: "Consideraciones de distribución para [mi sistema]"

System Design:
- Diseñar un sistema de e-commerce (45 min)
- Referencia: System Design Interview Vol. 1 — Cap 5 (Consistent Hashing)

---

## Semana 18 — Microservices: Lo que un Senior Necesita Saber

Leer:
- Building Microservices — Cap 1–3 (What, How to Model, Splitting)
- Microservices Patterns — Cap 1–2 (Monolithic Hell, Decomposition)
- Release It! — Cap 4–5 (Stability Antipatterns, Stability Patterns)

Conceptos:
- Monolith vs Modular Monolith vs Microservices — evolución, no big bang
- Comunicación: REST vs gRPC vs async (message queues)
- Circuit Breaker: proteger de cascading failures
- Retry con exponential backoff
- Timeout strategy
- Un Senior no decide la arquitectura macro, pero debe saber operar dentro de ella

API Design para microservices (leer: gRPC: Up and Running — Kasun Indrasiri, O'Reilly — Cap 1-4):
- gRPC vs REST: cuándo usar cada uno
  - gRPC: comunicación interna entre servicios (rápido, tipado fuerte)
  - REST: API pública para clientes externos (universal, fácil de debuggear)
- Protocol Buffers: definir contratos .proto versionados
- API versioning: URL versioning (/api/v1/orders) o header versioning
- Backward compatibility: agregar campos es safe, quitar rompe clientes

Ejercicio:
- [Go + NestJS] Comunicar un servicio Go con un servicio NestJS via gRPC:
  - Definir .proto compartido
  - Go como servidor gRPC
  - NestJS como cliente
- Implementar circuit breaker básico en ambos lenguajes

Proyecto E-Commerce:
- [Go] Circuit breaker en Payment Service (sony/gobreaker o manual)
- [TS/NestJS] Circuit breaker como Interceptor en Orders
- Retry con exponential backoff en las llamadas gRPC
- Timeout strategy en ambos servicios

Entregable:
- Código: comunicación gRPC entre Go y NestJS
- Circuit breaker implementado

System Design:
- Diseñar un sistema de chat (45 min)
- Después: leer System Design Interview Vol. 1 — Cap 12 (Design a Chat System)

---

# FASE 7 — OBSERVABILITY & SENIOR MINDSET (Semanas 19–20)

## Semana 19 — Observability para Seniors

Leer:
- Observability Engineering — Cap 1–2 (Qué es observability, cómo difiere de monitoring)
- Observability Engineering — Cap 5–7 (Structured events, tracing, OpenTelemetry)
- Observability Engineering — Cap 12 (SLOs for reliability)

Structured Logging:
- Por qué JSON logs > text logs
- Correlation IDs: rastrear un request a través de servicios
- Qué loggear y qué NO loggear (nunca passwords, PII, tokens)

Métricas:
- RED method: Rate, Errors, Duration (para servicios)
- USE method: Utilization, Saturation, Errors (para recursos)

Tracing:
- OpenTelemetry: instrumentar tu código para distributed tracing
- Span, Trace, Context propagation

Ejercicio:
- [Go] Implementar structured logging con slog + correlation IDs
- [TS/NestJS] Implementar structured logging con Pino + correlation IDs via middleware
- [Ambos] Integrar OpenTelemetry básico para tracing entre Go y NestJS

Proyecto E-Commerce:
- [Go] Structured logging con slog: JSON, correlation IDs
- [TS/NestJS] Structured logging con Pino: JSON, correlation IDs via middleware
- [Ambos] Integrar OpenTelemetry básico para tracing entre Go y NestJS
- Definir SLOs básicos para los endpoints más críticos

Entregable:
- Código: structured logging + tracing en ambos lenguajes
- Un request rastreable end-to-end entre los 2 servicios

---

## Semana 20 — Senior Mindset: Integración Total

Leer:
- Repasar notas de todas las fases
- System Design Interview Vol. 1 — Cap 1 y 3 (repasar framework)

Habilidades Senior que no son código:
- Code reviews: cómo dar feedback útil (no "nit: use const")
- Estimación: por qué es difícil y cómo mejorar (romper en tareas pequeñas)
- Debugging en producción: logs, tracing, métricas — no println
- Ownership: "mi feature" incluye tests, deploy, y monitoreo
- Mentoría implícita: tu código enseña — haz que enseñe bien

Ejercicio final — Diseñar e implementar un módulo completo:

Elegir uno de tu proyecto integrador:
1. Agregar un nuevo bounded context completo (ej: Reviews, Shipping, o Promotions)
2. Migrar un módulo de NestJS a Go (o viceversa) manteniendo compatibilidad

Debe incluir:
- Modelo de dominio con entities, VOs, aggregates, invariants
- Arquitectura hexagonal
- Tests: unit + integration
- Dockerizado
- Structured logging + correlation IDs
- Comunicación con al menos otro servicio (gRPC o events)
- Pipeline CI/CD
- Diagrama C4 (nivel Component)

Proyecto E-Commerce:
- Construir un nuevo bounded context completo desde cero (Reviews, Shipping, o Promotions):
  - Modelo de dominio con entities, VOs, aggregates, invariants
  - Arquitectura hexagonal desde el inicio
  - Tests: unit + integration
  - Dockerizado
  - Structured logging + correlation IDs
  - Comunicación con al menos otro servicio (gRPC o events)
  - Pipeline CI/CD
  - Diagrama C4 (nivel Component)
  - API documentada con Swagger

Entregable:
- Código completo del módulo con tests
- Diagrama C4
- Un pull request que tú mismo revisarías como "listo para merge"

---

# Rutina Semanal Recomendada

| Día | Actividad | Tiempo |
|-----|-----------|--------|
| Lunes | Lectura profunda + notas | 90 min |
| Martes | Lectura + releer notas | 90 min |
| Miércoles | Ejercicio práctico: código | 90 min |
| Jueves | Ejercicio práctico: código + tests | 90 min |
| Viernes | Completar entregable semanal | 90 min |
| Sábado | System design exercise (a partir de semana 11) | 60 min |
| Domingo | Repaso semanal | 30 min |

---

# Autoevaluación Mensual

Puntúa del 1 al 5 cada mes:

| Área | Mes 1 | Mes 2 | Mes 3 | Mes 4 | Mes 5 |
|------|-------|-------|-------|-------|-------|
| OOP & Clean Code | | | | | |
| Design Patterns | | | | | |
| SOLID & Refactoring | | | | | |
| Testing (unit + integration) | | | | | |
| Architecture (hexagonal, dependency rule) | | | | | |
| Domain Modeling (DDD) | | | | | |
| Databases (modeling, indexes, caching) | | | | | |
| DevOps (Docker, CI/CD) | | | | | |
| Distributed Systems Basics | | | | | |
| Observability (logging, tracing) | | | | | |
| System Design | | | | | |
| Code Reviews & Mentoring | | | | | |

---

# Resumen de Entregables por Fase

| Fase | Semanas | Entregables clave |
|------|---------|-------------------|
| 1 - Foundations | 1–4 | Auditoría SOLID, refactors con tests, 80% coverage |
| 2 - Patterns | 5–8 | Patrones implementados, anti-patterns documentados, refactoring commits |
| 3 - Architecture | 9–11 | Proyecto hexagonal, diagrama C4, primer system design |
| 4 - DDD | 12–14 | Modelo de dominio rico, CQRS básico, domain events |
| 5 - Databases & DevOps | 15–16 | Schema con indexes, Dockerfiles, CI/CD pipeline |
| 6 - Distributed | 17–18 | gRPC entre servicios, circuit breaker, system designs |
| 7 - Senior Mindset | 19–20 | Observability integrada, módulo completo end-to-end |

Total: ~14 entregables concretos + 4 system design exercises

---

# Diferencia clave: Senior vs Staff

Este roadmap te lleva a Senior. El roadmap de Staff/Principal (26 semanas) continúa desde aquí y agrega:

| Senior (este roadmap) | Staff (roadmap de 26 semanas) |
|---|---|
| Entiende la arquitectura de su sistema | Diseña la arquitectura de múltiples sistemas |
| Escribe buen código | Escribe código que define el estándar del equipo |
| Resuelve problemas en su equipo | Resuelve problemas que cruzan equipos |
| Sabe de DDD tactical | Domina DDD strategic + tactical |
| System design básico | System design completo con tradeoffs |
| Documenta su código | Escribe ADRs, RFCs, design docs |
| Entiende microservices | Decide si usar microservices o no |
| Opera dentro de la arquitectura | Define la arquitectura |

Cuando completes este roadmap y quieras seguir creciendo → pasa al roadmap Staff/Principal.

---

# Lecturas Adicionales de Referencia

Libros que NO son parte del roadmap pero son útiles para consultar.

## Bases de Datos
- **PostgreSQL: Up and Running** — Regina Obe (O'Reilly)
- **Redis in Action** — Josiah Carlson (O'Reilly)

## OOP
- **The Object-Oriented Thought Process (5th ed)** — Matt Weisfeld (O'Reilly)

## Concurrencia
- **Concurrency in Go** — Katherine Cox-Buday (O'Reilly) — goroutines, channels, patterns de concurrencia, errgroup. Si quieres dominar concurrencia en Go más allá de lo básico.

## DevOps
- **Docker: Up & Running** — Sean Kane (O'Reilly)

## API Design
- **API Design Patterns** — JJ Geewax (O'Reilly) — patterns para diseñar APIs robustas: naming, pagination, filtering, versioning. Referencia, no lectura lineal.
- **Designing Web APIs** — Brenda Jin et al. (O'Reilly) — más introductorio, cubre REST, webhooks, GraphQL, developer experience.
- **gRPC: Up and Running** — Kasun Indrasiri (O'Reilly) — gRPC a fondo: protocol buffers, streaming, interceptors. Cap 1-4 son los esenciales.

## Otros
- **Grokking Algorithms** — Aditya Bhargava (O'Reilly) — refrescar algoritmos de forma visual.
- **The Pragmatic Programmer** — Hunt & Thomas (O'Reilly) — clásico de mentalidad developer.

---

END.
