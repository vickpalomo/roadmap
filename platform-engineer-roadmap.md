# Platform Engineer Roadmap

Duración: 16 semanas (~4 meses)
Dedicación: 2 horas diarias (mínimo 1.5h)
Ratio: 4:1 código:lectura — 60 min de lectura los lunes, el resto se construye
Método: Encontrar consumidor → construir → medir adopción → iterar

---

# Por qué este roadmap es distinto a los otros 7

Los roadmaps anteriores de este repo fallaron por la misma razón: lectura primero, código después, y el proyecto era de juguete. Este invierte las tres cosas.

| Roadmap previo | Este |
|---|---|
| 22–26 semanas | 16 semanas |
| 13–26 libros | 8 libros, capítulos sueltos, ninguno completo |
| Proyecto e-commerce inventado | Plataformas que ya operas en producción |
| Entregable = documento | Entregable = artefacto que otro humano usa |
| Lunes + martes de lectura | Solo lunes, 60 min tope |

**Regla de hierro**: una semana no avanza si no hay un artefacto mergeado que otra persona puede usar. Si la semana no tiene consumidor identificado, se salta. Sin excepciones, sin "la retomo después".

---

# Principio Fundamental

Un Platform Engineer **no** es un DevOps Engineer con más herramientas.

| Rol | Qué entrega | A quién | Métrica de éxito |
|-----|-------------|---------|------------------|
| DevOps Engineer | Pipelines, infra, deploys | Al equipo, operando él mismo | Uptime, MTTR |
| **Platform Engineer** | **Un producto interno** | **A otros ingenieros, en self-service** | **Adopción y developer experience** |
| SRE | Confiabilidad medida | Al usuario final | Error budget |

La diferencia operativa: si los developers te piden permiso, te abren un ticket, o te preguntan cómo, **no tienes una plataforma — tienes un servicio de consultoría**. Una plataforma es aquello que se usa sin hablar contigo.

Corolarios que gobiernan todo el roadmap:

- **Guardrails, no gates.** Un gate bloquea y te vuelve cuello de botella. Un guardrail deja avanzar por el camino correcto y hace difícil el incorrecto.
- **Golden path, no golden cage.** El camino pavimentado es opt-in y es tan bueno que salirse duele. No se impone.
- **Thinnest viable platform** (Team Topologies). La plataforma más delgada que resuelve el dolor real. Todo lo demás es scope creep disfrazado de roadmap técnico.
- **Si no está instrumentado, no existe.** Adopción, tiempo al primer éxito y tasa de fallo son la única evidencia de que la plataforma funciona.

---

# Tu ventaja injusta

No arrancas de cero. Ya operas tres piezas de plataforma real, con consumidores reales:

| Lo que ya tienes | Por qué es platform engineering |
|---|---|
| `agents-registry` + MCP server | Catálogo versionado, instaladores multi-plataforma, detección de stack, análisis de impacto en consumidores. Es un IDP para tooling de developers. |
| Shared workflows de `tpc-development/github-actions` | Producto con consumidores, canal de bug reports, contratos versionados. |
| `create-repo-via-datadog` + `audit-repo-setup` | Scaffolding + drift detection contra un baseline. Ese es un golden path a medio construir. |
| Datadog service catalog | Registro de servicios ya poblado. Medio Backstage sin el portal. |
| Ingesta automática de learnings (Opus en Bedrock, OIDC) | Loop de feedback automatizado sobre la plataforma misma. |

Esto significa dos cosas. Una: **la parte más difícil de platform engineering — conseguir consumidores reales — ya está resuelta**. Dos: no hay excusa de "no tengo dónde practicar".

Además: Go es el lenguaje de la industria de plataforma (Kubernetes, Terraform, Crossplane, Prometheus, Backstage CLI — todo Go), y Go ya está en tu ruta de aprendizaje. Este roadmap lo convierte en el vehículo, no en un tema aparte.

---

# Prerequisitos honestos

Este roadmap arranca **después** de `devops-engineer-roadmap.md` fases 1–4. Necesitas poder hacer esto sin buscar en Google:

- [ ] Escribir un Dockerfile multi-stage y explicar por qué cada capa está donde está
- [ ] `kubectl` sin cheatsheet: describe, logs, exec, port-forward, get -o yaml
- [ ] Explicar qué hace un Deployment, Service, Ingress, ConfigMap, Secret y ServiceAccount
- [ ] Escribir un módulo de Terraform con variables y outputs, y explicar el state
- [ ] Un workflow de GitHub Actions con jobs, matrices, secrets y OIDC
- [ ] Leer un YAML de K8s roto y decir qué está mal
- [ ] Go: structs, interfaces, errores, goroutines básicas, `go mod`

