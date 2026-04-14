# ADR-005 - Propuesta de contenedorización técnica para PostgreSQL y Liquibase

## Título

Adoptar contenedorización para PostgreSQL y Liquibase como base técnica reproducible del proyecto [file:2].

## Contexto

El instrumento exige definir una estrategia de despliegue técnico con contenedores donde PostgreSQL pueda levantarse mediante contenedor y Liquibase quede integrado mediante contenedor o configuración compatible con el entorno del repositorio [file:2]. También se requiere que el proceso permita gestionar y aplicar el DDL de forma controlada [file:2].

## Problema

Sin contenedorización, los entornos locales pueden diferir entre equipos o fases del proyecto, dificultando reproducibilidad, validación de scripts y ejecución consistente del DDL versionado [file:2]. Además, una integración manual de PostgreSQL y Liquibase aumentaría el riesgo de errores de configuración y pérdida de trazabilidad técnica [file:2].

## Decisión

Se propone una estrategia de contenedorización basada en Docker Compose, con un servicio principal de PostgreSQL y un servicio de Liquibase integrado al mismo entorno técnico [file:2]. PostgreSQL actuará como base de ejecución local del modelo y Liquibase como mecanismo de aplicación controlada de changelogs del DDL [file:2].

## Justificación técnica

Esta decisión responde directamente a los entregables exigidos por la prueba y habilita un entorno reproducible para las siguientes fases del proyecto [file:2]. También facilita la continuidad del proceso desescolarizado, porque permite levantar de manera estandarizada la base de datos y aplicar el versionamiento del modelo sin depender de configuraciones manuales heterogéneas [file:2]. Al mantenerse separada la lógica del versionamiento por dominio funcional, la contenedorización complementa la mantenibilidad en lugar de complicarla [file:2].

## Consecuencias o impacto esperado

Como beneficio, el proyecto quedará mejor preparado para pruebas locales, integración de Liquibase y futuras validaciones del plan de datos de prueba [file:2]. Como consecuencia técnica, será necesario documentar variables de entorno, orden de ejecución y dependencias entre servicios, pero esto aportará claridad y repetibilidad al proceso de despliegue [file:2].
