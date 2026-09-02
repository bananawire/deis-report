# Capítulo IV: Product Design

## 4.1. Style Guidelines.

### 4.1.1. General Style Guidelines.

### 4.1.2. Web Style Guidelines.

### 4.1.3. Mobile Style Guidelines.

### 4.1.3.1. iOS Mobile Style Guidelines.

#### 4.1.3.2. Android Mobile Style Guidelines.

## 4.2. Information Architecture.

### 4.2.1. Organization Systems.

### 4.2.2. Labeling Systems.

### 4.2.3. SEO Tags and Meta Tags

### 4.2.4. Searching Systems.

### 4.2.5. Navigation Systems.

## 4.3. Landing Page UI Design.

### 4.3.1. Landing Page Wireframe.

### 4.3.2. Landing Page Mock-up.

## 4.4. Mobile Applications UX/UI Design.

### 4.4.1. Mobile Applications Wireframes.

### 4.4.2. Mobile Applications Wireflow Diagrams.

### 4.4.3. Mobile Applications Mock-ups.

### 4.4.4. Mobile Applications User Flow Diagrams.

## 4.5. Mobile Applications Prototyping.

### 4.5.1. Android Mobile Applications Prototyping.

### 4.5.2. iOS Mobile Applications Prototyping.

## 4.6. Web Applications UX/UI Design.

### 4.6.1. Web Applications Wireframes.

### 4.6.2. Web Applications Wireflow Diagrams.

### 4.6.3. Web Applications Mock-ups.

### 4.6.4. Web Applications User Flow Diagrams.

## 4.7. Web Applications Prototyping.

El prototipo de la aplicación web muestra la estructura general de navegación, el diseño de las principales vistas y las funcionalidades clave que tendrá la plataforma. Permite simular el flujo de navegación de los usuarios y visualizar cómo interactúan con los distintos módulos del sistema.

<img src="../assets/prototypes/webapp-proto.jpg" alt="webapp-proto" width="1000">

Web Application Prototype: https://sl1nk.com/1a68tor

<img src="../assets/prototypes/webapp-video.png" alt="webapp-proto" width="1000">

Video de presentación del prototipo Web Application: https://bit.ly/3Q84l7g

## 4.8. Domain-Driven Software Architecture.

### 4.8.1. Software Architecture Context Diagram.

El diagrama de contexto de sistema (System Context Diagram) representa el nivel de abstracción más alto de la arquitectura C4 para la plataforma **Vanana**. Este modelo delimita las fronteras del sistema de software principal, identificando sus interacciones directas con los actores y con los sistemas externos integrados en el ecosistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/context/VananaContext-dark.svg" alt="Vanana System Context Diagram" width="850">
</p>

Las interacciones clave representadas en el diagrama de contexto son las siguientes:

*   **Actores del Sistema:**
    *   **Home User y Facility Admin:** Interactúan directamente con la plataforma para la monitorización ambiental de sus respectivos entornos (hogares y locales comerciales). Ambos perfiles delegan la autenticación de sus credenciales al sistema externo de **Google** y la gestión de planes y transacciones monetarias al servicio de **Stripe**.
*   **Dispositivos de Hardware (Clair Hardware):**
    *   Los sensores y actuadores físicos establecen una comunicación bidireccional con la plataforma central, transmitiendo datos de telemetría de calidad del aire (CO₂, material particulado y temperatura) y ejecutando comandos automáticos de ventilación en respuesta a las evaluaciones ambientales.
*   **Servicios Externos de Soporte:**
    *   **Google OAuth2:** Provee el servicio de autenticación federada y validación de identidad.
    *   **Stripe:** Administra los flujos de cobro, procesamiento de pagos y el ciclo de vida de las suscripciones.
    *   **OneSignal:** Recibe peticiones de la plataforma para despachar notificaciones push a los dispositivos móviles de los usuarios.
    *   **Resend:** Gestiona el envío de correos electrónicos transaccionales con alertas críticas y reportes de analítica periódica.

### 4.8.2. Software Architecture Container Diagrams.

El **Container Diagram** (Diagrama de Contenedores) representa el Nivel 2 del modelo C4. Este diagrama detalla la composición interna de **Vanana Platform**, ilustrando cómo se distribuyen las responsabilidades del sistema entre los diferentes componentes ejecutables (aplicaciones web, móviles, bases de datos, brokers de mensajería y firmware embebido), especificando las tecnologías seleccionadas y los protocolos de comunicación utilizados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/VananaContainers-dark.svg" alt="Vanana Containers Diagram" width="850">
</p>

**Descripción de Contenedores y Decisiones Tecnológicas:**

*   **Aplicaciones Cliente (Frontend):**
    *   **Landing Page (HTML / CSS / JavaScript):** Sitio web estático público que presenta la propuesta de valor de la plataforma.
    *   **Single Page Application (SPA - Angular):** Aplicación web autenticada que permite a los administradores de instalaciones (Facility Admins) configurar espacios físicos, definir umbrales de alerta y visualizar paneles analíticos de calidad de aire en tiempo real.
    *   **Mobile App (Flutter):** Aplicación móvil multiplataforma orientada al usuario del hogar (Home User) para el monitoreo ágil y la recepción de notificaciones de alerta inmediata.
*   **Capa de Servicios de Backend:**
    *   **API Gateway (Spring Cloud Gateway / Java):** Punto único de entrada al backend encargado de la seguridad perimetral, balanceo de carga y enrutamiento de peticiones.
    *   **Platform API (Spring Boot / Java 25):** Núcleo de servicios empresariales que implementa las reglas de negocio críticas, incluyendo IAM, gestión de locales, e ingesta y evaluación de telemetría.
*   **Capa de Mensajería y Desacoplamiento:**
    *   **Kafka Message Broker (Apache Kafka):** Broker de mensajería asíncrona que desacopla la ingesta masiva de datos en el Edge del procesamiento interno de la plataforma, garantizando tolerancia a fallos y alta escalabilidad.
*   **Bases de Datos de la Plataforma:**
    *   **Platform PostgreSQL Database:** Almacenamiento relacional principal para entidades transaccionales (instalaciones, dispositivos asociados, históricos y preferencias).
    *   **Platform Redis Database:** Almacenamiento clave-valor en memoria utilizado para la gestión rápida de sesiones activas, tokens de seguridad temporales y control de tasas de peticiones (rate limiting).