**Si fallas 3 o más**: para. Haz las semanas correspondientes de `devops-engineer-roadmap.md` primero (Docker sem 5–6, K8s sem 9–12, Terraform sem 13–14, Go sem 4). Arrancar este roadmap sin base es garantizar el estancamiento número 8.

**Si fallas 1 o 2**: arranca, y cubre el hueco en la semana 0.

---

# Stack

| Área | Herramienta | Por qué esta |
|------|-------------|--------------|
| Lenguaje | **Go** | Todo el ecosistema de plataforma es Go. client-go, controller-runtime, cobra. |
| Control plane | Kubernetes API + CRDs | La plataforma se expone como API declarativa, no como scripts |
| Framework de operators | kubebuilder / controller-runtime | Estándar de facto |
| Infra declarativa | Crossplane | Terraform expuesto como API de K8s, self-service |
| IaC base | Terraform | Lo que ya usa la org por debajo |
| Policy | Kyverno (o OPA/Gatekeeper) | Guardrails en admission. Kyverno es YAML, menos fricción de adopción |
| Portal | Backstage | Catálogo + software templates + TechDocs |
| Supply chain | cosign / sigstore, Syft, SLSA | Firma, SBOM, provenance |
| Secrets | External Secrets Operator + OIDC federation | Cero llaves de larga vida |
| GitOps | ArgoCD | Reconciliación declarativa de la plataforma misma |
| Observabilidad | Datadog (lo de tu org) + OpenTelemetry | No peleas con el stack existente |
| CI | GitHub Actions | Ya eres dueño de los shared workflows |
| App de prueba | .NET (tu stack real) | Los golden paths se validan con el lenguaje que la org realmente usa |

Nota de versiones: el ecosistema de plataforma se mueve rápido (kubebuilder, Crossplane, Backstage cambian de API entre majors). Verifica la doc oficial vigente al llegar a cada semana en vez de confiar en la versión que asumo aquí.

---

# Biblioteca

Ocho libros. Ninguno se lee completo. Son referencia dirigida — abres el capítulo que resuelve el problema de la semana.

| # | Libro | Semanas | Alcance real |
|---|-------|---------|--------------|
| 1 | **Team Topologies** — Skelton & Pais | 1, 15 | Solo caps 3 y 5 (platform team, thinnest viable platform). ~40 páginas. |
| 2 | **Accelerate** — Forsgren, Humble & Kim | 2 | Caps 2–4 (las 4 métricas DORA y por qué predicen desempeño). |
| 3 | **Programming Kubernetes** — Hausenblas & Schimanski | 5–7 | Caps 1–3 (API machinery, client-go) + 4–6 (controllers, CRDs). **El libro clave.** |
| 4 | **Kubernetes Patterns** — Ibryam & Huß | 6–9 | Patrones de Configuration, Controller y Operator. Referencia, no lineal. |
| 5 | **Platform Engineering on Kubernetes** — Mauricio Salatino | 8–14 | El único libro que trata la plataforma como producto end-to-end. |
| 6 | **Site Reliability Engineering** (Google, gratis en sre.google) | 15 | Caps 3–4 (error budgets, SLOs). |
| 7 | **Learning Go** — Bodner | 4–7 | Consulta puntual. Ya lo tienes en otros roadmaps. |
| 8 | **Building Secure and Reliable Systems** (Google, gratis) | 10–12 | Caps de least privilege y supply chain. Consulta. |

Recursos web (gratis, y más actuales que cualquier libro aquí):

- `internaldeveloperplatform.org` — referencia canónica de qué es un IDP y sus componentes
- `book.kubebuilder.io` — el tutorial de operators, mejor que cualquier libro
- `docs.crossplane.io` — compositions y XRDs
- `backstage.io/docs` — catálogo y software templates
- `kyverno.io/policies` — biblioteca de policies listas para copiar
- `slsa.dev` — niveles de supply chain security
- `platformengineering.org` — comunidad, casos reales, anti-patrones
- Artículos de Manuel Pais y Syntasso sobre "platform as a product"

---

# SEMANA 0 — Baseline (no cuenta como semana del roadmap)

Antes de construir nada, mide lo que ya tienes. Sin baseline no puedes demostrar impacto, y demostrar impacto es la mitad del trabajo de un Platform Engineer.

Hacer:
- Inventario de consumidores de `agents-registry`: cuántas máquinas, cuántos repos, qué items instalados
- Inventario de consumidores de los shared workflows: `gh search code --owner tpc-development "uses: tpc-development/github-actions"`
- Para el flujo de crear un repo nuevo: cronometra el camino completo hoy, de "quiero un servicio nuevo" a "está en prod con CI verde y observabilidad". Minutos y número de pasos manuales.
- Cerrar los 1–2 huecos de prerequisitos si aplicó

Entregable:
- `docs/platform-baseline.md` — números crudos de hoy. Sin interpretación, sin plan. Solo el punto de partida.

