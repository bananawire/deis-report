# Part II: Verification, Validation & Pipeline

# Capítulo VI: Product Verification & Validation

## 6.1. Testing Suites & Validation

El backend de Clair Core (`clair-core`, Spring Boot 3.5.5 con Java 25) se prueba con cuatro suites. Las de Unit e Integration Tests corren dentro de la JVM con H2 en memoria, así que no necesitan Docker. Las de BDD y System Tests levantan la aplicación en un puerto real contra PostgreSQL y Redis, y la prueban por HTTP. Todas se ejecutan con `nix-shell --run "mvn test"` y cada prueba está asociada a una User Story (WS-US) del backlog.

| Suite | Nivel | Aísla | Tecnología | Pruebas |
|---|---|---|---|---|
| Unit Tests | Dominio | Sin Spring ni base de datos | JUnit 5 + Mockito | 49 (5 clases) |
| Integration Tests | Servicios de aplicación y persistencia, entre bounded contexts | Spring real sobre H2; solo se mockean los servicios externos | `@SpringBootTest` + JPA + `@MockitoBean` | 15 (5 clases) |
| Behavior-Driven Development | Especificación de negocio | TBD | TBD | TBD |
| System Tests | Sistema completo | TBD | TBD | TBD |

Convenciones que siguen todas las pruebas, según la rúbrica:

- La clase y cada prueba tienen un `@DisplayName` en español.
- El cuerpo sigue el patrón AAA, marcado con los comentarios `// Arrange`, `// Act` y `// Assert`.
- Cada prueba explica qué regla de negocio protege con un comentario `// Business / User Story Rational (WS-US-xx): ...`.
- No se prueban las validaciones de DTO (`@Valid`, bean validation). Se prueban las invariantes de los agregados y las reglas de negocio.
- Las suites se agregaron como clases nuevas, sin modificar las pruebas que ya tenía el proyecto ni el código de `src/main`. Tampoco se crearon migraciones ni seeds: cada prueba arma sus datos en el `Arrange`.

Las suites de Unit e Integration Tests cubren los bounded contexts IAM, Device, Evaluation, Alerting y Billing.

### 6.1.1. Core Entities Unit Tests.

Estas pruebas instancian los agregados y value objects del dominio directamente, sin contexto de Spring y sin base de datos. Algunas reglas no están en el agregado sino en su command service, como la severidad de una alerta o el límite de espacios del plan. En esos casos (`AlertUnitTest`, `OrganizationSpaceUnitTest` y `DeviceThresholdUnitTest`) se instancia el service con sus repositorios y dependencias externas reemplazados por mocks de Mockito. Cada clase tiene entre 9 y 10 pruebas y cubre las ocho categorías de la rúbrica: happy path, límite superior, límite inferior, datos insuficientes, estado inválido, condicional A, condicional B e integridad.

Ubicación: `src/test/java/com/claircore/<contexto>/unit/<Contexto>UnitTest.java`.

**`DeviceUnitTest`** (Device, 10 pruebas, WS-US-10 a WS-US-16)

Prueba los agregados `Device` y `DeviceAssignment` y los value objects `HardwareId` y `ClaimToken`.

| Categoría | Prueba | US |
|---|---|---|
| Happy | Reclamar un dispositivo emparejado lo asigna al espacio y al usuario | WS-US-11 |
| Límite superior | Un evento de presencia más de 5 minutos en el futuro es rechazado | WS-US-14 |
| Límite inferior | Un evento de presencia igual o anterior al último aplicado se ignora | WS-US-14 |
| Datos insuficientes | Un Hardware ID con formato inválido es rechazado | WS-US-10 |
| Estado inválido | Un dispositivo ya reclamado no puede reclamarse otra vez | WS-US-11 |
| Estado inválido | Renombrar un dispositivo con un nombre en blanco es rechazado | WS-US-15 |
| Condicional A | Un evento OFFLINE siempre cambia el estado, aunque el dispositivo esté en STANDBY | WS-US-14 |
| Condicional B | Un evento ONLINE no saca al dispositivo de STANDBY, solo refresca `lastSeenAt` | WS-US-14 |
| Integridad | Restablecer el nombre devuelve el nombre de fábrica | WS-US-16 |
| Integridad | Marcar un dispositivo en línea registra su estado y su `lastSeenAt` | WS-US-14 |

![DeviceUnitTest](../assets/testing/DeviceUnitTest.jpeg)

Las 10 pruebas pasan. Cinco de ellas tratan el estado de conexión, porque los eventos de presencia llegan desde el borde y pueden venir repetidos, desordenados o con el reloj adelantado.

**`OrganizationSpaceUnitTest`** (Device, 10 pruebas, WS-US-24 a WS-US-33)