*   **Capa IoT (Edge y Dispositivos Embebidos):**
    *   **Clair Embedded Application (Firmware Embebido):** Corre directamente sobre el microcontrolador físico del sensor. Mide los niveles ambientales y transmite los payloads localmente.
    *   **Clair Edge Station Application (Flask / Python):** Estación local que actúa como pasarela (Gateway local) para coordinar múltiples sensores Clair. Almacena temporalmente los datos en una **Edge SQLite Database** para garantizar la continuidad operativa ante pérdidas de conexión a Internet (sincronización offline).

**Protocolos y Mecanismos de Comunicación:**

*   **REST/HTTPS (JSON):** Utilizado para la comunicación síncrona entre las aplicaciones de cliente (Angular, Flutter, Edge Station) y el backend a través del API Gateway.
*   **Kafka Wire Protocol (TCP):** Utilizado para el envío asíncrono de lotes de telemetría desde la estación Edge hacia el broker de mensajería en la nube.
*   **JDBC/SQL:** Conexión nativa de base de datos para la persistencia transaccional entre Spring Boot y PostgreSQL.
*   **Redis Protocol (RESP):** Utilizado para operaciones de caché de baja latencia.

### 4.8.3. Software Architecture Components Diagrams.

#### 4.8.3.1 Bounded Context: Identity & Access (IAM)

Dentro del contenedor **Platform API**, el contexto acotado de **IAM** se organiza internamente siguiendo el patrón de arquitectura hexagonal estructurada en las cuatro capas tácticas (Interfaces, Application, Domain e Infrastructure).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/IamLayers-dark.svg" alt="IAM Layer Components Diagram" width="850">
</p>

*   **IAM Interfaces (Component):** Recibe las solicitudes HTTP/HTTPS provenientes del API Gateway y las delega al servicio correspondiente en la capa de aplicación. Utiliza Spring Security para interceptar peticiones y validar los JWT de acceso de forma perimetral.
*   **IAM Application (Component):** Orquesta los casos de uso llamando a los modelos de dominio. Envía eventos e interactúa con el componente de infraestructura.
*   **IAM Domain (Component):** Mantiene los modelos enriquecidos de dominio y define las interfaces que actúan como contratos de persistencia.
*   **IAM Infrastructure (Component):** Implementa las interfaces de repositorio de dominio mediante tecnologías específicas (Spring Data JPA conectando a la base de datos relacional PostgreSQL, e integraciones con Redis y el SDK de Google).

#### 4.8.3.2 Bounded Context: Billing

A nivel de contenedores en la API principal, el contexto de Billing descompone sus responsabilidades a través de componentes en capas:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/BillingLayers-dark.svg" alt="Billing Layer Components Diagram" width="850">
</p>

*   **Billing Interfaces (Component):** Expone los controladores de checkout y recepción de webhooks de Stripe.
*   **Billing Application (Component):** Orquesta los comandos de creación de cobros y escucha de registros de usuarios.
*   **Billing Domain (Component):** Contiene el modelo lógico de cobro y límites del plan de usuario.
*   **Billing Infrastructure (Component):** Implementa la integración técnica con el SDK de Stripe y la base de datos PostgreSQL.

#### 4.8.3.3 Bounded Context: Device & Space Management

Organización de capas de componentes en el contenedor principal de la API para Device & Space Management:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/DeviceSpaceLayers-dark.svg" alt="Device & Space Layer Components Diagram" width="850">
</p>

*   **DeviceSpace Interfaces (Component):** Expone las API HTTP REST para la manipulación de la organización y emparejamiento de hardware.
*   **DeviceSpace Application (Component):** Orquesta los casos de uso llamando al dominio y disparando publicadores.
*   **DeviceSpace Domain (Component):** Aloja las reglas de asignación y jerarquías lógicas de espacios.
*   **DeviceSpace Infrastructure (Component):** Implementa el acceso físico a las tablas relacionales y el encolamiento de eventos en Kafka.

#### 4.8.3.4 Bounded Context: Air Quality Evaluation

Dentro del backend de Platform API, las capas tácticas de Air Quality Evaluation se representan bajo los siguientes componentes organizados:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AirQualityLayers-dark.svg" alt="Air Quality Layer Components Diagram" width="850">
</p>

*   **AirQuality Interfaces (Component):** Expone las API HTTP y la Fachada interna de consulta del aire.
*   **AirQuality Application (Component):** Procesa de forma reactiva los eventos procedentes de Kafka y ejecuta comandos de persistencia.
*   **AirQuality Domain (Component):** Modela la estructura lógica de los gases y partículas finas.
*   **AirQuality Infrastructure (Component):** Implementa el repositorio conectándose a PostgreSQL para almacenar el histórico ambiental.

#### 4.8.3.5  Bounded Context: Alerting & Response

Estructuración de componentes internos para Alerting & Response en el contenedor principal de la API:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AlertingLayers-dark.svg" alt="Alerting Layer Components Diagram" width="850">
</p>

*   **Alerting Interfaces (Component):** Expone las API HTTP REST para la auditoría y gestión de alertas.
*   **Alerting Application (Component):** Consume lecturas e inicia la evaluación y despacho de eventos de incidentes.
*   **Alerting Domain (Component):** Define las reglas lógicas de incidentes y estados de severidad.
*   **Alerting Infrastructure (Component):** Conecta a PostgreSQL para almacenamiento y encola avisos en el broker de Kafka.

#### 4.8.3.6 Bounded Context: Analytics & Reporting

Organización de capas de componentes en el contenedor principal de la API para Analytics & Reporting:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AnalyticsLayers-dark.svg" alt="Analytics Layer Components Diagram" width="850">
</p>

*   **Analytics Interfaces (Component):** Expone las API HTTP REST y gestiona las conexiones abiertas para streams SSE.
*   **Analytics Application (Component):** Orquesta los schedulers, consume del bus de Kafka y escribe en memoria caché.
*   **Analytics Domain (Component):** Modela las fórmulas oficiales de AQI y agregaciones estadísticas.
*   **Analytics Infrastructure (Component):** Persiste los reportes e históricos de snapshots en las tablas relacionales de PostgreSQL.

#### 4.8.3.7 Bounded Context: Analytics & Notifications

