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

A continuación, se presentan los wireframes y mock-ups para la Landing Page de Clair, enfocada en comunicar de manera efectiva la propuesta de valor del producto y guiar al visitante hacia la conversión.

### 4.3.1. Landing Page Wireframe.

**Home**

<img src="../assets/landing-page-wireframes/WF-Home.png" alt="WF-Home" width="1000">

Presentación principal de Clair Alpha. Este esquema define la jerarquía principal del sitio. En la parte superior, se establece un Hero Section con mensajes claros y botones de conversión inmediata.

La sección central de Sensory Intelligence utiliza una estructura de tres columnas para presentar las métricas clave (PM2.5, CO₂ e Índice de Aire), permitiendo que el usuario entienda el valor del monitoreo de un vistazo. Finaliza con bloques de imagen y texto alternados para explicar la integración del dispositivo en espacios físicos.

**Product**

<img src="../assets/landing-page-wireframes/WF-Product.png" alt="WF-Product" width="1000">

Detalle técnico y funcional del dispositivo. Se enfoca en la arquitectura técnica del dispositivo. Utiliza un layout de rejilla (grid) para organizar las "Clair Specs", donde cada tarjeta contiene un icono, un título y una descripción breve. Este diseño está pensado para descomponer conceptos complejos (como sensores láser o procesamiento de datos) en fragmentos de información digeribles. Incluye un pie de página con un CTA de refuerzo para incentivar la compra tras leer las especificaciones.

**Pricing**

<img src="../assets/landing-page-wireframes/WF-Pricing.png" alt="WF-Pricing" width="1000">

Estructura de costos de los servicios de Clair Alpha. La estructura está diseñada para facilitar la comparativa de servicios. Presenta dos contenedores principales que separan el plan gratuito del plan avanzado ("Mesh Network").

Cada contenedor detalla mediante una lista de viñetas las funcionalidades incluidas, permitiendo al usuario diferenciar rápidamente entre el monitoreo local y la gestión centralizada multidispositivo. Además, el diseño ofrece una visualización limpia de los costos.

**About**

<img src="../assets/landing-page-wireframes/WF-About.png" alt="WF-About" width="1000">

Sección dedicada a la visión de la empresa y el equipo. En la parte inferior, se reserva un espacio para el "Clair Team", organizando al equipo por etiquetas funcionales (Ingeniería, Diseño, Investigación) para proyectar confianza y multidisciplinariedad.

### 4.3.2. Landing Page Mock-up.

**Home**

<img src="../assets/landing-page-mockups/Home.png" alt="MP-Home" width="1000">

Implementación visual final con un estilo minimalista y tecnológico. Se sustituyen los contenedores vacíos por imágenes fotorrealistas que muestran el dispositivo integrado en oficinas.

Los indicadores de calidad del aire ahora incluyen micro-interacciones visuales, como anillos de progreso y estados de color (verde para "Pristine Air"), que permiten una lectura intuitiva y rápida del estado ambiental.

**Product**

<img src="../assets/landing-page-mockups/Product.png" alt="MP-Product" width="1000">

Diseño detallado que muestra los componentes internos del ecosistema. Se detallan los componentes internos mediante una tipografía Space Grotesk y un espaciado amplio que evita la saturación visual.

Se han integrado los nombres específicos de los sensores (SCD41 y PMS5003) para dar credibilidad técnica al producto.

**Pricing**

<img src="../assets/landing-page-mockups/Pricing.png" alt="MP-Pricing" width="1000">

Interfaz de suscripción con un enfoque limpio y directo. Se utilizan tarjetas con bordes definidos y botones de acción claros. Los iconos de moneda y los botones de compra (CTA) siguen una estética de alto contraste (blanco sobre negro), asegurando que el proceso de selección de plan sea visualmente directo y libre de distracciones.

**About**

<img src="../assets/landing-page-mockups/About.jpg" alt="MP-About" width="1000">

Este mock-up utiliza la fotografía de alto impacto como eje central para conectar emocionalmente con el usuario. La sección presenta al equipo multidisciplinario con un diseño elegante que equilibra el espacio en blanco y el contenido textual.

## 4.4. Mobile Applications UX/UI Design.

Esta sección está dedicada al diseño de la experiencia de usuario (UX) y la interfaz de usuario (UI) de la aplicación móvil que forma parte de la solución Clair. El objetivo es crear interfaces funcionales, accesibles y visualmente coherentes que respondan a las necesidades y expectativas de los usuarios finales en un entorno mobile-first.

### 4.4.1. Mobile Applications Wireframes.

En esta sección se presentan los wireframes de la aplicación móvil, los cuales muestran el diseño estructural y la disposición de los elementos clave para la experiencia de usuario en dispositivos móviles.

**Login**

<img src="../assets/mobileapp-wf/WF-LOGIN.png" alt="wf-Login" width="300">

La interfaz de autenticación móvil adopta un diseño vertical y centrado, adaptado a la ergonomía del pulgar. El wireframe simplifica los elementos a un campo de correo electrónico, un botón de acción primario ("Login") de alto contraste y un enlace textual para el registro de nuevos usuarios. Este enfoque minimalista reduce la carga cognitiva y acelera el acceso a la plataforma, manteniendo la estética limpia y tecnológica característica de Clair en un entorno mobile-first.

