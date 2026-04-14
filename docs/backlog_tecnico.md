# Backlog técnico

## Propósito

La prueba exige organizar un backlog técnico en una herramienta como Git Project, Jira o Trello para visualizar tareas, dependencias, prioridades y seguimiento del proceso de estabilización de la base de datos [file:2]. Este documento define el backlog base que servirá como insumo para el tablero y como evidencia de planificación técnica coherente con los entregables del proyecto [file:2].

## Criterios de priorización

Las prioridades se definieron con base en las HU esenciales exigidas por el instrumento y en la necesidad de iniciar el trabajo con la primera HU priorizada durante la prueba supervisada [file:2]. Se priorizan primero el análisis del modelo y la estructura del trabajo, luego la base técnica para contenedores y Liquibase, y finalmente el plan de datos de prueba y el seguimiento documental [file:2].

## Tablero sugerido

Columnas recomendadas para Trello:

- Product Backlog
- Priorizado Sprint 1
- En progreso
- En validación
- Hecho
- Bloqueado

Esta organización permite mostrar seguimiento, prioridades y dependencias, tal como lo solicita la prueba [file:2].

## Historias de usuario esenciales

### HU-001 Identificar y documentar dominios funcionales del modelo existente

**Descripción:** Como responsable técnico del proyecto, necesito identificar y documentar los dominios funcionales del modelo `modelo_postgresql.sql` para comprender su organización lógica y sus dependencias principales antes de iniciar el versionamiento y la estabilización [file:2].

**Prioridad:** Alta [file:2]

**Dependencias:** Ninguna [file:2]

**Criterios de aceptación:**

- Se identifican los dominios funcionales observables en el modelo [file:2].
- Se documentan entidades principales por dominio [file:2].
- Se registran relaciones y dependencias relevantes entre dominios [file:2][file:1].
- Se deja evidencia en `docs/analisis_dominios.md` [file:2].

### HU-002 Organizar la estructura base del repositorio y definir ramas develop, qa y main

**Descripción:** Como responsable de la estabilización, necesito definir la estructura inicial de repositorios y ramas para asegurar orden, trazabilidad y control de cambios durante la evolución técnica del proyecto [file:2].

**Prioridad:** Alta [file:2]

**Dependencias:** HU-001 [file:2]

**Criterios de aceptación:**

- Se propone la estructura inicial del repositorio documental y del repositorio de base de datos [file:2].
- Se documenta el uso de ramas `develop`, `qa` y `main` [file:2].
- Se define una convención básica de ramas de trabajo por HU o feature [file:2].

### HU-003 Contenerizar PostgreSQL para levantar la base de datos en entorno local

**Descripción:** Como equipo técnico, necesitamos contenerizar PostgreSQL para disponer de un entorno reproducible de ejecución local de la base de datos [file:2].

**Prioridad:** Alta [file:2]

**Dependencias:** HU-002 [file:2]

**Criterios de aceptación:**

- Se define `docker-compose.yml` para PostgreSQL [file:2].
- Se documenta el proceso de arranque local [file:2].
- Se garantiza que el entorno pueda servir como base para Liquibase [file:2].

### HU-004 Contenerizar Liquibase e integrarlo al proyecto

**Descripción:** Como responsable técnico, necesito integrar Liquibase mediante contenedor o configuración compatible con el repositorio para administrar de manera controlada el versionamiento del DDL [file:2].

**Prioridad:** Alta [file:2]

**Dependencias:** HU-002, HU-003 [file:2]

**Criterios de aceptación:**

- Se define la estrategia de integración de Liquibase [file:2].
- Se documenta el uso de `changelog-master.xml` y changelogs por dominio [file:2].
- Se mantiene compatibilidad con PostgreSQL [file:2].

### HU-005 Separar el DDL en changelogs organizados por dominio funcional

**Descripción:** Como responsable del versionamiento, necesito dividir el DDL actual en changelogs organizados por dominio para evitar un changelog masivo y mantener trazabilidad técnica del modelo [file:2].

**Prioridad:** Alta [file:2]

**Dependencias:** HU-001, HU-004 [file:2]

**Criterios de aceptación:**

- Existe un `changelog-master.xml` [file:2].
- Cada changelog contiene entidades de un mismo dominio funcional [file:2].
- La separación respeta la organización lógica observada en el script base [file:1][file:2].

### HU-006 Diseñar e implementar estrategia de roles y permisos diferenciados