Organización de componentes en el Platform API para el contexto acotado de Notifications:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/NotificationsLayers-dark.svg" alt="Notifications Layer Components Diagram" width="850">
</p>

*   **Notifications Interfaces (Component):** Expone las interfaces REST y fachadas de llamadas internas.
*   **Notifications Application (Component):** Procesa eventos de incidentes de Kafka y formatea los templates de emails.
*   **Notifications Domain (Component):** Modela el estado lógico de envíos de alertas y correos.
*   **Notifications Infrastructure (Component):** Implementa el cliente SMTP, la integración HTTP de OneSignal y la persistencia JPA a PostgreSQL.

## 4.9. Software Object-Oriented Design.

### 4.9.1. Class Diagrams.

#### 4.9.1.1 Bounded Context: Identity & Access (IAM)

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.2 Bounded Context: Billing

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.3 Bounded Context: Device & Space Management

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.4 Bounded Context: Air Quality Evaluation

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.5 Bounded Context: Alerting & Response

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.6 Bounded Context: Analytics & Reporting

4.9.1.1.1 Domain Layer

4.9.1.1.2 Interface Layer

4.9.1.1.3 Application Layer

4.9.1.1.4 Infrastructure Layer

#### 4.9.1.7 Bounded Context: Analytics & Notifications

### 4.9.2. Class Dictionary.

#### 4.9.2.1 Bounded Context: Identity & Access (IAM)

El contexto acotado de **Identity & Access Management (IAM)** gestiona el registro de nuevos usuarios, la autenticación segura, el control de acceso basado en roles y el inicio de sesión federado (Google OAuth2). Asegura que los recursos de la plataforma Vanana estén protegidos y que solo los usuarios autorizados puedan interactuar con los sensores y actuadores.

**Diccionario de Clases del Contexto IAM**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase              | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                                | Relaciones de Asociación / Dependencia                       |
| :------------------------------ | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **User**                        | Dominio         | Representa la entidad de usuario en la plataforma. Actúa como raíz de agregado (*Aggregate Root*). | `id` (UUID), `email` (EmailAddress), `password` (Password), `status` (UserStatus), `googleUserId` (GoogleUserId) | `confirm()`, `linkGoogleAccount(googleUserId)`               | Contiene `EmailAddress` y `Password`.                        |
| **TokenSession**                | Dominio         | Representa una sesión activa de JWT emitida para un usuario específico. | `jti` (TokenJti), `userId` (UserId), `refreshToken` (String), `tokenType` (TokenType), `expiresAt` (Instant) | `invalidate()`                                               | Contiene `UserId`.                                           |
| **RegistrationSession**         | Dominio         | Entidad temporal que mantiene el estado de registro de un usuario pendiente de confirmación. | `id` (RegistrationSessionId), `email` (EmailAddress), `password` (Password), `verificationCode` (VerificationCode), `expiresAt` (Instant) | *N/A*                                                        | Contiene `EmailAddress`, `Password` y `VerificationCode`.    |
| **EmailAddress**                | Dominio         | Objeto de Valor (*Value Object*) que encapsula la lógica de validación del correo electrónico. | `value` (String)                                             | *N/A*                                                        | Composición en `User` y `RegistrationSession`.               |
| **Password**                    | Dominio         | Objeto de Valor que maneja el hash encriptado de la contraseña. | `encryptedValue` (String)                                    | *N/A*                                                        | Composición en `User` y `RegistrationSession`.               |
| **VerificationCode**            | Dominio         | Objeto de Valor que representa el código de 6 dígitos enviado por email. | `value` (String)                                             | *N/A*                                                        | Composición en `RegistrationSession`.                        |
| **UserRepository**              | Dominio         | Interfaz (Puerto) que define los métodos de persistencia del Agregado `User`. | *N/A*                                                        | `save()`, `findById()`, `findByEmail()`, `findByGoogleUserId()` | Utilizado por `UserCommandServiceImpl` e `UserQueryServiceImpl`. |
| **TokenSessionRepository**      | Dominio         | Interfaz (Puerto) para gestionar el ciclo de vida de persistencia rápida de `TokenSession`. | *N/A*                                                        | `save()`, `findByJti()`, `deleteByJti()`                     | Utilizado por `TokenCommandServiceImpl` y `TokenQueryServiceImpl`. |
| **GoogleTokenVerifier**         | Dominio         | Interfaz (Servicio de Dominio) para verificar tokens de identidad emitidos por Google. | *N/A*                                                        | `verify(idToken)`                                            | Utilizado por `GoogleAuthenticationCommandServiceImpl`.      |
| **AuthenticationController**    | Interfaz        | Controlador REST de entrada para flujos de autenticación local. | `userCommandService`, `tokenCommandService`                  | `signUp()`, `confirmSignUp()`, `signIn()`, `refreshToken()`, `signOut()` | Depende de `UserCommandServiceImpl` y `TokenCommandServiceImpl`. |
| **GoogleOAuthController**       | Interfaz        | Controlador REST para manejar la redirección y el callback de Google OAuth2. | `googleOAuthStateManager`, `googleOAuthCallbackApplicationService` | `redirectToGoogle()`, `handleCallback()`                     | Depende de `GoogleOAuthCallbackApplicationService`.          |
| **UserCommandServiceImpl**      | Aplicación      | Servicio de aplicación que orquesta el registro inicial y la confirmación mediante código. | `userRepository`, `registrationSessionRepository`, `asyncNotificationService` | `handle(InitiateRegistrationCommand)`, `handle(ConfirmRegistrationCommand)` | Usa `UserRepository`, `RegistrationSessionRepository` y `AsyncNotificationService`. |
| **TokenCommandServiceImpl**     | Aplicación      | Servicio de aplicación para la creación, rotación e invalidación de tokens JWT. | `tokenSessionRepository`, `userRepository`, `jwtTokenEncoder` | `handle(CreateTokenSessionCommand)`, `handle(RotateRefreshTokenCommand)`, `handle(InvalidateTokenSessionCommand)` | Usa `TokenSessionRepository`, `UserRepository` y `JwtTokenEncoder`. |
| **JpaUserRepository**           | Infraestructura | Adaptador concreto de persistencia relacional que interactúa con PostgreSQL mediante JPA. | *N/A*                                                        | `findByEmail()`, `existsByEmail()`                           | Implementa `UserRepository`.                                 |
| **RedisTokenSessionRepository** | Infraestructura | Adaptador concreto para almacenar y verificar sesiones de tokens de forma rápida en caché Redis. | `redisTemplate`, `objectMapper`                              | `save()`, `findByJti()`, `deleteByJti()`, `revokeAllTokensForUser()` | Implementa `TokenSessionRepository`.                         |