**Register**

<img src="../assets/mobileapp-wf/WF-REGISTER.png" alt="wf-Register" width="300">

El flujo de registro en dispositivos móviles prioriza la eficiencia y la seguridad mediante una estructura de pasos clara. El wireframe incorpora campos de entrada para correo electrónico y contraseña, acompañados de un componente de verificación (checkbox) para la aceptación de términos legales. Adicionalmente, se integran botones de autenticación con Google para facilitar el proceso, culminando con un enlace de navegación para usuarios ya registrados, todo ello dentro de un contenedor de bordes redondeados que sugiere una interfaz amigable y moderna.

**Dashboard**

<img src="../assets/mobileapp-wf/WF-DASHBOARD.png" alt="wf-Dashboard" width="300">

La pantalla principal de la aplicación presenta un panel de control resumido pero altamente informativo, ideal para la supervisión rápida del estado ambiental desde un dispositivo móvil.

**Sensor Selection**

<img src="../assets/mobileapp-wf/WF-SENSOR-SELECTION.png" alt="wf-Sensor-Selection" width="300">

La interfaz de selección de ubicación o dispositivo utiliza un patrón de navegación jerárquica común en móviles: una lista de selección que ocupa la mayor parte de la pantalla. Este patrón modal o de pantalla dedicada guía al usuario a través de la estructura física de la organización (Edificio → Piso) antes de visualizar datos específicos, reduciendo la complejidad y enfocando la atención en la decisión actual.

**Sensor Detail**

<img src="../assets/mobileapp-wf/WF-SENSOR.png" alt="wf-Sensor" width="300">

La vista de detalle de un sensor específico concentra la información técnica más relevante en una sola pantalla optimizada para consultas rápidas. Este diseño de alta densidad de información, pero visualmente ordenado, permite a los técnicos y administradores evaluar el estado operativo de un sensor de forma inmediata desde su dispositivo móvil.

**Settings**

<img src="../assets/mobileapp-wf/WF-SETTINGS.png" alt="wf-Settings" width="300">

La pantalla de configuración sigue el estándar de plataformas móviles (iOS/Android) mediante una vista de lista desplazable (table view) agrupada por categorías funcionales. La presencia de un botón de "LOGOUT" claramente diferenciado al final de la lista refuerza las normas de usabilidad y seguridad en aplicaciones móviles, ofreciendo un control total sobre la sesión del usuario.

**Alerts**

<img src="../assets/mobileapp-wf/WF-ALERTS.png" alt="wf-Alerts" width="300">

La pantalla de alertas consolida las notificaciones generadas por el sistema Clair, organizadas por niveles de prioridad para facilitar la atención diferenciada por parte del usuario. Cada alerta presenta un encabezado descriptivo, un mensaje contextual y un par de acciones rápidas que permiten responder de manera inmediata o ignorar la notificación. Refleja una arquitectura de notificaciones que equilibra la urgencia operativa con el mantenimiento programado, siguiendo las mejores prácticas de diseño de centros de control y monitoreo en aplicaciones móviles industriales o de seguridad.

### 4.4.2. Mobile Applications Wireflow Diagrams.

Esta sección presenta los diagramas de flujo (wireflows) de la aplicación móvil, que ilustran la navegación y las interacciones del usuario entre las diferentes pantallas, facilitando la comprensión del recorrido dentro del sistema.

**User Goals**

| ID | User Goal | Descripción operativa |
|:---:|:---|:---|
| **UG01** | Garantizar la salud ambiental | Mantener un aire fresco y libre de viciamento para que los clientes permanezcan más tiempo en el local. |
| **UG04** | Controlar síntomas crónicos | Reducir la frecuencia de episodios de rinitis alérgica, asma o dolores de cabeza asociados al ambiente cargado. |
| **UG06** | Crear un refugio seguro | Garantizar que, a pesar de la contaminación exterior de la ciudad, el interior de su hogar sea un espacio de respiración pura. |

**Wireflow: Gestión de alertas y activación de respuestas**

**User Goals cubiertos:**

| ID | User Goal |
|:---|:---|
| UG01 | Garantizar la salud ambiental: Mantener un aire fresco y libre de viciamento para que los clientes permanezcan más tiempo en el local |
| UG04 | Controlar síntomas crónicos: Reducir la frecuencia de episodios de rinitis alérgica, asma o dolores de cabeza asociados al ambiente cargado |

El usuario ingresa a la aplicación y visualiza el Dashboard principal, donde se muestran los indicadores de calidad del aire en tiempo real y el estado general por zonas. El sistema monitorea continuamente los sensores y, cuando detecta una condición crítica (UG01: CO₂/VOC elevado) o la superación de un umbral personalizado configurado desde la Web App (UG04), genera una notificación emergente en la parte superior de la pantalla.

El usuario ingresa a la lista de alerts mediante un tap en el ícono de campana o directamente en la notificación, accediendo a la pantalla Alerts donde la alerta aparece destacada con información contextual. El sistema muestra cada alerta con título, mensaje y botones de acción ("Activar respuesta" si está configurada, "Descartar", "Ver más").

