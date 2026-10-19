# Staff/Principal Engineer Roadmap — Plan Optimizado

Duración: 26 semanas (~6.5 meses)
Dedicación: 2 horas diarias (mínimo 1.5h)
Método: Diseñar → Fallar → Leer → Rediseñar

---

# Principio Fundamental

Un Staff Engineer NO es un Senior que sabe más tecnologías.
Un Staff Engineer:
- Reduce complejidad en sistemas que cruzan equipos
- Toma decisiones con tradeoffs explícitos y los documenta
- Diseña límites correctos entre sistemas y equipos
- Piensa en cómo evoluciona el sistema en 2 años
- Comunica decisiones de forma clara — a técnicos y no técnicos
- Lidera sin autoridad formal: influencia, no jerarquía
- **Sigue escribiendo código** — es el developer con más impacto técnico de la organización

---

# Evolución de Preguntas Mentales

| Nivel | Pregunta dominante | Impacto |
|-------|-------------------|---------|
| Junior | ¿Cómo funciona esto? | Tarea |
| Mid | ¿Cómo lo implemento correctamente? | Feature |
| Senior | ¿Dónde vive cada responsabilidad? ¿Cómo escala? | Sistema |
| Senior+ | ¿Cómo falla? ¿Qué pasa a las 3 AM? | Sistema + operación |
| Staff | ¿Qué tradeoff acepto y por qué? ¿Cómo afecta a otros equipos? | Múltiples sistemas |
| Principal | ¿Puede esta organización evolucionar estos sistemas? | Organización |

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

# Biblioteca Completa

| # | Libro | Fase | Prioridad | Dónde |
|---|-------|------|-----------|-------|
| 1 | Clean Code Fundamentals (2025) — Robert C. Martin | 1–3 | Alta | O'Reilly |
| 2 | A Philosophy of Software Design — John Ousterhout | 1 | Alta | O'Reilly |
| 3 | Head First Design Patterns — Freeman & Robson | 2 | Alta | O'Reilly |
| 4 | Refactoring — Martin Fowler | 2 | Media | O'Reilly |
| 6 | Fundamentals of Software Architecture — Richards & Ford | 3 | Alta | O'Reilly |
| 7 | Learning Domain-Driven Design — Vlad Khononov | 4 | Alta | O'Reilly |
| 8 | Domain-Driven Design Distilled — Vaughn Vernon | 4 | Complemento | O'Reilly |
| 9 | Building Microservices (2nd ed) — Sam Newman | 6 | Alta | O'Reilly |
| 10 | Designing Data-Intensive Applications (2nd ed, 2026) — Martin Kleppmann | 5–6 | Alta | O'Reilly |
| 11 | Microservices Patterns — Chris Richardson | 6 | Alta | O'Reilly |
| 12 | Release It! (2nd ed) — Michael Nygard | 7 | Alta | O'Reilly |
| 13 | Observability Engineering — Charity Majors et al. | 7 | Alta | O'Reilly |
| 14 | Software Architecture: The Hard Parts — Richards et al. | 7 | Alta | O'Reilly |
| 15 | Team Topologies — Skelton & Pais | 7 | Alta | O'Reilly |
| 16 | The Staff Engineer's Path — Tanya Reilly | 7 | Alta | O'Reilly |
| 17 | Staff Engineer — Will Larson | 7 | Alta | O'Reilly |
| 18 | Building Evolutionary Architectures — Ford, Parsons & Kua | 7 | Complemento | O'Reilly |
| 26 | The C4 Model — Simon Brown | 3 | Alta | O'Reilly |
| 19 | Learning Go (2nd ed) — Jon Bodner | 1–4 | Alta (paralelo) | O'Reilly |
| 20 | System Design Interview Vol. 1 — Alex Xu | 3–7 | Alta | Comprar aparte (bytebytego.com) |
| 21 | System Design Interview Vol. 2 — Alex Xu & Sahn Lam | 6–7 | Alta | Comprar aparte (bytebytego.com) |
| 22 | Understanding Distributed Systems — Roberto Vitillo | 6 | Complemento | Comprar aparte (understandingdistributed.systems) |
| 23 | Thinking in Systems — Donella Meadows | 7 | Complemento | Comprar aparte |
| 24 | Learning Systems Thinking — Diana Montalion | 7 | Complemento | O'Reilly |
| 25 | Think Distributed Systems — Dominik Tornow | 6 | Complemento | O'Reilly |

Sobre los libros fuera de O'Reilly:
- Alex Xu Vol. 1 y 2: los mejores recursos para system design paso a paso. No tienen reemplazo en O'Reilly.
- Understanding Distributed Systems (Vitillo): DDIA más corto y práctico (~250 páginas). Opcional pero muy útil.
- Thinking in Systems (Meadows): no es técnico — enseña a pensar en sistemas complejos, feedback loops, y efectos secundarios. Muy Staff/Principal mindset.

Sobre los libros Staff:
- The Staff Engineer's Path (Reilly): el libro más práctico sobre SER Staff — cómo elegir proyectos de impacto, liderar sin autoridad, escribir docs que convenzan, navegar la ambigüedad.
- Staff Engineer (Larson): los 4 arquetipos (Tech Lead, Architect, Solver, Right Hand) + historias de Staff Engineers reales. Te ayuda a identificar qué tipo de Staff quieres ser.

Recursos web (gratis):
- Refactoring.Guru — catálogo visual de design patterns
- c4model.com — guía oficial del modelo C4 (Simon Brown)
- martinfowler.com — artículos de CQRS, Event Sourcing, Microservices
- NestJS docs (docs.nestjs.com) — referencia oficial del framework
- ByteByteGo newsletter (blog.bytebytego.com) — artículos gratuitos de Alex Xu con diagramas de system design
- Google API Design Guide (cloud.google.com/apis/design) — estándar de diseño REST de Google
- Microsoft REST API Guidelines (github.com/microsoft/api-guidelines) — convenciones REST de Microsoft

---

## Arquitectura E-Commerce (hacia donde vas)

| Servicio | Lenguaje | Bounded Context | Por qué ese lenguaje |
|----------|----------|-----------------|---------------------|
| API Gateway / BFF | NestJS | Orquestación | Routing, auth, aggregation |
| Orders Service | NestJS | Orders (DDD + CQRS) | Domain model rico con clases |
| Payment Service | Go | Payments | Alto rendimiento, idempotency |
| Inventory Service | Go | Inventory | Concurrencia, stock locks |
| Notification Service | Go | Notifications | Workers async, alto throughput |

No empiezas con todo esto. Empiezas con un archivo y vas creciendo semana a semana.

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

Ejercicio:
- [TS/NestJS] Tomar un service de tu proyecto actual con más de 200 líneas
- Identificar violaciones de encapsulation y responsabilidad
- Refactorizar aplicando OOP correctamente
- [Go] Crear el mismo concepto usando structs + interfaces (sin clases)

Proyecto E-Commerce:
- [TS/NestJS] Orders module: crear un order (POST /orders), listar orders (GET /orders)
- [Go] Mismo concepto: HTTP server con chi/gin, crear y listar orders
- Base de datos: in-memory (array/map) — no DB real aún
- Aplicar REST best practices: naming, status codes, pagination, error format