#### 4.9.2.2 Bounded Context: Billing

El contexto acotado de **Billing** es responsable de administrar el modelo de monetización de la plataforma. Controla las pasarelas de pago, los límites operativos impuestos a los usuarios según su plan (Freemium o Premium) y el procesamiento de suscripciones mensuales, integrándose de forma directa con la API externa de Stripe.

**Diccionario de Clases del Contexto Billing**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                 | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                                | Relaciones de Asociación / Dependencia                       |
| :--------------------------------- | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **UserPlan**                       | Dominio         | Entidad raíz que define el plan de suscripción asignado a un usuario y sus fechas de vigencia. | `id` (UUID), `userId` (UserId), `planType` (PlanType), `startDate` (LocalDate), `endDate` (LocalDate) | `upgradeToPremium()`, `downgradeToFreemium()`, `isPremiumExpired()` | Contiene `UserId` y `PlanType`.                              |
| **PaymentRecord**                  | Dominio         | Entidad que registra el historial de cobros y transacciones de los usuarios. | `id` (UUID), `userId` (UserId), `amount` (Money), `status` (PaymentStatus), `stripePaymentIntentId` (String) | `markAsCompleted()`                                          | Contiene `UserId`, `Money` y `PaymentStatus`.                |
| **PaymentGateway**                 | Dominio         | Interfaz (Puerto) que define los métodos de interacción con pasarelas de cobro externas. | *N/A*                                                        | `createCheckoutSession()`, `createPaymentIntent()`           | Implementado por `StripePaymentGatewayAdapter`.              |
| **UserPlanRepository**             | Dominio         | Interfaz de repositorio para persistir y consultar el plan de un usuario. | *N/A*                                                        | `save()`, `findByUserId()`                                   | Utilizado por los servicios de comando y consulta de suscripciones. |
| **PaymentRecordRepository**        | Dominio         | Interfaz de repositorio para persistir transacciones financieras. | *N/A*                                                        | `save()`, `findByStripePaymentIntentId()`, `findByUserId()`  | Utilizado por los servicios de comando y consulta de suscripciones. |
| **SubscriptionController**         | Interfaz        | Controlador REST que expone endpoints para iniciar checkouts, degradar cuentas y ver planes activos. | `subscriptionCommandService`, `subscriptionQueryService`     | `createCheckoutSession()`, `getSubscriptionsByUserId()`, `downgradeToFreemium()` | Depende de `SubscriptionCommandServiceImpl` y `SubscriptionQueryServiceImpl`. |
| **StripeWebhookController**        | Interfaz        | Controlador de entrada que procesa eventos asíncronos enviados por webhooks de Stripe. | `subscriptionCommandService`, `stripeWebhookSecret`          | `handleWebhook()`                                            | Depende de `SubscriptionCommandServiceImpl`.                 |
| **BillingContextFacade**           | Interfaz        | Fachada expuesta para que otros contextos consulten límites de negocio (suscripción activa del usuario). | *N/A*                                                        | `getMaxOrganizations()`, `getMaxSpaces()`, `getMaxDevices()` | Implementado por `BillingContextFacadeImpl`.                 |
| **SubscriptionCommandServiceImpl** | Aplicación      | Servicio de aplicación que procesa comandos para actualizar suscripciones y registrar pagos exitosos. | `paymentGateway`, `paymentRecordRepository`, `userPlanRepository` | `handle(CreateCheckoutSessionCommand)`, `handle(FulfillSubscriptionCommand)` | Usa `PaymentGateway`, `PaymentRecordRepository` y `UserPlanRepository`. |
| **SubscriptionQueryServiceImpl**   | Aplicación      | Servicio de aplicación para consultar registros de pago e historial de planes activos. | `userPlanRepository`, `paymentRecordRepository`              | `handle(GetSubscriptionByIdQuery)`, `resolveUserPlan()`      | Usa `UserPlanRepository` y `PaymentRecordRepository`.        |
| **StripePaymentGatewayAdapter**    | Infraestructura | Adaptador que implementa el puerto `PaymentGateway` utilizando el SDK de Stripe. | `stripeApiKey`                                               | `createCheckoutSession()`, `createPaymentIntent()`           | Implementa `PaymentGateway`.                                 |
| **JpaUserPlanRepository**          | Infraestructura | Adaptador JPA que implementa `UserPlanRepository` para almacenar planes en PostgreSQL. | *N/A*                                                        | *N/A*                                                        | Implementa `UserPlanRepository`.                             |

#### 4.9.2.3 Bounded Context: Device & Space Management

El contexto acotado de **Device & Space Management** gestiona el inventario de hardware y la organización espacial lógica de la plataforma. Permite registrar dispositivos de sensores (`Device`), asignar ubicaciones organizacionales (`Organization` y `Space`), controlar las vinculaciones físicas (`DeviceAssignment`), registrar comandos enviados al hardware (`DeviceCommand`) y definir los umbrales personalizados de alerta por dispositivo.

