# ADR-003 - Implementación de Liquibase para administrar el versionamiento del DDL

## Título

Adoptar Liquibase como mecanismo de versionamiento controlado del DDL organizado por dominio funcional [file:2].

## Contexto

La prueba exige un ADR para implementar Liquibase y administrar el versionamiento del DDL [file:2]. También establece que el máximo por changelog debe corresponder a entidades de un mismo dominio funcional y que no se espera agrupar todo el proyecto en un único changelog masivo [file:2]. El modelo actual ya está separado por dominios funcionales en el SQL, lo que facilita su migración ordenada a una estrategia de changelogs [file:1].

## Problema

Mantener el modelo solo como un script monolítico dificulta trazabilidad de cambios, despliegues incrementales, control de evolución y repetibilidad entre entornos [file:2]. Sin una herramienta de versionamiento como Liquibase, la administración del DDL quedaría expuesta a cambios manuales menos controlados y más complejos de auditar [file:2].

## Decisión

Se adopta Liquibase como herramienta oficial de versionamiento del DDL del proyecto, usando un `changelog-master.xml` que incluya changelogs separados por dominio funcional [file:2]. La partición de los changelogs seguirá la estructura lógica observada en el modelo base, agrupando entidades como geografía y referencia, identidad, seguridad, clientes y fidelización, aeropuerto, aeronaves, operaciones de vuelo, ventas y reservas, abordaje, pagos y facturación [file:1][file:2].

## Justificación técnica

La decisión responde de forma directa al requerimiento del instrumento y aprovecha la madurez del modelo existente, que ya tiene bloques funcionales claros [file:1][file:2]. Además, Liquibase permite controlar la aplicación ordenada del DDL, mantener historial de cambios y mejorar la repetibilidad de despliegues sobre PostgreSQL [file:2]. La organización por dominio reduce acoplamiento, facilita mantenimiento y conserva trazabilidad funcional del modelo [file:2].

## Consecuencias o impacto esperado

Como impacto positivo, el proyecto podrá evolucionar con mayor control de cambios y mejor capacidad de despliegue entre entornos [file:2]. Como consecuencia técnica, será necesario invertir esfuerzo inicial en separar el DDL actual en changelogs coherentes y validar el orden de ejecución según dependencias entre dominios y tablas [file:1][file:2].
