# Seguimientos

## Propósito

La prueba exige documentar seguimiento, decisiones y dependencias, y además solicita un registro claro del seguimiento técnico realizado dentro del plan de poblamiento y de la ruta de estabilización del proyecto [file:2]. Este documento funciona como bitácora de avance para evidenciar trazabilidad durante la fase supervisada y servir como base del trabajo desescolarizado [file:2].

## Registro inicial

### Seguimiento 001 - Revisión del insumo base

**Fecha:** 2026-04-14  
**Actividad:** Revisión del archivo `modelo_postgresql.sql` entregado como insumo base [file:2].  
**Resultado:** Se confirma que el propósito no es rehacer el modelo sino analizar una base de datos funcional ya construida, organizada por dominios, con claves UUID, restricciones, checks, comentarios e índices [file:1][file:2].  
**Observaciones:** El modelo presenta separación clara por dominios, lo que habilita una estrategia posterior de Liquibase por changelogs funcionales [file:1][file:2].

### Seguimiento 002 - Identificación de dominios

**Fecha:** 2026-04-14  
**Actividad:** Identificación y documentación de dominios funcionales [file:2].  
**Resultado:** Se reconocen dominios de geografía y referencia, aerolínea, identidad, seguridad, clientes y fidelización, aeropuerto, aeronaves, operaciones de vuelo, ventas y reservas, abordaje, pagos y facturación [file:2].  
**Observaciones:** La estructura observada en el SQL confirma la separación por bloques funcionales y facilita la división futura del DDL [file:1].

### Seguimiento 003 - Definición del enfoque documental

**Fecha:** 2026-04-14  
**Actividad:** Organización del repositorio documental [file:2].  
**Resultado:** Se define un repositorio dedicado a documentación con `README.md`, carpeta `docs/` y carpeta `adr/`, alineado con la estructura sugerida por el instrumento [file:2].  
**Observaciones:** Se mantiene separación entre documentación y repositorio técnico de base de datos para facilitar trazabilidad [file:2].

### Seguimiento 004 - Redacción de ADR

**Fecha:** 2026-04-14  
**Actividad:** Elaboración de los cinco ADR obligatorios [file:2].  
**Resultado:** Se documentan decisiones sobre ampliación funcional, roles y permisos, versionamiento con Liquibase, ramas `develop/qa/main` y contenedorización técnica [file:2].  
**Observaciones:** Cada ADR conserva la estructura mínima exigida: título, contexto, problema, decisión, justificación técnica y consecuencias [file:2].

### Seguimiento 005 - Definición del backlog técnico

**Fecha:** 2026-04-14  
**Actividad:** Organización del backlog técnico e historias de usuario [file:2].  
**Resultado:** Se estructuran las HU-001 a HU-008 como guía mínima del proceso de estabilización [file:2].  
**Observaciones:** Se propone implementación del backlog en Trello con visualización de prioridades, dependencias y seguimiento [file:2].

### Seguimiento 006 - Ruta técnica para contenedores y Liquibase

**Fecha:** 2026-04-14  
**Actividad:** Definición de lineamientos para PostgreSQL y Liquibase [file:2].  
**Resultado:** Se establece que PostgreSQL debe poder levantarse mediante contenedor y que Liquibase debe integrarse mediante contenedor o configuración compatible con el entorno del repositorio [file:2].  
**Observaciones:** La estrategia propuesta organiza el DDL con un máximo por changelog correspondiente a entidades de un mismo dominio funcional [file:2].

### Seguimiento 007 - Plan de datos de prueba

**Fecha:** 2026-04-14  
**Actividad:** Diseño del plan de poblamiento [file:2].  
**Resultado:** Se define un orden de carga basado en dependencias entre dominios y tablas del modelo [file:1][file:2].  
**Observaciones:** Se plantea iniciar por geografía y catálogos base, continuar por identidad y seguridad, y luego seguir con dominios operativos y financieros [file:1].

## Riesgos identificados durante el seguimiento

- Rehacer el modelo sin justificación técnica, en contra de la orientación del instrumento [file:2].
- Perder coherencia entre ADR, backlog y estrategia técnica [file:2].
- No respetar dependencias entre tablas durante la carga de datos [file:1][file:2].
- Agrupar todo el versionamiento en un único changelog masivo, lo cual contradice el criterio de Liquibase por dominio [file:2].

## Acciones de control

- Mantener el modelo base como referencia técnica principal [file:1][file:2].
- Relacionar cada documento con una necesidad explícita del instrumento [file:2].
- Organizar el backlog por HU esenciales [file:2].
- Mantener la documentación actualizada al cerrar cada bloque de trabajo [file:2].

## Próximos pasos

- Crear el repositorio técnico de base de datos con Docker y Liquibase [file:2].
- Configurar ramas `develop`, `qa` y `main` [file:2].
- Definir `changelog-master.xml` y changelogs por dominio funcional [file:2].
- Preparar scripts de datos de prueba y consultas de validación [file:2][file:1].
- Continuar el proceso desescolarizado con base en esta documentación inicial [file:2].
