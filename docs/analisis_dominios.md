# Análisis de dominios del modelo

## Propósito del análisis

El propósito de este documento es identificar los dominios funcionales presentes en el archivo `modelo_postgresql.sql`, reconocer sus entidades principales y describir las relaciones más relevantes que soportan la operación del sistema [file:2]. La prueba establece que el análisis no debe rehacer el modelo desde cero, sino comprender una solución ya madura y proponer una ruta de estabilización, mantenimiento, versionamiento, despliegue y evolución [file:2].

## Criterios de lectura del modelo

El modelo entregado evidencia una organización por bloques funcionales claramente comentados, uso consistente de claves primarias UUID, múltiples restricciones `UNIQUE`, validaciones `CHECK`, claves foráneas, comentarios técnicos e índices de apoyo [file:1][file:2]. Esta organización permite separar el análisis por dominio funcional y facilita una futura migración del DDL a Liquibase sin alterar la intención del diseño original [file:1][file:2].

## Dominios identificados

El instrumento menciona que a partir del análisis del archivo entregado se observan dominios como geografía y datos de referencia, aerolínea, identidad, seguridad, clientes y fidelización, aeropuerto, aeronaves, operaciones de vuelo, ventas y reservas, abordaje, pagos y facturación [file:2]. El script confirma esa separación por medio de encabezados de bloque y agrupación de tablas relacionadas [file:1].

### 1. Geografía y datos de referencia

Este dominio contiene las tablas `time_zone`, `continent`, `country`, `state_province`, `city`, `district`, `address` y `currency`, que sirven como base transversal para localización, direcciones y manejo monetario del sistema [file:1]. La secuencia relacional muestra una jerarquía territorial desde continente hasta dirección, mientras que `currency` funciona como catálogo reutilizable en fidelización, ventas, pagos y facturación [file:1].

Relaciones principales:

- `country` depende de `continent` [file:1].
- `state_province` depende de `country` [file:1].
- `city` depende de `state_province` y `time_zone` [file:1].
- `district` depende de `city` [file:1].
- `address` depende de `district` [file:1].

### 2. Aerolínea

El dominio `AIRLINE` está representado por la tabla `airline`, que almacena datos centrales de la aerolínea como país base, códigos operativos y estado de actividad [file:1]. Aunque es un dominio corto en cantidad de tablas, su impacto es transversal porque se relaciona con programas de fidelización, aeronaves, vuelos y tarifas [file:1].

Relaciones principales:

- `airline.home_country_id` referencia `country` [file:1].
- `airline` es referenciada por `loyalty_program`, `customer`, `aircraft`, `flight` y `fare` [file:1].

### 3. Identidad

El bloque `IDENTITY` está conformado por `person_type`, `document_type`, `contact_type`, `person`, `person_document` y `person_contact`, y modela la identidad básica de individuos relacionados con el sistema [file:1]. Este dominio permite representar personas con tipología, nacionalidad, documentos y medios de contacto sin duplicar información en dominios operativos posteriores [file:1].

Relaciones principales:

- `person` depende de `person_type` y opcionalmente de `country` como nacionalidad [file:1].
- `person_document` depende de `person`, `document_type` y opcionalmente de `country` como país emisor [file:1].
- `person_contact` depende de `person` y `contact_type` [file:1].

### 4. Seguridad

El dominio `SECURITY` agrupa `user_status`, `security_role`, `security_permission`, `user_account`, `user_role` y `role_permission`, y provee la base para autenticación, autorización y trazabilidad de accesos [file:1]. El modelo ya contempla separación entre cuentas, roles y permisos, lo que habilita una estrategia de permisos diferenciados solicitada por la prueba [file:1][file:2].

Relaciones principales:

- `user_account` depende de `person` y `user_status` [file:1].
- `user_role` relaciona `user_account` con `security_role` y registra quién asignó el rol [file:1].
- `role_permission` relaciona `security_role` con `security_permission` [file:1].

### 5. Clientes y fidelización