Si el usuario realiza tap en el botón "Activar respuesta" correspondiente a la alerta, siempre que la acción haya sido preconfigurada desde la Web App, el sistema ejecuta la acción correctiva de inmediato (por ejemplo, activar ventilación o enviar notificación al administrador), muestra un toast o snackbar de confirmación y marca la alerta como "En proceso" o "Resuelta". Opcionalmente, el usuario puede tap en "Descartar" o "Recordar más tarde", en cuyo caso la alerta se archiva o se programa para reaparecer después de un tiempo definido.

UG01 y UG04 comparten el mismo wireflow para Mobile Application, ya que ambos flujos se detonan por una alerta automática o preventiva y conducen a la misma pantalla Alerts para la gestión de la respuesta. La diferencia radica en el origen de la regla: UG01 responde a reglas por defecto del sistema, mientras que UG04 responde a reglas personalizadas configuradas desde Web App. En ambos casos, la experiencia de usuario en mobile es idéntica.

<img src="../assets/mobileapp-wireflows/mobileapp-wflow1.png" alt="mobileapp-wflow1" width="600">

**Wireflow: Verificación de calidad del aire (Refugio seguro)**

**User Goals cubiertos:**

| ID | User Goal |
|:---|:---|
| UG06 | Crear un refugio seguro: Garantizar que, a pesar de la contaminación exterior de la ciudad, el interior de su hogar sea un espacio de respiración pura |

El usuario ingresa a la aplicación y visualiza el Dashboard principal. En esta pantalla, el sistema muestra los indicadores de calidad del aire (CO₂, VOC, temperatura, humedad), el estado general por zonas y el indicador AQI (Bueno/Moderado/Malo). El usuario visualiza el AQI y los valores de los sensores directamente en el Dashboard.

El sistema presenta el estado actual del aire, indicando si es saludable o no. Al observar que los indicadores están dentro de rangos saludables y que el AQI es "Bueno" o "Moderado", el usuario confirma que su hogar es un "refugio seguro", es decir, un espacio de respiración pura a pesar de la contaminación exterior del entorno urbano.

UG06 en Mobile se resuelve íntegramente en el Dashboard, ya que esta pantalla muestra el AQI y los valores de calidad del aire en tiempo real. No existe funcionalidad equivalente al widget de cumplimiento OMS en la versión mobile de Reports. El usuario valida que su hogar es un refugio seguro al observar indicadores saludables en el Dashboard.

<img src="../assets/mobileapp-wireflows/mobileapp-wflow2.png" alt="mobileapp-wflow2" width="340">

### 4.4.3. Mobile Applications Mock-ups.

**Login**

<img src="../assets/mobileapp-mockup/LOGIN.png" alt="LOGIN" width="300">

La pantalla de autenticación presenta una implementación visual final de estilo sobrio y corporativo, con fondo oscuro uniforme y el logotipo de Clair centrado en la parte superior. El mock-up dispone campos de entrada de bordes redondeados con etiquetas flotantes o internas, acompañados de un botón de acción primaria ("Login") de color de contraste moderado que ocupa el ancho completo. Un enlace textual secundario ("Register") permite la navegación al flujo de creación de cuenta, manteniendo una estética limpia, profesional y alineada con la identidad tecnológica de la marca en el ecosistema móvil.

**Register**

<img src="../assets/mobileapp-mockup/REGISTER.png" alt="mobile-register" width="300">

La interfaz de registro mantiene la coherencia visual con la pantalla de login, utilizando un fondo oscuro y una tarjeta central que organiza el contenido de forma vertical. El mock-up integra campos de entrada para correo electrónico y contraseña, este último con un indicador visual de caracteres enmascarados, acompañados de un componente de verificación para la aceptación de términos y condiciones. El botón de registro principal se complementa con una opción de autenticación con Google mediante un contenedor secundario. Finalmente, un enlace "Login" dirige a los usuarios ya registrados, completando un flujo de alta eficiente y visualmente consistente.

**Air Quality**

<img src="../assets/mobileapp-mockup/AIRQUALITY.png" alt="mobile-dashboard" width="300">

La pantalla de calidad del aire ofrece una visión centralizada y altamente legible del estado ambiental actual. En la parte superior, selectores desplegables permiten filtrar los datos por organización, espacio y dispositivo específico, lo cual se complementa con un indicador visual del "Air Quality Index" que clasifica la calidad del aire como "GOOD" con una puntuación numérica. Debajo, se despliegan tarjetas individuales para variables clave como material particulado (PM2.5), CO₂, temperatura y humedad, cada una con su valor actual y un indicador de estado. Finalmente, la sección de "Thresholds" proporciona una referencia clara de los límites operativos configurados para cada parámetro.

**Sensor Selection**

<img src="../assets/mobileapp-mockup/SENSOR-SELECTION1.png" alt="mobile-sensor-selection" width="300">

<img src="../assets/mobileapp-mockup/SENSOR-SELECTION2.png" alt="mobile-sensor-selection" width="300">

<img src="../assets/mobileapp-mockup/SENSOR-SELECTION3.png" alt="mobile-sensor-selection" width="300">

