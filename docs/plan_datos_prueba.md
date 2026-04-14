# Plan de datos de prueba

## Propósito

La prueba exige generar un plan para poblar datos de prueba de manera ordenada y coherente con las dependencias del modelo, incluyendo orden de inserción, scripts documentados, validaciones o pruebas unitarias asociadas y registro claro del seguimiento técnico realizado [file:2]. Este documento define la estrategia inicial para poblar el modelo respetando su integridad referencial y su organización por dominios [file:1][file:2].

## Principios del plan

El modelo entregado tiene una alta cantidad de claves foráneas entre dominios, por lo que el poblamiento debe seguir la dependencia natural entre tablas y no un orden arbitrario [file:1]. Dado que el script ya es una solución madura con integridad relacional, el plan de datos de prueba debe preservar esa consistencia y apoyar pruebas posteriores sobre Liquibase, contenedores y validaciones funcionales [file:1][file:2].

## Estrategia general de carga

La estrategia se basa en cargar primero catálogos y referencias base, luego identidades y seguridad, y finalmente dominios operativos y transaccionales [file:1]. Este orden reduce errores por referencias inexistentes y facilita la validación incremental de la base de datos [file:1][file:2].

## Orden de inserción por dominio

### Fase 1. Geografía y datos de referencia

Orden propuesto:

1. `time_zone` [file:1]
2. `continent` [file:1]
3. `country` [file:1]
4. `state_province` [file:1]
5. `city` [file:1]
6. `district` [file:1]
7. `address` [file:1]
8. `currency` [file:1]

Justificación: estas tablas sirven de base para país de aerolínea, nacionalidad de personas, direcciones de aeropuertos y proveedores, programas de fidelización, ventas, pagos y facturación [file:1].

### Fase 2. Aerolínea e identidad

Orden propuesto:

1. `airline` [file:1]
2. `person_type` [file:1]
3. `document_type` [file:1]
4. `contact_type` [file:1]
5. `person` [file:1]
6. `person_document` [file:1]
7. `person_contact` [file:1]

Justificación: `airline` depende de `country`, y el dominio de identidad debe estar disponible antes de crear cuentas de usuario, clientes y pasajeros [file:1].

### Fase 3. Seguridad

Orden propuesto:

1. `user_status` [file:1]
2. `security_role` [file:1]
3. `security_permission` [file:1]
4. `user_account` [file:1]
5. `role_permission` [file:1]
6. `user_role` [file:1]

Justificación: las cuentas de usuario requieren personas y estado, mientras que la asignación de roles solo puede realizarse cuando ya existan roles, permisos y cuentas [file:1].

### Fase 4. Clientes y fidelización

Orden propuesto:

1. `customer_category` [file:1]
2. `benefit_type` [file:1]
3. `loyalty_program` [file:1]
4. `loyalty_tier` [file:1]
5. `customer` [file:1]
6. `loyalty_account` [file:1]
7. `loyalty_account_tier` [file:1]
8. `miles_transaction` [file:1]
9. `customer_benefit` [file:1]

Justificación: el programa y los niveles deben existir antes de abrir cuentas de fidelización y registrar asignaciones de nivel o movimientos de millas [file:1].

### Fase 5. Aeropuerto

Orden propuesto:

1. `airport` [file:1]
2. `terminal` [file:1]
3. `boarding_gate` [file:1]
4. `runway` [file:1]
5. `airport_regulation` [file:1]

Justificación: el aeropuerto depende de dirección y luego habilita operaciones de vuelo y abordaje [file:1].

### Fase 6. Aeronaves

Orden propuesto:

1. `aircraft_manufacturer` [file:1]
2. `aircraft_model` [file:1]
3. `cabin_class` [file:1]
4. `aircraft` [file:1]
5. `aircraft_cabin` [file:1]
6. `aircraft_seat` [file:1]
7. `maintenance_provider` [file:1]
8. `maintenance_type` [file:1]
9. `maintenance_event` [file:1]

Justificación: las aeronaves requieren modelo y aerolínea, y los asientos solo pueden existir después de definir cabinas y aeronaves [file:1].

### Fase 7. Operaciones de vuelo

Orden propuesto:

1. `flight_status` [file:1]
2. `delay_reason_type` [file:1]
3. `flight` [file:1]
4. `flight_segment` [file:1]
5. `flight_delay` [file:1]

Justificación: los segmentos requieren vuelos y aeropuertos, y los retrasos dependen de segmentos ya creados [file:1].

### Fase 8. Ventas, reservas y ticketing

Orden propuesto:

1. `reservation_status` [file:1]
2. `sale_channel` [file:1]
3. `fare_class` [file:1]
4. `fare` [file:1]
5. `ticket_status` [file:1]
6. `reservation` [file:1]
7. `reservation_passenger` [file:1]
8. `sale` [file:1]
9. `ticket` [file:1]
10. `ticket_segment` [file:1]
11. `seat_assignment` [file:1]
12. `baggage` [file:1]