**Diccionario de Clases del Contexto Device & Space Management**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                           | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                             | Relaciones de Asociación / Dependencia                       |
| :------------------------------------------- | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------------------------------------------------- | :----------------------------------------------------------- |
| **Device**                                   | Dominio         | Representa el sensor físico registrado en el sistema global. | `id` (UUID), `serialNumber` (String), `name` (String), `hardwareId` (HardwareId), `apiKey` (ApiKey) | `rotateApiKey()`, `updateName()`                          | Contiene `HardwareId` y `ApiKey`.                            |
| **DeviceAssignment**                         | Dominio         | Entidad que modela el emparejamiento físico de un sensor a un espacio y usuario específico. | `id` (UUID), `device` (Device), `ownerUserId` (UserId), `spaceId` (UUID), `status` (DeviceStatus), `claimToken` (ClaimToken) | `claimToSpace()`, `markOnline()`, `markOffline()`         | Contiene `Device`.                                           |
| **DeviceCommand**                            | Dominio         | Entidad que almacena el historial y estado de comandos enviados a un actuador. | `id` (UUID), `deviceId` (UUID), `commandType` (String), `payload` (String), `status` (String) | `acknowledge()`                                           | Vinculado a `Device` por ID.                                 |
| **Organization**                             | Dominio         | Representa la agrupación lógica superior (empresa o cuenta principal) para locales comerciales. | `id` (UUID), `name` (String), `ownerUserId` (UserId)         | `updateName()`                                            | Vinculado a `UserId`.                                        |
| **Space**                                    | Dominio         | Representa un espacio o zona física específica asociada a una organización (ej: "Sala A"). | `id` (UUID), `name` (String), `organizationId` (UUID)        | `updateName()`                                            | Asociado a `Organization` por ID.                            |
| **DeviceRepository**                         | Dominio         | Interfaz de persistencia para el inventario de sensores registrados. | *N/A*                                                        | `save()`, `findById()`, `findByHardwareId()`              | Utilizado por `DeviceCommandServiceImpl`.                    |
| **DeviceAssignmentRepository**               | Dominio         | Interfaz de persistencia para los emparejamientos y estados de conexión en tiempo real. | *N/A*                                                        | `save()`, `findByDeviceId()`, `findBySpaceId()`           | Utilizado por los servicios de comando de dispositivos y espacios. |
| **DeviceController**                         | Interfaz        | Controlador REST para emparejar, reclamar, listar y renombrar dispositivos sensores. | `deviceCommandService`, `deviceQueryService`                 | `pairDevice()`, `claimDevice()`, `getDevices()`           | Depende de los servicios de aplicación de dispositivos.      |
| **DeviceCommandController**                  | Interfaz        | Controlador REST que permite emitir acciones o comandos manuales hacia los actuadores. | `deviceControlCommandService`                                | `createDeviceCommand()`, `getDeviceCommand()`             | Depende de `DeviceControlCommandServiceImpl`.                |
| **DeviceThresholdController**                | Interfaz        | Controlador REST para registrar y eliminar los umbrales de advertencia específicos de métricas de aire. | `thresholdCommandService`                                    | `writeThreshold()`, `removeThreshold()`                   | Depende de `DeviceThresholdCommandServiceImpl`.              |
| **OrganizationController**                   | Interfaz        | Controlador REST para crear, renombrar y eliminar organizaciones. | `organizationCommandService`                                 | `createOrganization()`, `updateOrganizationName()`        | Depende de `OrganizationCommandServiceImpl`.                 |
| **SpaceController**                          | Interfaz        | Controlador REST para crear y administrar los espacios de monitoreo. | `spaceCommandService`                                        | `createSpace()`, `updateSpaceName()`                      | Depende de `SpaceCommandServiceImpl`.                        |
| **DeviceCommandServiceImpl**                 | Aplicación      | Servicio de aplicación para el aprovisionamiento, vinculación y desvinculación de hardware Clair. | `deviceRepository`, `deviceAssignmentRepository`, `spaceRepository`, `publisher` | `handle(PairDeviceCommand)`, `handle(ClaimDeviceCommand)` | Usa repositorios y publica eventos vía Kafka.                |
| **DeviceControlCommandServiceImpl**          | Aplicación      | Servicio para emitir comandos y despachar colas de acciones pendientes hacia los sensores. | `deviceCommandRepository`, `publisher`                       | `handle(CreateDeviceCommandCommand)`                      | Usa `DeviceCommandRepository` y Kafka.                       |
| **ProvisioningDevicesChangedKafkaPublisher** | Infraestructura | Adaptador para publicar eventos de integración de cambio de dispositivos en Apache Kafka. | `kafkaTemplate`                                              | `publish()`                                               | Implementa el puerto de mensajería para eventos de aprovisionamiento. |
| **JpaDeviceRepository**                      | Infraestructura | Adaptador JPA que implementa `DeviceRepository` para la base de datos PostgreSQL. | *N/A*                                                        | `findByHardwareId()`                                      | Implementa `DeviceRepository`.                               |

#### 4.9.2.4 Bounded Context: Air Quality Evaluation

El contexto acotado de **Air Quality Evaluation** es el encargado de procesar, analizar y almacenar la telemetría en tiempo real recibida desde los sensores físicos. Realiza la validación de integridad técnica de los datos y la posterior evaluación de las métricas ambientales de salubridad ($CO_2$, material particulado, temperatura y humedad) contra los umbrales configurados para cada espacio.