La estructura de selección de sensores en Clair sigue una jerarquía de navegación lógica, diseñada para gestionar grandes despliegues de infraestructura de forma intuitiva. El sistema guía al usuario a través de niveles de agregación progresiva: desde el despliegue general de organizaciones, pasando por edificios específicos y niveles de planta, hasta llegar a la gestión individual de los dispositivos. Esta arquitectura jerárquica permite al usuario alternar entre vistas de cuadrícula (grid) y lista, proporcionando flexibilidad visual para monitorear el estado operativo y la última actividad de múltiples dispositivos simultáneamente.

**Sensor Detail**

<img src="../assets/mobileapp-mockup/SENSOR1.png" alt="mobile-sensor-detail" width="300">

<img src="../assets/mobileapp-mockup/SENSOR2.png" alt="mobile-sensor-detail" width="300">

La interfaz de detalle del sensor "Clair-01" proporciona un diagnóstico técnico integral y una capacidad de configuración precisa del entorno monitorizado. La vista principal despliega métricas de estado operativo como conectividad, tiempo de actividad (uptime), salud general del dispositivo y la antigüedad de la última actualización. Bajo este, la sección de umbrales permite el ajuste granular de parámetros críticos de calidad ambiental, como material particulado (PM2.5), CO₂, temperatura y humedad, a través de una interfaz interactiva de deslizadores.

**Settings**

<img src="../assets/mobileapp-mockup/SETTINGS.png" alt="mobile-settings" width="300">

La pantalla de configuración sigue el estándar de plataformas móviles mediante una vista de lista desplazable (table view) agrupada por categorías funcionales. El mock-up organiza las opciones en secciones claramente diferenciadas: "ACCOUNT", "PREFERENCES", "DEVICE SETTINGS" y "SUPPORT & LEGAL". Finalmente, un botón "LOGOUT" claramente diferenciado permite el cierre de sesión.

**Alerts**

<img src="../assets/mobileapp-mockup/ALERTS.png" alt="mobile-alerts" width="300">

La pantalla de alertas presenta un panel de control dentro del sistema Clair dedicado al monitoreo de alertas. En la parte superior, destaca un gráfico de barras que resume la frecuencia de eventos durante los últimos 30 días, permitiendo visualizar tendencias de actividad a lo largo del tiempo. Debajo, una interfaz tabulada divide la información en "Active Alerts" e "History", enfocándose en la gestión inmediata de incidencias críticas mediante una tabla organizada por severidad, ubicación y variable afectada, e integrando una navegación intuitiva con barra inferior para acceso rápido a otras funciones del sistema.

### 4.4.4. Mobile Applications User Flow Diagrams.

Esta sección presenta los diagramas de flujo de los usuarios en la aplicación móvil, los cuales ilustran las rutas y procesos que siguen dentro de Clair, facilitando la comprensión de la navegación y las interacciones clave.

**Mobile Application User Flow**

**User Flow: Gestión de alertas y activación de respuestas**

User Goals cubiertos:

| ID | User Goal |
|:---|:---|
| UG01 | Garantizar la salud ambiental: Mantener un aire fresco y libre de viciamento para que los clientes permanezcan más tiempo en el local |
| UG04 | Controlar síntomas crónicos: Reducir la frecuencia de episodios de rinitis alérgica, asma o dolores de cabeza asociados al ambiente cargado |

Ambos User Goals comparten el mismo flujo de interacción en Mobile Application. El usuario recibe una notificación emergente en el Dashboard cuando el sistema detecta una condición crítica (UG01) o la superación de un umbral personalizado (UG04). El usuario ingresa a la pantalla Alerts, visualiza la alerta destacada, y puede activar una respuesta preconfigurada, si está disponible desde Web App, o descartarla. La diferencia radica en el origen de la regla: UG01 responde a reglas por defecto del sistema, mientras que UG04 responde a reglas personalizadas configuradas desde Web App. En ambos casos, la experiencia de usuario en mobile es idéntica.

<img src="../assets/mobileapp-userflows/mobileapp-uflow1.png" alt="mobileapp-uflow1" width="1000">

**User Flow: Verificación de calidad del aire (Refugio seguro)**

User Goals cubiertos:

| ID | User Goal |
|:---|:---|
| UG06 | Crear un refugio seguro: Garantizar que, a pesar de la contaminación exterior de la ciudad, el interior de su hogar sea un espacio de respiración pura |

El usuario accede al Dashboard de Mobile Application. En esta pantalla, se muestran los indicadores de calidad del aire (CO₂, VOC, temperatura, humedad) y el indicador AQI (Bueno/Moderado/Malo). El usuario visualiza estos indicadores y verifica que el aire interior es saludable. Al observar que el AQI es "Bueno" o "Moderado" y que los valores están dentro de rangos saludables, el usuario confirma que su hogar es un "refugio seguro". No existe funcionalidad equivalente al widget de cumplimiento OMS en la versión mobile.

<img src="../assets/mobileapp-userflows/mobileapp-uflow2.png" alt="mobileapp-uflow2" width="600">

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

##### 4.9.1.1.1 Domain Layer

