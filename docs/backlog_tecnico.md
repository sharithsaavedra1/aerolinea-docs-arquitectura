# Backlog Técnico - Proyecto Airline DB

## 1. Propósito
[cite_start]Este documento organiza el backlog técnico para la estabilización de la base de datos, visualizando tareas, dependencias y prioridades[cite: 45]. [cite_start]La gestión se realiza mediante **Trello**, asegurando el seguimiento del proceso de ejecución técnica exigido por el instrumento[cite: 47, 51, 127].

## 2. Evidencia de Gestión (Tablero Trello)
Se implementó un tablero dinámico para reflejar el estado real del proyecto. Las columnas utilizadas son:
* [cite_start]**Product Backlog:** Historias de Usuario base[cite: 49].
* [cite_start]**To Do:** Tareas priorizadas para ejecución inmediata[cite: 45].
* [cite_start]**In Progress:** Tareas en desarrollo activo (Contenerización y Datos)[cite: 54, 57].
* [cite_start]**Done:** Requerimientos finalizados y verificados técnicamente[cite: 122].

![ya con las hu ](docs/img/terminando.png)


![desarrollando las hu  ](docs/img/en proceso.png)


![iniciando trello  ](docs/img/inicio .png)

## 3. Historias de Usuario (HU) Esenciales

### HU-001: Análisis de Dominios Funcionales
* [cite_start]**Descripción:** Identificar la organización lógica del modelo `modelo_postgresql.sql`[cite: 19, 49].
* [cite_start]**Prioridad:** Alta[cite: 127].
* [cite_start]**Criterios de Aceptación:** Documento `analisis_dominios.md` finalizado con entidades y relaciones clave[cite: 20, 84].

### HU-002: Estructura de Repositorio y Ramas
* [cite_start]**Descripción:** Definir carpetas y estrategia de ramas `develop`, `qa` y `main`[cite: 38, 50].
* [cite_start]**Prioridad:** Alta[cite: 116, 127].
* [cite_start]**Criterios de Aceptación:** Repositorio estructurado según guía del SENA[cite: 80, 101].

### HU-003: Contenerización de PostgreSQL
* [cite_start]**Descripción:** Levantar la base de datos en un entorno local reproducible usando Docker[cite: 51, 59].
* [cite_start]**Prioridad:** Alta[cite: 120, 127].
* [cite_start]**Criterios de Aceptación:** Archivo `docker-compose.yml` funcional en puerto local[cite: 97, 127].

### HU-004: Integración de Liquibase
* [cite_start]**Descripción:** Contenerizar Liquibase para administrar el versionamiento del DDL[cite: 51, 60].
* [cite_start]**Prioridad:** Alta[cite: 127].
* [cite_start]**Criterios de Aceptación:** Conexión exitosa entre Liquibase y PostgreSQL vía Docker[cite: 61].

### HU-005: Separación de DDL por Dominios
* [cite_start]**Descripción:** Organizar el código SQL en changelogs por dominio funcional[cite: 52, 64].
* [cite_start]**Prioridad:** Alta[cite: 107, 121].
* [cite_start]**Criterios de Aceptación:** Máximo un changelog por dominio (ej. `001-geography.xml`)[cite: 121, 127].

### HU-006: Estrategia de Roles y Permisos
* [cite_start]**Descripción:** Diseñar el manejo de seguridad y trazabilidad de accesos[cite: 25, 53].
* [cite_start]**Prioridad:** Media-Alta[cite: 113, 127].
* [cite_start]**Criterios de Aceptación:** Registro de decisión en ADR-002[cite: 91, 127].

### HU-007: Plan de Poblamiento de Datos
* [cite_start]**Descripción:** Definir orden lógico de carga según dependencias (Continent -> Country)[cite: 54, 69].
* [cite_start]**Prioridad:** Media-Alta[cite: 122, 127].
* [cite_start]**Criterios de Aceptación:** Scripts de inserción documentados en la carpeta `data/`[cite: 73, 127].

### HU-008: Seguimiento Técnico y ADR
* [cite_start]**Descripción:** Documentar las decisiones arquitectónicas del proyecto[cite: 55].
* [cite_start]**Prioridad:** Media[cite: 122, 127].
* [cite_start]**Criterios de Aceptación:** Cinco ADR completos entregados en la carpeta `adr/`[cite: 23, 90].

## 4. Tareas Técnicas y Dependencias
| ID | Tarea | Dependencia | Estado |
|---|---|---|---|
| T-01 | Crear `docker-compose.yml` | HU-002 | Hecho |
| T-02 | Configurar `changelog-master.xml` | HU-004 | Hecho |
| T-03 | Definir orden de carga SQL | HU-007 | En Progreso |

![Detalle de HU con Checklists](docs/img/trello_detalle.png)
*Figura 2: Detalle de criterios de aceptación y prioridades en Trello.*
