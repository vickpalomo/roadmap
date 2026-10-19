# DevOps Engineer Roadmap

Duración: 24 semanas (~6 meses)
Dedicación: 2 horas diarias (mínimo 1.5h)
Método: Construir → Romper → Automatizar → Monitorear

---

# Principio Fundamental

Un DevOps Engineer NO es un sysadmin que sabe CI/CD.
Un DevOps Engineer:
- Automatiza todo lo que se pueda automatizar
- Trata la infraestructura como código — versionada, revisable, reproducible
- Piensa en reliability desde el día 1, no como afterthought
- Reduce el tiempo entre "escribí código" y "está en producción sirviendo usuarios"
- Construye plataformas que permiten a los developers ir rápido sin romper cosas
- **Su producto son los pipelines, la infra, y la confiabilidad del sistema**

---

# Tu Ventaja: Developer → DevOps

Vienes de development (C#/.NET, aprendiendo Go + TS). Eso te da ventajas enormes:
- Ya sabes programar — muchos DevOps no saben, y eso los limita
- Go es EL lenguaje de DevOps: Docker, Kubernetes, Terraform, Prometheus, Grafana Loki — todo Go
- Entiendes qué necesitan los developers porque eres uno
- Puedes escribir herramientas internas, CLIs, operators de Kubernetes

---

# Evolución DevOps

| Nivel | Pregunta dominante |
|-------|-------------------|
| Junior DevOps | ¿Cómo configuro esto? |
| Mid DevOps | ¿Cómo lo automatizo? |
| Senior DevOps | ¿Cómo lo hago resiliente y escalable? |
| Staff/Platform | ¿Cómo construyo una plataforma que los developers usen sin pensarlo? |
| SRE | ¿Cuál es el error budget? ¿Qué SLO protege a los usuarios? |

---

# Stack Tecnológico

| Área | Herramientas |
|------|-------------|
| Lenguaje principal | Go (CLIs, tools, operators) + Bash (scripts, glue) + Python (automation, scripting) |
| Containers | Docker, containerd |
| Orquestación | Kubernetes |
| IaC | Terraform (o Pulumi si prefieres code) |
| CI/CD | GitHub Actions, GitLab CI, ArgoCD |
| Cloud | AWS (principal) o GCP — elegir uno y profundizar |
| Monitoring | Prometheus + Grafana |
| Logging | Loki o ELK (Elasticsearch + Logstash + Kibana) |
| Tracing | OpenTelemetry + Jaeger |
| Configuration | Ansible (servidores), Helm (Kubernetes) |
| Security | Trivy, Falco, OPA (conceptual) |
| GitOps | ArgoCD o Flux |

---

# Biblioteca

| # | Libro | Fase | Prioridad | Dónde |
|---|-------|------|-----------|-------|
| 1 | The Linux Command Line — William Shotts | 1 | Alta | O'Reilly (gratis en linuxcommand.org) |
| 2 | Linux Bible — Christopher Negus | 1 | Complemento | O'Reilly |
| 3 | Networking Fundamentals — Gordon Davies | 1 | Alta | O'Reilly |
| 4 | Docker: Up & Running (3rd ed) — Sean Kane | 2 | Alta | O'Reilly |
| 5 | Kubernetes: Up and Running (3rd ed) — Brendan Burns et al. | 3 | Alta | O'Reilly |
| 6 | Terraform: Up and Running (3rd ed) — Yevgeniy Brikman | 4 | Alta | O'Reilly |
| 7 | Learning GitHub Actions — Brent Laster | 2 | Alta | O'Reilly |
| 8 | aci (3rd ed) — Andreas Wittig | 4 | Alta | O'Reilly |
| 9 | Prometheus: Up & Running — Julien Pivotto | 5 | Alta | O'Reilly |
| 10 | Observability Engineering — Charity Majors et al. | 5 | Alta | O'Reilly |
| 11 | Site Reliability Engineering — Google (Betsy Beyer et al.) | 6 | Alta | O'Reilly (gratis en sre.google) |
| 12 | The Site Reliability Workbook — Google | 6 | Media | O'Reilly (gratis en sre.google) |
| 13 | Release It! (2nd ed) — Michael Nygard | 5 | Media | O'Reilly |
| 14 | Chaos Engineering — Casey Rosenthal & Nora Jones | 6 | Complemento | O'Reilly |
| 15 | Learning Go (2nd ed) — Jon Bodner | 1–2 | Alta (paralelo) | O'Reilly |
| 16 | The Phoenix Project — Gene Kim et al. | 1 | Alta | O'Reilly |

Recursos web (gratis):
- roadmap.sh/devops — roadmap visual de la comunidad
- kubernetes.io/docs — documentación oficial de K8s
- learn.hashicorp.com — tutoriales oficiales de Terraform
- docs.aws.amazon.com — documentación AWS
- 12factor.net — The Twelve-Factor App
- sre.google — libros SRE de Google gratis

---

# FASE 1 — LINUX, NETWORKING & SCRIPTING (Semanas 1–4)

## Semana 1 — Linux Fundamentals

Leer:
- The Linux Command Line — Cap 1–8 (Navigation, Manipulation, Redirection, Pipes)
- The Phoenix Project — Cap 1–10 (la novela — entender la cultura DevOps)

Aprender:
- Shell basics: navigation, file manipulation, permissions (chmod, chown)
- Pipes y redirection: |, >, >>, 2>&1
- Process management: ps, top, htop, kill, systemctl
- File system: /etc, /var, /usr, /tmp — qué vive dónde
- Package managers: apt (Debian/Ubuntu), yum/dnf (RHEL)
- SSH: conectar, keys, config file, tunneling

Ejercicio:
- Configurar una VM Linux (usar multipass, Vagrant, o una instancia cloud gratuita)
- Navegar, crear usuarios, configurar SSH keys
- Escribir tu primer script que automatice la configuración de un servidor

Entregable:
- Script bash que configure un servidor Linux desde cero (instalar packages, crear user, configurar SSH)

---

## Semana 2 — Bash Scripting & Automation

Leer:
- The Linux Command Line — Cap 24–33 (Shell Scripting)
- Learning Go — Cap 1–4 (en paralelo — setup, basics)

Aprender:
- Variables, condicionales, loops en bash
- Funciones en bash
- Error handling: set -euo pipefail
- Herramientas esenciales: grep, awk, sed, jq, curl, wget
- Cron jobs: automatización por horario
- Makefiles: automatización de tareas de proyecto

Ejercicio:
- Script que haga backup de una base de datos PostgreSQL y lo suba a un bucket S3
- Script que monitoree el uso de disco y envíe alerta si pasa del 80%
- Makefile para tu proyecto Go + NestJS: build, test, lint, docker-build

Entregable:
- 3 scripts bash útiles y reutilizables
- Makefile del proyecto

---

## Semana 3 — Networking Fundamentals

Leer:
- Networking Fundamentals — Gordon Davies — Cap 1–6 (OSI model, TCP/IP, DNS, HTTP)

Aprender:
- Modelo OSI / TCP/IP: no memorizar capas, entender el flujo de un request
- DNS: cómo un nombre se convierte en IP (A records, CNAME, NS, TTL)
- HTTP/HTTPS: métodos, status codes, headers, TLS/SSL
- TCP vs UDP: cuándo cada uno
- Puertos: qué es un puerto, puertos comunes (80, 443, 22, 5432, 6379)
- Firewalls y Security Groups: conceptual
- Load balancers: L4 vs L7, round robin, health checks
- Herramientas: ping, traceroute, dig, nslookup, netstat, ss, curl

Ejercicio:
- Usar dig para resolver DNS de varios dominios — entender la cadena
- Configurar NGINX como reverse proxy para tu app NestJS
- Configurar TLS/SSL con Let's Encrypt (o self-signed para dev)

Entregable:
- NGINX config como reverse proxy + TLS
- Documento: "Cómo un request llega desde el browser a mi servicio" — diagrama completo

---

## Semana 4 — Python for Automation + Go CLI Tools

Leer:
- Learning Go — Cap 5–9 (funciones, tipos, interfaces, errors)

Python (lo básico para automation):
- Requests: hacer HTTP calls
- Boto3: interactuar con AWS desde Python
- YAML/JSON parsing
- Scripting de infraestructura: crear/destruir recursos programáticamente
- No necesitas ser expert en Python — solo lo suficiente para automatizar

Go para DevOps:
- Go ya lo estás aprendiendo — enfocarse en CLIs
- cobra: framework para CLI tools (lo usa kubectl, docker, hugo)
- os/exec: ejecutar comandos del sistema
- net/http: hacer health checks programáticos

Ejercicio:
- [Python] Script que liste todas las instancias EC2 de tu cuenta AWS (boto3)
- [Go] CLI tool simple que haga health check de N endpoints y reporte status
- Comparar: cuándo usar bash vs python vs go para automation

Entregable:
- Python script para AWS
- Go CLI tool con cobra

---

# FASE 2 — CONTAINERS & CI/CD (Semanas 5–8)

## Semana 5 — Docker Deep Dive

Leer:
- Docker: Up & Running — Cap 1–5 (Getting Started, Images, Containers, Docker Compose)

Aprender:
- Images: Dockerfile, layers, caching, multi-stage builds
- Containers: lifecycle, networking, volumes, bind mounts
- Docker Compose: multi-container applications
- Registry: Docker Hub, GitHub Container Registry, ECR
- Best practices:
  - No correr como root
  - Multi-stage builds (builder → runtime)
  - .dockerignore
  - Minimizar layers
  - Usar alpine o distroless como base

Ejercicio:
- Dockerfile optimizado para Go (multi-stage: build con golang:alpine → runtime con scratch/distroless)
- Dockerfile optimizado para NestJS (multi-stage: build → production con node:alpine)
- Docker Compose: Go + NestJS + PostgreSQL + Redis + NGINX como reverse proxy
- Comparar tamaño de imágenes antes y después de optimizar

Entregable:
- Dockerfiles optimizados para Go y NestJS
- docker-compose.yml que levante el stack completo
- Documento: comparación de tamaños de imagen

---

## Semana 6 — Docker Avanzado + Container Security

Leer:
- Docker: Up & Running — Cap 6–10 (Networking, Storage, Security)

Aprender:
- Docker networking: bridge, host, overlay, custom networks
- Docker volumes: named volumes, bind mounts, tmpfs
- Docker security:
  - Escaneo de imágenes con Trivy
  - No correr como root (USER en Dockerfile)
  - Read-only file systems
  - Resource limits (memory, CPU)
- Container registries: push, pull, tagging strategy (semver, git SHA)
- Docker buildx: multi-architecture builds

Ejercicio:
- Configurar Trivy para escanear tus imágenes — corregir vulnerabilidades encontradas
- Docker network: aislar servicios en redes separadas (frontend, backend, data)
- Implementar healthchecks en Docker (HEALTHCHECK instruction)

Entregable:
- Imágenes sin vulnerabilidades críticas (Trivy clean)
- Docker Compose con redes segregadas y healthchecks

---

## Semana 7 — CI/CD Fundamentals

Leer:
- Learning GitHub Actions — Cap 1–6 (Workflows, Jobs, Actions, Environments)

Aprender:
- CI vs CD vs CD (Continuous Integration vs Delivery vs Deployment)
- GitHub Actions:
  - Workflows, jobs, steps
  - Triggers: push, PR, schedule, manual
  - Secrets management
  - Matrix builds (múltiples versiones)
  - Caching (node_modules, Go modules)
  - Artifacts
- Pipeline stages: lint → test → build → scan → push → deploy
- Branch strategy: trunk-based development vs GitFlow

Ejercicio:
- Pipeline para Go: lint (golangci-lint) → test → build → docker build → push to registry
- Pipeline para NestJS: lint (eslint) → test (jest) → build → docker build → push to registry
- Agregar: cache de dependencias, matrix build (múltiples versiones de Node/Go)

Entregable:
- 2 pipelines CI/CD completos (Go + NestJS)
- Tiempo de pipeline < 5 minutos

---

## Semana 8 — CI/CD Avanzado + Deployment Strategies

Leer:
- Learning GitHub Actions — Cap 7–10 (Environments, Deployment, Security)
- Building Microservices — Cap 6 (Deployment)

Aprender:
- Deployment strategies:
  - Rolling update: gradual, sin downtime
  - Blue-Green: 2 ambientes, switch instantáneo
  - Canary: % del tráfico al nuevo version
  - Feature flags: deploy dark, activar por flag
- Environments: dev → staging → production
- Rollback strategy: cómo volver atrás rápido
- GitOps conceptual: el repo es la fuente de verdad del estado deseado

Ejercicio:
- Configurar GitHub Actions con environments: staging → production (con approval)
- Implementar deployment a staging automático en push a main
- Implementar rollback: volver a la versión anterior con un click

Entregable:
- Pipeline con environments + approval gates
- Rollback documentado y probado

---

# FASE 3 — KUBERNETES (Semanas 9–12)

## Semana 9 — Kubernetes Fundamentals

Leer:
- Kubernetes: Up and Running — Cap 1–5 (Intro, Containers, Deploying, Pods, Labels)

Setup:
- Instalar minikube o kind (Kubernetes local)
- kubectl: la herramienta fundamental — aprender los 20 comandos esenciales

Aprender:
- Arquitectura K8s: control plane (API server, scheduler, etcd) + worker nodes (kubelet, kube-proxy)
- Pods: la unidad mínima — por qué no es lo mismo que un container
- Labels y selectors: cómo K8s organiza todo
- Namespaces: aislamiento lógico
- kubectl: get, describe, logs, exec, apply, delete

Ejercicio:
- Desplegar tu servicio Go como Pod en minikube
- Explorar: kubectl get pods, kubectl describe pod, kubectl logs
- Entrar al pod: kubectl exec -it

Entregable:
- Pod manifest (YAML) para tu servicio Go
- Documento: "20 comandos kubectl que uso todos los días"

---

## Semana 10 — Workloads & Networking en K8s

Leer:
- Kubernetes: Up and Running — Cap 6–10 (Services, ReplicaSets, Deployments, DaemonSets)

Aprender:
- Deployments: declarar el estado deseado, K8s se encarga del resto
- ReplicaSets: mantener N réplicas corriendo
- Services:
  - ClusterIP: comunicación interna
  - NodePort: exponer en el nodo
  - LoadBalancer: exponer al mundo
- Ingress: routing HTTP(S) externo → servicios internos
- ConfigMaps: configuración externalizada
- Secrets: datos sensibles (encrypted at rest)

Ejercicio:
- Deployment + Service para Go y NestJS
- Ingress: /api → NestJS, /payments → Go
- ConfigMaps para variables de entorno
- Secrets para credenciales de DB

Entregable:
- Manifests YAML: Deployment, Service, Ingress, ConfigMap, Secret para ambos servicios
- Stack completo corriendo en minikube

---

## Semana 11 — Kubernetes Avanzado

Leer:
- Kubernetes: Up and Running — Cap 11–16 (Storage, ConfigMaps, RBAC, DaemonSets, Jobs)

Aprender:
- PersistentVolumes y PersistentVolumeClaims: storage en K8s
- StatefulSets: para bases de datos (PostgreSQL en K8s)
- Jobs y CronJobs: tareas batch y scheduled
- Horizontal Pod Autoscaler (HPA): escalar por CPU/memoria/custom metrics
- Resource requests y limits: cuánta CPU/memoria garantizas y limitas
- Liveness, Readiness, Startup probes: K8s sabe si tu app está sana
- RBAC: quién puede hacer qué en el cluster

Ejercicio:
- Desplegar PostgreSQL como StatefulSet con PV
- Configurar HPA para tu servicio NestJS: escalar de 2 a 10 pods por CPU
- Configurar probes: liveness (app alive), readiness (app ready to serve traffic)
- Resource limits: definir requests y limits para cada pod

Entregable:
- StatefulSet de PostgreSQL
- HPA configurado y probado (simular carga)
- Probes en todos los servicios

---

## Semana 12 — Helm + GitOps con ArgoCD

Leer:
- Kubernetes: Up and Running — Cap 17–18 (Extending Kubernetes)

Aprender Helm:
- Qué es: package manager para K8s
- Charts: templates + values
- Crear tu propio chart para tu stack
- Helm install, upgrade, rollback
- Values.yaml para diferentes environments

Aprender GitOps / ArgoCD:
- GitOps: el repo Git es la fuente de verdad — K8s se sincroniza automáticamente
- ArgoCD: herramienta de GitOps para K8s
- App of Apps pattern: manejar múltiples aplicaciones
- Sync policies: auto vs manual

Ejercicio:
- Crear Helm chart para tu stack Go + NestJS + PostgreSQL + Redis
- Diferentes values para dev y staging
- Instalar ArgoCD en minikube
- Conectar ArgoCD a tu repo: push = deploy automático

Entregable:
- Helm chart completo
- ArgoCD configurado y sincronizando
- Demo: push to main → ArgoCD detecta → deploy automático

---

# FASE 4 — INFRASTRUCTURE AS CODE & CLOUD (Semanas 13–16)

## Semana 13 — Terraform Fundamentals

Leer:
- Terraform: Up and Running — Cap 1–3 (Why Terraform, Getting Started, State)

Aprender:
- IaC: por qué infraestructura como código > clickear en consola
- HCL: el lenguaje de Terraform
- Providers: AWS, GCP, Azure — plugin model
- Resources: declarar lo que quieres, Terraform calcula el diff
- State: cómo Terraform sabe qué existe (.tfstate)
- Plan → Apply: siempre revisar antes de aplicar
- terraform init, plan, apply, destroy

Ejercicio:
- Crear una VPC en AWS con Terraform: VPC + subnets + security groups
- Crear una instancia EC2 con Terraform
- Entender el state: qué pasa si modificas algo manualmente en AWS

Entregable:
- Terraform code que cree una VPC + EC2 en AWS
- El recurso debe crearse y destruirse limpiamente

---

## Semana 14 — Terraform Avanzado

Leer:
- Terraform: Up and Running — Cap 4–7 (Modules, State Management, Loops, Production-Grade)

Aprender:
- Modules: reutilizar infraestructura como bloques
- Remote state: S3 + DynamoDB para state compartido en equipo
- Workspaces: múltiples environments con el mismo código
- Variables, outputs, locals
- Loops: count, for_each, dynamic blocks
- Data sources: leer infraestructura existente
- Import: traer recursos existentes a Terraform

Ejercicio:
- Crear module reutilizable para un ECS/EKS service
- Remote state en S3 con locking en DynamoDB
- Desplegar el mismo módulo para dev y staging con diferentes variables

Entregable:
- Terraform modules para tu infraestructura
- Remote state configurado
- 2 environments desplegados desde el mismo código

---

## Semana 15 — AWS Deep Dive

Leer:
- Amazon Web Services in Action — Cap 1–6 (Intro, EC2, Networking, Storage, Databases)
- Amazon Web Services in Action — Cap 10–12 (ECS, EKS, Serverless)

Servicios AWS esenciales para DevOps:
- Compute: EC2, ECS (Fargate), EKS, Lambda
- Networking: VPC, Subnets, Security Groups, ALB/NLB, Route 53
- Storage: S3, EBS, EFS
- Databases: RDS (PostgreSQL), ElastiCache (Redis), DynamoDB
- Messaging: SQS, SNS, EventBridge
- Containers: ECR (registry), ECS (orquestación), EKS (Kubernetes managed)
- IAM: users, roles, policies — el sistema de permisos de AWS
- Secrets: Secrets Manager, Parameter Store

Cuándo usar qué:
- ECS Fargate: containers sin administrar servers — el más simple
- EKS: Kubernetes managed — si ya sabes K8s o lo necesitas
- Lambda: funciones event-driven — para tareas cortas y esporádicas

Ejercicio:
- Desplegar tu stack con Terraform en AWS:
  - VPC + subnets
  - ECS Fargate (Go service) o EKS
  - RDS PostgreSQL
  - ElastiCache Redis
  - ALB como load balancer
  - ECR para tus imágenes
- Configurar IAM roles con least privilege

Entregable:
- Infraestructura completa en AWS creada con Terraform
- Diagrama de arquitectura AWS
- Servicios accesibles y funcionando

---

## Semana 16 — Security & Networking en Cloud

Leer:
- Amazon Web Services in Action — Cap 7–9 (Security, Networking, HA)

Aprender:
- Security:
  - IAM: least privilege principle — cada servicio solo accede a lo que necesita
  - Security Groups: firewall a nivel de instancia
  - NACLs: firewall a nivel de subnet
  - Encryption: at rest (KMS) y in transit (TLS)
  - Secrets management: AWS Secrets Manager o Parameter Store
  - Container security: image scanning con ECR, no correr como root
- Networking avanzado:
  - VPC Peering: conectar VPCs
  - Private subnets: servicios que no necesitan internet público
  - NAT Gateway: acceso a internet desde subnets privadas
  - VPN / Direct Connect: conectar con on-premise
- High Availability:
  - Multi-AZ: distribuir en múltiples zonas de disponibilidad
  - Auto Scaling Groups: escalar EC2 automáticamente
  - Cross-region: para disaster recovery

Ejercicio:
- Configurar red con public subnets (ALB) + private subnets (servicios + DB)
- Rotar secrets automáticamente con Secrets Manager
- Escanear imágenes Docker en ECR — corregir vulnerabilidades

Entregable:
- Infraestructura con separación public/private
- Secrets management configurado
- Documento: "Security checklist para mi infraestructura"

---

# FASE 5 — MONITORING & OBSERVABILITY (Semanas 17–20)

## Semana 17 — Prometheus + Grafana

Leer:
- Prometheus: Up & Running — Cap 1–6 (Intro, Getting Started, Instrumentation, Querying, Rules)

Aprender:
- Prometheus: pull-based metrics collection
- Metric types: counter, gauge, histogram, summary
- PromQL: el lenguaje de queries de Prometheus
- Grafana: dashboards y visualización
- Exporters: node_exporter (sistema), blackbox_exporter (endpoints)
- Instrumentar tu código:
  - [Go] prometheus/client_golang — métricas custom
  - [NestJS] prom-client — métricas custom
- Alerting: Alertmanager, routing, silences

Ejercicio:
- Desplegar Prometheus + Grafana en K8s (helm charts oficiales)
- Instrumentar tus servicios Go y NestJS con métricas custom
- Crear dashboards en Grafana: RED metrics (Rate, Errors, Duration) por servicio
- Configurar alertas: latencia p99 > 500ms, error rate > 5%

Entregable:
- Prometheus + Grafana corriendo en K8s
- Servicios instrumentados con métricas custom
- Dashboard con RED metrics
- Al menos 3 alertas configuradas

---

## Semana 18 — Logging: Structured Logs & Aggregation

Leer:
- Observability Engineering — Cap 1–2 (Observability vs Monitoring)
- Observability Engineering — Cap 5 (Structured Events)

Aprender:
- Structured logging: JSON > texto plano
- Log levels: debug, info, warn, error — cuándo usar cada uno
- Correlation IDs: rastrear un request a través de servicios
- Log aggregation: centralizar logs de todos los servicios
- Stack de logging:
  - Loki + Grafana (lightweight, label-based) — recomendado para empezar
  - ELK: Elasticsearch + Logstash + Kibana (más poderoso, más complejo)
- Qué loggear: request/response metadata, errores, decisiones de negocio
- Qué NO loggear: passwords, tokens, PII, datos sensibles

Implementar:
- [Go] slog (standard library Go 1.21+) → structured JSON logs
- [NestJS] Pino → structured JSON logs
- Correlation ID via middleware/interceptor en ambos

Ejercicio:
- Implementar structured logging en Go (slog) y NestJS (Pino)
- Desplegar Loki + Grafana en K8s
- Agregar correlation IDs que se propaguen entre servicios
- Crear dashboard en Grafana: logs por servicio, filtrar por correlation ID

Entregable:
- Structured logging en ambos servicios
- Loki agregando logs de todo el stack
- Dashboard de logs en Grafana
- Un request rastreable end-to-end por correlation ID

---

## Semana 19 — Distributed Tracing con OpenTelemetry

Leer:
- Observability Engineering — Cap 6–7 (Tracing, OpenTelemetry)
- opentelemetry.io/docs — guía oficial

Aprender:
- Distributed tracing: ver el camino completo de un request
- OpenTelemetry: el estándar para instrumentación (traces, metrics, logs)
- Conceptos: Span, Trace, Context Propagation, Baggage
- Collector: recibir, procesar y exportar telemetría
- Backends: Jaeger (tracing), Tempo (Grafana ecosystem)
- Auto-instrumentation vs manual instrumentation

Ejercicio:
- Instrumentar Go y NestJS con OpenTelemetry SDK
- Desplegar OpenTelemetry Collector + Jaeger (o Tempo) en K8s
- Propagar contexto entre servicios (Go ↔ NestJS via gRPC/HTTP headers)
- Ver traces completos: request llega a NestJS → llama a Go via gRPC → responde

Entregable:
- OpenTelemetry instrumentado en ambos servicios
- Traces visibles end-to-end en Jaeger/Tempo
- Dashboard en Grafana que correlacione metrics + logs + traces

---

## Semana 20 — SLIs, SLOs & Alerting Strategy

Leer:
- Observability Engineering — Cap 12–13 (SLOs, Debugging SLO-based alerts)
- Site Reliability Engineering (Google) — Cap 4 (Service Level Objectives)
- Site Reliability Engineering — Cap 6 (Monitoring Distributed Systems)

Aprender:
- SLI: Service Level Indicator — la métrica (ej: latencia p99)
- SLO: Service Level Objective — el target (ej: p99 < 200ms, 99.9% del tiempo)
- SLA: Service Level Agreement — el contrato con el cliente
- Error budget: cuánto puedes fallar antes de violar el SLO
- Alerting strategy:
  - Alert on SLOs, not on symptoms
  - Burn rate alerts: alerta cuando el error budget se consume rápido
  - Reducir alert fatigue: menos alertas, más accionables
- Dashboards para oncall: qué necesita ver alguien a las 3 AM

Ejercicio:
- Definir SLIs y SLOs para tus servicios:
  - Availability: % de requests exitosos
  - Latency: p50, p95, p99
  - Throughput: requests por segundo
- Configurar alertas basadas en SLOs en Prometheus/Grafana
- Crear runbook: "Qué hacer cuando la alerta X se dispara"

Entregable:
- Documento: SLIs/SLOs definidos para cada servicio
- Alertas SLO-based configuradas
- Runbook para las 3 alertas más importantes
- Dashboard de oncall en Grafana

---

# FASE 6 — SRE PRACTICES & SENIOR DEVOPS (Semanas 21–24)

## Semana 21 — Site Reliability Engineering

Leer:
- Site Reliability Engineering (Google) — Cap 1–3 (Intro, SRE Principles, Risk)
- Site Reliability Engineering — Cap 5 (Eliminating Toil)
- The Site Reliability Workbook — Cap 1–4

Aprender:
- SRE como disciplina: software engineering aplicado a operations
- Toil: trabajo manual, repetitivo, automatizable — eliminarlo es el objetivo
- Error budgets en la práctica: cuándo pausar features para mejorar reliability
- Incident management: cómo responder a incidentes
- Postmortems: blameless, aprender de los fallos
- Capacity planning: cuántos recursos necesitas y cuándo escalar

Ejercicio:
- Identificar toil en tu workflow actual — automatizar al menos 2 tareas
- Escribir un postmortem template
- Simular un incidente: matar un pod, ver cómo el sistema responde, documentar

Entregable:
- 2 tareas de toil automatizadas
- Postmortem template
- Incident simulation documentada

---

## Semana 22 — Chaos Engineering & Resilience

Leer:
- Chaos Engineering — Casey Rosenthal — Cap 1–4 (Principles of Chaos, Experiments)
- Release It! — Cap 4–5 (Stability Antipatterns, Stability Patterns)

Aprender:
- Chaos Engineering: inyectar fallos intencionalmente para encontrar debilidades
- Principios: hipótesis, experimentos controlados, blast radius mínimo
- Herramientas:
  - Chaos Mesh (para Kubernetes)
  - Litmus Chaos
  - Gremlin (SaaS)
- Stability patterns: circuit breaker, bulkhead, retry, timeout, backpressure
- Game days: ejercicios de equipo para practicar respuesta a incidentes

Ejercicio:
- Instalar Chaos Mesh en tu cluster K8s
- Experimentos:
  - Matar un pod random — ¿se recupera?
  - Agregar latencia a la red entre servicios — ¿el circuit breaker se activa?
  - Llenar el disco de un pod — ¿qué pasa?
- Documentar resultados y mejoras necesarias

Entregable:
- 3 experimentos de chaos engineering ejecutados
- Documento: "Hallazgos y mejoras de resiliencia"
- Mejoras implementadas (circuit breaker, probes, resource limits)

---

## Semana 23 — Configuration Management + Advanced IaC

Leer:
- Terraform: Up and Running — Cap 8–9 (Production-Grade Terraform, Testing)

Aprender:
- Ansible básico: configuration management para servidores
  - Playbooks, roles, inventories
  - Cuándo Ansible vs cuándo Terraform (infra vs config)
- Terraform avanzado:
  - Testing: terratest, terraform validate, tflint
  - CI/CD for infrastructure: plan en PR, apply en merge
  - Drift detection: detectar cambios manuales
  - State management avanzado: import, move, refactor
- Pulumi como alternativa: IaC con Go/TypeScript en vez de HCL

Ejercicio:
- Ansible playbook que configure un servidor: instalar Docker, configurar monitoring agent
- Terraform CI/CD: pipeline que hace plan en PR y apply en merge a main
- Terraform tests con terratest (en Go)

Entregable:
- Ansible playbook funcional
- Pipeline CI/CD para Terraform
- Al menos 2 tests de infraestructura

---

## Semana 24 — DevOps Simulation: Integración Total

Leer:
- Repasar notas de todas las fases
- The Phoenix Project — terminar si no lo acabaste (la novela)

Ejercicio final — Construir una plataforma completa:

Desplegar tu stack Go + NestJS en AWS con todo lo aprendido:

Infraestructura (Terraform):
- VPC con public + private subnets
- EKS cluster (o ECS Fargate)
- RDS PostgreSQL
- ElastiCache Redis
- ALB como load balancer
- ECR para imágenes
- S3 para backups/assets
- IAM con least privilege
- Secrets Manager

Kubernetes:
- Deployments, Services, Ingress para cada servicio
- HPA configurado
- Probes en todos los pods
- Helm charts
- ArgoCD sincronizando desde Git

CI/CD:
- Pipeline completo: lint → test → build → scan → push → deploy a staging
- Approval gate para production
- Rollback automático si health check falla

Observability:
- Prometheus + Grafana (metrics)
- Loki (logs)
- OpenTelemetry + Jaeger/Tempo (traces)
- SLOs definidos con alertas
- Dashboard de oncall
- Runbooks para alertas principales

Security:
- Imágenes escaneadas con Trivy
- Network policies en K8s
- Secrets en Secrets Manager (no en código)
- TLS everywhere

Resiliencia:
- Al menos 1 experimento de chaos engineering documentado
- Circuit breakers en comunicación entre servicios

Entregable:
- Infraestructura completa funcionando en AWS
- Todo como código: Terraform + Helm + GitHub Actions + ArgoCD
- Observability stack completo con dashboards
- Documento: "Runbook de operaciones para [mi plataforma]"
- Diagrama de arquitectura completo

---

# Rutina Semanal Recomendada

| Día | Actividad | Tiempo |
|-----|-----------|--------|
| Lunes | Lectura + notas | 90 min |
| Martes | Lectura + labs/práctica | 90 min |
| Miércoles | Hands-on: construir/configurar | 90 min |
| Jueves | Hands-on: construir/configurar | 90 min |
| Viernes | Completar entregable semanal | 90 min |
| Sábado | Romper cosas: troubleshooting, chaos, debugging | 60 min |
| Domingo | Repaso semanal | 30 min |

Nota: DevOps se aprende HACIENDO. La proporción debería ser 30% lectura, 70% hands-on.

---

# Autoevaluación Mensual

Puntúa del 1 al 5 cada mes:

| Área | Mes 1 | Mes 2 | Mes 3 | Mes 4 | Mes 5 | Mes 6 |
|------|-------|-------|-------|-------|-------|-------|
| Linux & CLI | | | | | | |
| Bash & Scripting | | | | | | |
| Networking | | | | | | |
| Docker | | | | | | |
| CI/CD | | | | | | |
| Kubernetes | | | | | | |
| Terraform / IaC | | | | | | |
| AWS Cloud | | | | | | |
| Prometheus & Grafana | | | | | | |
| Logging & Tracing | | | | | | |
| SRE Practices (SLOs, incidents) | | | | | | |
| Security | | | | | | |

---

# Resumen de Entregables por Fase

| Fase | Semanas | Entregables clave |
|------|---------|-------------------|
| 1 - Linux & Scripting | 1–4 | Scripts bash, NGINX config, Go CLI tool, Python automation |
| 2 - Containers & CI/CD | 5–8 | Dockerfiles optimizados, pipelines CI/CD, deployment strategies |
| 3 - Kubernetes | 9–12 | K8s manifests, Helm charts, ArgoCD GitOps |
| 4 - IaC & Cloud | 13–16 | Terraform modules, infra AWS completa, security hardened |
| 5 - Observability | 17–20 | Prometheus/Grafana, structured logging, tracing, SLOs |
| 6 - SRE & Senior DevOps | 21–24 | Chaos experiments, Ansible, plataforma completa |

Total: ~18 entregables concretos + plataforma completa al final

---

# Tu Ventaja Competitiva

Con tu background de developer + este roadmap DevOps, tu perfil es:

| DevOps "clásico" | Tú (Developer + DevOps) |
|---|---|
| Configura pipelines | Configura pipelines + escribe herramientas custom en Go |
| Usa Terraform | Usa Terraform + escribe providers/modules avanzados |
| Monitorea servicios | Monitorea + entiende el código que está fallando |
| Opera Kubernetes | Opera K8s + puede escribir operators en Go |
| Automatiza con bash | Automatiza con bash + Go + Python |

Este perfil se llama **Platform Engineer** o **SRE** y es el más demandado y mejor pagado del espectro DevOps.

---

# Cómo Conecta con tus Otros Roadmaps

| Roadmap | Para qué | Duración |
|---------|----------|----------|
| Senior Engineer | Ser un developer excelente | 20 semanas |
| Staff/Principal | Liderar técnicamente sin ser manager | 26 semanas |
| DevOps (este) | Construir la plataforma donde corre el código | 24 semanas |

No los hagas todos en paralelo. Recomendación:
1. Senior Engineer primero (foundations sólidos)
2. Después elegir: Staff/Principal O DevOps según lo que te atraiga más
3. O combinar: Senior → DevOps basics → Staff con mentalidad de plataforma

---

# Lecturas Adicionales de Referencia

## Kubernetes Avanzado
- **Kubernetes Patterns** — Bilgin Ibryam (O'Reilly) — patterns de diseño para K8s
- **Programming Kubernetes** — Michael Hausenblas (O'Reilly) — escribir operators y controllers en Go
- **Cloud Native DevOps with Kubernetes** — John Arundel (O'Reilly)

## Cloud
- **Google Cloud Platform in Action** — JJ Geewax (O'Reilly) — si prefieres GCP sobre AWS
- **Azure for Architects** — Ritesh Modi (O'Reilly) — si te toca Azure

## Security
- **Container Security** — Liz Rice (O'Reilly) — security profundo para containers
- **Hacking Kubernetes** — Andrew Martin (O'Reilly) — K8s security ofensivo/defensivo

## SRE
- **Implementing Service Level Objectives** — Alex Hidalgo (O'Reilly) — SLOs en profundidad

---

END.