Esto se compara contra los mismos números en la semana 16. Es tu evidencia.

---

# FASE 1 — PLATAFORMA COMO PRODUCTO (Semanas 1–3)

El error universal es arrancar por la tecnología. Tres semanas de producto primero — sin esto, construyes cosas correctas que nadie usa.

## Semana 1 — Consumidores, dolor y la plataforma más delgada

Leer (60 min lunes):
- Team Topologies, cap 5 (Platform como servicio, thinnest viable platform)
- `internaldeveloperplatform.org` — la página de componentes core

Aprender:
- Platform team vs stream-aligned team vs enabling team
- Cognitive load como criterio de diseño: la plataforma existe para bajarlo, no para moverlo de lugar
- Thinnest Viable Platform: puede ser un wiki bien escrito antes de ser software
- Anti-patrón: la plataforma que agrega una capa de abstracción sin quitar una de complejidad

Construir:
- Entrevista a 3 compañeros reales que consuman `agents-registry` o los shared workflows. Tres preguntas, nada más: ¿qué te tomó más tiempo la última vez que arrancaste algo nuevo? ¿qué paso te hizo pedir ayuda? ¿qué evitas usar porque es más fácil hacerlo a mano?
- Del resultado, elige **un** dolor. Uno.

Entregable:
- One-pager de producto: quiénes son los usuarios, el dolor elegido, qué NO va a hacer la plataforma, cómo se mide el éxito. Máximo una página.
- Notas de las 3 entrevistas, verbatim.

Criterio de fallo: si el one-pager describe tecnología en vez de dolor de usuario, reescríbelo.

---

## Semana 2 — Instrumentar developer experience

Leer (60 min lunes):
- Accelerate, caps 2–3 (las 4 métricas y qué predicen)

Aprender:
- Las 4 métricas DORA: deployment frequency, lead time for changes, change failure rate, time to restore
- Métricas específicas de plataforma: **time to first success** (de cero a "funcionó"), tasa de adopción, tasa de abandono
- Por qué "líneas de YAML ahorradas" no es una métrica y "horas de onboarding" sí

Construir:
- Instrumentar el MCP server de `agents-registry`: emitir un evento por install/list/suggest con item, resultado y duración. Enviar a Datadog.
- Dashboard con: instalaciones por item, tasa de fallo de install, items sugeridos vs instalados (esa brecha es señal de fricción real)
- Para shared workflows: extraer duración y tasa de fallo por repo consumidor vía `gh api`

Entregable:
- Dashboard en vivo con datos reales de consumidores
- `docs/platform-metrics.md` — qué mides, por qué, y qué decisión tomarías con cada número

Nota Platform: la instrumentación es lo primero que se construye y lo último que se recuerda. Un Platform Engineer que no puede responder "¿cuánta gente usa esto?" con un número está adivinando.

---

## Semana 3 — Golden path #1: de cero a producción

Construir el camino pavimentado para el dolor de la semana 1. Casi seguro es "arrancar un servicio nuevo".

Leer (60 min lunes):
- Platform Engineering on Kubernetes, cap 1–2 (el problema y la forma del golden path)

Aprender:
- Golden path = opinionado, completo y opt-in. No es un template vacío.
- Scaffolding vs generación: el scaffold debe salir con CI verde, no con TODOs
- Day-2 ownership: quién mantiene lo que el template generó, y cómo se le hacen updates después

Construir:
- Un solo comando (o un workflow dispatch) que produzca un servicio .NET con: repo creado, CI que corre tests de verdad (no solo build), Dockerfile multi-stage, health endpoint, logging estructurado, entrada en el service catalog de Datadog, y las reglas del registry ya instaladas
- Componer lo que ya existe: `create-repo-via-datadog` + `audit-repo-setup` + la instalación de items del registry. No reescribir.
- Cerrar el loop: `audit-repo-setup` corriendo contra el repo generado debe salir sin gaps. Si el propio golden path no pasa tu baseline, el baseline o el path están mal.

Entregable:
- Golden path funcionando end-to-end
- **Un compañero lo usa sin tu ayuda, delante de ti, y tú no hablas.** Cronometra. Anota cada vez que dudó.
- Comparación contra el número de la semana 0: minutos antes vs después, pasos manuales antes vs después

Criterio de fallo: si tuviste que intervenir, no es self-service. Arréglalo y repite con otra persona.

---

# FASE 2 — GO COMO LENGUAJE DE PLATAFORMA (Semanas 4–6)

Aquí se cruza la línea de "configuro herramientas" a "construyo herramientas". Es la fase que separa Platform Engineer de DevOps Engineer, y es la más código-intensiva del roadmap.

## Semana 4 — CLIs de plataforma en Go

Leer (60 min lunes):
- Learning Go: consulta puntual sobre `flag`/cobra, `os/exec`, embed
- Doc de cobra