Entregable:
- Documento breve: "3 problemas OOP que encontré y cómo los resolví"
- Reflexión: ¿Qué cambia al pensar en composición (Go) vs herencia (TS)?

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
- Por qué los comentarios malos son peores que ningún comentario
- Go: packages como unidad de modularidad (exported vs unexported)

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
- ISP: interfaces pequeñas y específicas

Entregable:
- Documento: "Auditoría SOLID de mi proyecto"
- Comparación: cómo Go y NestJS resuelven DI de formas opuestas

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

Complemento: Concurrency in Go — Katherine Cox-Buday (O'Reilly) — libro dedicado, leer Cap 1–4 si quieres profundizar

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
- Go: table-driven tests (patrón idiomático), testing package nativo, no necesitas framework
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
- [TS/NestJS] Tests de integración con TestingModule
- TDD: Red → Green → Refactor para una feature nueva (ej: validar que order no exceda stock)
- Go: provocar race condition en inventory → resolverla con mutex

Entregable:
- Suite de tests en Go y NestJS para el código refactorizado
- Worker pool en Go con goroutines + channels
- Race condition detectada con go run -race y corregida

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
- Código en ambos lenguajes + diagrama UML de cada patrón
- Nota: ¿Cómo cambia la implementación de Factory sin herencia (Go)?

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
- [TS/NestJS] Command pattern usando @nestjs/cqrs CommandBus

Proyecto E-Commerce:
- [TS/NestJS] Strategy: diferentes formas de calcular shipping (flat, by weight, by distance)
- [TS/NestJS] Observer con EventEmitter2: cuando se crea un order → notificar inventory
- [Go] Strategy con interfaces para shipping calculation
- [Go] Observer con channels: order created → channel → inventory listener

Entregable:
- Antes/después del refactor en ambos lenguajes
- Insight: Go resuelve Strategy con funciones, TS lo resuelve con clases — ambos son válidos

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

Ejercicio:
- [TS/NestJS] Auditar tu proyecto buscando anti-patterns
- [Go] Implementar Repository pattern con interface + struct concreto
- Comparar: DI manual en Go vs @Injectable/@Module en NestJS

Proyecto E-Commerce:
- [TS/NestJS] Reemplazar in-memory repository por PostgreSQL (TypeORM o Prisma)
- [Go] Reemplazar in-memory repository por PostgreSQL (pgx o sqlx)
- Agregar Redis para cache de Products
- Mediator: OrderService coordina Order + Payment + Inventory sin que se conozcan
- Documentar API con OpenAPI/Swagger

Entregable:
- Documento: "Anti-patterns encontrados y plan de corrección"

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
- Proyecto milestone: al terminar semana 8 debes tener un mini-proyecto en Go y otro en NestJS con tests, patterns aplicados y código limpio

---

# FASE 3 — SOFTWARE ARCHITECTURE FOUNDATIONS (Semanas 9–12)

## Semana 9 — Qué es Arquitectura REALMENTE

Stack: Agnóstico (conceptual) — aplicar análisis a tus proyectos Go y NestJS

Leer:
- Fundamentals of Software Architecture — Cap 1–3
- Clean Code Fundamentals (2025) — Cap 23–24 (Two Values of Software, Independence)

Conceptos:
- Arquitectura = las decisiones difíciles de revertir
- Architecture characteristics (ilities): scalability, availability, etc.
- Architectural thinking vs developer thinking
- Modularity: cohesion, coupling, connascence

Ejercicio:
- Analizar tus mini-proyectos Go y NestJS de las fases anteriores:
  - ¿Cuáles son las decisiones arquitectónicas implícitas?
  - ¿Qué coupling existe entre módulos/packages?
  - ¿Qué architecture characteristics prioriza cada uno?
  - ¿Cuál es más modular? ¿Por qué?

Proyecto E-Commerce:
- Analizar tu monolito e-commerce: ¿qué coupling existe? ¿qué characteristics prioriza?
- Documentar las decisiones arquitectónicas implícitas que ya tomaste
- Identificar qué módulos están acoplados y por qué
- No construir código nuevo — solo analizar y documentar

Entregable:
- Documento: "Análisis arquitectónico comparado: Go vs NestJS"

Nota Staff: Un Staff no solo analiza — presenta. Practica explicar este análisis a alguien no técnico en 5 minutos. Si no puedes, simplifica.

---

## Semana 10 — Estilos Arquitectónicos

Stack: NestJS (hexagonal natural) + Go (hexagonal manual)

Leer:
- Fundamentals of Software Architecture — Cap 9–15
- Clean Code Fundamentals (2025) — Cap 25–27 (Architectural Boundaries, Clean Boundaries, Clean Architecture)

Estilos a entender:
- Layered architecture — el default (y sus problemas)
- Hexagonal / Ports & Adapters — inversión de dependencias real
- Clean Architecture (estilo) — la dependency rule (Cap 27 de Clean Code Fundamentals)
- Onion Architecture — capas concéntricas
- Modular Monolith — el sweet spot ignorado
- Microkernel — plugins y extensibilidad

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
- Tu API HTTP es un adapter, no parte del domain

Entregable:
- Diagrama C4 (nivel Container) de ambos proyectos como hexagonal
- Código reestructurado en ambos lenguajes

---

## Semana 11 — Architecture Characteristics y Tradeoffs

Leer:
- Fundamentals of Software Architecture — Cap 4 (Architecture Characteristics Defined)
- Fundamentals of Software Architecture — Cap 5 (Identifying Architecture Characteristics)
- Fundamentals of Software Architecture — Cap 6 (Measuring and Governing Architecture Characteristics)
- Fundamentals of Software Architecture — Cap 7–8 (Scope, Component-based Thinking)
- Clean Code Fundamentals (2025) — Cap 27 (The Clean Architecture: Dependency Rule, Crossing Boundaries)
- Building Evolutionary Architectures — Cap 2 (Fitness Functions) — referencia para este concepto específico

Aprender:
- Cómo identificar los ilities que importan — no todos importan (Fundamentals Cap 5)
- Tradeoff analysis: cada decisión tiene costo (Fundamentals Cap 4)
- Architecture fitness functions: tests automatizados de arquitectura (Building Evolutionary Cap 2)
- Architecture quantum: unidad desplegable independiente (Fundamentals Cap 8)

Ejercicio:
- Para tu proyecto: elegir los 3 architecture characteristics más importantes
- Para cada uno: qué decisiones lo favorecen y qué sacrificas

Proyecto E-Commerce:
- Elegir los 3 architecture characteristics más importantes para el e-commerce
- Escribir ADR formal: "Por qué elegimos hexagonal para Orders"
- Implementar fitness function: test que verifica que domain/ no importa de infrastructure/

Entregable:
- ADR (Architecture Decision Record) formal sobre una decisión de tu proyecto

Nota Staff: Un Staff justifica tradeoffs con datos y métricas, no con opinión. "Elegimos eventual consistency porque nuestro SLO de latencia es 200ms p99 y strong consistency agrega 80ms" > "Elegimos eventual consistency porque es más rápido".

---

## Semana 12 — Diagramas C4 y Comunicación Arquitectónica

Leer:
- The C4 Model — Simon Brown (O'Reilly) — Cap 1–6 (los 4 niveles: System Context, Container, Component, Code)
- The C4 Model — Cap 7–9 (Dynamic, Deployment, System Landscape — diagramas complementarios)
- Fundamentals of Software Architecture — Cap 21–24 (Diagramming, Presenting)
- Documenting Software Architectures (O'Reilly) — Cap 1–3 (cómo documentar decisiones)

Artículos (web):
- "Architecture Decision Records" — Michael Nygard (cognitect.com/blog)
- "Design Docs at Google" — artículo en web (buscar "design docs at google industrial empathy")

Aprender:
- Modelo C4: Context, Container, Component, Code
- Cuándo usar cada nivel
- Cómo escribir un ADR correctamente
- Cómo escribir un RFC / Design Document

Ejercicio:
- Crear diagrama C4 completo (4 niveles) de tu proyecto
- Escribir un RFC proponiendo un cambio arquitectónico

Proyecto E-Commerce:
- Diagrama C4 completo (4 niveles) del e-commerce
- RFC: "Propuesta para separar Orders y Payments en servicios independientes"

Entregable:
- Diagrama C4 completo
- RFC con: Contexto, Opciones, Decisión, Consecuencias

Primer System Design mini:
- Leer antes: System Design Interview Vol. 1 — Cap 1 (Scale From Zero to Millions) + Cap 3 (A Framework for System Design Interviews)
- Diseñar un URL shortener (30 min, papel/whiteboard)
- Después: leer Vol. 1 — Cap 8 (Design a URL Shortener) y comparar con tu diseño

---

# FASE 4 — DOMAIN-DRIVEN DESIGN (Semanas 13–16)

## Semana 13 — DDD Strategic: El Mapa del Territorio

Leer:
- Learning Domain-Driven Design — Cap 1–3
- Domain-Driven Design Distilled — Cap 1–2 (opcional)

Conceptos:
- Domain, subdomain, core domain
- Ubiquitous language — el lenguaje compartido con negocio
- Problem space vs solution space

Ejercicio:
- Mapear los subdomains de tu proyecto/empresa
- Clasificar: Core, Supporting, Generic
- Identificar dónde el lenguaje técnico diverge del lenguaje del negocio

Proyecto E-Commerce:
- Mapear los subdomains del e-commerce:
  - Core: Orders, Payments (lo que te diferencia)
  - Supporting: Inventory, Shipping
  - Generic: Notifications, Auth
- Definir ubiquitous language: ¿un "Order" significa lo mismo en todos los contextos?
- Context Map: cómo se relacionan los bounded contexts

Entregable:
- Mapa de subdomains con clasificación

System Design mini:
- Diseñar un sistema de notificaciones (30 min)
- Después: leer System Design Interview Vol. 1 — Cap 10 (Design a Notification System) y comparar

---

## Semana 14 — DDD Tactical: El Modelo Rico

Stack: NestJS (modelo rico con clases) + Go (modelo rico con structs)

Leer:
- Learning DDD — Cap 4–7

Conceptos:
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
- Insight: TS permite private/protected para encapsular, Go usa unexported — mismo efecto, diferente mecanismo

---

## Semana 15 — Bounded Contexts y Context Mapping

Leer:
- Learning DDD — Cap 8 (Bounded Contexts: definición, boundaries, physical vs logical)
- Learning DDD — Cap 9 (Context Mapping: relaciones entre bounded contexts)
- Learning DDD — Cap 10 (Evolutionary Design)
- Microservices Patterns — Cap 2, sección "Decompose by Subdomain" (cómo bounded contexts mapean a microservices)
- Building Microservices — Cap 2 (cómo DDD informa el modelado de servicios)

Conceptos:
- Bounded Context: el límite donde un modelo tiene significado (Learning DDD Cap 8)
- Context Map: cómo se relacionan los contextos (Learning DDD Cap 9)
- Relaciones: Partnership, Customer-Supplier, Conformist, Anti-Corruption Layer (Learning DDD Cap 9)
- Shared Kernel vs Separate Ways (Learning DDD Cap 9)

Ejercicio:
- Dibujar el Context Map de tu sistema
- Identificar dónde necesitas Anti-Corruption Layer

Proyecto E-Commerce:
- [TS/NestJS] Separar en NestJS modules que son bounded contexts reales:
  - OrdersModule, PaymentsModule, InventoryModule
  - Anti-Corruption Layer entre Orders y Payments
- [Go] Separar en packages aislados con la misma lógica

Entregable:
- Context Map diagram
- Documento: "Bounded Contexts de [mi proyecto] y sus relaciones"

System Design mini:
- Diseñar un sistema de e-commerce (45 min)
- Referencia: System Design Interview Vol. 2 — Cap 7 (Hotel Reservation System) — mismo patrón de inventory + booking
- Complementar con: Vol. 1 — Cap 5 (Consistent Hashing) para entender distribución de datos

---

## Semana 16 — Domain Events y Integración entre Contextos

Stack: NestJS (@nestjs/cqrs) + Go (channels / event bus simple)

Leer:
- Learning DDD — Cap 11 (Domain Events)
- Clean Code Fundamentals (2025) — Cap 20 (Component Principles: cohesion, coupling, dependencies)
- Microservices Patterns — Chris Richardson — Cap 3 (Inter-process Communication) — sección de Domain Events y Messaging

Artículos (web):
- martinfowler.com/eaaDev/DomainEvent.html — "Domain Event" by Martin Fowler
- "Introducing EventStorming" — Alberto Brandolini (leanpub, también en O'Reilly) — Cap 1–3 para entender la técnica

Conceptos:
- Domain Events: hechos que ya ocurrieron en el dominio
- Event publishing interno (in-process)
- Integración entre Bounded Contexts vía eventos
- Event Storming como técnica de descubrimiento

Ejercicio:
- [TS/NestJS] Implementar domain events usando @nestjs/cqrs EventBus:
  - OrderCreatedEvent → handler en otro module
  - Usar IEventHandler para desacoplar bounded contexts
- [Go] Implementar event bus simple con channels:
  - Publicar eventos en un channel
  - Consumir desde otro package (bounded context)
  - Alternativa: implementar un EventBus con observer pattern

Proyecto E-Commerce:
- [TS/NestJS] Domain events con @nestjs/cqrs EventBus:
  - OrderCreatedEvent → PaymentsModule escucha y crea PaymentIntent
  - PaymentCompletedEvent → OrdersModule actualiza status
  - OrderShippedEvent → NotificationsModule envía email
- [Go] Event bus simple con channels entre packages

Entregable:
- Código con domain events implementados en ambos lenguajes
- Diagrama de flujo de eventos entre contextos

---

# FASE 5 — DATABASES & DEVOPS FOR STAFF (Semanas 17–18)

## Semana 17 — Databases en la Práctica

Stack: Go (pgx, go-redis) + TypeScript (TypeORM/Prisma en NestJS, ioredis)

Leer:
- DDIA 2nd ed — Cap 3 (Data Models and Query Languages: relational vs document vs graph)
- DDIA 2nd ed — Cap 4 (Storage and Retrieval: B-Trees, LSM, column-oriented)
- Fundamentals of Software Architecture — Cap 16 (Choosing the Appropriate Architecture: data considerations)

Bases de datos — cuándo usar cada una:
- PostgreSQL: tu default para casi todo — ACID, JSON support, full-text search, extensiones
- MongoDB: documentos flexibles, esquema variable, prototipado rápido — NO es "más escalable que SQL"
- Redis: cache, session store, pub/sub, rate limiting, leaderboards — in-memory, no es DB primaria
- Elasticsearch: búsqueda full-text, logs, analytics — complemento, no reemplazo de DB
- DynamoDB / Cassandra: write-heavy, distribución masiva — solo si realmente lo necesitas

Modelado de datos:
- Normalización vs denormalización: tradeoffs reales (no dogma)
- Indexes: cómo funcionan, cuándo crearlos, cuándo son contraproducentes (DDIA 2nd ed Cap 4)
- Migrations: estrategias para cambios de schema sin downtime
- N+1 queries: el problema más común y cómo resolverlo

Caching:
- Cache-aside pattern (el más común)
- Write-through vs write-behind
- Cache invalidation: "las 2 cosas difíciles en CS" — TTL, event-based invalidation
- Redis como cache: cuándo sí y cuándo es overkill

Ejercicio:
- [TS/NestJS] Modelar el schema de tu proyecto con TypeORM o Prisma — justificar cada decisión de index
- [Go] Conectar a PostgreSQL con pgx + implementar cache-aside con Redis
- Comparar: cuándo elegirías MongoDB sobre PostgreSQL para un servicio específico de tu sistema

Proyecto E-Commerce:
- Separar bases de datos por bounded context:
  - Orders: PostgreSQL, Payments: PostgreSQL, Inventory: Redis + PostgreSQL, Products: PostgreSQL + Redis
- Dockerizar todo: Dockerfile multi-stage para Go y NestJS
- docker-compose.yml: todos los servicios + todas las DBs + Redis + NGINX

Entregable:
- Documento: "Estrategia de datos para [mi sistema]" — qué DB para qué servicio y por qué
- Schema con indexes justificados + query plan analysis de tus 3 queries más importantes

Nota Staff: Un Staff que dice "usemos MongoDB porque es moderno" pierde credibilidad. Un Staff que dice "usemos PostgreSQL para orders porque necesitamos ACID y transactions, y Redis para cache de catálogo porque el 80% de reads son los mismos 1000 productos" gana confianza.

---

## Semana 18 — DevOps & Cloud para Staff Engineers

Stack: Docker + CI/CD + Kubernetes conceptual

Leer:
- Building Microservices — Cap 6 (Deployment)
- Building Microservices — Cap 7 (Testing in Production, Progressive Delivery)
- Building Microservices — Cap 8 (Monitoring and Observability — preview de semana 23)

Artículos/recursos (web):
- Docker docs: docs.docker.com/get-started — fundamentals
- Kubernetes docs: kubernetes.io/docs/concepts — solo conceptos, no necesitas ser admin
- 12factor.net — The Twelve-Factor App (metodología para apps cloud-native)

Containers:
- Docker mental model: image → container → registry
- Dockerfile: multi-stage builds para Go y Node/NestJS
- Docker Compose: orquestar múltiples servicios localmente
- Por qué containers importan para un Staff: reproducibilidad, aislamiento, deployment uniforme

CI/CD:
- Pipeline básico: lint → test → build → deploy
- GitHub Actions o GitLab CI: configurar pipeline para tu proyecto Go + NestJS
- Deployment strategies: rolling update, blue-green, canary
- Feature flags como alternativa a branches largos

Kubernetes conceptual (no necesitas ser admin):
- Pods, Services, Deployments, Ingress — qué hace cada uno
- Scaling: horizontal pod autoscaler
- ConfigMaps y Secrets: configuración externalizada
- Por qué un Staff necesita entender K8s: tomar decisiones de arquitectura que sean deployables

Infrastructure as Code (conceptual):
- Terraform / Pulumi: qué son y por qué importan
- GitOps: infraestructura como código versionado
- No necesitas ser expert — necesitas saber que existe y cuándo pedirlo

Ejercicio:
- Dockerizar tu proyecto Go + NestJS (multi-stage builds)
- Docker Compose: levantar ambos servicios + PostgreSQL + Redis localmente
- Crear pipeline CI/CD básico (GitHub Actions): lint → test → build image
- Escribir Kubernetes manifests básicos: Deployment + Service para cada microservicio

Proyecto E-Commerce:
- GitHub Actions pipeline para Go y NestJS: lint → test → build → docker build → push
- Environments: staging (auto-deploy on push to main) + production (manual approval)
- Deployment strategy: rolling update

Entregable:
- Dockerfile para Go y NestJS (optimizados con multi-stage)
- docker-compose.yml que levante el sistema completo
- Pipeline CI/CD funcional
- Documento: "Deployment strategy para [mi sistema]" — cómo despliegas, cómo haces rollback

Nota Staff: Un Staff no opera la infra, pero diseña sistemas que se PUEDEN operar. Si tu arquitectura hexagonal perfecta no se puede deployar sin 45 pasos manuales, no sirve.

---

# FASE 6 — MICROSERVICES & DISTRIBUTED SYSTEMS (Semanas 19–22)

## Semana 19 — Microservices: Cuándo SÍ y Cuándo NO

Stack: Conceptual + planear cómo splitear tus proyectos Go/NestJS

Leer:
- Building Microservices (2nd ed) — Cap 1 (What Are Microservices: definición, ventajas, dolor)
- Building Microservices — Cap 2 (How to Model Microservices: bounded contexts como guía)
- Building Microservices — Cap 3 (Splitting the Monolith: strangler fig, branch by abstraction)
- Microservices Patterns — Cap 1 (Escaping Monolithic Hell) + Cap 2 (Decomposition Strategies: by business capability, by subdomain)
- Monolith to Microservices — Sam Newman (O'Reilly) — Cap 1–2 (opcional, profundiza en migración)

Conceptos:
- Microservices como bounded contexts deployed independientemente (Building MS Cap 2)
- Monolith → Modular Monolith → Microservices — evolución, no big bang (Monolith to MS Cap 1)
- Decomposition patterns: by business capability, by subdomain (Microservices Patterns Cap 2)
- El costo real de microservices: red, consistencia, deployment, debugging (Building MS Cap 1)

Aprender a evaluar:
- ¿Tu equipo tiene la madurez operacional? (Building MS Cap 1)
- ¿El dominio justifica la distribución? (Microservices Patterns Cap 2)
- ¿Cuál es el costo de un monolito modular vs microservices? (Building MS Cap 3)

Nota Staff: Esta evaluación es una de las decisiones más Staff que existen. No es solo técnica — involucra capacidad del equipo, timeline de producto, y costo operacional. Un Staff que recomienda microservices sin evaluar si el equipo puede operarlos está creando más problemas de los que resuelve.

Visión del stack:
- NestJS: ideal para modular monolith que evoluciona a microservices (@nestjs/microservices)
- Go: ideal para microservices individuales de alto rendimiento
- Combo real: NestJS como API gateway / BFF + Go para servicios internos hot-path

Ejercicio:
- Evaluar tu proyecto: ¿debería ser monolito, modular monolith, o microservices?
- Diseñar: ¿qué servicios irían en NestJS y cuáles en Go? ¿Por qué?
- Escribir ADR justificando la decisión

Proyecto E-Commerce:
- Extraer Orders y Payments en servicios independientes
- Comunicación sync: gRPC entre Orders y Payments (.proto compartido)
- API Gateway (NestJS): recibe HTTP del frontend, llama a servicios internos

Entregable:
- ADR: "Monolith vs Microservices para [mi proyecto]"
- Diagrama: qué lenguaje para qué servicio y por qué

System Design:
- Diseñar un sistema de chat (45 min)
- Después: leer System Design Interview Vol. 1 — Cap 12 (Design a Chat System) y comparar
- Complementar con: Vol. 2 — Cap 4 (Distributed Message Queue) para la capa de mensajería

---

## Semana 20 — Comunicación entre Servicios

Stack: NestJS (microservices module, gRPC) + Go (gRPC nativo, NATS/RabbitMQ)

Leer:
- Building Microservices — Cap 4–5 (Integration, Splitting)
- Microservices Patterns — Cap 3 (Inter-process Communication: REST, gRPC, messaging)
- Microservices Patterns — Cap 7 (CQRS: implementing query side, maintaining read models)
- Microservices Patterns — Cap 8 (API Gateway pattern, BFF pattern)

Artículos (web):
- martinfowler.com/bliki/CQRS.html — "CQRS" by Martin Fowler
- grpc.io/docs — documentación oficial de gRPC + guía de .proto files

Referencia NestJS:
- docs.nestjs.com/microservices/basics — módulo de microservices
- docs.nestjs.com/microservices/grpc — integración gRPC en Nest

Conceptos:
- Sync: REST, gRPC — cuándo usar cada uno
- Async: Message queues, Event-driven
- CQRS: Commands vs Queries, Read models separados
- API Gateway pattern
- Service mesh conceptual

Ejercicio:
- [TS/NestJS] Implementar CQRS con @nestjs/cqrs:
  - CommandBus para writes
  - QueryBus para reads
  - Separar handlers
- [Go + NestJS] Comunicar un servicio Go con un servicio NestJS via gRPC:
  - Definir .proto compartido
  - Go como servidor gRPC
  - NestJS como cliente con @grpc/grpc-js
- Diseñar la comunicación entre 3 servicios: qué es sync y qué es async

Proyecto E-Commerce:
- [TS/NestJS] CQRS en Orders Service con @nestjs/cqrs:
  - Commands: CreateOrderCommand, CancelOrderCommand, AddItemCommand
  - Queries: GetOrderQuery, ListOrdersQuery
  - CommandBus y QueryBus separados
- Write DB (PostgreSQL normalizado) + Read DB (PostgreSQL desnormalizado o Redis)

Entregable:
- Código: CQRS en NestJS + comunicación gRPC entre Go y NestJS
- Diagrama de comunicación entre servicios con justificación

---

## Semana 21 — Data en Sistemas Distribuidos

Leer:
- DDIA 2nd ed — Cap 1 (Trade-Offs in Data Systems Architecture)
- DDIA 2nd ed — Cap 2 (Defining Nonfunctional Requirements) — NUEVO en 2nd ed, muy relevante para Staff
- DDIA 2nd ed — Cap 3 (Data Models and Query Languages)
- DDIA 2nd ed — Cap 4 (Storage and Retrieval: B-Trees vs LSM, indexes)
- DDIA 2nd ed — Cap 6 (Replication: leader-follower, multi-leader, leaderless)
- DDIA 2nd ed — Cap 7 (Sharding: range vs hash, secondary indexes)
- Microservices Patterns — Cap 6 (Database per Service, Saga + Database, Shared Database antipattern)
- Building Microservices — Cap 6 (Deployment)

Conceptos:
- Nonfunctional requirements como herramienta de decisión (DDIA 2nd ed Cap 2)
- Database per service: por qué y cómo (Microservices Patterns Cap 6)
- Storage engines: B-Trees vs LSM (DDIA 2nd ed Cap 4)
- Indexes: cómo funcionan y tradeoffs (DDIA 2nd ed Cap 4)
- Data replication: leader-follower, multi-leader, leaderless (DDIA 2nd ed Cap 6)
- Sharding: range vs hash (DDIA 2nd ed Cap 7)

Complemento: Think Distributed Systems — Tornow — Cap 1–2 (Models, order, time) + Cap 7–8 (Partitioning, Replication) — segunda perspectiva más concisa que DDIA sobre los mismos temas

Nota Staff: El Cap 2 de DDIA 2nd ed sobre nonfunctional requirements es oro para un Staff — te da el lenguaje para justificar decisiones de infra con datos, no con opinión.

Ejercicio:
- Para tu sistema: ¿qué base de datos usarías para cada servicio y por qué?
- Diseñar estrategia de partitioning para una tabla de alto volumen

Proyecto E-Commerce:
- Agregar RabbitMQ (o NATS) como message broker
- Reemplazar eventos in-process por eventos async entre servicios
- [Go] Notification worker: consume eventos y envía emails (mock)
- Implementar idempotency en consumers

Entregable:
- Documento: "Estrategia de datos para [mi sistema]"

System Design:
- Diseñar un ride-sharing system (1 hora)
- Referencia: System Design Interview Vol. 2 — Cap 1 (Proximity Service) + Cap 2 (Nearby Friends)
- Estos capítulos cubren geolocation, real-time matching y proximity search — el core de ride-sharing

---

## Semana 22 — Consistencia, Eventos y Sagas

Stack: NestJS (saga orchestrator) + Go (workers de compensación)

Leer:
- DDIA 2nd ed — Cap 8 (Transactions: ACID, isolation levels, serializability)
- DDIA 2nd ed — Cap 10 (Consistency and Consensus: linearizability, CAP theorem)
- Microservices Patterns — Cap 4 (Sagas: orchestration vs choreography, compensation logic) — CAPÍTULO CLAVE
- Microservices Patterns — Cap 3, sección "Transactional Outbox" (outbox pattern)
- Building Microservices — Cap 11–12 (Scale, Resilience)

Artículos (web):
- martinfowler.com/articles/patterns-of-distributed-systems — "Idempotent Receiver" pattern
- "Life Beyond Distributed Transactions" — Pat Helland (paper clásico, buscar en ACM o web)

Referencia NestJS:
- docs.nestjs.com/recipes/cqrs — sección Sagas con @Saga() decorator

Conceptos:
- CAP theorem y por qué es simplificado (DDIA 2nd ed Cap 10 lo explica mejor que nadie)
- Eventual consistency: qué significa en la práctica (DDIA 2nd ed Cap 6 + Microservices Patterns Cap 4)

Complemento: Think Distributed Systems — Tornow — Cap 3–6 (Failure tolerance, Message delivery, Transactions, Distributed transactions) + Cap 9–11 (Consistency, Consensus, Durable executions)
- Idempotency: por qué toda operación distribuida debe ser idempotente (Microservices Patterns Cap 3)
- Saga pattern: orquestación vs coreografía (Microservices Patterns Cap 4)
- Compensation logic: rollback en sistemas distribuidos (Microservices Patterns Cap 4)
- Dead Letter Queues (DLQ) (Building Microservices Cap 11)
- Outbox pattern (Microservices Patterns Cap 3)

Ejercicio:
- [TS/NestJS] Implementar saga orchestrator con @nestjs/cqrs Saga:
  - Order → Payment → Inventory → Notification
  - Usar @Saga() decorator
- [Go] Implementar workers de compensación:
  - Listener en queue que ejecuta rollback
  - Idempotency check antes de procesar
- Definir compensaciones para cada paso que puede fallar

Proyecto E-Commerce:
- Saga: Create Order flow completo:
  1. Orders → CreateOrder (PENDING) → publish OrderCreatedEvent
  2. Inventory → ReserveStock → Payments → ChargePayment → Orders → ConfirmOrder
  - Compensaciones si falla algún paso
- [TS/NestJS] Saga orchestrator con @nestjs/cqrs @Saga()
- [Go] Compensation workers
- Implementar Outbox pattern + Dead Letter Queue

Entregable:
- Diagrama de saga con flujo feliz y compensaciones
- Código: NestJS orchestrator + Go compensation workers

---

# FASE 7 — RESILIENCE, SYSTEM DESIGN & STAFF MINDSET (Semanas 23–26)

## Semana 23 — Resilience Patterns y Observabilidad

Stack: Go (circuit breaker nativo) + NestJS (interceptors para resilience) + OpenTelemetry (ambos)

Leer resiliencia:
- Release It! (2nd ed) — Cap 4 (Stability Antipatterns) + Cap 5 (Stability Patterns: Circuit Breaker, Bulkhead, Timeout, Retry)
- Microservices Patterns — Cap 3, sección "Circuit Breaker" + "Service Discovery"
- DDIA 2nd ed — Cap 9 (The Trouble with Distributed Systems: timeouts, clocks, faults)

Leer observabilidad:
- Observability Engineering — Charity Majors — Cap 1–2 (Qué es observability, cómo difiere de monitoring)
- Observability Engineering — Cap 5–7 (Structured events, tracing, instrumentación con OpenTelemetry)
- Observability Engineering — Cap 12–13 (SLOs for reliability, debugging SLO-based alerts)
- Site Reliability Engineering (Google SRE book, O'Reilly gratis) — Cap 4 (SLOs: definición de SLI, SLO, SLA, error budgets)

Artículos (web):
- opentelemetry.io/docs — guía oficial de OpenTelemetry
- "USE Method" — Brendan Gregg (brendangregg.com/usemethod.html)
- "RED Method" — Tom Wilkie (grafana.com/blog)

Complemento:
- Chaos Engineering — Casey Rosenthal & Nora Jones (O'Reilly) — inyectar fallos intencionalmente para probar resiliencia. Netflix inventó esto con Chaos Monkey. Leer Cap 1–4 para entender el framework.

Conceptos de resiliencia:
- Circuit Breaker: proteger de cascading failures (Release It! Cap 5)
- Bulkhead: aislar fallos (Release It! Cap 5)
- Retry con exponential backoff + jitter (Microservices Patterns Cap 3)
- Timeout strategy (Release It! Cap 5 + DDIA 2nd ed Cap 9)
- Backpressure: qué hacer cuando el sistema se satura (Release It! Cap 5)
- Graceful degradation (Release It! Cap 5)

Observabilidad (los 3 pilares):
- Structured events como building blocks (Observability Engineering Cap 5)
- Distributed Tracing: stitching events into traces (Observability Engineering Cap 6)
- Instrumentación con OpenTelemetry (Observability Engineering Cap 7)
- Metrics: RED method, USE method (web: Brendan Gregg, Tom Wilkie)
- SLI / SLO / SLA: cómo definir "qué tan bien funciona" (Observability Engineering Cap 12 + Google SRE Cap 4)

Ejercicio:
- [Go] Implementar circuit breaker (sony/gobreaker o manual) + structured logging (slog)
- [TS/NestJS] Implementar circuit breaker como Interceptor + Winston/Pino para structured logs
- [Ambos] Integrar OpenTelemetry para tracing entre servicio Go y NestJS
- Definir SLOs para tus 3 endpoints más críticos

Proyecto E-Commerce:
- [Go] Circuit breaker en Payment Service (sony/gobreaker)
- [NestJS] Circuit breaker como Interceptor en Orders
- [Go] Structured logging con slog: JSON, correlation IDs
- [NestJS] Structured logging con Pino: JSON, correlation IDs
- OpenTelemetry: traces entre API Gateway → Orders → Payments → Inventory
- Definir SLOs: Orders p99 < 300ms, Payments p99 < 500ms, Inventory p99 < 100ms

Entregable:
- Documento: "Resilience & Observability strategy"
- Código: circuit breaker + structured logging + tracing en ambos lenguajes
- Dashboard conceptual con métricas clave

System Design:
- Diseñar un payment platform (1 hora)
- Después: leer System Design Interview Vol. 2 — Cap 11 (Payment System) + Cap 12 (Digital Wallet)
- Estos son los capítulos más relevantes para fintech — cubren idempotency, reconciliation, ledger design

---

## Semana 24 — Architecture Decisions & Hard Parts

Leer:
- Software Architecture: The Hard Parts — Cap 1–2 (What Happens When There Are No Best Practices, Discerning Coupling)
- Software Architecture: The Hard Parts — Cap 3–4 (Architectural Decomposition, breaking apart monoliths)
- Software Architecture: The Hard Parts — Cap 5–6 (Component-based Decomposition, data ownership)
- Fundamentals of Software Architecture — Cap 19 (Architecture Decisions: cómo escribir ADRs)
- Fundamentals of Software Architecture — Cap 20 (Analyzing Architecture Risk)

Artículos (web):
- "Managing Technical Debt" — martinfowler.com/bliki/TechnicalDebt.html
- "Consumer-Driven Contracts" — martinfowler.com (contratos entre servicios)

Conceptos:
- Descomposición: cuándo partir y cuándo no (Hard Parts Cap 3–4)
- Data ownership en architectura distribuida (Hard Parts Cap 5–6)
- Contratos entre servicios: cómo evolucionarlos sin romper (Building Microservices Cap 4)
- Architecture fitness functions: tests automatizados de arquitectura (Building Evolutionary Cap 2)
- Technical debt: cuándo pagar y cuándo aceptar (Fundamentals Cap 20)

ADR como práctica continua:
- Contexto → Opciones → Decisión → Consecuencias
- Todo Staff escribe decisiones, no solo código

Nota Staff: Technical debt es una herramienta de negociación con Product. "Podemos entregar en 2 semanas con esta deuda técnica, pero si no la pagamos en Q3, la velocidad del equipo cae 30%" es lenguaje Staff. Datos > quejas.

Ejercicio:
- Escribir 3 ADRs sobre decisiones reales de tu proyecto
- Review cruzado: ¿alguien más entiende tu decisión sin contexto previo?

Proyecto E-Commerce:
- Escribir 3 ADRs reales del proyecto:
  1. "Por qué NestJS para Orders y Go para Payments"
  2. "Por qué CQRS en Orders pero no en Inventory"
  3. "Por qué saga orchestration y no choreography"

Entregable:
- 3 ADRs formales

---

## Semana 25 — Staff Engineer Skills: Liderazgo Técnico sin Autoridad

Leer:
- The Staff Engineer's Path — Tanya Reilly — Cap 1–3 (Big Picture Thinking, Executing Staff Projects, Leveling Up)
- Learning Systems Thinking — Diana Montalion — Cap 1–4 (opcional, complementa el mindset de systems thinking, conceptual integrity, self-awareness)
- The Staff Engineer's Path — Cap 4–5 (Aligning with Authority, Managing Your Time)
- Staff Engineer — Will Larson — Cap 1–3 (Staff Archetypes, Operating as Staff, Getting the Title)
- Team Topologies — Cap 1–5 (Team types, cognitive load, Conway's Law)

Los 4 arquetipos de Staff (Larson):
- Tech Lead: lidera la ejecución técnica de un equipo
- Architect: define dirección técnica cross-team (sin dejar de codear)
- Solver: entra a resolver los problemas más difíciles donde se necesite
- Right Hand: extiende la capacidad de un VP/Director de Engineering

Pregunta clave: ¿cuál te atrae más? No tienes que elegir ahora, pero saberlo te ayuda a enfocar.

Habilidades Staff:
- Liderar sin autoridad: influencia técnica, no jerarquía (Reilly Cap 3)
- Elegir en qué trabajar: no todo lo urgente es importante — un Staff maximiza impacto (Reilly Cap 5)
- Escribir design docs que convenzan: no solo documenten (Reilly Cap 2)
- Sponsor de proyectos cross-team: navegar la política organizacional (Reilly Cap 4)
- Conway's Law: la arquitectura refleja la estructura del equipo (Team Topologies Cap 1)
- Inverse Conway Maneuver: diseñar equipos para la arquitectura que quieres
- Team types: Stream-aligned, Platform, Enabling, Complicated Subsystem (Team Topologies Cap 3)
- Cognitive load: cuánto puede manejar un equipo (Team Topologies Cap 2)
- Service ownership: quién es dueño de qué

Pregunta clave:
> ¿Puede este equipo operar y evolucionar este sistema de forma autónoma?

Ejercicio:
- Mapear la estructura actual de tu organización
- ¿Se alinea con la arquitectura? ¿Dónde hay fricción?
- Proponer reorganización siguiendo Team Topologies
- Escribir un "Staff project proposal": identifica el problema cross-team más importante de tu organización, propón una solución técnica, y escribe el pitch para conseguir buy-in

Proyecto E-Commerce:
- Mapear los equipos necesarios para operar el e-commerce (Team Topologies):
  - Stream-aligned: Orders team, Payments team
  - Platform: Infrastructure/DevOps
- Escribir design doc / RFC: "Propuesta de evolución del e-commerce"
- Preparar presentación para VP de Engineering + Product

Entregable:
- Documento: "Análisis socio-técnico de [mi organización]"
- Staff project proposal con: problema, impacto, solución, plan, equipos involucrados, riesgos

System Design:
- Diseñar un sistema de streaming de video (1 hora)
- Referencia: System Design Interview Vol. 2 — Cap 9 (S3-like Object Storage) para entender storage de video a escala
- Complementar con: Vol. 2 — Cap 5 (Metrics Monitoring) para el sistema de analytics del streaming
- Para CDN y encoding: Vol. 1 — Cap 1 (Scale from Zero to Millions) cubre CDN conceptual

---

## Semana 26 — Staff Simulation: Integración Total

Leer:
- Building Evolutionary Architectures — Cap 1–4 (opcional, complementa)
- The Staff Engineer's Path — Cap 6–7 (repasar secciones sobre ejecución de proyectos Staff)
- Repasar notas de todas las fases

Ejercicio final — Diseñar un sistema completo desde cero Y venderlo a la organización:

Stack: Go + NestJS (decidir qué va en cada uno como parte del diseño)

Elegir uno:
1. Marketplace (compradores, vendedores, pagos, reviews, búsqueda) — refs: Xu Vol. 2 Cap 7 + Vol. 1 Cap 13
2. Fintech: sistema de pagos entre personas — refs: Xu Vol. 2 Cap 11 + Cap 12 + Cap 13
3. Plataforma de delivery (riders, restaurantes, usuarios, tracking) — refs: Xu Vol. 2 Cap 1 + Cap 2 + Vol. 1 Cap 10

PARTE 1 — Diseño técnico (debe incluir):
- Bounded contexts identificados
- Context map con relaciones
- Diagrama C4 (4 niveles)
- Estilo arquitectónico justificado (monolith modular, microservices, etc.)
- Decisión de stack por servicio: qué va en Go, qué va en NestJS, y por qué
- Comunicación: sync (REST/gRPC) vs async (queues/events) justificado
- Estrategia de datos: qué DB para qué servicio
- CQRS donde aplique (NestJS con @nestjs/cqrs)
- Al menos 1 saga diseñada con compensaciones
- Resilience patterns aplicados (circuit breaker, retry, bulkhead)
- Observabilidad: métricas, logs, tracing con OpenTelemetry
- SLOs definidos
- Scaling strategy
- 3+ ADRs sobre decisiones clave

PARTE 2 — Impacto organizacional (lo que hace esto un ejercicio Staff):
- Análisis de equipo: qué equipos necesitas (Team Topologies)
- Plan de migración incremental: cómo llegar ahí sin parar todo — fases, milestones, rollback plan
- Estrategia de buy-in: cómo convencer a VP Engineering + Product Manager
- Análisis de riesgo: qué puede salir mal y cómo mitigarlo
- Nonfunctional requirements definidos con métricas (DDIA 2nd ed Cap 2)
- Technical debt aceptada explícitamente: qué deuda tomas conscientemente y cuándo la pagas

Proyecto E-Commerce:
- Design Document completo del e-commerce:
  - Bounded contexts + Context Map, Diagrama C4 (4 niveles)
  - Stack por servicio justificado, Comunicación sync vs async
  - Estrategia de datos, CQRS + Saga documentados
  - Resilience patterns, Observabilidad + SLOs, Scaling strategy
  - Team structure, 3+ ADRs
- Presentación de 15 min como si fuera para comité técnico + product
- Plan de migración incremental

Entregable:
- Design Document / RFC completo (puede ser 10-15 páginas)
- Código esquelético: estructura de carpetas de cada servicio (Go y NestJS)
- Presentación de 15 min como si fuera para VP de Engineering + Product (no solo técnicos)
- One-pager ejecutivo: resumen de 1 página para stakeholders no técnicos

---

# Rutina Semanal Recomendada

| Día | Actividad | Tiempo |
|-----|-----------|--------|
| Lunes | Lectura profunda + notas | 90 min |
| Martes | Lectura + releer notas del lunes | 90 min |
| Miércoles | Diagramas + mapas conceptuales | 90 min |
| Jueves | Ejercicio práctico: código o diseño | 90 min |
| Viernes | Completar entregable semanal | 90 min |
| Sábado | System design exercise (a partir de semana 12) | 60 min |
| Domingo | Repaso semanal + actualizar notas | 30 min |

---

# Autoevaluación Mensual

Puntúa del 1 al 5 cada mes:

| Área | Mes 1 | Mes 2 | Mes 3 | Mes 4 | Mes 5 | Mes 6 |
|------|-------|-------|-------|-------|-------|-------|
| OOP & Clean Code | | | | | | |
| Design Patterns | | | | | | |
| SOLID & Refactoring | | | | | | |
| Architecture Styles | | | | | | |
| Domain Modeling (DDD) | | | | | | |
| Microservices & Integration | | | | | | |
| Distributed Systems | | | | | | |
| Resilience & Observability | | | | | | |
| System Design | | | | | | |
| Communication (ADR, RFC, C4) | | | | | | |
| Tradeoff Thinking | | | | | | |
| Organizational Architecture | | | | | | |
| Technical Leadership (influencia sin autoridad) | | | | | | |
| Cross-team Impact | | | | | | |
| Design Docs que convenzan | | | | | | |

---

# Resumen de Entregables por Fase

| Fase | Semanas | Entregables clave |
|------|---------|-------------------|
| 1 - Foundations | 1–4 | Auditoría SOLID, refactors con tests |
| 2 - Patterns | 5–8 | Patrones implementados, anti-patterns documentados |
| 3 - Architecture | 9–12 | Diagrama C4, ADR, RFC, primer system design |
| 4 - DDD | 13–16 | Context map, modelo de dominio, domain events |
| 5 - Databases & DevOps | 17–18 | Estrategia de datos, Dockerfiles, CI/CD pipeline, deployment strategy |
| 6 - Distributed | 19–22 | ADR microservices, saga diseñada, estrategia de datos distribuidos |
| 7 - Staff Mindset | 23–26 | Resilience strategy, ADRs, Staff project proposal, diseño final + pitch |

Total: ~19 entregables concretos + 6 system design exercises + 1 Staff project proposal

---

# Lo que Acelera x3

El error común:
leer arquitectura → entender → sentir que aprendiste

El orden correcto:

diseñar algo (en papel, 30 min)
↓
sentir que no sabes cómo decidir
↓
leer el capítulo
↓
rediseñar con lo aprendido
↓
escribir un ADR explicando tu decisión

Si no puedes explicar tu decisión por escrito, no la entendiste.

Para Staff específicamente: si no puedes explicar tu decisión a un Product Manager en 2 minutos, no la entendiste lo suficiente.

---

# Guía Rápida: Cuándo Go vs NestJS

| Criterio | Go | NestJS (TypeScript) |
|----------|-----|---------------------|
| Alto rendimiento / hot-path | X | |
| Concurrencia pesada (miles de goroutines) | X | |
| CLI tools, infra, devtools | X | |
| gRPC server (alto throughput) | X | |
| API REST / GraphQL con lógica de negocio | | X |
| CQRS + Event-driven (con @nestjs/cqrs) | | X |
| BFF (Backend for Frontend) | | X |
| Prototipado rápido | | X |
| Domain model rico (DDD tactical) | Posible | X (más natural con clases) |
| Workers / consumers de queues | X | Posible |
| Observability sidecar / agent | X | |

Regla general:
- Go cuando necesitas rendimiento, simplicidad y concurrencia
- NestJS cuando necesitas estructura, DDD y velocidad de desarrollo
- Ambos se conectan via gRPC o message queues

---

# Lecturas Adicionales de Referencia

Libros que NO son parte del roadmap pero son útiles para consultar cuando necesites profundizar en un tema específico. No los leas de punta a punta — búscalos cuando tengas un problema concreto.

## Bases de Datos
- **PostgreSQL: Up and Running** — Regina Obe (O'Reilly) — queries, indexes, tuning, extensiones. Consultar si PostgreSQL es tu DB principal.
- **Redis in Action** — Josiah Carlson (O'Reilly) — patterns de caching, queues, pub/sub, rate limiting. Consultar si vas a usar Redis heavy.
- **MongoDB: The Definitive Guide** — Shannon Bradshaw (O'Reilly) — modelado de documentos, aggregation pipeline, sharding. Consultar si te toca MongoDB.
- **Database Internals** — Alex Petrov (O'Reilly) — cómo funcionan las DBs por dentro: storage engines, B-Trees, LSM trees, distributed storage. Para los curiosos — DDIA ya cubre lo esencial.

## Resilience
- **Chaos Engineering** — Casey Rosenthal & Nora Jones (O'Reilly) — teoría y práctica de inyección de fallos en producción. Originado en Netflix. Consultar si quieres ir más allá de los stability patterns de Release It!

## DevOps / Cloud
- **Docker: Up & Running** — Sean Kane (O'Reilly) — referencia completa de Docker si necesitas más que lo básico.
- **Kubernetes: Up and Running** — Brendan Burns et al. (O'Reilly) — si necesitas ir más allá de lo conceptual con K8s.
- **Terraform: Up and Running** — Yevgeniy Brikman (O'Reilly) — Infrastructure as Code con Terraform.

## OOP
- **The Object-Oriented Thought Process (5th ed)** — Matt Weisfeld (O'Reilly) — OOP desde cero: cómo pensar en objetos, inheritance vs composition, SOLID. Bueno para repensar OOP si vienes de un lenguaje donde lo usas por inercia.

## Concurrencia
- **Concurrency in Go** — Katherine Cox-Buday (O'Reilly) — goroutines, channels, patterns de concurrencia, errgroup. Si quieres dominar concurrencia en Go más allá de lo básico.

## API Design
- **API Design Patterns** — JJ Geewax (O'Reilly) — patterns para diseñar APIs robustas: naming, pagination, filtering, long-running operations, versioning. Referencia, no lectura lineal.
- **Designing Web APIs** — Brenda Jin et al. (O'Reilly) — más introductorio, cubre REST, webhooks, GraphQL, developer experience.
- **gRPC: Up and Running** — Kasun Indrasiri (O'Reilly) — gRPC a fondo: protocol buffers, streaming, interceptors, error handling. Cap 1-4 son los esenciales.

## Otros
- **Grokking Algorithms** — Aditya Bhargava (O'Reilly) — si sientes que necesitas refrescar algoritmos de forma visual y amigable.
- **The Pragmatic Programmer** — Hunt & Thomas (O'Reilly) — clásico de mentalidad developer. Si no lo leíste, vale la pena.

---

END.