Prueba los agregados `Organization` y `Space`.

| Categoría | Prueba | US |
|---|---|---|
| Happy | Crear una organización la deja asociada a su dueño | WS-US-24 |
| Límite superior | Con el plan que permite 1 espacio, crear el segundo es rechazado | WS-US-46 |
| Límite inferior | Un nombre de organización de un solo carácter es aceptado | WS-US-24 |
| Datos insuficientes | Crear una organización sin nombre es rechazado | WS-US-24 |
| Estado inválido | Eliminar un espacio con sensores registrados es rechazado | WS-US-32 |
| Estado inválido | Un espacio sin organización no puede existir | WS-US-29 |
| Estado inválido | Crear un espacio sin dueño es rechazado | WS-US-29 |
| Condicional A | Renombrar un espacio con un nombre válido actualiza solo el nombre | WS-US-33 |
| Condicional B | Un nombre en blanco para el espacio se rechaza antes de llegar al agregado | WS-US-33 |
| Integridad | Dos espacios de la misma organización tienen identidades distintas | WS-US-31 |

![OrganizationSpaceUnitTest](../assets/testing/OrganizationSpaceUnitTest.jpeg)

Las 10 pruebas pasan. El límite superior depende del plan del usuario y no de una constante del agregado: con un plan de un solo espacio, el segundo `CreateSpaceCommand` se rechaza.

**`DeviceThresholdUnitTest`** (Device, 10 pruebas, WS-US-17 a WS-US-20)

Prueba el value object `MetricThreshold` y la clase `DeviceMetricThresholdConfiguration`, que guarda los umbrales dentro de `DeviceAssignment`.

| Categoría | Prueba | US |
|---|---|---|
| Happy | Un umbral de PM2.5 válido queda configurado y habilitado | WS-US-18 |
| Límite superior | Un umbral de CO2 muy alto (5000 ppm) es aceptado | WS-US-18 |
| Límite inferior | Un umbral exactamente en cero es aceptado | WS-US-18 |
| Límite inferior | Un umbral negativo es rechazado | WS-US-18 |
| Datos insuficientes | Un umbral sin métrica es rechazado | WS-US-18 |
| Estado inválido | Registrar un umbral para una métrica que ya tiene uno es rechazado | WS-US-18 |
| Condicional A | Un umbral deshabilitado conserva su valor configurado | WS-US-19 |
| Condicional B | La intención UPDATE se conserva en el comando de escritura | WS-US-19 |
| Integridad | Agregar y quitar la configuración de un umbral deja la asignación sin él | WS-US-20 |
| Integridad | La etiqueta y la unidad de cada métrica son las que ve el usuario | WS-US-17 |

![DeviceThresholdUnitTest](../assets/testing/DeviceThresholdUnitTest.jpeg)

Las 10 pruebas pasan. El límite inferior se prueba por los dos lados: cero se acepta y un valor negativo se rechaza.

**`AlertUnitTest`** (Alerting, 9 pruebas, WS-US-34, WS-US-36 y WS-US-49)

Prueba el agregado `Alert` y la regla que asigna la severidad (`AlertSeverity`) al evaluar una lectura de telemetría.

| Categoría | Prueba | US |
|---|---|---|
| Happy | Una alerta nueva nace ACTIVA con los valores de la lectura | WS-US-34 |
| Límite superior | Una lectura de 1.5 veces el umbral es CRITICAL | WS-US-49 |
| Límite inferior | Una lectura exactamente igual al umbral abre una alerta LOW | WS-US-49 |
| Datos insuficientes | Una lectura sin todas sus métricas no puede evaluarse | WS-US-49 |
| Estado inválido | Una métrica con una alerta ya abierta no abre una segunda alerta | WS-US-36 |
| Condicional A | Una lectura entre 1.2 y 1.5 veces el umbral es WARNING | WS-US-49 |
| Condicional B | Una lectura justo debajo de 1.2 veces el umbral sigue siendo LOW | WS-US-49 |
| Integridad | Resolver una alerta registra su cierre y conserva los valores originales | WS-US-36 |
| Integridad | El mensaje de la alerta muestra la métrica, el valor leído y el umbral con su unidad | WS-US-34 |

![AlertUnitTest](../assets/testing/AlertUnitTest.jpeg)

Las 9 pruebas pasan. Los cortes de severidad se prueban en sus valores exactos: una lectura igual al umbral es LOW, desde 1.2 veces el umbral es WARNING y desde 1.5 veces es CRITICAL.

**`IamUnitTest`** (IAM, 10 pruebas, WS-US-01 a WS-US-04)

Prueba los agregados `User` y `RegistrationSession` y los value objects `VerificationCode`, `Password` y `EmailAddress`.