Aprender:
- Un binario estático es el mejor mecanismo de distribución interna: sin runtime, sin `npm install`, sin versión de Python
- Diseño de CLI: verbos, salida legible para humanos **y** `--output json` para scripts, exit codes que signifiquen algo
- Cross-compilation: `GOOS`/`GOARCH`, un binario por plataforma desde un solo pipeline
- Aplica la regla `cross-platform-paths`: `path.Join`, nunca concatenar separadores. Tus consumidores están en Windows y macOS.

Construir:
- Portar a Go una pieza real del registry. Candidato natural: los scripts de validación (`check-version-sync`, `check-catalog-sync`) unificados en un `registryctl validate`.
- `--output json` para que la CI lo consuma, salida con colores para humanos
- Release en GitHub Actions con binarios para darwin/arm64, darwin/amd64, linux/amd64, windows/amd64
- Tests de tabla para la lógica de validación

Entregable:
- Binario distribuido, instalable en un comando
- La CI del registry usando el binario en vez de los scripts de Node
- Nota: "Qué gané y qué perdí al mover esto de Node a Go"

---

## Semana 5 — La API de Kubernetes como interfaz, no como kubectl

Leer (60 min lunes):
- Programming Kubernetes, caps 1–3 (API machinery, client-go, informers)

Aprender:
- Todo en K8s es un objeto REST con un resource, un group y una version. `kubectl` es solo un cliente.
- client-go: clientset, dynamic client, discovery
- **Informers y watch**: por qué nunca haces polling contra la API. Cache local, event handlers, resync.
- Modelo declarativo: spec es deseo, status es realidad, el controller cierra la brecha
- Level-triggered vs edge-triggered — el concepto más importante de la fase. Reconcilias hacia el estado deseado, no reaccionas a eventos.

Construir:
- Un programa Go que use client-go contra un cluster local (kind o k3d) y liste pods con un label selector
- Convertirlo a informer: reaccionar a creaciones, actualizaciones y borrados
- Algo con valor real: un reporter que recorra namespaces y reporte cargas sin resource limits, sin liveness probe, o sin owner en labels. Salida JSON.
- Correrlo contra un cluster real de la org (read-only) y ver qué encuentra

Entregable:
- Reporter funcionando, con hallazgos reales
- Nota: "Qué me sorprendió del modelo de la API de K8s viniendo de REST tradicional"

---

## Semana 6 — Tu primer controller: CRD + reconcile loop

Leer (60 min lunes):
- Programming Kubernetes, caps 4–6 (custom resources, controllers)
- El tutorial de `book.kubebuilder.io` (se sigue construyendo, no leyendo)

Aprender:
- CRD: extender la API de K8s con tus propios tipos. Tu plataforma se vuelve una API declarativa.
- El reconcile loop: idempotente, sin estado propio, tolerante a ser invocado con el mismo input mil veces
- Requeue, backoff y por qué el reconciler **nunca** asume que corre una sola vez
- Owner references y garbage collection

Construir:
- Con kubebuilder, un operator con un CRD simple pero útil. Sugerencia por ser trivialmente demostrable: `PreviewEnvironment` — spec con repo y branch, y el controller crea namespace + quota + RBAC.
- Reconcile idempotente: aplicarlo 20 veces seguidas no debe cambiar nada después de la primera
- Test con envtest (el harness de controller-runtime)

Entregable:
- Operator corriendo en kind, CRD aplicable con `kubectl apply`
- Test que prueba idempotencia
- Nota: "El reconcile loop vs un script imperativo — qué problema resuelve realmente"

Milestone de fase: ya escribes software de plataforma, no configuración.

---

# FASE 3 — CONTROL PLANE (Semanas 7–9)

## Semana 7 — Operators de verdad: status, conditions, finalizers

Leer (60 min lunes):
- Kubernetes Patterns: patrones Controller y Operator
- Convenciones de API de K8s sobre conditions (doc oficial)

Aprender:
- **Status y conditions**: cómo el operator comunica qué está pasando. Sin buen status, tu CRD es una caja negra y tus usuarios te preguntan a ti.
- Finalizers: cleanup ordenado antes del borrado, y cómo un finalizer con bug bloquea el delete para siempre
- Manejo de errores: qué es transitorio (requeue con backoff) y qué es permanente (reflejar en status y parar)
- Observabilidad del operator: métricas de reconcile, duración, errores
- Aplica tu regla `fix-one-branch-miss-other`: la rama de éxito y la de error del reconciler necesitan el mismo cuidado. Resetear estado "siempre" en vez de "solo en éxito" es exactamente el bug de esa regla.

Construir:
- Endurecer el operator de la semana 6: conditions (`Ready`, `Progressing`, `Degraded`), status con información útil, finalizer que limpia de verdad
- Métricas Prometheus del reconciler
- Provocar fallos: borrar recursos hijos a mano, meter specs inválidos, matar el operator a medio reconcile. Debe converger solo en los tres casos.
- Documentar el CRD para el consumidor: ejemplos, no referencia de campos