El bloque `CUSTOMER AND LOYALTY` incluye `customer_category`, `benefit_type`, `loyalty_program`, `loyalty_tier`, `customer`, `loyalty_account`, `loyalty_account_tier`, `miles_transaction` y `customer_benefit`, y modela la relación comercial recurrente con clientes y programas de acumulación de millas [file:1]. Este dominio conecta información de aerolínea, personas, moneda, beneficios y trazabilidad de cambios de nivel y movimientos de millas [file:1].

Relaciones principales:

- `customer` depende de `airline`, `person` y opcionalmente `customer_category` [file:1].
- `loyalty_program` depende de `airline` y `currency` [file:1].
- `loyalty_tier` depende de `loyalty_program` [file:1].
- `loyalty_account` depende de `customer` y `loyalty_program` [file:1].
- `loyalty_account_tier` depende de `loyalty_account` y `loyalty_tier` [file:1].
- `miles_transaction` depende de `loyalty_account` [file:1].
- `customer_benefit` depende de `customer` y `benefit_type` [file:1].

### 6. Aeropuerto

El dominio `AIRPORT` contiene `airport`, `terminal`, `boarding_gate`, `runway` y `airport_regulation`, y representa la infraestructura operativa donde se desarrollan los procesos de embarque y movimiento aéreo [file:1]. Este bloque depende de `address` y luego sirve de base para operaciones de vuelo y validaciones de abordaje [file:1].

Relaciones principales:

- `airport` depende de `address` [file:1].
- `terminal` depende de `airport` [file:1].
- `boarding_gate` depende de `terminal` [file:1].
- `runway` depende de `airport` [file:1].
- `airport_regulation` depende de `airport` [file:1].

### 7. Aeronaves

El bloque `AIRCRAFT` agrupa `aircraft_manufacturer`, `aircraft_model`, `cabin_class`, `aircraft`, `aircraft_cabin`, `aircraft_seat`, `maintenance_provider`, `maintenance_type` y `maintenance_event`, y modela la capacidad física y técnica de la flota [file:1]. Este dominio soporta asignación de aeronaves a vuelos, estructura interna de cabinas y asientos, y seguimiento de mantenimiento [file:1].

Relaciones principales:

- `aircraft_model` depende de `aircraft_manufacturer` [file:1].
- `aircraft` depende de `airline` y `aircraft_model` [file:1].
- `aircraft_cabin` depende de `aircraft` y `cabin_class` [file:1].
- `aircraft_seat` depende de `aircraft_cabin` [file:1].
- `maintenance_provider` puede depender de `address` [file:1].
- `maintenance_event` depende de `aircraft`, `maintenance_type` y opcionalmente `maintenance_provider` [file:1].

### 8. Operaciones de vuelo

El dominio `FLIGHT OPERATIONS` contiene `flight_status`, `delay_reason_type`, `flight`, `flight_segment` y `flight_delay`, y describe la planificación y ejecución operativa de los vuelos [file:1]. La presencia de segmentos permite manejar itinerarios con escalas, y las restricciones temporales del modelo protegen la consistencia entre horarios programados y reales [file:1].

Relaciones principales:

- `flight` depende de `airline`, `aircraft` y `flight_status` [file:1].
- `flight_segment` depende de `flight`, `airport` origen y `airport` destino [file:1].
- `flight_delay` depende de `flight_segment` y `delay_reason_type` [file:1].

### 9. Ventas, reservas y ticketing

El bloque `SALES, RESERVATION, TICKETING` agrupa `reservation_status`, `sale_channel`, `fare_class`, `fare`, `ticket_status`, `reservation`, `reservation_passenger`, `sale`, `ticket`, `ticket_segment`, `seat_assignment` y `baggage`, y representa el flujo comercial y operativo desde la reserva hasta la asignación de asiento y equipaje [file:1]. Este dominio es uno de los núcleos transaccionales del sistema porque conecta clientes, personas, vuelos, tarifas, asientos y equipaje [file:1].

Relaciones principales:

