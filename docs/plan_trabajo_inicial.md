# Plan de trabajo inicial

## Propósito

La prueba supervisada tiene una duración de 5 horas y exige dejar estructurada la base técnica y documental del proyecto para continuar luego con el componente desescolarizado [file:2]. Este plan organiza el trabajo inicial para asegurar criterio técnico, orden, trazabilidad y una ruta real de ejecución [file:2].

## Objetivo de la fase supervisada

El objetivo es interpretar el modelo existente, identificar dominios funcionales, documentar cinco ADR, organizar backlog y HU, definir estrategia de ramas, dejar planteada la contenedorización de PostgreSQL y Liquibase, y establecer el plan de datos de prueba sin rehacer el modelo base [file:2]. La prueba busca dejar definida una ruta para estabilización, mantenimiento, versionamiento, despliegue y evolución del proyecto [file:2].

## Entregables de esta fase

Durante la fase inicial deben quedar listos como mínimo el análisis de dominios, los cinco ADR, el backlog técnico, la propuesta de ramas `develop/qa/main`, la estructura inicial del repositorio, la estrategia de contenedorización, la estrategia de Liquibase y el plan de poblamiento de datos de prueba [file:2]. Además, debe iniciarse la primera HU priorizada para que el trabajo no quede solo en análisis [file:2].

## Primera HU priorizada

La HU inicial será `HU-001: Identificar y documentar dominios funcionales del modelo existente`, porque es la base del resto de decisiones técnicas y está incluida dentro de las HU esenciales del instrumento [file:2]. Esta decisión también facilita justificar posteriormente la separación de changelogs por dominio y el orden del backlog [file:2][file:1].

## Cronograma propuesto para 5 horas

### Bloque 1. Análisis inicial del modelo

**Duración estimada:** 60 minutos [file:2]

Actividades:

- Revisar el script `modelo_postgresql.sql` [file:2].
- Confirmar bloques funcionales presentes en el SQL [file:1].
- Identificar entidades principales y dependencias relevantes [file:1].
- Redactar `docs/analisis_dominios.md` [file:2].

Resultado esperado: dominio funcional identificado y HU-001 iniciada con evidencia documental [file:2].

### Bloque 2. Estructura del proyecto y versionamiento

**Duración estimada:** 40 minutos [file:2]

Actividades:

- Definir estructura del repositorio documental [file:2].
- Proponer estructura del repositorio técnico de base de datos [file:2].
- Establecer ramas `develop`, `qa` y `main` [file:2].
- Documentar criterios básicos de flujo de cambios [file:2].

Resultado esperado: base de organización y trazabilidad del trabajo [file:2].

### Bloque 3. ADR obligatorios

**Duración estimada:** 90 minutos [file:2]

Actividades:

- Redactar ADR-001 sobre nuevo dominio funcional [file:2].
- Redactar ADR-002 sobre roles y permisos diferenciados [file:2].
- Redactar ADR-003 sobre implementación de Liquibase [file:2].
- Redactar ADR-004 sobre ramas `develop/qa/main` [file:2].
- Redactar ADR-005 sobre contenedorización técnica como aporte adicional a la estabilización [file:2].

Resultado esperado: cinco ADR completos con título, contexto, problema, decisión, justificación técnica y consecuencias [file:2].

### Bloque 4. Backlog técnico e historias de usuario

**Duración estimada:** 40 minutos [file:2]

Actividades:

- Documentar HU-001 a HU-008 [file:2].
- Definir prioridades y dependencias [file:2].
- Diseñar el tablero para Trello [file:2].
- Registrar backlog técnico en `docs/backlog_tecnico.md` [file:2].

Resultado esperado: backlog viable con ruta mínima de estabilización [file:2].

### Bloque 5. Estrategia técnica y plan de datos

**Duración estimada:** 50 minutos [file:2]

Actividades:

- Definir propuesta de contenedorización PostgreSQL y Liquibase [file:2].
- Definir estrategia de Liquibase por dominio funcional [file:2].
- Elaborar plan de datos de prueba con orden de carga y validaciones [file:2].

Resultado esperado: lineamientos técnicos claros para el siguiente repositorio y para la continuidad del proyecto [file:2].

### Bloque 6. Revisión final y seguimiento

**Duración estimada:** 20 minutos [file:2]

Actividades:

- Revisar coherencia entre análisis, ADR, backlog y plan de datos [file:2].
- Actualizar `docs/seguimientos.md` [file:2].
- Verificar que la documentación sea clara, ordenada y trazable [file:2].

Resultado esperado: evidencia documental consolidada y alineada con los criterios de evaluación [file:2].

## Dependencias del trabajo

El trabajo documental depende directamente del análisis del script base, porque la prueba exige comprender el modelo antes de tomar decisiones de evolución [file:2]. A nivel técnico, la contenedorización, Liquibase y el plan de datos dependen de haber identificado correctamente los dominios y las relaciones principales del modelo [file:1][file:2].

## Riesgos y controles

Riesgos principales:

- Rehacer el modelo en lugar de analizarlo [file:2].
- No mantener coherencia entre dominios, ADR, backlog y estrategia técnica [file:2].
- Proponer changelogs masivos sin separación por dominio [file:2].
- No dejar evidencia de inicio real de la primera HU [file:2].

Controles:

- Basar toda decisión en el script existente [file:1][file:2].
- Mantener trazabilidad documental por archivo [file:2].
- Usar la lista de chequeo del instrumento como verificación final [file:2].

## Criterios de cierre de la fase inicial

La fase inicial se considera cerrada cuando estén documentados los dominios funcionales, redactados los cinco ADR, definido el backlog con HU esenciales, propuesta la estrategia de ramas, planteada la contenedorización y elaborado el plan de datos de prueba [file:2]. El resultado debe permitir continuar el proceso desescolarizado con una base técnica y documental estable y trazable [file:2].