La capa de dominio de IAM contiene las reglas fundamentales de negocio independientes de cualquier infraestructura. Define las entidades críticas del ciclo de vida de usuario y las abstracciones de persistencia (puertos).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/domain-layer.svg" alt="IAM Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `User` actúa como la raíz de agregado que mantiene la identidad de la persona y sus vinculaciones externas (como Google). `TokenSession` es la entidad que administra la sesión del usuario a nivel de tokens JWT, permitiendo su revocación inmediata (`invalidate()`). `RegistrationSession` resguarda de manera temporal la contraseña encriptada y el código de verificación del flujo de registro.
*   **Value Objects:** `EmailAddress`, `Password` y `VerificationCode` encapsulan las restricciones estructurales y aseguran la validez y encapsulamiento de los datos del dominio desde el momento de su instanciación.
*   **Ports (Interfaces):** `UserRepository`, `TokenSessionRepository` y `RegistrationSessionRepository` definen las operaciones lógicas de almacenamiento sin depender de tecnologías específicas como JPA o Redis.

##### 4.9.1.1.2 Interface Layer

La capa de interfaz expone las API REST del contexto acotado, traduciendo las peticiones JSON HTTP externas en comandos de aplicación fuertemente tipados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/interfaces-layer.svg" alt="IAM Interface Layer Class Diagram" width="750">
</p>

*   **AuthenticationController:** Expone endpoints HTTP estándar para el registro local (`signUp`), confirmación vía código por correo (`confirmSignUp`), inicio de sesión (`signIn`), renovación de tokens (`refreshToken`) y cierre de sesión (`signOut`).
*   **GoogleOAuthController:** Administra el flujo federado de OpenID Connect. Redirecciona al usuario al servidor de autorización de Google y recibe el código de autorización en el endpoint de callback para autenticar la sesión.
*   **UserController:** Controlador simple que recupera los datos del perfil del usuario autenticado con base en la sesión de seguridad actual.

##### 4.9.1.1.3 Application Layer

Esta capa actúa como el orquestador principal del contexto acotado. Implementa los casos de uso definidos del sistema, interactuando con las interfaces de dominio y coordinando el flujo de las transacciones sin contener lógica de negocio directa.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/application-layer.svg" alt="IAM Application Layer Class Diagram" width="750">
</p>

*   **Command Handlers:** `UserCommandServiceImpl` implementa la lógica para iniciar el registro enviando un código de confirmación asíncrono (`InitiateRegistrationCommand`) y para validar el código y persistir definitivamente al usuario en el sistema (`ConfirmRegistrationCommand`).
*   **TokenCommandServiceImpl:** Orquesta las transacciones relacionadas con la sesión de tokens, controlando la persistencia de las firmas de tokens de refresco y su rotación segura para mitigar ataques de replay.
*   **GoogleOAuthCallbackApplicationService:** Orquesta el flujo de inicio de sesión social. Convierte el código de Google en un perfil de usuario verificado y delega la creación de tokens en el servicio de tokens de la aplicación.
*   **AsyncNotificationService (Port):** Interfaz que permite al servicio de aplicación delegar el envío de correos electrónicos a un sistema de mensajería asíncrono o un proveedor de correo externo sin acoplarse directamente a este.

##### 4.9.1.1.4 Infrastructure Layer

La capa de infraestructura implementa las interfaces de dominio (puertos) y provee los adaptadores concretos para interactuar con bases de datos relacionales, almacenamiento en memoria caché Redis, servicios OAuth2 y generadores de tokens criptográficos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/infrastructure-layer.svg" alt="IAM Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Persistencia:** `JpaUserRepository` utiliza Spring Data JPA e Hibernate para persistir usuarios en la base de datos central PostgreSQL. Para las sesiones de tokens y registro temporal de alta volatilidad, `RedisTokenSessionRepository` y `RedisRegistrationSessionRepository` encapsulan el acceso mediante `StringRedisTemplate`, configurando tiempos de expiración automáticos (TTL).
*   **GoogleTokenVerifierImpl:** Adaptador que consume las librerías cliente de Google para validar de forma criptográfica la autenticidad del ID Token recibido durante el flujo de OAuth2.
*   **JwtTokenEncoder:** Clase de infraestructura encargada de firmar algoritmos criptográficos HMAC-SHA256 para generar los Access Tokens (de corta duración) y Refresh Tokens (de larga duración).

#### 4.9.1.2 Bounded Context: Billing

##### 4.9.1.2.1 Domain Layer

La capa de dominio de Billing resguarda la consistencia del modelo de monetización y límites de la plataforma.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/domain-layer.svg" alt="Billing Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `UserPlan` mantiene las reglas de upgrade/downgrade temporal, determinando si el periodo de cobro ha expirado. `PaymentRecord` almacena el estado de cada pago (`PENDING`, `COMPLETED`, `FAILED`).
*   **Value Objects:** `Money` encapsula el monto y divisa de transacciones, mientras que `UserId` e `PlanType` regulan tipados y accesos.
*   **Ports:** `PaymentGateway` abstrae la lógica del cobro para no depender directamente de las librerías de Stripe a nivel de dominio.

##### 4.9.1.2.2 Interface Layer