| Categoría | Prueba | US |
|---|---|---|
| Happy | Confirmar el registro activa al usuario | WS-US-02 |
| Límite superior | Un código válido justo antes de expirar todavía se acepta | WS-US-02 |
| Límite inferior | Un código correcto pero ya expirado es rechazado | WS-US-02 |
| Datos insuficientes | Un correo vacío no permite crear la cuenta | WS-US-01 |
| Datos insuficientes | Un código de verificación con formato inválido es rechazado | WS-US-02 |
| Estado inválido | Un usuario registrado con correo queda pendiente de verificación | WS-US-03 |
| Condicional A | Un usuario creado con correo y contraseña no es usuario OAuth | WS-US-03 |
| Condicional B | Un usuario creado con Google nace activo y es usuario OAuth | WS-US-04 |
| Integridad | Un código distinto al enviado no verifica la sesión | WS-US-02 |
| Integridad | Vincular Google a una cuenta existente conserva su correo e identidad | WS-US-04 |

![IamUnitTest](../assets/testing/IamUnitTest.jpeg)

Las 10 pruebas pasan. Las condicionales separan los dos tipos de cuenta: la creada con correo queda pendiente hasta confirmar el código, y la creada con Google nace activa porque Google ya verificó el correo.

### 6.1.2. Core Integration Tests.

Estas pruebas levantan el contexto completo de Spring con `@SpringBootTest` y usan los command services, query services y repositorios JPA reales sobre H2 en memoria. Cada prueba pasa por al menos dos capas o dos bounded contexts. Llaman a los services y no a los controllers, porque los controllers ya están cubiertos por las pruebas `@WebMvcTest` del proyecto.

Ubicación: `src/test/java/com/claircore/integration/`.

La suite se apoya en dos piezas:

- El perfil `it` (`src/test/resources/application-it.properties`) usa H2 en memoria, desactiva Flyway y genera el esquema con `ddl-auto=create-drop`. También apaga el local edge y los jobs en segundo plano, que escribirían datos mientras corre una prueba, y pone valores ficticios para JWT, Google, Stripe y OneSignal.
- La clase base `AbstractIntegrationTest` activa ese perfil y reemplaza con `@MockitoBean` solo lo que sale del proceso: las sesiones de IAM guardadas en Redis (`TokenSessionRepository`, `RegistrationSessionRepository`), el pago con Stripe (`PaymentGateway`), el envío de correos y notificaciones push (`EmailDeliveryService`, `PushNotificationDeliveryService`, `AsyncNotificationService`) y Google OAuth (`GoogleTokenVerifier`, `GoogleTokenExchange`). La caché, que en producción usa Redis, se cambia por un `NoOpCacheManager`.

La clase base no lleva `@Transactional`. Los handlers que conectan un contexto con otro escuchan en `AFTER_COMMIT`, y si la prueba hiciera rollback nunca se ejecutarían. Por eso las tablas se vacían en un `@AfterEach` después de cada prueba.

En las capturas, cada ejecución tarda entre 12 y 16 segundos. Casi todo ese tiempo es el arranque del contexto de Spring; las pruebas de cada clase suman menos de 600 ms.

**`DeviceClaimIntegrationTest`**

| Contexto | Prueba | Verifica | US |
|---|---|---|---|
| Device | Un dispositivo emparejado y reclamado aparece en el listado de su espacio | El pair y el claim se persisten y la query del espacio los devuelve | WS-US-10, WS-US-11, WS-US-12 |
| Device | El código de reclamo se consume: no se puede volver a usar para otro usuario | El `ClaimToken` es de un solo uso | WS-US-11 |
| Device + Billing | Con plan Freemium, Billing limita a 1 el número de dispositivos reclamados | Device consulta a Billing el límite del plan antes de aceptar el reclamo | WS-US-11, WS-US-46 |

![DeviceClaimIntegrationTest](../assets/testing/DeviceClaimIntegrationTest.jpeg)

Las 3 pruebas pasan. La tercera es la que cruza contextos: el segundo reclamo de un usuario Freemium falla por el límite que devuelve Billing.

**`MultiTenantIntegrationTest`**

| Contexto | Prueba | Verifica | US |
|---|---|---|---|
| Device | El dueño ve su organización, su espacio y su dispositivo persistidos | Las queries `...ForUserQuery` devuelven los recursos propios | WS-US-25, WS-US-30, WS-US-13 |
| Device | Otro usuario no puede leer la organización, el espacio ni el dispositivo ajenos | Las mismas queries no devuelven nada a un usuario distinto del dueño | WS-US-25, WS-US-30, WS-US-13 |
| Device | Listar los dispositivos de un espacio ajeno es denegado | Solo el dueño del espacio puede listar sus sensores | WS-US-12 |