Entregable:
- Operator resiliente con evidencia de los 3 fallos provocados y su recuperación
- Doc de usuario del CRD

---

## Semana 8 — Infra declarativa: Crossplane vs Terraform

Leer (60 min lunes):
- Platform Engineering on Kubernetes, capítulos de Crossplane
- `docs.crossplane.io` — compositions y XRDs

Aprender:
- Control plane vs pipeline: Terraform corre cuando alguien lo dispara; un control plane reconcilia continuamente y corrige drift
- Compositions y XRDs: exponer una abstracción de alto nivel (`PostgresInstance`) que por debajo provisiona lo que sea
- Cuándo Crossplane **no** vale la pena: si el equipo ya opera Terraform bien y el dolor no es self-service, Crossplane agrega un control plane que hay que operar
- Tu regla `supabase-migrations-via-cli` es este mismo tema: cambios fuera del flujo declarativo generan drift silencioso que rompe cosas semanas después

Construir:
- Crossplane en kind, con un provider (nop provider si no puedes tocar cloud; AWS si tienes sandbox)
- Una Composition que exponga una abstracción propia de tu org: `ServiceDatabase` con parámetros de size y environment, que por debajo arme lo real
- Un developer la consume con 6 líneas de YAML sin saber nada de lo de abajo
- Demostrar corrección de drift: cambia el recurso subyacente a mano y observa la reconciliación

Entregable:
- Composition funcionando + evidencia de corrección de drift
- **ADR: "Crossplane vs módulos de Terraform para self-service de infra"** — con la recomendación real para tu org, incluyendo la opción de no adoptarlo

---

## Semana 9 — Multi-tenancy y self-service con límites

Leer (60 min lunes):
- Kubernetes Patterns: patrones de Configuration
- Doc de K8s sobre ResourceQuota, LimitRange y RBAC

Aprender:
- Namespace-as-a-service: la unidad de tenancy más simple que funciona
- ResourceQuota y LimitRange: sin esto, un tenant tumba a todos
- RBAC a escala: roles por equipo, no por persona; ClusterRole + RoleBinding
- Aislamiento más fuerte: NetworkPolicy, y cuándo escalar a vcluster o clusters separados
- Atribución de costo: sin showback, la plataforma es un buffet gratis y el consumo crece sin techo

Construir:
- Extender el operator: `Tenant` o `Workspace` como CRD que provisiona namespace + quota + limitrange + RBAC + NetworkPolicy default-deny + labels de costo
- Un developer pide su entorno con un YAML de 5 líneas y en 30 segundos tiene un espacio aislado y acotado
- Probar el aislamiento: desde el tenant A, intentar leer secrets del tenant B y alcanzarlo por red. Ambas deben fallar.

Entregable:
- Self-service de tenancy funcionando
- Evidencia de aislamiento (los dos intentos fallidos, documentados)
- Reporte de atribución de costo por tenant

---

# FASE 4 — GUARDRAILS, NO GATES (Semanas 10–12)

## Semana 10 — Policy as code

Leer (60 min lunes):
- `kyverno.io` — introducción y biblioteca de policies
- Building Secure and Reliable Systems: capítulo de least privilege

Aprender:
- Admission control: validating, mutating y por qué mutating es más amable que validating (arregla en vez de rechazar)
- Policy as code vs revisión humana: la policy escala, la revisión no
- **Rollout de policies**: `Audit` primero, `Enforce` después. Nunca al revés.
- Tu regla `security-gate-rollout` aplica literal aquí: una policy en Enforce es un boolean flip, sin estado intermedio. Si la metes sin fase de audit, rompes a todos los consumidores a la vez.

Construir:
- Kyverno en el cluster, con policies que resuelvan misconfigs reales encontradas por el reporter de la semana 5
- Al menos una de cada tipo: validate (rechazar imagen con tag `latest`), mutate (inyectar labels de ownership y costo automáticamente), generate (crear NetworkPolicy default al crear namespace)
- Correrlas en modo `Audit` contra un cluster real y publicar el reporte de qué se rompería
- Solo después, `Enforce` en un namespace acotado

Entregable:
- Policies desplegadas, con evidencia del reporte de audit **antes** de enforce
- Doc para consumidores: qué se bloquea, por qué, y cómo cumplir. Con ejemplos de arreglo, no solo la regla.

Nota Platform: una policy sin fase de audit y sin doc de remediación no es un guardrail, es un gate — y te vuelve el cuello de botella que la plataforma existía para eliminar.

---

## Semana 11 — Supply chain: firma, SBOM y provenance

Leer (60 min lunes):
- `slsa.dev` — niveles y modelo de amenazas
- Doc de sigstore/cosign