Se encarga de recibir peticiones de cobro web y registrar webhooks provenientes de la pasarela de pagos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/interfaces-layer.svg" alt="Billing Interface Layer Class Diagram" width="750">
</p>

*   **SubscriptionController:** Permite a los clientes iniciar la pasarela de checkout redirigiendo al portal de Stripe.
*   **StripeWebhookController:** Endpoint de escucha perimetral que recibe y valida firmas HMAC de Stripe para autorizar el cobro y aprovisionar el plan del usuario de forma asíncrona.
*   **BillingContextFacade:** Puerto expuesto internamente que permite a contextos externos (como Device Management) consultar los límites del plan (`getMaxDevices()`) para denegar emparejamientos si el plan del usuario es Freemium y ya alcanzó su cupo.

##### 4.9.1.2.3 Application Layer

Se encarga de recibir peticiones de cobro web y registrar webhooks provenientes de la pasarela de pagos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/interfaces-layer.svg" alt="Billing Interface Layer Class Diagram" width="750">
</p>

*   **SubscriptionController:** Permite a los clientes iniciar la pasarela de checkout redirigiendo al portal de Stripe.
*   **StripeWebhookController:** Endpoint de escucha perimetral que recibe y valida firmas HMAC de Stripe para autorizar el cobro y aprovisionar el plan del usuario de forma asíncrona.
*   **BillingContextFacade:** Puerto expuesto internamente que permite a contextos externos (como Device Management) consultar los límites del plan (`getMaxDevices()`) para denegar emparejamientos si el plan del usuario es Freemium y ya alcanzó su cupo.

##### 4.9.1.2.4 Infrastructure Layer

Provee la comunicación externa con Stripe y la persistencia de datos financieros.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/infrastructure-layer.svg" alt="Billing Infrastructure Layer Class Diagram" width="750">
</p>

*   **StripePaymentGatewayAdapter:** Consume la API externa de Stripe para generar enlaces de pago de manera dinámica.
*   **Adaptadores de base de datos:** `JpaUserPlanRepository` y `JpaPaymentRecordRepository` realizan la persistencia relacional en PostgreSQL para garantizar transacciones ACID.

#### 4.9.1.3 Bounded Context: Device & Space Management

##### 4.9.1.3.1 Domain Layer

La capa de dominio define el inventario físico y la jerarquía organizacional del sistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/domain-layer.svg" alt="Device Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `Device` es el agregado de hardware. `DeviceAssignment` es la raíz de agregado que controla si un dispositivo está online/offline y en qué espacio físico y usuario está asignado. `DeviceCommand` controla el ciclo de vida de confirmación de órdenes. `Organization` y `Space` estructuran la geografía física de los sensores.
*   **Value Objects:** `HardwareId` (ID físico MAC/serie) y `ApiKey` (clave criptográfica de comunicación del sensor).
*   **Ports:** Interfaces de repositorio (`DeviceRepository`, `DeviceAssignmentRepository`, `DeviceCommandRepository`, `OrganizationRepository`, `SpaceRepository`).

##### 4.9.1.3.2 Interface Layer

Provee la interfaz REST para la gestión física del hardware y la estructuración espacial.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/interfaces-layer.svg" alt="Device Interface Layer Class Diagram" width="750">
</p>

*   **DeviceController:** Registra y empareja dispositivos en el sistema.
*   **DeviceThresholdController:** Endpoint para configurar los límites seguros de las lecturas.
*   **OrganizationController y SpaceController:** API para configurar la estructura de locales y áreas.

##### 4.9.1.3.3 Application Layer

Orquesta los flujos de configuración del entorno e ingesta/acciones del hardware.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/application-layer.svg" alt="Device Application Layer Class Diagram" width="750">
</p>

*   **DeviceCommandServiceImpl:** Coordina el emparejamiento seguro de dispositivos, validando las existencias de espacio y publicando en Kafka los cambios de asignación.
*   **DeviceControlCommandServiceImpl:** Administra el envío y despacho de comandos asíncronos para activar extractores o ventanas de ventilación inteligentes.
*   **SpaceCommandServiceImpl:** Orquesta el ciclo de vida del local, verificando a través del servicio externo `BillingContextFacade` (comunicación inter-contexto) si el plan del usuario tiene permisos para crear nuevos espacios.

##### 4.9.1.3.4 Infrastructure Layer

Proporciona persistencia SQL relacional para la configuración e integra mensajería Kafka.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/infrastructure-layer.svg" alt="Device Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Persistencia:** Repositorios Spring Data JPA que implementan los puertos de dominio para PostgreSQL.
*   **Kafka Publishers:** Adaptadores `ProvisioningDevicesChangedKafkaPublisher` y `DeviceCommandsPendingKafkaPublisher` que formatean y transmiten los payloads hacia las colas correspondientes de Apache Kafka.

#### 4.9.1.4 Bounded Context: Air Quality Evaluation

##### 4.9.1.4.1 Domain Layer