**Diccionario de Clases del Contexto Air Quality Evaluation**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                        | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                                | Relaciones de Asociación / Dependencia                       |
| :---------------------------------------- | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **TelemetryEvaluation**                   | Dominio         | Entidad raíz del agregado que consolida los datos ambientales de un sensor e indica su estado de salud general. | `id` (UUID), `deviceId` (DeviceId), `airQuality` (AirQuality), `particulateMatter` (ParticulateMatter), `connectivity` (Connectivity), `location` (Location) | *N/A*                                                        | Contiene `DeviceId`, `AirQuality`, `ParticulateMatter`, `Connectivity` y `Location`. |
| **DeviceId**                              | Dominio         | Objeto de Valor (*Value Object*) que tipa de manera fuerte el identificador único del sensor. | `value` (UUID)                                               | *N/A*                                                        | Composición en `TelemetryEvaluation`.                        |
| **AirQuality**                            | Dominio         | Objeto de Valor que encapsula los niveles medidos de dióxido de carbono, temperatura y humedad. | `co2` (Double), `temperature` (Double), `humidity` (Double)  | *N/A*                                                        | Composición en `TelemetryEvaluation`.                        |
| **ParticulateMatter**                     | Dominio         | Objeto de Valor que agrupa la densidad medida de polvo y partículas suspendidas. | `pm1_0` (Double), `pm2_5` (Double), `pm10` (Double)          | *N/A*                                                        | Composición en `TelemetryEvaluation`.                        |
| **Connectivity**                          | Dominio         | Objeto de Valor que almacena datos de diagnóstico del hardware (señal, red, estado). | `status` (String), `network` (String), `signalStrength` (Double) | *N/A*                                                        | Composición en `TelemetryEvaluation`.                        |
| **Location**                              | Dominio         | Objeto de Valor que identifica la localización geográfica del dispositivo reportado. | `country` (String)                                           | *N/A*                                                        | Composición en `TelemetryEvaluation`.                        |
| **TelemetryEvaluationRepository**         | Dominio         | Interfaz (Puerto) que define los métodos de persistencia para el histórico de evaluaciones ambientales. | *N/A*                                                        | `save()`, `findByDeviceId()`, `findFirstByDeviceIdValueOrderByRecordedAtDesc()` | Utilizado por los servicios de comando y consulta de telemetría. |
| **TelemetryEvaluationController**         | Interfaz        | Controlador REST para solicitar evaluaciones manuales y obtener históricos o la última lectura de un dispositivo. | `telemetryEvaluationQueryService`, `telemetryEvaluationCommandService` | `evaluateTelemetry()`, `getLatestEvaluationByDevice()`       | Depende de `TelemetryEvaluationCommandServiceImpl` y `TelemetryEvaluationQueryServiceImpl`. |
| **EvaluationContextFacade**               | Interfaz        | Fachada expuesta para que otros contextos consulten históricos agregados (como el módulo de Analytics). | *N/A*                                                        | `getLatestEvaluationRecordedAt()`, `getHourlyTelemetryAggregation()` | Implementado por `EvaluationContextFacadeImpl`.              |
| **TelemetryEvaluationCommandServiceImpl** | Aplicación      | Servicio de aplicación que procesa el comando de ingesta, evalúa los umbrales y guarda el registro. | `telemetryEvaluationRepository`                              | `handle(EvaluateTelemetryCommand)`                           | Usa `TelemetryEvaluationRepository` para persistir la evaluación. |
| **TelemetryEvaluationQueryServiceImpl**   | Aplicación      | Servicio de aplicación para consultar evaluaciones históricas de forma paginada o el último registro recibido. | `telemetryEvaluationRepository`                              | `handle(GetEvaluationsByDeviceQuery)`, `handle(GetLatestEvaluationByDeviceQuery)` | Usa `TelemetryEvaluationRepository`.                         |
| **TelemetryRecordedKafkaConsumer**        | Aplicación      | Consumidor (Listener) de Kafka que procesa asíncronamente los mensajes de telemetría e inicia la evaluación. | `telemetryEvaluationCommandService`, `externalDeviceService` | `consume()`                                                  | Recibe datos crudos, resuelve el ID mediante `ExternalDeviceService` y delega a `TelemetryEvaluationCommandService`. |
| **ExternalDeviceService**                 | Aplicación      | Interfaz (Puerto de comunicación inter-contexto) para validar la existencia y pertenencia de un dispositivo. | *N/A*                                                        | `findDeviceIdByHardwareId()`, `isDeviceOwnedByUser()`        | Consumido por el controlador y el consumidor Kafka.          |
| **JpaTelemetryEvaluationRepository**      | Infraestructura | Adaptador JPA que implementa `TelemetryEvaluationRepository` para PostgreSQL. | *N/A*                                                        | *N/A*                                                        | Implementa `TelemetryEvaluationRepository`.                  |

#### 4.9.2.5 Bounded Context: Alerting & Response

El contexto acotado de **Alerting & Response** es responsable del ciclo de vida de los incidentes de calidad del aire. Evalúa de forma continua la telemetría recibida contra los umbrales específicos de seguridad, dispara alertas ante transgresiones de límites de contaminantes, gestiona el acuse de recibo de los operadores y despacha comandos de respuesta hacia los dispositivos inteligentes de forma autónoma.

**Diccionario de Clases del Contexto Alerting & Response**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                         | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                                | Relaciones de Asociación / Dependencia                       |
| :----------------------------------------- | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **Alert**                                  | Dominio         | Entidad raíz del agregado que modela el ciclo de vida de un incidente ambiental (abierto, reconocido, cerrado). | `id` (UUID), `deviceId` (UUID), `spaceId` (UUID), `metric` (MetricType), `thresholdValue` (BigDecimal), `actualValue` (BigDecimal), `message` (String), `status` (AlertStatus), `severity` (AlertSeverity), `occurredAt` (Instant), `resolvedAt` (Instant) | `acknowledge()`, `resolve(resolvedAt)`                       | Contiene `MetricType`, `AlertStatus` y `AlertSeverity`.      |
| **MetricType**                             | Dominio         | Enumeración que define las métricas propensas a generar alertas. | *N/A*                                                        | *N/A*                                                        | Composición en `Alert`.                                      |
| **AlertSeverity**                          | Dominio         | Enumeración que indica la gravedad de la alerta (Low, Warning, Critical). | *N/A*                                                        | *N/A*                                                        | Composición en `Alert`.                                      |
| **AlertStatus**                            | Dominio         | Enumeración para controlar el estado de atención del incidente (Active, Acknowledged, Resolved). | *N/A*                                                        | *N/A*                                                        | Composición en `Alert`.                                      |
| **AlertRepository**                        | Dominio         | Interfaz (Puerto) que define los métodos de persistencia para las alertas. | *N/A*                                                        | `save()`, `findById()`, `findFirstByDeviceIdAndMetricAndStatusIn()` | Utilizado por los servicios de aplicación de alertas.        |
| **AlertController**                        | Interfaz        | Controlador REST para consultar alertas de dispositivos, espacios y obtener resúmenes. | `alertQueryService`                                          | `getAlertsByDevice()`, `getAlertsBySpace()`, `getDailySummary()` | Depende de `AlertQueryServiceImpl`.                          |
| **AlertingContextFacade**                  | Interfaz        | Fachada interna expuesta para que otros contextos consulten detalles específicos de incidentes. | *N/A*                                                        | `findAlertDetailsById()`                                     | Implementado por `AlertingContextFacadeImpl`.                |
| **AlertCommandServiceImpl**                | Aplicación      | Servicio de aplicación para evaluar telemetría, generar incidentes o resolverlos automáticamente. | `alertRepository`, `externalThresholdService`, `externalDeviceService`, `publisher` | `handle(EvaluateTelemetryForAlertsCommand)`                  | Usa `AlertRepository`, puertos externos de consulta y publica en Kafka. |
| **AlertQueryServiceImpl**                  | Aplicación      | Servicio de consulta para obtener historiales de incidentes filtrados y resúmenes diarios. | `alertRepository`, `externalDeviceService`                   | `handle(GetAlertsByDeviceQuery)`, `handle(GetAlertsByOwnerQuery)` | Usa `AlertRepository` y `ExternalAlertingDeviceService`.     |
| **AlertingTelemetryRecordedKafkaConsumer** | Aplicación      | Consumidor asíncrono de Kafka que procesa lecturas reportadas para gatillar la detección de alertas. | `alertCommandService`                                        | `consume()`                                                  | Delega a `AlertCommandServiceImpl` la evaluación del payload recibido. |
| **ExternalAlertingDeviceService**          | Aplicación      | Interfaz (Puerto de comunicación inter-contexto) para obtener nombres y localizaciones del hardware. | *N/A*                                                        | `fetchSpaceIdByDeviceId()`, `fetchDeviceNameByDeviceId()`    | Utilizado por `AlertCommandServiceImpl`.                     |
| **ExternalAlertingThresholdService**       | Aplicación      | Interfaz (Puerto de comunicación inter-contexto) para obtener los umbrales habilitados por sensor. | *N/A*                                                        | `fetchEnabledThresholdsByDeviceId()`                         | Utilizado por `AlertCommandServiceImpl`.                     |
| **JpaAlertRepository**                     | Infraestructura | Adaptador JPA que implementa `AlertRepository` para almacenar alertas en PostgreSQL. | *N/A*                                                        | *N/A*                                                        | Implementa `AlertRepository`.                                |
| **AlertIncidentsChangedKafkaPublisher**    | Infraestructura | Adaptador que publica eventos de integración de cambio de estado de alertas en Apache Kafka. | `kafkaTemplate`                                              | `publish()`                                                  | Publica eventos consumidos por otros contextos (como notificaciones). |