Justificación: el dominio comercial necesita estados, tarifas, reserva, pasajeros, venta y ticket antes de poder asignar segmentos, asientos y equipaje [file:1].

### Fase 9. Abordaje

Orden propuesto:

1. `boarding_group` [file:1]
2. `check_in_status` [file:1]
3. `check_in` [file:1]
4. `boarding_pass` [file:1]
5. `boarding_validation` [file:1]

Justificación: el check-in depende del ticket segment y el boarding pass depende del check-in, mientras que la validación final requiere boarding pass y opcionalmente puerta de abordaje y usuario validador [file:1].

### Fase 10. Pagos

Orden propuesto:

1. `payment_status` [file:1]
2. `payment_method` [file:1]
3. `payment` [file:1]
4. `payment_transaction` [file:1]
5. `refund` [file:1]

Justificación: el pago depende de la venta, y las transacciones y reembolsos dependen del pago [file:1].

### Fase 11. Facturación

Orden propuesto:

1. `tax` [file:1]
2. `exchange_rate` [file:1]
3. `invoice_status` [file:1]
4. `invoice` [file:1]
5. `invoice_line` [file:1]

Justificación: la factura depende de la venta y la moneda, y sus líneas solo pueden existir cuando la factura ya fue creada [file:1].

## Scripts de inserción documentados

Se propone organizar los scripts de prueba por dominio funcional, manteniendo coherencia con la futura estrategia de changelogs en Liquibase [file:2]. Una estructura sugerida para el repositorio técnico sería la siguiente:

```text
data-test/
├── 001-geography-reference.sql
├── 002-airline-identity.sql
├── 003-security.sql
├── 004-customer-loyalty.sql
├── 005-airport.sql
├── 006-aircraft.sql
├── 007-flight-operations.sql
├── 008-sales-reservation-ticketing.sql
├── 009-boarding.sql
├── 010-payment.sql
└── 011-billing.sql
```

Esta estructura facilita ejecutar cargas parciales, aislar errores y evidenciar trazabilidad por dominio [file:2].

## Datos mínimos sugeridos por dominio

Para prueba inicial se recomienda cargar un volumen bajo pero suficiente para validar relaciones [file:1]. Un conjunto mínimo podría incluir una zona horaria, un continente, dos países, un estado, una ciudad, un distrito, una dirección, una moneda, una aerolínea, tipos de persona, tipos documentales, tipos de contacto, al menos dos personas, una cuenta de usuario, roles y permisos básicos, un cliente, un programa de fidelización, un aeropuerto origen y uno destino, una aeronave con cabina y asientos, un vuelo con segmento, una reserva, un ticket, un check-in, un pago y una factura [file:1].

## Validaciones asociadas

La prueba solicita incluir validaciones o pruebas unitarias asociadas a la dependencia de datos [file:2]. Se propone validar al menos los siguientes puntos:

- Verificar que no existan claves foráneas huérfanas tras cada fase de carga [file:1].
- Verificar que las restricciones `CHECK` se cumplan, por ejemplo en coordenadas, longitudes de códigos, fechas de vigencia, cantidades y montos positivos [file:1].
- Verificar unicidad en catálogos y códigos operativos como `iata_code`, `icao_code`, `reservation_code`, `ticket_number`, `payment_reference` e `invoice_number` [file:1].
- Verificar la secuencia lógica entre reserva, venta, ticket, check-in, pago y factura [file:1].

## Consultas de verificación sugeridas

Ejemplos de validación técnica posterior a la carga:

```sql
SELECT COUNT(*) FROM country;
SELECT COUNT(*) FROM airline;
SELECT COUNT(*) FROM person;
SELECT COUNT(*) FROM user_account;
SELECT COUNT(*) FROM customer;
SELECT COUNT(*) FROM airport;
SELECT COUNT(*) FROM aircraft;
SELECT COUNT(*) FROM flight;
SELECT COUNT(*) FROM reservation;
SELECT COUNT(*) FROM ticket;
SELECT COUNT(*) FROM payment;
SELECT COUNT(*) FROM invoice;
```

También se pueden preparar consultas de consistencia relacional, como verificar tickets sin venta, vuelos sin segmentos o validaciones de abordaje sin boarding pass [file:1].

## Riesgos del poblamiento

Los mayores riesgos están en cargar dominios operativos sin haber insertado catálogos y referencias base, o en romper restricciones de unicidad y checks al insertar datos sin orden de dependencia [file:1]. Otro riesgo es poblar volúmenes excesivos en la etapa inicial, lo que dificultaría identificar errores de integridad durante la estabilización [file:2].

## Seguimiento del plan

Cada ejecución de carga debe registrar fecha, script ejecutado, resultado y observaciones en el documento de seguimiento técnico, ya que la prueba exige dejar un registro claro del seguimiento realizado [file:2]. El plan de datos de prueba se considera exitoso cuando el modelo puede poblarse de forma ordenada, verificable y repetible en el entorno contenerizado [file:2].