La capa de dominio modela las especificaciones físicas de calidad del aire y la integridad de las lecturas ambientales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/domain-layer.svg" alt="Evaluation Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `TelemetryEvaluation` representa el agregado principal que encapsula el estado físico del aire medido en un punto temporal específico.
*   **Value Objects:** `AirQuality` (parámetros de gases y ambiente), `ParticulateMatter` (concentración de polvo PM1.0, PM2.5, PM10), `Connectivity` (diagnóstico de señal), `Location` (país de reporte) y `DeviceId`.
*   **Ports:** `TelemetryEvaluationRepository` es el puerto de repositorio para guardar y recuperar mediciones.

##### 4.9.1.4.2 Interface Layer

Provee los endpoints HTTP y fachadas internas para consultar las evaluaciones y estados ambientales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/interfaces-layer.svg" alt="Evaluation Interface Layer Class Diagram" width="750">
</p>

*   **TelemetryEvaluationController:** Expone endpoints RESTful para obtener la telemetría en tiempo real de un dispositivo o su histórico paginado de evaluaciones.
*   **EvaluationContextFacade:** Fachada de comunicación interna utilizada por el contexto acotado de Analytics & Reporting para recuperar consolidados de telemetría horaria sin acoplarse a los repositorios de este contexto.

##### 4.9.1.4.3 Application Layer

Orquesta la ingesta de eventos de telemetría y ejecuta los flujos de consulta ambiental.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/application-layer.svg" alt="Evaluation Application Layer Class Diagram" width="750">
</p>

*   **TelemetryRecordedKafkaConsumer (Event Handler):** Suscriptor de Kafka que escucha de forma reactiva y no bloqueante los eventos del bus de mensajería asíncrona cuando un sensor Clair reporta telemetría.
*   **TelemetryEvaluationCommandServiceImpl:** Recibe el comando de validación, realiza los cálculos de salubridad y guarda la evaluación con base en los umbrales configurados.
*   **ExternalDeviceService (Port):** Puerto para interactuar de forma segura con el contexto de `Device Management` y validar la existencia y propietario de los sensores.

##### 4.9.1.4.4 Infrastructure Layer

Provee el acceso físico al motor de series temporales/PostgreSQL.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/infrastructure-layer.svg" alt="Evaluation Infrastructure Layer Class Diagram" width="750">
</p>

*   **JpaTelemetryEvaluationRepository:** Adaptador que traduce las consultas y escrituras del dominio en sentencias SQL a través de Spring Data JPA sobre PostgreSQL.

#### 4.9.1.5 Bounded Context: Alerting & Response

##### 4.9.1.5.1 Domain Layer

La capa de dominio gestiona la lógica del ciclo de vida de los incidentes y las reglas de severidad del aire.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/domain-layer.svg" alt="Alerting Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `Alert` actúa como agregado que encapsula los datos puntuales del incidente, implementando los métodos de negocio `acknowledge()` (acuse de recibo humano) y `resolve()` (cierre técnico de la alerta).
*   **Value Objects / Enums:** Enums `MetricType` (CO₂, PM2.5, temperatura, humedad), `AlertStatus` y `AlertSeverity`.
*   **Ports:** `AlertRepository` define el contrato para almacenar y consultar alertas activas de sensores.

##### 4.9.1.5.2 Interface Layer

Expone las API para la consulta de incidentes y provee fachadas para la interacción inter-contextos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/interfaces-layer.svg" alt="Alerting Interface Layer Class Diagram" width="750">
</p>

*   **AlertController:** Controlador REST para listar alertas e incidentes históricos o activos por local o dispositivo.
*   **AlertingContextFacade:** Fachada de comunicación directa utilizada para que otros contextos de la aplicación consulten la gravedad de un incidente específico de forma rápida.

##### 4.9.1.5.3 Application Layer

Orquesta la evaluación reactiva de las lecturas físicas e inicia el despacho de notificaciones de incidentes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/application-layer.svg" alt="Alerting Application Layer Class Diagram" width="750">
</p>

*   **AlertingTelemetryRecordedKafkaConsumer:** Listener asíncrono que procesa las lecturas de telemetría emitidas en el broker.
*   **AlertCommandServiceImpl:** Resuelve el caso de uso central: analiza la lectura recibida contra los umbrales configurados (obtenidos mediante `ExternalAlertingThresholdService`). Si hay transgresión y no existe una alerta activa para esa métrica, crea un nuevo incidente `Alert` y publica un evento `AlertIncidentChangedIntegrationEvent` en Kafka.
*   **Ports de consulta:** `ExternalAlertingDeviceService` y `ExternalAlertingThresholdService` resuelven datos de otros contextos de forma desacoplada.

##### 4.9.1.5.4 Infrastructure Layer

Provee almacenamiento relacional SQL y control del encolamiento de eventos de incidentes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/infrastructure-layer.svg" alt="Alerting Infrastructure Layer Class Diagram" width="750">
</p>

*   **JpaAlertRepository:** Adaptador concreto que persiste los registros de incidentes en PostgreSQL.
*   **AlertIncidentsChangedKafkaPublisher:** Adaptador que despacha los eventos de integración de alertas abiertas/resueltas a colas de Apache Kafka.

#### 4.9.1.6 Bounded Context: Analytics & Reporting

##### 4.9.1.6.1 Domain Layer