Aprender:
- La cadena: source → build → artifact → deploy, y qué se puede comprometer en cada eslabón
- SBOM: qué hay realmente dentro de tu imagen
- Firma con cosign y **keyless** con OIDC — sin llaves de larga vida que rotar
- Provenance de SLSA: prueba criptográfica de dónde y cómo se construyó un artefacto
- Cerrar el loop: verificación en admission. Una imagen sin firma no arranca.

Construir:
- En los shared workflows que ya posees: generar SBOM (Syft), firmar la imagen (cosign keyless con el OIDC de GitHub Actions), adjuntar provenance
- Kyverno verificando firmas en admission: imagen sin firma válida = rechazada
- Demostrar el ataque: intentar desplegar una imagen no firmada y que sea bloqueada
- Aplicar tu regla `no-secrets-in-argv` al implementarlo — nada de tokens en argv de subprocesos

Entregable:
- Pipeline firmando, cluster verificando, evidencia del bloqueo
- Diagrama de la cadena de confianza end-to-end
- **Impacto en consumidores**: qué repos se rompen cuando esto sea obligatorio, y el plan de migración por fases

---

## Semana 12 — Identidad y secretos como servicio de plataforma

Leer (60 min lunes):
- Doc de External Secrets Operator
- Building Secure and Reliable Systems: capítulo de identidad de workloads

Aprender:
- Por qué las llaves de larga vida son el problema, no la solución
- Workload identity y OIDC federation: el pod prueba quién es, y recibe credenciales efímeras
- External Secrets Operator: los secretos viven en un secret manager, K8s los sincroniza, nadie los commitea
- Ya haces esto: la ingesta de learnings usa OIDC de GitHub Actions hacia AWS sin llaves. Generalízalo.

Construir:
- External Secrets Operator sincronizando desde AWS Secrets Manager (o el equivalente de tu org)
- Un `ServiceIdentity` como CRD: el developer declara qué secretos necesita, el operator provisiona ServiceAccount + IRSA/workload identity + ExternalSecret
- Auditoría: buscar llaves de larga vida en los repos que puedas ver, y documentar el plan de migración
- Aplica `doc-sensitivity-audit` al escribir ese reporte: **no reproduzcas los valores que estás recomendando rotar**

Entregable:
- Self-service de secretos funcionando, con cero llaves de larga vida en el camino nuevo
- Reporte de auditoría (redactado) + plan de migración

---

# FASE 5 — PORTAL Y SELF-SERVICE (Semanas 13–14)

## Semana 13 — Catálogo y portal

Leer (60 min lunes):
- `backstage.io/docs` — catálogo y software templates
- Platform Engineering on Kubernetes: capítulos de developer portal

Aprender:
- El catálogo como fuente de verdad: qué servicios existen, quién es dueño, en qué estado están
- Software templates: el golden path de la semana 3 ahora vive en un formulario, no en un README
- TechDocs: docs junto al código, publicados centralmente
- Decisión real: Backstage es un producto que hay que operar. Si tu org ya tiene el service catalog de Datadog poblado, quizá el portal sea overkill y baste el scaffolder. Decídelo con datos, no con hype.

Construir:
- Backstage local, con el catálogo poblado desde los repos reales (descubrimiento por `catalog-info.yaml`)
- El golden path de la semana 3 como software template: formulario → repo creado, CI verde, catalogado
- Ficha de servicio útil: dueño, dependencias, links a dashboards de Datadog, on-call

Entregable:
- Portal con catálogo real y el template funcionando
- **ADR: "Backstage vs extender el catálogo de Datadog"** — con recomendación honesta, incluyendo "no adoptar"

---

## Semana 14 — Entornos efímeros

Leer (60 min lunes):
- Platform Engineering on Kubernetes: capítulos de developer experience y entornos

Aprender:
- Preview environment por PR: el ciclo de feedback más corto que existe
- Ciclo de vida: crear al abrir el PR, actualizar en cada push, **destruir al cerrar** (el paso que todos olvidan y que quema presupuesto)
- Paridad con producción: qué se puede simular y qué no. Sé explícito sobre las diferencias.
- Costo: un preview env que no se destruye es una fuga silenciosa
- Tu regla `supabase-migrations-via-cli` documenta exactamente el fallo de este flujo: drift de migraciones bloquea la creación de preview branches **en silencio**. Diseña la detección de drift desde el día 1.

Construir:
- Cerrar el operator `PreviewEnvironment` de la semana 6: integrarlo con ArgoCD, aplicar el tenancy de la semana 9, las policies de la semana 10
- Workflow de GitHub Actions: PR abierto → env creado → URL comentada en el PR; PR cerrado → destruido
- TTL forzado: los envs mueren a las N horas aunque el PR quede abierto
- Reporte de costo por preview env
- Detección de drift de migraciones **antes** de intentar crear el env, con mensaje de error que diga qué hacer

