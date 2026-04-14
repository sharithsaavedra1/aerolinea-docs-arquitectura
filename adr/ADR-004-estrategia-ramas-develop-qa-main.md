# ADR-004 - Estrategia de versionamiento del repositorio con ramas develop, qa y main

## Título

Definir flujo de versionamiento del repositorio con ramas `develop`, `qa` y `main` para estabilización controlada del proyecto [file:2].

## Contexto

La prueba exige evidenciar una estrategia de trabajo con ramas `develop`, `qa` y `main`, y además incluirla como uno de los cinco ADR obligatorios [file:2]. También solicita una propuesta de flujo de versionamiento como parte del backlog y de la estructura inicial del repositorio [file:2].

## Problema

Sin una estrategia clara de ramas, los cambios documentales y técnicos del proyecto pueden mezclarse sin control, dificultando validación, seguimiento y preparación de entregables estables [file:2]. Esto es especialmente sensible en un proceso que debe combinar documentación, Liquibase, contenedores y evolución estructurada del DDL [file:2].

## Decisión

Se adopta una estrategia de tres ramas principales: `develop` para integración diaria de trabajo, `qa` para validación funcional y técnica previa a consolidación, y `main` para el estado estable y entregable del proyecto [file:2]. Adicionalmente, se permite el uso de ramas auxiliares por historia de usuario o funcionalidad, por ejemplo `feature/hu-001-analisis-dominios` o `feature/hu-004-liquibase`, las cuales deben integrarse primero a `develop` [file:2].

## Justificación técnica

La decisión responde exactamente al requerimiento del instrumento y proporciona un flujo simple, trazable y fácil de sustentar [file:2]. Separar `develop`, `qa` y `main` facilita el control de calidad de los cambios antes de consolidarlos como entregables, y evita que el estado final del proyecto se vea afectado por trabajo aún no validado [file:2]. Esta estructura también es coherente con una evolución posterior del repositorio técnico y del repositorio documental [file:2].

## Consecuencias o impacto esperado

Como efecto positivo, el proyecto tendrá una ruta clara de integración, validación y liberación [file:2]. Como impacto operativo, será necesario aplicar disciplina en nombres de ramas, mensajes de commit y criterios de paso entre `develop`, `qa` y `main` para mantener la trazabilidad que exige la prueba [file:2].
