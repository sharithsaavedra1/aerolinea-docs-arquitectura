# airline-db-docs

Repositorio documental para la estabilización técnica del proyecto de base de datos entregado en `modelo_postgresql.sql`. El propósito de este repositorio es organizar la evidencia exigida por la prueba: análisis de dominios, ADR, backlog técnico, plan de datos de prueba, plan de trabajo inicial y seguimiento técnico, sin rehacer el modelo base y manteniendo coherencia entre dominios, versionamiento, contenedorización y ruta de evolución del proyecto [file:2].

## Objetivo

Este repositorio documenta la interpretación del modelo existente y define la ruta de estabilización para que la base de datos pueda evolucionar de forma mantenible, versionada y desplegable con PostgreSQL y Liquibase [file:2]. El modelo entregado ya presenta separación por dominios funcionales, uso consistente de UUID como claves primarias, relaciones entre entidades, restricciones de integridad, validaciones `CHECK`, comentarios e índices de apoyo, por lo que la estrategia propuesta parte de una base madura y no de un rediseño desde cero [file:1][file:2].

## Alcance documental

La prueba exige como evidencia de producto un documento de análisis de dominios, cinco ADR documentados, backlog técnico, definición de HU esenciales, estructura inicial del repositorio, propuesta de contenedorización PostgreSQL y Liquibase, plan de poblamiento de datos de prueba y plan de trabajo inicial [file:2]. Este repositorio concentra la evidencia documental de esa ruta de trabajo y se complementa con un segundo repositorio técnico orientado exclusivamente a base de datos, Docker y Liquibase [file:2].

## Estructura del repositorio

```text
airline-db-docs/
├── README.md
├── docs/
│   ├── analisis_dominios.md
│   ├── backlog_tecnico.md
│   ├── plan_datos_prueba.md
│   ├── plan_trabajo_inicial.md
│   └── seguimientos.md
└── adr/
    ├── ADR-001-nuevo-dominio-funcional.md
    ├── ADR-002-roles-y-permisos-diferenciados.md
    ├── ADR-003-liquibase-versionamiento-ddl.md
    ├── ADR-004-estrategia-ramas-develop-qa-main.md
    └── ADR-005-contenedorizacion-tecnica.md
```

La estructura sigue la organización sugerida por el instrumento, que propone carpetas de documentación y ADR como parte de la evidencia entregable [file:2].

## Relación con el modelo base

Del análisis del archivo `modelo_postgresql.sql` se identifican dominios como geografía y datos de referencia, aerolínea, identidad, seguridad, clientes y fidelización, aeropuerto, aeronaves, operaciones de vuelo, ventas y reservas, abordaje, pagos y facturación [file:2]. Esa separación también se observa de forma explícita en el script por medio de bloques comentados como `GEOGRAPHY AND REFERENCE DATA`, `AIRLINE`, `IDENTITY`, `SECURITY`, `CUSTOMER AND LOYALTY`, `AIRPORT`, `AIRCRAFT`, `FLIGHT OPERATIONS`, `SALES, RESERVATION, TICKETING`, `BOARDING`, `PAYMENT` y `BILLING` [file:1].

## Ruta de trabajo propuesta

1. Identificar y documentar los dominios funcionales del modelo existente [file:2].
2. Definir backlog técnico e historias de usuario esenciales para la estabilización [file:2].
3. Formalizar decisiones arquitectónicas mediante cinco ADR obligatorios [file:2].
4. Organizar repositorios y estrategia de ramas `develop`, `qa` y `main` [file:2].
5. Preparar la integración técnica con contenedores para PostgreSQL y Liquibase [file:2].
6. Versionar el DDL por dominio funcional en changelogs independientes [file:2].
7. Definir plan de poblamiento de datos de prueba según dependencias del modelo [file:2].

## Criterios de coherencia

La documentación debe mantener alineación entre análisis de dominios, ADR, backlog, HU y propuesta técnica, porque ese es uno de los criterios explícitos de evaluación [file:2]. Además, no se deben agrupar cambios sin control y la estrategia de Liquibase debe organizar el DDL con un máximo por changelog correspondiente a entidades de un mismo dominio funcional [file:2].

## Resultado esperado

Al finalizar esta fase, el proyecto debe quedar con una base documental trazable que permita continuar el proceso desescolarizado con una ruta real de ejecución técnica [file:2]. Esa ruta parte de un modelo funcional ya construido y busca estabilizarlo, mantenerlo, versionarlo y desplegarlo de forma controlada [file:2].

link repositorio BD https://github.com/sharithsaavedra1/aerolinea-bd-engine.git
