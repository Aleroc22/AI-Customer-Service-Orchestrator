# AI Customer Service Orchestrator

**Proyecto integrador — Automatización Avanzada con IA | Coderhouse**

Sistema de orquestación multiagente desarrollado en **n8n**, orientado a automatizar la recepción, clasificación, priorización y seguimiento de solicitudes de atención al cliente en una empresa de tecnología médica.

El proyecto evoluciona incrementalmente a lo largo de los módulos del curso, incorporando agentes especializados, memoria persistente, integraciones empresariales y controles de gobernanza operativa.

## Objetivo

Diseñar un sistema inteligente de Customer Service capaz de:

- Interpretar solicitudes en lenguaje natural.
- Clasificar y priorizar incidentes y requerimientos.
- Coordinar agentes especializados mediante una arquitectura Manager–Worker.
- Mantener el contexto de las conversaciones entre ejecuciones.
- Integrarse con sistemas externos de CRM, correo electrónico y mensajería.
- Aplicar controles preventivos, trazabilidad y supervisión humana.

## Arquitectura y evolución del proyecto

### Módulo 1 — Customer Service Triage Agent

**Estado: Completado**

Implementación del agente central de clasificación y priorización.

- Clasificación de solicitudes: Support, Service, Applications, Commercial y Other.
- Priorización según urgencia e impacto.
- Registro de casos en Google Sheets.
- Guardrails para solicitudes sensibles y situaciones críticas.
- Observabilidad mediante Gmail.
- Separación entre respuestas al cliente y registros técnicos.

### Módulo 2 — Multi-Agent Orchestration

**Estado: Completado**

Evolución hacia una arquitectura de orquestación multiagente.

- Manager central responsable de la clasificación y el enrutamiento.
- Incident Intake Worker para solicitudes de soporte técnico.
- Planned Service Intake Worker para mantenimiento y servicios programados.
- Workers implementados como subworkflows independientes.
- Comunicación mediante Execute Workflow.
- Contratos de datos estructurados y limpieza de payloads.
- Manejo de errores y derivación humana cuando corresponde.

### Módulo 3 — Persistent Memory & Context Engineering

**Estado: Completado**

Incorporación de memoria persistente de largo plazo mediante Airtable.

- Identificación y aislamiento de conversaciones mediante Session_ID.
- Recuperación de contexto histórico antes de ejecutar el Manager.
- Creación y actualización de registros de memoria.
- Consolidación automática de contexto al superar cinco mensajes.
- Summarization mediante Cohere y salida JSON estructurada.
- Delimitadores de seguridad para separar instrucciones del contexto histórico.
- Persistencia de resúmenes y datos accionables, evitando transcripciones completas.

### Módulo 4 — Enterprise Integrations & Operational Governance

**Estado: Implementado — validación final**

Integración del orquestador con herramientas externas reales en un entorno de pruebas.

**Integraciones:**
- **HubSpot:** búsqueda, creación y actualización controlada de contactos.
- **Gmail:** recepción de solicitudes y generación de borradores de respuesta.
- **Slack:** notificaciones operativas con payloads limitados.
- **Airtable:** continuidad de memoria entre conversaciones.
- **Google Sheets:** registro de casos.

**Controles implementados:**
- IF anti-auto-reply inmediatamente después de Gmail Trigger.
- Búsqueda previa en HubSpot para evitar contactos duplicados.
- Gmail Create Draft como mecanismo Human-in-the-loop, sin envío automático al cliente.
- Nodos Set para normalización, validación y limpieza de datos.
- Control de eventos repetidos e idempotencia mediante registros técnicos.
- Manejo conservador de errores y contingencias.

## Tecnologías

| Componente | Tecnología |
|---|---|
| Orquestación | n8n |
| Modelos de IA | Cohere |
| Memoria persistente | Airtable |
| Registro de casos | Google Sheets |
| CRM | HubSpot |
| Correo electrónico | Gmail |
| Notificaciones | Slack |
| Control de versiones | GitHub |

## Principios de diseño

- Arquitectura modular y evolución incremental.
- Separación de responsabilidades entre Manager y Workers.
- Minimización de datos y aislamiento de sesiones.
- Validaciones deterministas antes de operaciones externas.
- Prevención de duplicados y respuestas automáticas.
- Human-in-the-loop para comunicaciones con clientes.
- Observabilidad y manejo conservador de errores.
- Separación entre entornos académicos y productivos.

## Roadmap

Los próximos módulos incorporarán nuevas capacidades del programa, incluyendo recuperación aumentada de información (RAG), herramientas adicionales y mecanismos avanzados de supervisión, según los requisitos de cada checkpoint.

La optimización integral de la arquitectura y su evaluación para un eventual uso corporativo se realizarán al finalizar el proyecto integrador.