#### 4.9.2.6 Bounded Context: Analytics & Reporting

El contexto acotado de **Analytics & Reporting** se encarga de estructurar el análisis retrospectivo del aire, consolidar métricas de telemetría en series temporales agregadas (diarias y mensuales), y generar los reportes de salubridad y dashboards interactivos. Utiliza técnicas de Server-Sent Events (SSE) para servir telemetría en tiempo real y programadores de tareas en segundo plano (*schedulers*) para consolidar reportes históricos.

**Diccionario de Clases del Contexto Analytics & Reporting**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                    | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                            | Relaciones de Asociación / Dependencia                       |
| :------------------------------------ | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------------------------------------------- | :----------------------------------------------------------- |
| **DeviceAnalyticsSnapshot**           | Dominio         | Entidad que almacena promedios ambientales calculados para un sensor en una ventana temporal (ej: 1 hora). | `id` (UUID), `deviceId` (DeviceId), `timeWindowStart` (Instant), `averageCo2` (Double), `calculatedAqi` (AirQualityIndex) | *N/A*                                                    | Contiene `DeviceId` y `AirQualityIndex`.                     |
| **DeviceDailySummary**                | Dominio         | Entidad raíz del agregado para reportes históricos consolidados de un día. | `id` (UUID), `deviceId` (DeviceId), `summaryDate` (LocalDate), `co2` (MetricStats), `pm2_5` (MetricStats), `averageAqi` (Integer) | *N/A*                                                    | Contiene `DeviceId`, `MetricStats` y `AqiCategoryBreakdown`. |
| **DeviceMonthlySummary**              | Dominio         | Entidad raíz del agregado para consolidados históricos por mes. | `id` (UUID), `deviceId` (DeviceId), `summaryMonth` (LocalDate), `daysCovered` (int) | *N/A*                                                    | Contiene `DeviceId` y `MetricStats`.                         |
| **MetricStats**                       | Dominio         | Objeto de Valor (*Value Object*) que agrupa estadísticas mínimas, máximas y promedio de una métrica. | `avg` (Double), `min` (Double), `max` (Double)               | *N/A*                                                    | Composición en los resúmenes diario y mensual.               |
| **AqiCategoryBreakdown**              | Dominio         | Objeto de Valor que segmenta la cantidad de horas en que el aire estuvo en cada estado de riesgo. | `good` (Long), `moderate` (Long), `hazardous` (Long)         | `plus()`, `dominant()`                                   | Composición en los resúmenes diario y mensual.               |
| **AirQualityIndex**                   | Dominio         | Objeto de Valor que encapsula la escala y categoría oficial de AQI (Índice de Calidad del Aire). | `value` (Double), `category` (AqiCategory)                   | *N/A*                                                    | Composición en `DeviceAnalyticsSnapshot`.                    |
| **AqiCalculationDomainService**       | Dominio         | Servicio de Dominio que implementa las fórmulas oficiales EPA para calcular el nivel de AQI. | *N/A*                                                        | `calculateAqi(pm2_5, co2)`                               | Utilizado por los generadores de reportes y schedulers.      |
| **DeviceAnalyticsSnapshotRepository** | Dominio         | Interfaz de repositorio para almacenar y recuperar snapshots temporales. | *N/A*                                                        | `save()`, `findByDeviceIdAndTimeWindowStartBetween()`    | Utilizado por servicios de consulta de tendencias.           |
| **AnalyticsController**               | Interfaz        | Controlador REST para servir streams en tiempo real vía SSE e históricos de tendencias. | `kpiDashboardMetricsQueryService`, `analyticsSseService`     | `getLiveMetrics()`, `streamLiveMetrics()`, `getTrends()` | Depende de los servicios de aplicación del dashboard.        |
| **ReportController**                  | Interfaz        | Controlador REST que exporta los resúmenes en formato de reportes diarios y mensuales. | `dailyReportQueryService`, `externalBillingService`          | `getDailyReport()`, `getMonthlyReport()`                 | Valida permisos llamando a `ExternalBillingService`.         |
| **KpiLiveMetricsCommandServiceImpl**  | Aplicación      | Servicio de aplicación que procesa la telemetría en caliente, refresca la caché y transmite vía SSE. | `kpiLiveMetricsCache`, `analyticsSseService`                 | `handle(ProcessTelemetryAnalyticCommand)`                | Actualiza la caché y activa difusión SSE.                    |
| **DailyReportAggregationService**     | Aplicación      | Generador programado por lotes que procesa lecturas diarias anteriores para emitir reportes históricos. | `dailySummaryRepository`, `aqiCalculationDomainService`      | `aggregatePreviousDay()`                                 | Ejecuta agregación SQL masiva e inserta reportes en PostgreSQL. |
| **TelemetryAnalyticKafkaConsumer**    | Aplicación      | Consumidor de Kafka que escucha la telemetría recibida para actualizar de forma asíncrona la caché KPI. | `kpiLiveMetricsCommandService`                               | `consume()`                                              | Transmite datos al procesador de métricas en vivo.           |
| **ExternalBillingService**            | Aplicación      | Interfaz (Puerto de comunicación inter-contexto) para validar límites del plan antes de servir reportes. | *N/A*                                                        | `canAccessMonthlyReports()`                              | Consumido por el `ReportController`.                         |
| **DeviceDailySummaryRepository**      | Infraestructura | Puerto (Interfaz de persistencia relacional) para guardar y buscar reportes de resumen diario. | *N/A*                                                        | `findByDeviceIdAndDate()`, `existsByDeviceIdAndDate()`   | Implementado en la capa de infraestructura.                  |