![MultiTenantIntegrationTest](../assets/testing/MultiTenantIntegrationTest.jpeg)

Las 3 pruebas pasan. Se crean los recursos con un usuario y se consultan con otro, sobre los mismos datos persistidos.

**`DowngradeIntegrationTest`**

| Contexto | Prueba | Verifica | US |
|---|---|---|---|
| Billing (fachada) | Un pago confirmado sube el plan a Premium y los otros contextos ven los límites nuevos | Tras confirmar el pago, el plan queda en Premium y `BillingContextFacade` devuelve 10 dispositivos y acceso a reportes mensuales | WS-US-48, WS-US-46 |
| Billing (fachada) | Degradar a Freemium persiste el plan y reduce los límites que ven los otros contextos | El plan vuelve a Freemium y la fachada devuelve 1 dispositivo y sin reportes mensuales | WS-US-47 |
| Billing | Degradar a un usuario sin plan registrado es rechazado | Solo se degrada un plan que existe | WS-US-47 |

![DowngradeIntegrationTest](../assets/testing/DowngradeIntegrationTest.jpeg)

Las 3 pruebas pasan. Los límites se leen a través de `BillingContextFacade` porque Device y Analytics consultan el plan por esa fachada, desde sus adaptadores `ExternalBillingService`.

**`TelemetryAlertIntegrationTest`**

| Contexto | Prueba | Verifica | US |
|---|---|---|---|
| Device + Evaluation + Alerting | Una lectura de PM2.5 por encima del umbral abre una alerta CRITICAL para el dispositivo | El `TelemetryRecordedIntegrationEvent` de Evaluation activa el handler de Alerting, que compara la lectura con el umbral configurado en Device y guarda la alerta | WS-US-18, WS-US-49, WS-US-34 |
| Evaluation + Alerting | Una lectura por debajo del umbral no abre ninguna alerta | Con aire limpio no se generan alertas falsas | WS-US-49, WS-US-34 |
| Evaluation + Alerting | Una lectura posterior por debajo del umbral resuelve la alerta abierta | La alerta se cierra sola cuando la lectura vuelve a estar bajo el umbral | WS-US-36, WS-US-49 |

![TelemetryAlertIntegrationTest](../assets/testing/TelemetryAlertIntegrationTest.jpeg)

Las 3 pruebas pasan. El evento de telemetría se publica dentro de una transacción para que el handler, que escucha en `AFTER_COMMIT`, se ejecute igual que en producción.

**`UserPlanIntegrationTest`**

| Contexto | Prueba | Verifica | US |
|---|---|---|---|
| IAM + Billing | Registrar y confirmar una cuenta persiste al usuario activo y Billing le asigna Freemium | Al confirmar el registro, `UserRegisteredEventHandler` crea el plan Freemium del usuario | WS-US-01, WS-US-02, WS-US-46 |
| IAM + Billing | Un código de verificación incorrecto no crea usuario ni plan | Si el registro no se confirma, no se guarda nada en IAM ni en Billing | WS-US-02 |
| IAM | Un correo ya registrado no puede iniciar un segundo registro | Un correo identifica a una sola cuenta | WS-US-01 |

![UserPlanIntegrationTest](../assets/testing/UserPlanIntegrationTest.jpeg)

Las 3 pruebas pasan. La segunda revisa los dos contextos a la vez: con un código incorrecto no queda un usuario sin plan ni un plan sin usuario.

### 6.1.3. Core Behavior-Driven Development

### 6.1.4. Core System Tests.







**“This will be included in the next submission.”**

## 6.2. Static testing & Verification

### 6.2.1. Static Code Analysis

#### 6.2.1.1. Coding standard & Code conventions.

#### 6.2.1.2. Code Quality & Code Security.

### 6.2.2. Reviews

## 6.3. Validation Interviews.

### 6.3.1. Diseño de Entrevistas.

## 6.3.2. Registro de Entrevistas.

### 6.3.3. Evaluacionessegún heurísticas.

## 6.4. Auditoría de Experiencias de Usuario

### 6.4.1. Auditoría realizada.

#### 6.4.1.1. Información del grupo auditado.

#### 6.4.1.2. Cronograma de auditoría realizada.

#### 6.4.1.3. Contenido de auditoría realizada.

## 6.4.2. Auditoría recibida.

#### 6.4.2.1. Información del grupo auditor.

#### 6.4.2.2. Cronograma de auditoría recibida.

#### 6.4.2.3. Contenido de auditoría recibida.

#### 6.4.2.4. Resumen de modificaciones para subsanar hallazgos.