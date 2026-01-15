Este es un microservicio de facturación (Billing) construido con Spring Boot 2.6.6 en Java 17. Está diseñado para gestionar facturas de clientes. Aquí te detallo qué hace:

Arquitectura General
Es una aplicación REST API con arquitectura en capas:

Controller: Maneja las peticiones HTTP
DTO (Data Transfer Objects): Objetos para entrada/salida
Entity: Modelo de datos de la base de datos
Repository: Acceso a datos
Mapper: Conversión entre DTOs y Entities (usa MapStruct)
Exception Handler: Manejo centralizado de errores
Componentes Principales
1. InvoiceApplication.java - Punto de entrada

Inicia la aplicación Spring Boot
Desactiva la seguridad por defecto: @SpringBootApplication(exclude = { SecurityAutoConfiguration.class })
Activa Swagger para documentación automática de la API
Define información de la API (título, descripción, contacto, versión 1.0)
2. InvoiceRestController.java - Controlador REST
Expone 5 endpoints CRUD en /billing:

Método	Endpoint	Función
GET	/billing	Obtiene todas las facturas
GET	/billing/{id}	Obtiene una factura por ID
POST	/billing	Crea una nueva factura
PUT	/billing/{id}	Actualiza una factura existente
DELETE	/billing/{id}	Elimina una factura
GET	/billing/person/{id}	Endpoint adicional que retorna datos de una persona (hardcodeado)
3. Invoice.java - Entidad JPA

4. DTOs (Data Transfer Objects)

InvoiceRequest.java: Datos que envía el cliente para crear/actualizar
InvoiceResponse.java: Datos que retorna el servidor
5. Mappers (Conversión de datos)

InvoiceRequestMapper.java: Convierte InvoiceRequest → Invoice
Mapea customer → customerId
InvoiceResposeMapper.java: Convierte Invoice → InvoiceResponse
Mapea customerId → customer
Mapea id → invoiceId
6. ApiExceptionHandler.java - Manejo de Excepciones

Maneja excepciones de forma centralizada usando @RestControllerAdvice
Implementa estándar RFC 7807 para respuestas de error
Retorna respuestas estructuradas con código de error y mensaje
Base de Datos
application.properties: Configuración
Base de datos H2 en memoria para testing
Puerto: 7080
Driver: H2
JPA automáticamente crea las tablas
Dependencias Principales
Spring Boot Web: Para REST
Spring Security: Para autenticación (pero desactivada)
Spring Data JPA: ORM con Hibernate
PostgreSQL: Driver para conectar a PostgreSQL
H2: Base de datos en memoria para testing
Swagger/Springfox: Documentación interactiva de la API
Lombok: Generación automática de getters/setters
MapStruct: Mapeo de objetos
Caso de Uso
Es un servicio para:

✅ Crear facturas (POST)
✅ Consultar facturas (GET)
✅ Actualizar facturas (PUT)
✅ Eliminar facturas (DELETE)
Esto es típico de una arquitectura de microservicios DevOps donde cada servicio maneja su dominio específico (en este caso, facturación).