Entregable:
- Preview envs en producción, usados en un PR real de otro equipo
- Evidencia de destrucción automática (sin envs huérfanos después de una semana)
- Números de costo por env

Milestone de fase: la plataforma tiene portal, catálogo, golden path, guardrails y entornos self-service. Es un IDP.

---

# FASE 6 — OPERAR LA PLATAFORMA (Semanas 15–16)

## Semana 15 — Platform SRE: SLOs de aquello de lo que todos dependen

Leer (60 min lunes):
- Google SRE, caps 3–4 (error budgets, SLOs)
- Team Topologies, cap 3 (tipos de equipo, interacciones)

Aprender:
- Una plataforma es un single point of failure organizacional. Cuando se cae, N equipos se detienen.
- SLOs de la plataforma misma: disponibilidad del control plane, latencia de provisioning, tasa de éxito de builds, tiempo del golden path
- Blast radius: qué falla cuando el operator se cae, cuando Crossplane se cae, cuando el portal se cae. Deben degradar distinto.
- **Graceful degradation obligatoria**: si el portal muere, los deploys deben seguir. Si el operator muere, los workloads existentes deben seguir corriendo.
- Versionado y deprecación de la plataforma: tus CRDs y templates son contratos públicos. Ya tienes esta disciplina en `manifest.json` con `status: deprecated` — es la misma cosa.

Construir:
- SLOs definidos y medidos en Datadog para: éxito del golden path, latencia de provisioning, disponibilidad del control plane
- Prueba de blast radius: mata cada componente por separado y documenta qué se rompe y qué sobrevive
- Runbook: qué hacer cuando cada pieza falla
- Política de deprecación de APIs de la plataforma (CRDs, templates, workflows): ventana de aviso, período de soporte dual, mecanismo de migración

Entregable:
- SLOs en vivo con datos reales
- Matriz de blast radius (componente → qué se rompe → qué sobrevive → qué hacer)
- Política de deprecación escrita

---

## Semana 16 — Capstone: migrar un equipo real y medir

No es un ejercicio de diseño. Es adopción real, con datos.

Leer (60 min lunes):
- Repasar `docs/platform-baseline.md` de la semana 0

Construir:
- Elegir un equipo o servicio real de la org. Migrarlo al golden path completo: catalogado, con guardrails, con preview envs, con secretos self-service.
- Acompañar la migración sin hacerla por ellos. Cada vez que tengan que preguntarte algo, es un bug de la plataforma — anótalo y arréglalo.
- Medir los mismos números de la semana 0.

Entregables:

1. **Platform RFC** (~6 páginas, no 15): qué se construyó, para quién, qué dolor resuelve, arquitectura, los ADRs, qué deuda se tomó a propósito, plan de los siguientes 6 meses
2. **Datos de adopción**: baseline de semana 0 vs semana 16, en la misma tabla. Minutos, pasos manuales, tasa de fallo, número de consumidores.
3. **Retro de la migración**: cada momento en que el equipo tuvo que preguntarte algo, y el fix. Esta lista es el backlog real de la plataforma.
4. **Diagrama C4 nivel Container** de la plataforma
5. **Presentación de 15 min** para un público mixto (ingeniería + management). Sin YAML en las slides. La primera slide es un número de negocio, no una arquitectura.
6. **One-pager ejecutivo**: el impacto en una página, para quien no va a leer el RFC

Criterio de éxito real: **otro equipo desplegó a producción usando tu plataforma sin escribirte un solo mensaje**. Si no pasó, el roadmap no terminó — sigue arreglando la lista del retro.

---

# Rutina Semanal

| Día | Actividad | Tiempo |
|-----|-----------|--------|
| Lunes | Lectura dirigida + notas | 60 min |
| Martes | Construir | 120 min |
| Miércoles | Construir | 120 min |
| Jueves | Construir + romper a propósito | 120 min |
| Viernes | Entregable + demo a un humano real | 90 min |
| Sábado | Cerrar huecos o descansar | 60 min |
| Domingo | Libre | — |

Ratio: 60 min de lectura contra 450+ de construcción. Eso es 7:1, no 4:1. Es a propósito — platform engineering se aprende operando, y tu historial dice que el desbalance previo era el problema.

**El viernes es no negociable.** Demo a una persona real, aunque sea de 5 minutos por Slack. Un entregable que nadie vio no cuenta como entregable.

---

# Reglas de rescate (aprendidas de los 7 roadmaps anteriores)