**Descripción:** Como responsable de seguridad, necesito fortalecer el manejo de roles y permisos diferenciados para mejorar seguridad, trazabilidad y control de acceso en el sistema [file:2].

**Prioridad:** Media-Alta [file:2]

**Dependencias:** HU-001, HU-005 [file:2]

**Criterios de aceptación:**

- Se documenta el diseño de roles y permisos [file:2].
- Se alinea con las tablas `security_role`, `security_permission`, `user_account`, `user_role` y `role_permission` ya existentes en el modelo [file:1].
- Se registra la decisión en ADR [file:2].

### HU-007 Construir plan de datos de prueba con orden de carga por dependencias

**Descripción:** Como responsable de pruebas, necesito definir un plan de datos de prueba con orden de carga lógico para asegurar inserciones válidas y pruebas de integridad relacional [file:2].

**Prioridad:** Media-Alta [file:2]

**Dependencias:** HU-001, HU-005 [file:2]

**Criterios de aceptación:**

- Se define el orden de inserción entre tablas según dependencias [file:2].
- Se documentan scripts de inserción [file:2].
- Se incluyen validaciones asociadas a la dependencia de datos [file:2].

### HU-008 Documentar seguimiento técnico y decisiones arquitectónicas

**Descripción:** Como responsable del proyecto, necesito mantener registro de decisiones, avances y observaciones para garantizar trazabilidad y claridad documental durante la estabilización [file:2].

**Prioridad:** Media [file:2]

**Dependencias:** Transversal a todas [file:2]

**Criterios de aceptación:**

- Se registran los cinco ADR obligatorios [file:2].
- Se actualiza `docs/seguimientos.md` [file:2].
- Se mantiene coherencia con backlog, dominios y propuesta técnica [file:2].

## Tareas técnicas derivadas

| ID | Tarea | HU asociada | Prioridad | Dependencias |
|---|---|---|---|---|
| T-001 | Revisar el script base y separar dominios observables | HU-001 | Alta [file:2] | Ninguna |
| T-002 | Documentar entidades y relaciones por dominio | HU-001 | Alta [file:2] | T-001 |
| T-003 | Crear estructura de repositorios | HU-002 | Alta [file:2] | HU-001 |
| T-004 | Definir estrategia de ramas `develop`, `qa`, `main` | HU-002 | Alta [file:2] | T-003 |
| T-005 | Diseñar `docker-compose` para PostgreSQL | HU-003 | Alta [file:2] | HU-002 |
| T-006 | Diseñar integración de Liquibase | HU-004 | Alta [file:2] | HU-003 |
| T-007 | Crear esquema de changelog master y changelogs por dominio | HU-005 | Alta [file:2] | HU-004 |
| T-008 | Diseñar propuesta de roles y permisos diferenciados | HU-006 | Media-Alta [file:2] | HU-005 |
| T-009 | Definir orden de carga de datos de prueba | HU-007 | Media-Alta [file:2] | HU-001 |
| T-010 | Documentar ADR y seguimiento técnico | HU-008 | Media [file:2] | Transversal |

## Priorización inicial

Orden recomendado de ejecución:

1. HU-001 [file:2]
2. HU-002 [file:2]
3. HU-003 [file:2]
4. HU-004 [file:2]
5. HU-005 [file:2]
6. HU-006 [file:2]
7. HU-007 [file:2]
8. HU-008 [file:2]

Este orden permite responder al requerimiento de iniciar la primera HU priorizada y dejar una ruta real de ejecución técnica dentro de la prueba supervisada [file:2].

## Dependencias globales

El análisis del modelo muestra que las dependencias de datos comienzan por tablas de referencia geográfica y catálogos base, luego continúan con identidad y seguridad, y después habilitan los dominios operativos y transaccionales como clientes, aeropuerto, aeronaves, operaciones de vuelo, ventas, abordaje, pagos y facturación [file:1]. Esta lógica también justifica que las tareas de poblamiento y versionamiento deban respetar el orden funcional del modelo [file:1][file:2].

## Uso en Trello

Cada HU debe registrarse como tarjeta principal y cada tarea técnica derivada puede registrarse como checklist o subtarea dentro de la tarjeta correspondiente [file:2]. Para reforzar trazabilidad, cada tarjeta debería incluir prioridad, dependencias, estado, evidencias y enlace al archivo documental o técnico asociado [file:2].