La capa de dominio de Analytics implementa las estructuras estadísticas y cálculos matemáticos para reportes y AQI.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/domain-layer.svg" alt="Analytics Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `DeviceDailySummary` y `DeviceMonthlySummary` son los agregados a largo plazo que consolidan el historial de calidad del aire. `DeviceAnalyticsSnapshot` es la entidad utilizada para agrupar lecturas en micro-ventanas de análisis.
*   **Value Objects:** `MetricStats` (mín/máx/promedio), `AqiCategoryBreakdown` (distribución de riesgo diario), `AirQualityIndex` e `DeviceId`.
*   **Domain Services:** `AqiCalculationDomainService` (calcula el índice oficial de calidad del aire), `MetricsAggregationDomainService` (funciones estadísticas de agregación) y `TrendAnalysisDomainService` (análisis de variación de contaminantes).

##### 4.9.1.6.2 Interface Layer

Provee interfaces para la visualización en vivo de métricas y la descarga de resúmenes estructurados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/interfaces-layer.svg" alt="Analytics Interface Layer Class Diagram" width="750">
</p>

*   **AnalyticsController:** Provee endpoints tradicionales para consultar métricas, así como conexiones asíncronas persistentes basadas en Server-Sent Events (SSE) a través de `SseEmitter` para empujar lecturas en vivo a las aplicaciones cliente sin sobrecargar el servidor.
*   **AnalyticsOverviewController:** Consolida los indicadores de salud y estados de conexión para la vista del panel principal.
*   **ReportController:** Expone la obtención de reportes diarios y mensuales, validando la autorización mediante llamadas desacopladas.

##### 4.9.1.6.3 Application Layer

Orquesta los flujos de analítica en tiempo real y el procesamiento diferido de reportes por lotes (*batch*).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/application-layer.svg" alt="Analytics Application Layer Class Diagram" width="750">
</p>

*   **KpiLiveMetricsCommandServiceImpl:** Recibe eventos de Kafka en caliente, actualiza un caché rápido en memoria `KpiLiveMetricsCache` y transmite la información vía SSE.
*   **Daily/Monthly Report Aggregation Service:** Tareas del sistema que leen de forma asíncrona datos del día/mes anterior para consolidar métricas transaccionales masivas.
*   **SnapshotAggregationScheduler:** Componente temporizado que ejecuta periódicamente promedios de telemetría y los guarda en base de datos.

##### 4.9.1.6.4 Infrastructure Layer

Implementa la persistencia a largo plazo para agregados analíticos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/infrastructure-layer.svg" alt="Analytics Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Repositorio:** `JpaDeviceAnalyticsSnapshotRepository`, `DeviceDailySummaryRepository` y `DeviceMonthlySummaryRepository` implementan los puertos de dominio persistiendo en PostgreSQL.

#### 4.9.1.7 Bounded Context: Analytics & Notifications

##### 4.9.1.7.1 Domain Layer

La capa de dominio de Notifications contiene los modelos para auditoría de entrega de mensajes y los puertos de infraestructura.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/domain-layer.svg" alt="Notifications Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `EmailLog` (auditoría de correos enviados, registrando errores si fallan) y `PushNotificationLog` (auditoría de notificaciones móviles con su respectivo ID externo del proveedor).
*   **Value Objects:** `EmailRecipient` (correo destinatario), `EmailSubject` y `EmailContent`.
*   **Ports:** Interfaces de servicios técnicos (`EmailDeliveryService`, `PushNotificationDeliveryService`) e interfaces de repositorio (`EmailLogRepository`, `PushNotificationLogRepository`).

##### 4.9.1.7.2 Interface Layer

Expone las fachadas internas del sistema para delegar envíos de forma rápida.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/interfaces-layer.svg" alt="Notifications Interface Layer Class Diagram" width="750">
</p>

*   **NotificationController:** Endpoint REST utilitario de prueba.
*   **NotificationsContextFacade:** Fachada de comunicación directa que permite al contexto de IAM gatillar el envío de códigos de confirmación de forma síncrona sin acoplarse a SMTP.

##### 4.9.1.7.3 Application Layer

Orquesta los flujos de mensajería y procesa los eventos procedentes del bus asíncrono.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/application-layer.svg" alt="Notifications Application Layer Class Diagram" width="750">
</p>

*   **AlertIncidentChangedKafkaConsumer:** Listener asíncrono que reacciona de forma inmediata a los eventos de incidentes modificados. Cuando una alerta crítica es detectada, consulta al contexto de dispositivo (`ExternalDeviceService`) para obtener al propietario y despacha la notificación push.
*   **EmailCommandServiceImpl:** Recibe comandos para formatear plantillas de correos electrónicos transaccionales y delega la transmisión física al servicio de entrega.

##### 4.9.1.7.4 Infrastructure Layer

Conecta la aplicación a servidores de correo electrónico y servicios externos de mensajería push.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/infrastructure-layer.svg" alt="Notifications Infrastructure Layer Class Diagram" width="750">
</p>

*   **SmtpEmailService:** Adaptador SMTP estándar.
*   **OneSignalPushNotificationService:** Adaptador que realiza peticiones HTTP seguras a la API de OneSignal para encolar las alertas push móviles.
*   **Repositorios JPA:** Adaptadores Spring Data JPA para la persistencia del log histórico en PostgreSQL.

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