- `fare_class` depende de `cabin_class` [file:1].
- `fare` depende de `airline`, `airport` origen, `airport` destino, `fare_class` y `currency` [file:1].
- `reservation` depende de `reservation_status`, `sale_channel` y opcionalmente `customer` [file:1].
- `reservation_passenger` depende de `reservation` y `person` [file:1].
- `sale` depende de `reservation` y `currency` [file:1].
- `ticket` depende de `sale`, `reservation_passenger`, `fare` y `ticket_status` [file:1].
- `ticket_segment` depende de `ticket` y `flight_segment` [file:1].
- `seat_assignment` depende de `ticket_segment`, `flight_segment` y `aircraft_seat` [file:1].
- `baggage` depende de `ticket_segment` [file:1].

### 10. Abordaje

El dominio `BOARDING` está compuesto por `boarding_group`, `check_in_status`, `check_in`, `boarding_pass` y `boarding_validation`, y gestiona la preparación final del pasajero antes del ingreso al vuelo [file:1]. Este bloque se apoya en `ticket_segment`, `user_account` y `boarding_gate`, por lo que integra información comercial, operativa y de seguridad [file:1].

Relaciones principales:

- `check_in` depende de `ticket_segment`, `check_in_status`, `boarding_group` y opcionalmente `user_account` [file:1].
- `boarding_pass` depende de `check_in` [file:1].
- `boarding_validation` depende de `boarding_pass`, opcionalmente `boarding_gate` y `user_account` [file:1].

### 11. Pagos

El bloque `PAYMENT` incluye `payment_status`, `payment_method`, `payment`, `payment_transaction` y `refund`, y administra el ciclo de pago asociado a las ventas [file:1]. Este dominio permite registrar el pago principal, transacciones del proveedor y devoluciones, manteniendo trazabilidad financiera por referencia y por estado [file:1].

Relaciones principales:

- `payment` depende de `sale`, `payment_status`, `payment_method` y `currency` [file:1].
- `payment_transaction` depende de `payment` [file:1].
- `refund` depende de `payment` [file:1].

### 12. Facturación

El dominio `BILLING` contiene `tax`, `exchange_rate`, `invoice_status`, `invoice` e `invoice_line`, y soporta la emisión de documentos facturables y el cálculo asociado de impuestos y monedas [file:1]. Este bloque se conecta especialmente con `sale` y `currency`, cerrando el flujo comercial posterior al pago [file:1].

Relaciones principales:

- `exchange_rate` relaciona moneda origen y destino usando la tabla `currency` [file:1].
- `invoice` depende de `sale`, `invoice_status` y `currency` [file:1].
- `invoice_line` depende de `invoice` y opcionalmente `tax` [file:1].

## Dependencias transversales relevantes

El modelo presenta dependencias entre dominios que deben respetarse en cualquier estrategia de poblamiento o versionamiento [file:1][file:2]. Geografía y datos de referencia actúan como base para aerolínea, identidad, aeropuerto, pagos y facturación, mientras que identidad alimenta seguridad y clientes, y los dominios de aeronaves, aeropuerto y operaciones de vuelo sostienen ventas, abordaje y parte del flujo financiero posterior [file:1].

## Observaciones técnicas del modelo

El modelo usa `uuid` con `gen_random_uuid()` como estrategia uniforme de claves primarias, lo cual favorece consistencia y desacoplamiento entre procesos de inserción [file:1]. También incorpora restricciones de unicidad, checks temporales y comentarios técnicos como los asociados a `reservation`, `ticket_segment`, `seat_assignment`, `loyalty_account_tier` e `invoice_line`, lo que confirma un diseño orientado a trazabilidad y consistencia relacional [file:1][file:2].

## Conclusión técnica del análisis

El script entregado corresponde a una base de datos funcional ya construida y organizada por dominios, por lo que la ruta correcta no es rediseñar el modelo sino estabilizarlo mediante documentación, versionamiento, contenedorización y una estrategia controlada de evolución [file:2]. La separación observada en el SQL permite trasladar la estructura a changelogs por dominio funcional y sostener un backlog técnico coherente con las HU mínimas solicitadas en la prueba [file:1][file:2].
