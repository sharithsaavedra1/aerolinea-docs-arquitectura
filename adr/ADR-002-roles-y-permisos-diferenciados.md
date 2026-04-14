# ADR-002 - Manejo de roles con permisos diferenciados para fortalecer seguridad y trazabilidad

## Título

Fortalecer el dominio de seguridad mediante una estrategia de roles y permisos diferenciados basada en el modelo existente [file:2].

## Contexto

La prueba exige un ADR específico para diseñar manejo de roles con permisos diferenciados y fortalecer seguridad y trazabilidad [file:2]. El modelo ya dispone de las tablas `security_role`, `security_permission`, `user_account`, `user_role` y `role_permission`, lo que evidencia una base relacional apta para un esquema formal de control de acceso [file:1].

## Problema

Aunque el modelo ya incorpora entidades para roles y permisos, la prueba requiere dejar definida una estrategia clara de uso y evolución de ese componente [file:2]. Sin una política formal de segmentación de permisos, el sistema puede terminar con accesos demasiado amplios, baja trazabilidad de asignaciones y dificultades para separar responsabilidades operativas, comerciales y administrativas [file:2].

## Decisión

Se adopta una estrategia de control de acceso basada en RBAC, usando roles funcionales y permisos granulares asignados a cada rol a través de `role_permission`, y asignando roles a usuarios mediante `user_role` [file:1]. Los roles deben representar responsabilidades diferenciadas, por ejemplo administración, operaciones de vuelo, ventas, abordaje, atención al cliente y finanzas, mientras que los permisos deben describir acciones concretas sobre dominios o procesos [file:1][file:2].

## Justificación técnica

La decisión aprovecha directamente la estructura ya presente en el modelo y evita introducir una solución paralela o contradictoria [file:1]. También mejora trazabilidad, porque `user_role` registra la asignación del rol y el usuario que la realizó, lo que aporta control administrativo sobre cambios de acceso [file:1]. Esta estrategia responde al criterio del instrumento de definir una ruta clara de roles, permisos y evolución técnica [file:2].

## Consecuencias o impacto esperado

Como beneficio, el sistema podrá separar responsabilidades y aplicar principio de mínimo privilegio con mayor claridad [file:2]. Como impacto operativo, será necesario definir un catálogo inicial de roles y permisos y mantener su administración como parte del backlog técnico y del futuro versionamiento del DDL [file:1][file:2].
