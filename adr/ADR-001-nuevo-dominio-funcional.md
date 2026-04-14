# ADR-001 - Ampliación de un nuevo dominio funcional relacionado con el sistema existente

## Título

Ampliar el modelo con un nuevo dominio funcional de incidencias y reclamaciones postventa asociado al flujo comercial existente [file:2].

## Contexto

La prueba exige que uno de los cinco ADR proponga la ampliación de un nuevo dominio funcional relacionado con el sistema existente [file:2]. El modelo actual cubre geografía, aerolínea, identidad, seguridad, clientes y fidelización, aeropuerto, aeronaves, operaciones de vuelo, ventas y reservas, abordaje, pagos y facturación, pero no se observa un bloque específico orientado a la gestión de incidencias, solicitudes o reclamaciones posteriores a la venta y al viaje [file:1][file:2].

## Problema

El modelo representa de forma robusta el ciclo comercial, operativo y financiero, pero no centraliza en un dominio propio la trazabilidad de reclamaciones o incidentes asociados a reservas, tickets, equipaje, reembolsos o experiencia del cliente [file:1]. Sin un dominio especializado, el proyecto quedaría limitado para evolucionar hacia procesos de servicio postventa, seguimiento de casos y análisis de calidad operativa [file:2].

## Decisión

Se propone ampliar el sistema con un dominio funcional denominado `customer_service_case` o equivalente conceptual, enfocado en la gestión de incidencias y reclamaciones del cliente [file:2]. Este dominio se relacionaría principalmente con `customer`, `reservation`, `ticket`, `baggage`, `payment`, `refund` y `user_account`, manteniendo coherencia con la estructura ya existente del modelo [file:1].

## Justificación técnica

La ampliación propuesta no rehace el modelo base, sino que lo complementa con un dominio directamente relacionado con procesos ya representados en ventas, equipaje y pagos [file:1][file:2]. También es consistente con el propósito de estabilización y evolución del proyecto, porque agrega capacidad funcional sin romper la separación por dominios ni la trazabilidad del sistema [file:2]. Además, al tratarse de un dominio nuevo y delimitado, puede implementarse más adelante como changelog independiente en Liquibase sin afectar los dominios existentes [file:2].

## Consecuencias o impacto esperado

Como impacto positivo, el proyecto quedará preparado para evolucionar hacia un componente de atención postventa y seguimiento de casos [file:2]. Como consecuencia técnica, será necesario definir nuevas entidades, relaciones, estados y reglas de trazabilidad, pero la ampliación podrá mantenerse aislada como dominio funcional independiente y coherente con la arquitectura actual [file:1][file:2].