#### 4.9.2.7 Bounded Context: Analytics & Notifications

El contexto acotado de **Notifications** unifica el envío de mensajes a los usuarios a través de múltiples canales, incluyendo correos electrónicos transaccionales y notificaciones push en dispositivos móviles. Actúa como un módulo puramente utilitario y reactivo que responde a eventos disparados por otros contextos de la aplicación (como alertas críticas o códigos de registro).

**Diccionario de Clases del Contexto Notifications**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase                    | Capa            | Propósito / Responsabilidad                                  | Atributos Principales                                        | Métodos Clave                                                | Relaciones de Asociación / Dependencia                       |
| :------------------------------------ | :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **EmailLog**                          | Dominio         | Entidad que registra el historial, estado y errores de los envíos de correos electrónicos. | `id` (UUID), `recipient` (EmailRecipient), `subject` (EmailSubject), `content` (EmailContent), `status` (String), `sentAt` (Instant) | *N/A*                                                        | Contiene `EmailRecipient`, `EmailSubject` y `EmailContent`.  |
| **PushNotificationLog**               | Dominio         | Entidad que registra las notificaciones push despachadas a los dispositivos de los usuarios. | `id` (UUID), `userId` (UUID), `title` (String), `message` (String), `status` (String), `sentAt` (Instant), `externalId` (String) | *N/A*                                                        | Vinculado a `UserId` por ID.                                 |
| **EmailDeliveryService**              | Dominio         | Interfaz (Puerto) que define la firma técnica para despachar correos electrónicos. | *N/A*                                                        | `send()`                                                     | Implementado por `SmtpEmailService` o adaptadores externos.  |
| **PushNotificationDeliveryService**   | Dominio         | Interfaz (Puerto) que define el envío de alertas push directas al smartphone. | *N/A*                                                        | `sendPush()`                                                 | Implementado por `OneSignalPushNotificationService`.         |
| **EmailRecipient**                    | Dominio         | Objeto de Valor (*Value Object*) para encapsular la dirección de correo destinataria. | `value` (String)                                             | *N/A*                                                        | Composición en `EmailLog`.                                   |
| **EmailSubject**                      | Dominio         | Objeto de Valor que encapsula el asunto o título del correo. | `value` (String)                                             | *N/A*                                                        | Composición en `EmailLog`.                                   |
| **EmailContent**                      | Dominio         | Objeto de Valor para el cuerpo y formato del correo.         | `value` (String)                                             | *N/A*                                                        | Composición en `EmailLog`.                                   |
| **EmailLogRepository**                | Dominio         | Interfaz de persistencia para auditar el historial de emails enviados. | *N/A*                                                        | `save()`                                                     | Utilizado por `EmailCommandServiceImpl`.                     |
| **PushNotificationLogRepository**     | Dominio         | Interfaz de persistencia para auditar las alertas push.      | *N/A*                                                        | `save()`                                                     | Utilizado por `AlertIncidentChangedKafkaConsumer`.           |
| **NotificationController**            | Interfaz        | Controlador REST utilitario para realizar tests rápidos de conectividad y envíos. | *N/A*                                                        | `testEmail()`                                                | Depende de `EmailCommandServiceImpl`.                        |
| **NotificationsContextFacade**        | Interfaz        | Fachada expuesta internamente para ordenar envíos rápidos de emails de verificación. | *N/A*                                                        | `sendVerificationCode()`                                     | Implementado por `NotificationsContextFacadeImpl`.           |
| **EmailCommandServiceImpl**           | Aplicación      | Servicio de aplicación que procesa comandos de envío de correos (código, bienvenida). | `emailDeliveryService`, `emailLogRepository`                 | `handle(SendVerificationCodeCommand)`, `handle(SendWelcomeEmailCommand)` | Usa `EmailDeliveryService` y `EmailLogRepository`.           |
| **AlertIncidentChangedKafkaConsumer** | Aplicación      | Consumidor asíncrono de Kafka que escucha cambios en incidentes de alertas para despachar notificaciones push. | `pushNotificationDeliveryService`, `externalDeviceService`, `externalAlertingService` | `consume()`                                                  | Resuelve detalles de hardware e incidentes y envía push a través del SDK. |
| **SmtpEmailService**                  | Infraestructura | Adaptador concreto que despacha correos utilizando SMTP local o servidor de correo de Spring. | `mailSender`                                                 | `send()`                                                     | Implementa `EmailDeliveryService`.                           |
| **OneSignalPushNotificationService**  | Infraestructura | Adaptador que implementa `PushNotificationDeliveryService` utilizando la API de OneSignal. | `oneSignalApiKey`                                            | `sendPush()`                                                 | Implementa `PushNotificationDeliveryService`.                |

## 4.10. Database Design.

### 4.10.1. Relational/Non-Relational Database Diagram.

Dado que la arquitectura del backend sigue un enfoque de monolito modular, todos los Bounded Contexts comparten una única base de datos relacional PostgreSQL. El siguiente diagrama presenta el diseño completo de la base de datos, incluyendo las tablas, columnas, tipos de datos, constraints (primary keys, foreign keys) y las relaciones entre tablas que permiten la persistencia de información para los contextos del sistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/database/database.png" alt="Bounded Context Database Design Diagram - Analytics and Reporting" width="850">
</p>