1. **Sin artefacto mergeado, no avanza la semana.** No hay semanas "parcialmente completas" que se retoman después.
2. **Sin consumidor identificado, se salta la semana.** Es mejor un roadmap de 12 semanas completado que uno de 16 abandonado.
3. **Lectura con tope duro de 60 min.** Si el capítulo no cabe, lees menos capítulo, no más tiempo.
4. **Ningún libro se termina.** Terminar libros no es una meta. Resolver el problema de la semana sí.
5. **Un roadmap activo a la vez.** Este pausa a codex y a v2. Explícitamente.
6. **Revisión cada 4 semanas**: ¿en qué semana estoy vs en qué semana debería estar? Si el atraso es mayor a 2 semanas, se recorta scope — no se extiende el calendario. Recortar es la decisión correcta, no la derrota.
7. **Si en la semana 4 sigues en la semana 1**, el problema no es el roadmap. Para y cambia el formato antes de escribir el noveno archivo en este directorio.

---

# Autoevaluación (cada 4 semanas)

Puntúa 1–5. La columna que importa es la última.

| Área | Mes 1 | Mes 2 | Mes 3 | Mes 4 |
|------|-------|-------|-------|-------|
| Platform-as-product mindset | | | | |
| Medición de developer experience | | | | |
| Go para tooling de plataforma | | | | |
| API de Kubernetes y client-go | | | | |
| Controllers y operators | | | | |
| Infra declarativa (Crossplane) | | | | |
| Multi-tenancy y aislamiento | | | | |
| Policy as code | | | | |
| Supply chain security | | | | |
| Identidad y secretos | | | | |
| Portal y catálogo | | | | |
| Entornos efímeros | | | | |
| SLOs de plataforma | | | | |
| **Adopción real conseguida** | | | | |

---

# Preguntas que debes poder responder al final

- ¿Cuántas personas usan tu plataforma? Dame el número y de dónde sale.
- ¿Cuánto tarda hoy un servicio nuevo de cero a producción? ¿Cuánto tardaba antes?
- ¿Cuál es la diferencia entre un guardrail y un gate? Dame un ejemplo de cada uno de los tuyos.
- ¿Por qué el reconcile loop es idempotente y qué se rompe si no lo es?
- Se cae tu operator. ¿Qué deja de funcionar y qué sigue funcionando?
- ¿Por qué Crossplane en lugar de módulos de Terraform? ¿O por qué no?
- ¿Cómo desplegarías una policy nueva sin romper a 40 repos consumidores el lunes?
- Una imagen sin firmar llega al cluster. ¿Qué la detiene y en qué punto exacto?
- ¿Cuántas llaves de larga vida quedan en tu camino de deploy? ¿Por qué siguen ahí?
- ¿Cuál es el SLO de tu plataforma y cuál es su error budget?
- Deprecas un CRD del que dependen 3 equipos. ¿Cuál es el proceso?
- ¿Qué construiste que nadie usó? ¿Por qué?
- ¿Qué pieza de tu plataforma deberías borrar?

La última es la más importante. Un Platform Engineer que solo agrega está construyendo la próxima carga de mantenimiento de alguien más.

---

# Cómo conecta con tus otros roadmaps

| Roadmap | Relación |
|---|---|
| `devops-engineer-roadmap.md` | **Prerequisito.** Fases 1–4 (Linux, Docker, K8s, Terraform) son la base. Este arranca donde ese llega a la línea 39: *"¿Cómo construyo una plataforma que los developers usen sin pensarlo?"* |
| `codex_roadmap_sr.md` | **Complementario, en pausa.** El código de plataforma también necesita diseño limpio, tests e inversión de dependencias. Retómalo después, o toma solo su fase 4 (bases de datos) que es el hueco más grande de este roadmap. |
| `software-architect-roadmap-v2.md` | **Pausado.** Su material de Staff (Team Topologies, Reilly, Larson) tiene más sentido *después* de haber construido y operado una plataforma real. Con la experiencia, esos libros se leen en la mitad del tiempo. |
| `senior-engineer-roadmap.md`, `ruta-completa-senior-to-staff.md` | Superpuestos con los anteriores. No los abras durante estas 16 semanas. |

Lo que este roadmap **no** cubre y tendrás que buscar aparte: bases de datos a profundidad (está en codex fase 4), diseño de sistemas distribuidos, y el track de liderazgo/organización de v2 fase 7.

---

# Criterio de Éxito

Terminas este roadmap cuando:

- Otro equipo desplegó a producción por tu golden path sin preguntarte nada
- Puedes decir cuánta gente usa tu plataforma, con un número que sale de instrumentación real
- Escribiste y operas un controller de Kubernetes en Go que corre en un cluster real
- Tus guardrails bloquean misconfiguraciones reales, y los consumidores saben cómo cumplir sin escribirte
- Ninguna llave de larga vida queda en el camino nuevo de deploy
- Tu plataforma tiene SLO, error budget y runbook
- Puedes explicar en 15 minutos, sin YAML, por qué esto valió la pena — y tienes los números

Eso es Platform Engineer.

---

END.
