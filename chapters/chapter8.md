# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

En esta sección el equipo Bananawire parte del estado actual de Clair, el producto construido y validado en las entregas anteriores, para identificar qué no sabemos todavía y convertirlo en preguntas que se puedan responder con experimentos. El insumo principal son los hallazgos de las entrevistas de validación (sección 6.3), la evaluación heurística (sección 6.3.3), los supuestos e hipótesis Lean UX del Capítulo I y el Product Backlog del Capítulo III.

### 8.1.1. As-Is Summary.

Clair es una plataforma de monitoreo de calidad del aire interior para dos segmentos de Lima Metropolitana: **administradores de establecimientos** (Facility Admin) y **personas preocupadas por el aire en su hogar** (Home User). Al cierre de la entrega anterior, el producto se encuentra en el siguiente estado:

| Componente | Estado actual (As-Is) | Evidencia |
|---|---|---|
| **Dispositivo Clair Alpha** | Sensor sin pantalla que mide variables del aire interior, como CO₂ y material particulado (PM2.5 y PM10), y envía lecturas a la plataforma. | Capítulo IV y Capítulo V |
| **Landing Page** | Presenta la propuesta de valor, las especificaciones del dispositivo, los planes (Free y Premium a S/ 29.90 al mes), el equipo y los canales de contacto. | Sección 5.2.2 |
| **Web Application** (Angular) | Permite gestionar organizaciones, espacios y dispositivos, configurar umbrales, revisar alertas y consultar analítica y reportes. | Sección 5.2.3 |
| **Mobile Application** (Flutter) | Muestra el dashboard del aire, tendencias, detalle por sensor, reglas de alerta y notificaciones push. | Sección 5.2.5 |
| **Web Services** (Spring Boot) | API REST organizada en bounded contexts: IAM, Device, Evaluation, Alerting, Notifications, Analytics, Billing y Assistant. Las lecturas se clasifican por severidad (LOW, WARNING y CRITICAL según qué tanto superan el umbral). | Secciones 5.2.6, 5.2.7 y 6.1.1 |
| **Pipeline y calidad** | Suites de pruebas unitarias, de integración, BDD y de sistema en backend, web y móvil, con análisis estático y Quality Gate. | Capítulos VI y VII |

**Lo que ya sabemos.** Las 6 sesiones de validación (3 Facility Admin y 3 Home User) dieron una utilidad percibida promedio de **4.5 / 5** (dos sesiones con 4 y cuatro con 5), y los 6 participantes manifestaron, de forma explícita o implícita, que recomendarían Clair. El monitoreo en tiempo real y las alertas al celular son lo que más confianza genera.

**Lo que falla o falta.** La evaluación heurística dejó cinco problemas abiertos:

| # | Problema | Severidad | Qué deja sin resolver |
|---|---|---|---|
| 1 | El costo del dispositivo y del mantenimiento no es evidente en la primera vista de la Landing Page. | 3 | No sabemos si mostrar el precio antes aumenta o reduce la intención de registro. |
| 2 | Las alertas muestran valores y colores, pero no recomiendan qué hacer. | 3 | El 100% de los participantes pidió recomendaciones accionables; no sabemos cuánto cambia la respuesta real del usuario. |
| 3 | No se muestra información de calibración ni de precisión del sensor. | 2 | 5 de 6 participantes condicionaron su uso continuo a que las mediciones sean confiables. |
| 4 | El semáforo de estado no tiene texto ni leyenda accesible en todas las vistas. | 2 | No sabemos si los usuarios interpretan el color sin ayuda. |
| 5 | Configurar reglas personalizadas en la app móvil puede volverse confuso. | 2 | No sabemos cuántos usuarios abandonan la configuración. |

**Limitaciones de la evidencia actual.** Todo lo anterior proviene de entrevistas moderadas con una muestra pequeña (6 personas) y de lo que los usuarios *dicen* que harían. Todavía no tenemos datos de comportamiento real: cuántas personas se registran desde la landing, cuántas alertas se atienden, con qué frecuencia vuelven a la app o cuántos usuarios Free pasan a Premium. Por eso, el Capítulo VIII se enfoca en pasar de opiniones declaradas a métricas observadas.

### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims.

Reunimos la materia prima de los experimentos en cuatro tipos: **supuestos** (lo que creemos cierto sin haberlo probado), **vacíos de conocimiento** (lo que no sabemos y necesitamos saber), **ideas** (cambios que podríamos construir) y **afirmaciones** (lo que decimos del producto y debemos poder demostrar).

| ID | Tipo | Descripción | Fuente |
|---|---|---|---|
| A-01 | Supuesto | Los administradores revisarán el estado del aire con regularidad si la información se presenta de forma rápida y visual. | Lean UX Assumptions (1.2.2.2) |
| A-02 | Supuesto | Los usuarios confiarán más en Clair si cada alerta incluye una explicación breve y una recomendación concreta. | Lean UX Assumptions (1.2.2.2) y Problema #2 (6.3.3) |
| A-03 | Supuesto | El precio accesible y la facilidad de instalación son condiciones necesarias para la adopción. | Entrevistas (2.2.3) y VI-02 |
| A-04 | Supuesto | Los usuarios prefieren recibir alertas en el celular antes que revisar el panel web. | VI-01 (H-VI01-05) y 2.2.3 |
| A-05 | Supuesto | Los usuarios del plan Free pasarán a Premium cuando necesiten monitorear más de un espacio o dispositivo. | Modelo de suscripción (Billing) |
| K-01 | Vacío de conocimiento | No sabemos qué porcentaje de alertas termina en una acción real del usuario (ventilar, revisar el ambiente). | Capítulo VI: no hay datos de uso |
| K-02 | Vacío de conocimiento | No sabemos si mostrar el precio en la primera vista de la landing aumenta o reduce los registros. | Problema #1 (6.3.3) |
| K-03 | Vacío de conocimiento | No sabemos qué evidencia de precisión (calibración, comparación con un equipo de referencia, certificaciones) genera más confianza. | Problema #3 (6.3.3) |
| K-04 | Vacío de conocimiento | No sabemos si los usuarios interpretan correctamente el semáforo sin texto de apoyo. | Problema #4 (6.3.3) |
| K-05 | Vacío de conocimiento | No sabemos cuántos usuarios abandonan la creación de una regla de alerta en la app móvil. | Problema #5 (6.3.3) |
| K-06 | Vacío de conocimiento | No conocemos la frecuencia real de uso semanal de la app después de la primera semana. | Hipótesis 3 (1.2.2.3) |
| I-01 | Idea | Agregar una recomendación accionable a cada alerta y notificación push, con un botón "Ya lo hice" para registrar la acción. | Recomendación del Problema #2 |
| I-02 | Idea | Mostrar el precio del dispositivo y del plan en el hero de la landing, con un desglose "pago único + mensual". | Recomendación del Problema #1 |
| I-03 | Idea | Publicar una sección "¿Qué tan preciso es Clair?" con la ficha de los sensores, el método de calibración y una comparación contra un equipo de referencia. | Recomendación del Problema #3 |
| I-04 | Idea | Acompañar el semáforo con una etiqueta de texto ("Bueno", "Moderado", "Malo") y una leyenda en todas las vistas. | Recomendación del Problema #4 |
| I-05 | Idea | Ofrecer plantillas de reglas ("Oficina", "Dormitorio", "Local con público") para crear una regla en un solo paso. | Recomendación del Problema #5 |
| I-06 | Idea | Usar el asistente conversacional de Clair (bounded context Assistant) para explicar una alerta en lenguaje simple. | Backend actual (Assistant) |
| C-01 | Afirmación | "Clair te dice cuándo ventilar sin que tengas que interpretar datos técnicos." | Propuesta de valor (1.2.2.4) |
| C-02 | Afirmación | "Las alertas de Clair ayudan a mejorar el aire de tu espacio." | Landing Page |
| C-03 | Afirmación | "Instalar Clair toma pocos minutos y no necesita un técnico." | Landing Page y VI-02 |

### 8.1.3. Experiment-Ready Questions.

A partir de la materia prima, formulamos preguntas que cumplen tres condiciones: se refieren a un comportamiento observable, se pueden responder con una métrica y su respuesta cambia una decisión de producto.

| ID | Pregunta | Materia prima | Decisión que habilita |
|---|---|---|---|
| Q-01 | ¿Agregar una recomendación accionable a la alerta aumenta el porcentaje de alertas que el usuario atiende? | A-02, K-01, I-01, C-01 | Hacer obligatoria la recomendación en todas las alertas. |
| Q-02 | ¿Las alertas con recomendación reducen el tiempo que el espacio permanece en estado WARNING o CRITICAL? | K-01, I-01, C-02 | Mantener o reformular la afirmación C-02 en la landing. |
| Q-03 | ¿Mostrar el precio en la primera vista de la landing aumenta la tasa de registro? | A-03, K-02, I-02 | Rediseñar el hero y la sección de precios. |
| Q-04 | ¿Mostrar evidencia de precisión del sensor aumenta la confianza declarada y la conversión a registro? | K-03, I-03 | Invertir en una prueba de calibración publicable. |
| Q-05 | ¿Agregar una etiqueta de texto al semáforo aumenta la interpretación correcta del estado del aire? | K-04, I-04 | Estandarizar el componente de estado en web y móvil. |
| Q-06 | ¿Las plantillas de reglas aumentan la tasa de reglas creadas con éxito en la app móvil? | K-05, I-05 | Reemplazar el flujo actual de reglas personalizadas. |
| Q-07 | ¿Los usuarios que reciben alertas push vuelven a la app más veces por semana que los que solo usan el panel web? | A-04, K-06 | Priorizar la app móvil como canal principal. |
| Q-08 | ¿Qué porcentaje de usuarios Free pasa a Premium cuando alcanza el límite de espacios o dispositivos? | A-05 | Ajustar los límites del plan Free y el precio de Premium. |
| Q-09 | ¿Explicar una alerta con el asistente conversacional mejora la comprensión frente a una recomendación fija? | I-06, A-02 | Decidir si el asistente forma parte del flujo de alertas. |
| Q-10 | ¿Un usuario nuevo puede instalar y vincular el dispositivo sin ayuda en menos de 10 minutos? | A-03, C-03 | Mantener o corregir la afirmación C-03. |

### 8.1.4. Question Backlog.

Priorizamos las preguntas con tres criterios, cada uno de 1 a 5:

- **Impacto:** cuánto afecta la respuesta a la adopción, la retención o los ingresos.
- **Incertidumbre:** qué tan poco sabemos hoy (5 = no tenemos ningún dato).
- **Facilidad:** qué tan barato y rápido es responderla con lo que ya está construido (5 = muy fácil).

El **puntaje** es la suma de los tres criterios (máximo 15). A igual puntaje, tiene prioridad la pregunta con mayor impacto.

| Prioridad | ID | Pregunta (resumen) | Impacto | Incertidumbre | Facilidad | Puntaje |
|---|---|---|---|---|---|---|
| 1 | Q-01 | Recomendación en la alerta → alertas atendidas | 5 | 5 | 4 | **14** |
| 2 | Q-03 | Precio en la primera vista → tasa de registro | 4 | 5 | 5 | **14** |
| 3 | Q-05 | Etiqueta en el semáforo → interpretación correcta | 4 | 4 | 5 | **13** |
| 4 | Q-06 | Plantillas de reglas → reglas creadas con éxito | 4 | 4 | 4 | **12** |
| 5 | Q-04 | Evidencia de precisión → confianza y registro | 4 | 5 | 3 | **12** |
| 6 | Q-07 | Push vs. panel web → frecuencia de uso | 4 | 4 | 3 | **11** |
| 7 | Q-10 | Instalación sin ayuda en menos de 10 minutos | 4 | 3 | 3 | **10** |
| 8 | Q-02 | Recomendación → menos tiempo en WARNING/CRITICAL | 5 | 4 | 1 | **10** |
| 9 | Q-08 | Conversión Free → Premium al llegar al límite | 5 | 4 | 1 | **10** |
| 10 | Q-09 | Asistente conversacional vs. recomendación fija | 3 | 4 | 2 | **9** |

Las seis primeras preguntas pasan a experimentos en este ciclo. Q-02 y Q-08 tienen alto impacto, pero necesitan semanas de datos de uso real y una base de usuarios activa; quedan para el siguiente ciclo, cuando Q-01 y Q-07 ya hayan generado esa base. Q-09 depende del resultado de Q-01: solo tiene sentido comparar el asistente si la recomendación fija demuestra valor.

### 8.1.5. Experiment Cards.

Cada tarjeta resume un experimento con el formato: pregunta, por qué importa, qué construimos, hipótesis, cómo medimos y cuándo lo damos por validado.

#### Experiment Card EXP-01: Alertas con recomendación accionable

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-01: ¿Agregar una recomendación accionable a la alerta aumenta el porcentaje de alertas que el usuario atiende? |
| **Por qué** | Es el problema de mayor severidad de la evaluación heurística (#2) y lo pidió el 100% de los participantes. Sostiene la propuesta de valor C-01. |
| **Qué** | La alerta en la web, la app y la notificación push incluye una recomendación según la métrica y la severidad (por ejemplo, "CO₂ elevado: abre ventanas o enciende la ventilación por 10 minutos") y un botón "Ya lo hice". |
| **Hipótesis** | Creemos que mostrar una recomendación concreta junto a la alerta hará que los usuarios atiendan más alertas que con la alerta actual, que solo muestra valor y color. |
| **Método** | Prueba A/B en la app móvil y la web. Grupo A: alerta actual. Grupo B: alerta con recomendación y botón "Ya lo hice". Asignación aleatoria por cuenta. |
| **Métrica principal** | Tasa de alertas atendidas: alertas marcadas como revisadas o con "Ya lo hice" dentro de los 30 minutos ÷ alertas emitidas. |
| **Criterio de éxito** | El grupo B supera al grupo A en al menos 15 puntos porcentuales. |
| **Duración** | 2 semanas. |

#### Experiment Card EXP-02: Precio visible en la primera vista de la landing

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-03: ¿Mostrar el precio en la primera vista de la landing aumenta la tasa de registro? |
| **Por qué** | Problema #1 (severidad 3). Los tres administradores (VI-01, VI-02 y VI-03) tuvieron dudas sobre el costo del dispositivo o del servicio mensual. |
| **Qué** | Variante del hero con el precio del dispositivo y del plan Premium (S/ 29.90 al mes), el desglose "pago único + mensual" y la mención del plan Free. |
| **Hipótesis** | Creemos que mostrar el precio desde el inicio reducirá la incertidumbre y aumentará los registros, aunque disminuya el número de clics hacia la página de precios. |
| **Método** | Prueba A/B en la landing con división 50/50 del tráfico. |
| **Métrica principal** | Tasa de conversión a registro: visitantes que completan el registro en la Web App ÷ visitantes únicos de la landing. |
| **Criterio de éxito** | La variante supera al control en al menos un 20% relativo, sin aumentar la tasa de rebote en más de 5 puntos. |
| **Duración** | 2 semanas o hasta alcanzar el tamaño de muestra necesario. |

#### Experiment Card EXP-03: Semáforo con etiqueta de texto

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-05: ¿Agregar una etiqueta de texto al semáforo aumenta la interpretación correcta del estado del aire? |
| **Por qué** | Problema #4 (severidad 2) y Hipótesis 1 del Capítulo I. Un indicador que solo depende del color excluye a usuarios con daltonismo y genera dudas en los demás. |
| **Qué** | El indicador de estado muestra el color, un ícono y una etiqueta ("Bueno", "Moderado", "Malo"), con una leyenda accesible en todas las vistas de web y móvil. |
| **Hipótesis** | Creemos que acompañar el color con texto hará que más usuarios interpreten correctamente el estado y elijan una acción adecuada. |
| **Método** | Prueba de 5 segundos y de primer clic con dos versiones de la pantalla (con y sin etiqueta), con usuarios de ambos segmentos. |
| **Métrica principal** | Tasa de interpretación correcta: participantes que identifican el estado y eligen una acción adecuada ÷ participantes. |
| **Criterio de éxito** | Al menos el 80% interpreta correctamente la versión con etiqueta (meta de la Hipótesis 1). |
| **Duración** | 1 semana. |

#### Experiment Card EXP-04: Plantillas de reglas en la app móvil

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-06: ¿Las plantillas de reglas aumentan la tasa de reglas creadas con éxito en la app móvil? |
| **Por qué** | Problema #5 (severidad 2). Configurar una regla es necesario para que las alertas sean útiles, y hoy exige varios pasos. |
| **Qué** | Al crear una regla, el usuario puede elegir una plantilla ("Oficina", "Dormitorio", "Local con público") que precarga las métricas y los umbrales, y luego ajustarla. |
| **Hipótesis** | Creemos que las plantillas permitirán que más usuarios completen la creación de una regla, en menos tiempo y con menos errores. |
| **Método** | Prueba A/B en la app móvil (flujo actual frente a flujo con plantillas), complementada con una prueba de usabilidad moderada de la tarea T10. |
| **Métrica principal** | Tasa de reglas completadas: usuarios que guardan una regla ÷ usuarios que inician el flujo. |
| **Criterio de éxito** | La tasa de reglas completadas sube al menos 20 puntos porcentuales y la mediana del tiempo de la tarea baja al menos un 30%. |
| **Duración** | 2 semanas. |

#### Experiment Card EXP-05: Evidencia de precisión del sensor

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-04: ¿Mostrar evidencia de precisión del sensor aumenta la confianza declarada y la conversión a registro? |
| **Por qué** | Problema #3. Cinco de seis participantes condicionaron su recomendación a la precisión de las mediciones. |
| **Qué** | Sección "¿Qué tan preciso es Clair?" en la landing y en la app: ficha técnica de los sensores, método de calibración y una gráfica que compara Clair con un equipo de referencia durante 48 horas. |
| **Hipótesis** | Creemos que mostrar evidencia verificable de precisión aumentará la confianza en las mediciones y, con ella, la intención de registro. |
| **Método** | Prueba A/B en la landing (con y sin la sección) y una encuesta corta de confianza de 1 a 5 al final de la visita. |
| **Métricas principales** | Confianza declarada promedio y tasa de conversión a registro. |
| **Criterio de éxito** | La confianza promedio sube al menos 0.5 puntos y la conversión no disminuye. |
| **Duración** | 2 semanas. |

#### Experiment Card EXP-06: Alertas push frente a panel web

| Campo | Detalle |
|---|---|
| **Pregunta** | Q-07: ¿Los usuarios que reciben alertas push vuelven a la app más veces por semana que los que solo usan el panel web? |
| **Por qué** | Supuesto A-04 e Hipótesis 3 del Capítulo I. Define cuál es el canal principal en el que invertir. |
| **Qué** | Se activan las notificaciones push por defecto para un grupo de usuarios nuevos; el otro grupo recibe las alertas solo dentro del panel web. |
| **Hipótesis** | Creemos que las notificaciones push harán que los usuarios consulten Clair con más frecuencia y atiendan más alertas que quienes dependen del panel web. |
| **Método** | Prueba A/B por cohorte de registro. |
| **Métricas principales** | Sesiones por usuario por semana y porcentaje de usuarios activos en la segunda semana. |
| **Criterio de éxito** | Al menos el 70% de los usuarios con push consulta Clair semanalmente (meta de la Hipótesis 3) y supera al grupo de panel web en al menos 25% relativo. |
| **Duración** | 3 semanas. |

## 8.2. Experiment Design

### 8.2.1. Hypotheses.

Cada experimento de la sección 8.1.5 se formaliza con una hipótesis en formato Lean UX y su par de hipótesis estadísticas: la **hipótesis nula (H0)**, que asume que el cambio no tiene efecto, y la **hipótesis alternativa (H1)**, que es la que esperamos demostrar. Rechazamos H0 cuando la diferencia observada es estadísticamente significativa (nivel de significancia α = 0.05) y además alcanza el criterio de éxito de la tarjeta.

| ID | Pregunta | Creencia | Hipótesis | H0 (nula) | H1 (alternativa) |
|---|---|---|---|---|---|
| H-01 | Q-01 | Los usuarios no actúan ante una alerta porque no saben qué hacer. | Creemos que mostrar una recomendación accionable en cada alerta **para Facility Admin y Home User** aumentará el porcentaje de alertas atendidas. Sabremos que es cierto cuando la tasa de alertas atendidas del grupo con recomendación supere a la del grupo control en al menos 15 puntos porcentuales. | La tasa de alertas atendidas es igual con y sin recomendación. | La tasa de alertas atendidas es mayor con recomendación. |
| H-02 | Q-03 | Los visitantes no se registran porque no saben cuánto cuesta Clair. | Creemos que mostrar el precio del dispositivo y del plan en la primera vista de la landing **para visitantes de ambos segmentos** aumentará la tasa de registro. Sabremos que es cierto cuando la conversión a registro de la variante supere al control en al menos 20% relativo, sin elevar el rebote en más de 5 puntos. | La conversión a registro es igual con el precio en el hero y sin él. | La conversión a registro es mayor con el precio en el hero. |
| H-03 | Q-05 | El color por sí solo no basta para entender el estado del aire. | Creemos que acompañar el semáforo con una etiqueta de texto y una leyenda **para todos los usuarios** aumentará la interpretación correcta del estado. Sabremos que es cierto cuando al menos el 80% de los participantes interprete correctamente la versión con etiqueta. | La tasa de interpretación correcta es igual con y sin etiqueta. | La tasa de interpretación correcta es mayor con etiqueta. |
| H-04 | Q-06 | Los usuarios abandonan la configuración de reglas porque tiene demasiados pasos. | Creemos que ofrecer plantillas de reglas **para Home User en la app móvil** aumentará la cantidad de reglas creadas con éxito. Sabremos que es cierto cuando la tasa de reglas completadas suba al menos 20 puntos porcentuales y el tiempo de la tarea baje al menos un 30%. | La tasa de reglas completadas es igual con y sin plantillas. | La tasa de reglas completadas es mayor con plantillas. |
| H-05 | Q-04 | Los usuarios dudan de la precisión del sensor porque no ven ninguna prueba. | Creemos que mostrar evidencia de precisión del sensor **para visitantes de ambos segmentos** aumentará la confianza en las mediciones. Sabremos que es cierto cuando la confianza declarada promedio suba al menos 0.5 puntos (escala de 1 a 5) sin que baje la conversión a registro. | La confianza promedio es igual con y sin la sección de precisión. | La confianza promedio es mayor con la sección de precisión. |
| H-06 | Q-07 | Los usuarios olvidan revisar el panel si Clair no los busca. | Creemos que activar las notificaciones push por defecto **para usuarios nuevos** aumentará la frecuencia de consulta semanal. Sabremos que es cierto cuando al menos el 70% de los usuarios con push consulte Clair cada semana y el grupo supere al de panel web en al menos 25% relativo en sesiones semanales. | Las sesiones semanales por usuario son iguales con y sin push. | Las sesiones semanales por usuario son mayores con push. |

### 8.2.2. Domain Business Metrics

Las métricas de negocio se definen a partir de los bounded contexts de Clair, de modo que cada una se pueda calcular con eventos que el sistema ya registra o que se agregarán con los experimentos. Se organizan desde la métrica que resume el valor entregado (North Star) hasta las métricas de cada etapa del ciclo de vida del usuario.

**North Star Metric:** *Alertas atendidas por espacio activo por semana.* Resume la propuesta de valor de Clair: no basta con medir el aire, el usuario tiene que actuar a tiempo. Crece cuando hay más espacios monitoreados, más alertas útiles y más usuarios que las atienden.

| Etapa | Métrica | Definición / fórmula | Bounded context fuente | Hipótesis |
|---|---|---|---|---|
| Adquisición | Tasa de conversión a registro | Cuentas creadas ÷ visitantes únicos de la landing | Landing Page + IAM | H-02, H-05 |
| Adquisición | Confianza declarada | Promedio de la encuesta "¿Confías en las mediciones de Clair?" (1 a 5) | Landing Page | H-05 |
| Activación | Tasa de activación | Cuentas con al menos un dispositivo vinculado y una lectura recibida en las primeras 48 horas ÷ cuentas creadas | IAM + Device + Evaluation | Q-10 |
| Activación | Tasa de reglas completadas | Reglas de alerta guardadas ÷ flujos de creación de regla iniciados | Alerting | H-04 |
| Activación | Tiempo de instalación | Mediana de minutos entre el registro y la primera lectura del dispositivo | Device + Evaluation | Q-10 |
| Engagement | Tasa de alertas atendidas | Alertas reconocidas o marcadas "Ya lo hice" en 30 minutos ÷ alertas emitidas | Alerting + Notifications | H-01 |
| Engagement | Interpretación correcta del estado | Participantes que identifican el estado y la acción adecuada ÷ participantes | Analytics (prueba de usabilidad) | H-03 |
| Engagement | Sesiones semanales por usuario | Sesiones en web y móvil ÷ usuarios activos, por semana | IAM + Notifications | H-06 |
| Retención | Retención semanal (semana 2 y semana 4) | Usuarios activos en la semana N ÷ usuarios registrados en la cohorte | IAM | H-06 |
| Resultado ambiental | Tiempo en estado crítico | Minutos promedio que un espacio permanece en WARNING o CRITICAL después de una alerta | Evaluation + Alerting | Q-02 |
| Monetización | Conversión Free → Premium | Cuentas que pasan a Premium ÷ cuentas Free que alcanzaron el límite de su plan | Billing | Q-08 |
| Monetización | Ingreso mensual recurrente (MRR) | Suscripciones Premium activas × S/ 29.90 | Billing | Q-08 |
| Monetización | Churn mensual | Suscripciones Premium canceladas en el mes ÷ suscripciones activas al inicio del mes | Billing | Q-08 |

Estas métricas no tienen todavía una línea base, porque el producto no ha estado en manos de usuarios reales fuera de las sesiones de validación. La primera medición de cada una se tomará en el grupo control de los experimentos de la sección 8.1.5, y será la línea base contra la que se comparen las siguientes iteraciones.

### 8.2.3. Measures.

Las métricas de negocio de la sección 8.2.2 describen el producto; las **medidas** de esta sección son su definición operativa para cada experimento: qué se cuenta exactamente, en qué unidad, en qué ventana de tiempo y de qué evento sale el dato. Se clasifican en tres tipos:

- **Primaria:** la medida con la que se decide si se rechaza H0. Hay una por hipótesis (dos en H-04, donde deben cumplirse ambas).
- **Secundaria:** ayuda a explicar *por qué* cambió la primaria, pero no decide el experimento.
- **Guardrail (de resguardo):** debe mantenerse dentro de un límite; si se rompe, el cambio no se adopta aunque la primaria mejore.

| ID | Medida | Tipo | Definición operacional | Unidad y escala | Fuente | Métrica (8.2.2) | Hip. |
|---|---|---|---|---|---|---|---|
| M-01 | Tasa de alertas atendidas | Primaria | Alertas con acción registrada ("Ya lo hice") o reconocimiento dentro de los 30 minutos desde su emisión ÷ alertas emitidas. | Proporción (0 a 1), por grupo | Alerting (`emitted_at`, `acknowledged_at`) y evento `alert_action_done` | Tasa de alertas atendidas | H-01 |
| M-02 | Tasa de conversión a registro | Primaria | Visitantes únicos que completan el registro en las 24 h siguientes a su primera visita ÷ visitantes únicos de la landing. | Proporción, por variante | Eventos `experiment_exposure` y `signup_completed` | Tasa de conversión a registro | H-02 |
| M-03 | Tasa de interpretación correcta | Primaria | Participantes que identifican el estado del aire y eligen la acción adecuada ÷ participantes que vieron la versión. | Proporción, por versión | Herramienta de prueba de 5 segundos | Interpretación correcta del estado | H-03 |
| M-04 | Tasa de reglas completadas | Primaria | Usuarios que guardan una regla (`rule_saved`) ÷ usuarios que inician el flujo (`rule_creation_started`) en la misma sesión. | Proporción, por variante | Evento móvil | Tasa de reglas completadas | H-04 |
| M-05 | Tiempo de tarea de creación de regla | Primaria | Mediana de segundos entre `rule_creation_started` y `rule_saved`, solo en flujos completados. | Segundos (razón); se reporta la mediana por sesgo de la cola larga | Evento móvil (`duration_ms`) | (apoya H-04) | H-04 |
| M-06 | Confianza declarada | Primaria | Respuesta a "¿Confías en las mediciones de Clair?" de 1 a 5, de quienes responden la encuesta. | Likert de 1 a 5 (ordinal); se reporta media y mediana | Evento `trust_survey_answered` | Confianza declarada | H-05 |
| M-07 | Sesiones semanales por usuario | Primaria | Sesiones (web y móvil, con 30 min de inactividad como corte) ÷ usuarios del grupo, en cada semana desde el registro. | Conteo por usuario-semana (razón) | `session_start` de GA4 y Firebase | Sesiones semanales por usuario | H-06 |
| M-08 | Usuarios con consulta semanal | Primaria | Usuarios del grupo con al menos una sesión en la semana ÷ usuarios del grupo, para las semanas 2 y 3. | Proporción por semana | `session_start` | Retención semanal | H-06 |
| M-09 | Tasa de rebote de la landing | Guardrail | Sesiones de la landing sin interacción ni segunda página ÷ sesiones de la landing. | Proporción | GA4 (sesiones no "engaged") | (límite de H-02) | H-02 |
| M-10 | Clic hacia la página de precios | Secundaria | Visitantes que hacen clic en el enlace de precios ÷ visitantes únicos. | Proporción | Evento `pricing_cta_clicked` | — | H-02 |
| M-11 | Tiempo hasta atender la alerta | Secundaria | Mediana de minutos entre la emisión y la acción registrada, en alertas atendidas. | Minutos (razón) | Alerting | — | H-01 |
| M-12 | Latencia de la alerta | Guardrail | Segundos entre la lectura que supera el umbral y la emisión de la alerta. | Segundos (razón) | Evaluation y Alerting | — | H-01 |
| M-13 | Tasa de entrega de push | Guardrail | Notificaciones con confirmación de entrega ÷ notificaciones enviadas. | Proporción | Notifications y FCM | — | H-01, H-06 |
| M-14 | Tasa de desactivación de push | Guardrail | Usuarios que desactivan las notificaciones en las 3 semanas ÷ usuarios con push activado por defecto. | Proporción | Evento `push_disabled` | — | H-06 |
| M-15 | Errores de validación por intento | Secundaria | Eventos `rule_validation_error` ÷ flujos de regla iniciados. | Razón | Evento móvil | — | H-04 |
| M-16 | Tasa de respuesta de la encuesta | Secundaria | Encuestas respondidas ÷ encuestas mostradas. Sirve para detectar sesgo de respuesta entre variantes. | Proporción | Eventos de encuesta | — | H-05 |
| M-17 | Conversión a registro (resguardo de H-05) | Guardrail | Igual que M-02, medida en las variantes con y sin la sección de precisión. | Proporción | Igual que M-02 | Tasa de conversión a registro | H-05 |

**Reglas comunes de medición**

- La **unidad de análisis** es la cuenta en los experimentos de producción (H-01, H-04 y H-06), el visitante único en la landing (H-02 y H-05) y el participante en la prueba de usabilidad (H-03). En H-01 la medida se calcula por alerta, pero el análisis agrupa por cuenta, porque las alertas de una misma cuenta no son independientes.
- Se **excluyen** las cuentas del equipo, las cuentas de demostración, los dispositivos de prueba y el tráfico de bots. Una cuenta solo entra al análisis de H-01 si recibió al menos una alerta durante la ventana.
- La asignación se **registra una sola vez**, en el evento `experiment_exposure`, y se analiza según el grupo asignado (intención de tratar), no según lo que el usuario terminó viendo.
- Las medidas M-01, M-11, M-12, M-13 y el cálculo de M-08 salen del **backend**, que es la fuente de verdad; los eventos del cliente solo se usan donde el backend no tiene el dato (por ejemplo, el rebote o los pasos del flujo de reglas).

### 8.2.4. Conditions.

Las condiciones definen contra qué se compara cada cambio, a quién se le muestra y bajo qué reglas se considera válido el resultado.

**Condiciones generales de todos los experimentos**

| Condición | Valor |
|---|---|
| Nivel de significancia | α = 0.05, prueba unilateral (las hipótesis H1 de 8.2.1 tienen dirección) |
| Potencia estadística | 80% (β = 0.20) |
| Reparto entre grupos | 50% control y 50% tratamiento |
| Asignación | Aleatoria y determinista: un *hash* del identificador de cuenta (o del identificador anónimo en la landing) decide el grupo, de modo que la misma persona siempre ve la misma versión |
| Momento del análisis | Una sola vez, al final de la ventana. No se revisan los resultados para detener el experimento antes de tiempo |
| Cambios durante la ventana | Los flujos, textos y umbrales del experimento no se modifican mientras dure; los despliegues no relacionados sí están permitidos |

**Condiciones por experimento**

| Experimento | Unidad de asignación | Control (A) | Tratamiento (B) | Segmento y plataforma | Inclusión y exclusión | Ventana |
|---|---|---|---|---|---|---|
| EXP-01 (H-01) | Cuenta | Alerta actual: valor y color | Alerta con recomendación según métrica y severidad, y botón "Ya lo hice" | Facility Admin y Home User; web, móvil y push | Cuentas con al menos un dispositivo vinculado y una alerta emitida | 2 semanas |
| EXP-02 (H-02) | Visitante (cookie) | Hero actual, sin precio | Hero con precio del dispositivo, plan Premium (S/ 29.90 al mes), desglose "pago único + mensual" y mención del plan Free | Visitantes de ambos segmentos; landing | Se excluye tráfico de bots y del equipo; cada visitante cuenta una vez | 4 semanas (ver 8.2.5) |
| EXP-03 (H-03) | Participante | Pantalla con semáforo de color e ícono | Pantalla con color, ícono, etiqueta ("Bueno", "Moderado", "Malo") y leyenda | Todos los usuarios; prueba de 5 segundos sobre web y móvil | Participantes sin experiencia previa con Clair; cada uno ve solo una versión; mitad Facility Admin y mitad Home User | 1 semana |
| EXP-04 (H-04) | Cuenta | Flujo actual de reglas personalizadas | Flujo con plantillas ("Oficina", "Dormitorio", "Local con público") | Home User; app móvil | Solo usuarios que inician el flujo de reglas | 2 semanas, ampliable hasta 4 (ver 8.2.5) |
| EXP-05 (H-05) | Visitante (cookie) | Landing sin la sección de precisión | Landing con la sección "¿Qué tan preciso es Clair?" | Visitantes de ambos segmentos; landing | Igual que EXP-02; la encuesta se muestra tras 30 segundos o al llegar al 50% de la página | 4 semanas, en paralelo con EXP-02 |
| EXP-06 (H-06) | Cuenta, al registrarse | Alertas solo en el panel web | Notificaciones push activadas por defecto | Usuarios nuevos; web y móvil | Solo cuentas creadas durante la ventana de reclutamiento; cada usuario se observa 3 semanas desde su registro | 3 semanas de observación por usuario |

**Interacciones entre experimentos.** Varios experimentos tocan la misma pantalla o a los mismos usuarios, y si se ejecutan sin coordinar se contaminan entre sí:

- **EXP-02 y EXP-05 comparten la landing.** Se ejecutan como un **diseño factorial 2×2** sobre el mismo tráfico: cada visitante recibe una combinación (precio sí o no, precisión sí o no), con cuatro celdas. Los dos efectos principales se estiman cada uno con la mitad del tráfico frente a la otra mitad, de modo que no se necesita más tráfico que para un solo experimento, y además se puede comprobar si los dos cambios interactúan.
- **EXP-01, EXP-04 y EXP-06 comparten la aplicación.** Se asignan de forma **independiente** (un *hash* distinto por experimento), así que las mismas cuentas sirven para los tres. Se reportará el tamaño de cada combinación para verificar que no haya celdas vacías.
- **EXP-03 es una prueba controlada** fuera de producción y no se cruza con ningún otro.

**Condiciones de validez.** Un experimento solo se considera interpretable si se cumplen todas estas condiciones; si alguna falla, el resultado se declara no concluyente y se repite, sin importar la diferencia observada.

| ID | Condición de validez | Umbral | Experimentos | Qué falla si no se cumple |
|---|---|---|---|---|
| V-01 | **Sin desbalance de muestra (SRM):** el reparto real entre grupos coincide con el 50/50 esperado | Prueba χ² con p ≥ 0.01 | Todos los de producción | La aleatorización está rota y los grupos no son comparables |
| V-02 | **Eventos completos:** las sesiones, alertas y registros del backend coinciden con los eventos recibidos | Al menos 95% de coincidencia | Todos | Las medidas quedan vacías o sesgadas (ver 8.2.8) |
| V-03 | **Dispositivos en línea:** el dispositivo de cada espacio analizado envía lecturas durante la ventana | Al menos 90% del tiempo | EXP-01, EXP-06 | Un sensor caído no genera alertas, y el espacio parecería "sin problemas" sin estarlo |
| V-04 | **Notificaciones entregadas** | M-13 de al menos 95% | EXP-01, EXP-06 | La alerta existe pero el usuario no se entera; se confunde "no actuó" con "no supo" |
| V-05 | **Alertas puntuales:** la latencia de emisión se mantiene dentro del límite | M-12 de máximo 60 s (umbral propuesto) | EXP-01 | Una alerta tardía no se puede atender en 30 minutos aunque tenga recomendación |
| V-06 | **Sin cambios en el flujo evaluado** durante la ventana | Cero despliegues sobre el flujo | Todos | Se mezclan efectos de dos versiones distintas |
| V-07 | **Sin discrepancia de respuesta** entre variantes | Diferencia de M-16 de máximo 10 puntos | EXP-05 | La confianza medida solo refleja a quienes contestan, no a los visitantes |

### 8.2.5. Scale Calculations and Decisions.

**Parámetros y fórmulas.** Todas las pruebas son unilaterales con α = 0.05 (z<sub>α</sub> = 1.645) y potencia de 80% (z<sub>β</sub> = 0.842). El tamaño de muestra por grupo se calcula así:

- Para **proporciones** (H-01, H-02, H-03, H-04): n = [ z<sub>α</sub>·√(2·p̄·(1 − p̄)) + z<sub>β</sub>·√(p<sub>0</sub>·(1 − p<sub>0</sub>) + p<sub>1</sub>·(1 − p<sub>1</sub>)) ]² ÷ (p<sub>1</sub> − p<sub>0</sub>)², donde p<sub>0</sub> es la proporción del control, p<sub>1</sub> la que esperamos en el tratamiento y p̄ su promedio.
- Para **medias** (H-04 en tiempo, H-05, H-06): n = 2·[ (z<sub>α</sub> + z<sub>β</sub>) ÷ d ]², donde d es el efecto estandarizado (diferencia esperada ÷ desviación estándar).
- Para **alertas agrupadas por cuenta** (H-01): el n anterior se multiplica por el efecto de diseño DEFF = 1 + (m − 1)·ρ, con m alertas por cuenta y ρ la correlación entre alertas de una misma cuenta.

**Supuestos de línea base.** Clair todavía no tiene datos de uso real (sección 8.2.2), así que los valores de partida son **supuestos de planificación**. La semana 0 de cada experimento medirá la línea base real y los cálculos se repetirán con esos valores antes de iniciar.

| Hip. | Medida | Línea base supuesta (p<sub>0</sub> o media) | Meta (criterio de 8.2.1) | Otros supuestos |
|---|---|---|---|---|
| H-01 | M-01 | 30% de alertas atendidas | 45% (+15 pp) | 6 alertas por cuenta en 2 semanas; ρ = 0.10, DEFF = 1.5 |
| H-02 | M-02 | 3% de conversión | 3.6% (+20% relativo) | 100 visitantes únicos por día en la landing |
| H-03 | M-03 | 55% de interpretación correcta | 80% | — |
| H-04 | M-04 y M-05 | 40% de reglas completadas; tiempo con coeficiente de variación de 0.5 | 60% (+20 pp) y tiempo −30% (d = 0.6) | — |
| H-05 | M-06 | Desviación estándar de 1.0 punto | +0.5 punto (d = 0.5) | 20% de respuesta a la encuesta |
| H-06 | M-07 y M-08 | 2.0 sesiones por semana, desviación estándar de 1.5; 55% con consulta semanal | +25% relativo (d = 0.33) y 70% con consulta semanal | — |

**Tamaños de muestra requeridos**

| Hip. | Cálculo | n por grupo | Total | Unidad |
|---|---|---|---|---|
| H-01 | 128 alertas × DEFF 1.5 = 192 alertas, entre 6 alertas por cuenta | 32 cuentas | 64 cuentas | Cuentas con alertas |
| H-02 | Proporciones, 3% frente a 3.6% | 10,960 | 21,920 | Visitantes únicos |
| H-03 | Proporciones, 55% frente a 80% | 43 | 86 | Participantes |
| H-04 | Proporciones, 40% frente a 60% (el tiempo requiere solo 35 por grupo) | 77 | 154 | Flujos iniciados |
| H-05 | Medias, d = 0.5 | 50 | 100 | Respuestas a la encuesta |
| H-06 | Medias, d = 0.33 (el criterio de 70% con consulta semanal requiere 65 usuarios en el grupo con push) | 112 | 224 | Usuarios nuevos |

**Decisiones**

| ID | Decisión | Justificación |
|---|---|---|
| D-01 | **H-01:** reclutar **40 cuentas por grupo** (80 en total) en lugar de las 32 calculadas. | Deja un margen de 25% por cuentas que no reciban alertas. Con 40 cuentas se detecta una mejora de hasta 13.4 puntos, menor que la meta de 15. |
| D-02 | **H-02:** el tamaño requerido (10,960 por grupo) no es alcanzable con el tráfico esperado. Se ejecuta **4 semanas** (unos 2,800 visitantes, 1,400 por brazo del factorial) y se complementa con tráfico dirigido (redes del equipo y contactos de los entrevistados). Con 1,400 por brazo se detecta una conversión de 4.8%, es decir, una mejora relativa de 61%. | Con 2 semanas (700 por brazo) solo se detectaría una mejora de 91% relativo, lejos del 20% de la hipótesis. Ampliar la ventana es lo que permite la tarjeta EXP-02 ("o hasta alcanzar el tamaño de muestra necesario"). |
| D-03 | **Regla de lectura de H-02:** si la mejora observada es de al menos 20% y p < 0.05, la hipótesis queda **confirmada**; si es de al menos 20% pero p ≥ 0.05, queda **prometedora, no confirmada** y se repite con más tráfico; en cualquier otro caso se rechaza. Siempre se reporta el intervalo de confianza. | Evita declarar éxito o fracaso con un experimento que no tiene potencia para detectar el efecto de la meta. |
| D-04 | **H-03:** reclutar **90 participantes** (45 por versión, 22 o 23 de cada segmento por versión) con una prueba no moderada en línea durante una semana. | Cumple el mínimo de 43 por grupo y mantiene el equilibrio entre Facility Admin y Home User. |
| D-05 | **H-04:** correr hasta **77 flujos por grupo**, con un máximo de 4 semanas. Si no se alcanzan, la decisión se toma con M-05 (tiempo de tarea, que requiere 35 por grupo) y M-04 se reporta como **dirección del efecto con su intervalo de confianza**. Con 40 flujos por grupo solo se detectaría una mejora de 27 puntos, mayor que los 20 de la meta. | Evita no poder decidir nada si el flujo de reglas se usa poco. |
| D-06 | **H-05:** no se reduce la muestra. Con 20% de respuesta, 700 visitantes por brazo del factorial dan unas 140 respuestas por brazo, más que las 50 necesarias. La conversión (M-17) se vigila como guardrail pero **no tiene potencia** para demostrar que "no baja": se reporta con intervalo de confianza. | Demostrar que una métrica no empeora requiere mucha más muestra que demostrar que mejora. |
| D-07 | **H-06:** reclutar **224 usuarios nuevos** (112 por grupo) en una ventana de hasta 4 semanas. El criterio de 70% con consulta semanal se contrasta con una prueba binomial exacta sobre el grupo con push (mínimo 65 usuarios). Con 40 por grupo solo se detectaría una mejora de 42% en sesiones, mayor que el 25% de la meta. | El experimento más exigente en usuarios, por lo que fija la meta de reclutamiento de la app. |
| D-08 | **Meta de reclutamiento de la app:** unas **230 cuentas nuevas**, de las cuales al menos 155 deben ser Home User con la app móvil. Como EXP-01, EXP-04 y EXP-06 se asignan de forma independiente, **las mismas cuentas sirven para los tres**. | Evita reclutar tres veces. Si no se alcanza la meta, se aplican las reglas D-05 y D-07. |
| D-09 | **Corrección por comparaciones múltiples:** no se aplica entre hipótesis, porque cada una es una decisión de producto separada. En H-04, donde deben cumplirse **ambos** criterios (completadas y tiempo), no hace falta ajustar α, porque el cambio solo se adopta si los dos pasan. | Mantiene α = 0.05 en cada decisión sin perder potencia. |
| D-10 | **Parada de emergencia:** un experimento se detiene antes de tiempo solo si un guardrail se rompe de forma grave: rebote de la landing más de 10 puntos sobre el control, o más de 30% de desactivación de push. | Protege a los usuarios y al producto sin abrir la puerta a revisar resultados a mitad de camino. |

Los cálculos se verificaron con un script de Python que aplica las fórmulas anteriores. Antes de iniciar cada experimento se repiten con la línea base medida en la semana 0.

### 8.2.6. Methods Selection.

Cada método se eligió según qué se está comparando, qué tipo de dato produce y cuánto cuesta ejecutarlo con lo que Clair ya tiene construido.

| Hip. | Experimento | Método experimental | Prueba estadística | Herramienta | Por qué este método | Alternativas descartadas |
|---|---|---|---|---|---|---|
| H-01 | EXP-01 | **Prueba A/B** en producción, asignación por cuenta | Prueba z de dos proporciones con errores estándar agrupados por cuenta (equivalente a regresión logística con errores robustos por cuenta) | *Feature flag* en el backend (campo `experiment_variant` del contexto IAM) y Firebase Remote Config en móvil | Mide comportamiento real (alertas atendidas), no lo que el usuario dice que haría, que fue lo único que dieron las entrevistas | **Comparación antes y después:** se confunde con cambios en la calidad del aire. **Más entrevistas:** ya mostraron que el 100% quiere recomendaciones, pero no cuánto cambia la acción |
| H-02 | EXP-02 | **Prueba A/B** en la landing, en **diseño factorial 2×2** junto con EXP-05 | Prueba z de dos proporciones sobre el efecto principal; prueba de interacción | Asignación en el cliente con cookie y eventos en Google Analytics 4 | La landing es estática en Vercel, sin servidor propio; la asignación en el cliente es la opción más simple | **Pruebas multivariantes completas:** exigen mucho más tráfico del que hay |
| H-03 | EXP-03 | **Prueba de 5 segundos y de primer clic**, entre grupos (cada participante ve una sola versión) | Prueba z de dos proporciones; prueba exacta de Fisher si algún grupo es menor a 30 | Herramienta de pruebas de usabilidad no moderadas (Maze o Lyssna); si no hay licencia, un formulario con imágenes | El estado del aire debe entenderse de un vistazo, y la prueba de 5 segundos mide justo eso | **Prueba intra-sujeto:** el participante aprendería la respuesta en la primera versión. **Prueba moderada:** demasiado costosa para 90 personas |
| H-04 | EXP-04 | **Prueba A/B** en la app móvil, complementada con una **prueba de usabilidad moderada** de la tarea de crear una regla | Prueba z de dos proporciones (M-04); prueba U de Mann-Whitney (M-05, por la forma sesgada de los tiempos) | Firebase Remote Config y A/B Testing; eventos del flujo | La A/B mide cuántos terminan; la prueba moderada explica *dónde* se traban, y es lo que la tarjeta EXP-04 pide | **Solo prueba moderada:** muestra pequeña, no estima tasas |
| H-05 | EXP-05 | **Prueba A/B** en la landing (factorial con EXP-02) más **encuesta de un ítem** | Prueba U de Mann-Whitney sobre M-06 (escala ordinal), con la diferencia de medias y su intervalo de confianza; M-17 como guardrail | Google Analytics 4 y un componente propio de encuesta | La confianza es una percepción: solo una pregunta directa la mide, y la A/B asegura que la diferencia viene de la sección y no de quién visita | **Encuesta única a todos:** sin grupo de comparación no se sabe qué la causa |
| H-06 | EXP-06 | **Prueba A/B por cohorte de registro**: la cuenta se asigna al crearse, no por semana de calendario | Prueba t de Welch o U de Mann-Whitney sobre M-07 (con regresión binomial negativa como verificación de la sobredispersión del conteo); prueba binomial exacta unilateral sobre M-08 | Firebase Analytics y backend (Notifications) | Asignar por cuenta evita confundir el efecto con la semana del año o con campañas | **Comparar cohortes de semanas distintas:** mezcla el efecto del push con el efecto del calendario |

**Criterios comunes para el análisis**

- **Estimación con intervalos:** además del valor p, cada resultado se reporta con el tamaño del efecto y su intervalo de confianza de 90% (consistente con la prueba unilateral al 5%).
- **Hipótesis con dos criterios:** en H-04, la hipótesis solo se confirma si M-04 y M-05 alcanzan su meta; en H-05, la confianza (M-06) decide y la conversión (M-17) solo puede vetar.
- **Cada hipótesis, una decisión:** los seis experimentos no se promedian ni se ordenan entre sí; cada uno responde a su pregunta Q-xx del backlog de la sección 8.1.4.
- **Análisis reproducible:** el análisis se ejecuta con scripts de Python (las herramientas del equipo ya incluyen Python para analítica, sección 5.1.1) sobre datos exportados, de modo que cualquier integrante pueda repetirlo.

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection.

**Objetivos de analítica.** Cada objetivo parte de una pregunta de negocio y termina en las métricas que la responden.

| ID | Objetivo de negocio | Pregunta analítica | Etapa | KPI que la responde | Hip. |
|---|---|---|---|---|---|
| G-1 | Que más visitantes se conviertan en cuentas | ¿Qué parte de quienes llegan a la landing se registra, y confía en lo que mide Clair? | Adquisición | Tasa de conversión a registro; confianza declarada | H-02, H-05 |
| G-2 | Que cada cuenta nueva llegue pronto al primer valor | ¿Cuántas cuentas vinculan un dispositivo y reciben una lectura? ¿Cuánto tardan? | Activación | Tasa de activación; tiempo de instalación; tasa de reglas completadas | H-04 |
| G-3 | Que los usuarios actúen cuando hay una alerta | ¿Cuántas alertas terminan en una acción? ¿Se entiende el estado del aire? | Engagement | Alertas atendidas por espacio activo por semana (North Star); tasa de alertas atendidas; interpretación correcta | H-01, H-03 |
| G-4 | Que Clair se vuelva un hábito | ¿Cuántas veces por semana vuelven? ¿Siguen activos en la semana 2 y 4? | Retención | Sesiones semanales por usuario; retención semanal | H-06 |
| G-5 | Que usar Clair mejore el aire del espacio | ¿Cuánto tiempo pasa un espacio en WARNING o CRITICAL tras una alerta? | Resultado ambiental | Tiempo en estado crítico | (Q-02, siguiente ciclo) |
| G-6 | Que el modelo de suscripción sea sostenible | ¿Cuántas cuentas Free pasan a Premium y cuántas se quedan? | Monetización | Conversión Free → Premium; MRR; churn | (Q-08, siguiente ciclo) |

**Criterios de selección.** De las 13 métricas de la sección 8.2.2, un indicador pasa a ser **KPI** de este ciclo solo si cumple los cuatro criterios:

1. **Decide algo:** el equipo cambia una decisión de producto según su valor (por ejemplo, adoptar o descartar una variante).
2. **Se puede calcular:** sale de los eventos del plan de seguimiento (sección 8.2.8) sin esperar datos que todavía no existen.
3. **Se puede influir:** un cambio del equipo mueve la métrica; no depende de factores externos.
4. **No es una métrica de vanidad:** un número que solo sube (registros acumulados, visitas, descargas) no entra, porque no dice si el producto funciona.

**KPIs seleccionados**

| KPI | Fórmula | Fuente | Frecuencia | Meta o umbral | Decisión que habilita |
|---|---|---|---|---|---|
| **North Star:** alertas atendidas por espacio activo por semana | Alertas atendidas en la semana ÷ espacios con al menos una lectura en la semana | Alerting y Device | Semanal | Línea base de la semana 0 (sin meta previa) | Si el valor del producto crece o se estanca |
| Tasa de alertas atendidas (M-01) | Ver 8.2.3 | Alerting | Diaria durante EXP-01 | +15 puntos frente al control | Hacer obligatoria la recomendación (Q-01) |
| Tasa de conversión a registro (M-02) | Ver 8.2.3 | Landing y IAM | Diaria durante EXP-02 | +20% relativo, con rebote no mayor a +5 puntos | Rediseñar el hero (Q-03) |
| Confianza declarada (M-06) | Ver 8.2.3 | Landing | Diaria durante EXP-05 | +0.5 punto | Invertir en una prueba de calibración publicable (Q-04) |
| Interpretación correcta (M-03) | Ver 8.2.3 | Prueba de usabilidad | Al cierre de EXP-03 | 80% | Estandarizar el indicador de estado (Q-05) |
| Tasa de reglas completadas (M-04) y tiempo de tarea (M-05) | Ver 8.2.3 | App móvil | Diaria durante EXP-04 | +20 puntos y tiempo −30% | Reemplazar el flujo de reglas (Q-06) |
| Sesiones semanales por usuario (M-07) | Ver 8.2.3 | GA4 y Firebase | Semanal durante EXP-06 | +25% relativo | Priorizar la app móvil como canal (Q-07) |
| Tasa de activación | Cuentas con dispositivo vinculado y una lectura en 48 h ÷ cuentas creadas | IAM, Device y Evaluation | Semanal | Línea base de la semana 0 | Corregir el proceso de instalación (Q-10) |
| Tiempo de instalación | Mediana de minutos entre el registro y la primera lectura | Device y Evaluation | Semanal | Menos de 10 minutos (Q-10) | Mantener o corregir la afirmación "instalar toma pocos minutos" (C-03) |

**Métricas que no son KPI en este ciclo.** Conversión Free → Premium, MRR y churn dependen de una base de usuarios activa que todavía no existe; se registran, pero no se usan para decidir hasta el siguiente ciclo (Q-08). El tiempo en estado crítico necesita semanas de datos de uso real y también queda para el siguiente ciclo (Q-02).

**Guardrails**

| Guardrail | Medida | Umbral | Origen del umbral |
|---|---|---|---|
| Rebote de la landing | M-09 | No más de +5 puntos sobre el control | Criterio de H-02 (sección 8.2.1) |
| Entrega de push | M-13 | Al menos 95% | Propuesto por el equipo |
| Desactivación de push | M-14 | No más de 30% del grupo con push | Propuesto por el equipo |
| Latencia de la alerta | M-12 | No más de 60 segundos | Propuesto por el equipo |

**Tableros y ritmo de revisión**

| Tablero | Contenido | Frecuencia | Audiencia |
|---|---|---|---|
| Salud del experimento | Reparto entre grupos (V-01), volumen de eventos (V-02), guardrails y estado de los dispositivos | Diaria | Equipo de desarrollo |
| KPIs del producto | North Star y KPIs de la tabla anterior, por semana y por segmento | Semanal, en la revisión del sprint | Todo el equipo |
| Lectura del experimento | Resultado de cada hipótesis, con efecto, intervalo de confianza y decisión | Al cierre de cada experimento | Todo el equipo y docente |

Los tableros se arman en Looker Studio conectado a Google Analytics 4 y a consultas del backend (contexto Analytics); la lectura final de cada experimento se calcula con scripts de Python.

### 8.2.8. Web and Mobile Tracking Plan.

El plan de seguimiento define qué eventos se registran, cuándo se disparan y con qué propiedades, de manera que cada medida de la sección 8.2.3 se pueda calcular y verificar.

**Herramientas por plataforma** (propuesta del equipo)

| Plataforma | Tecnología | Herramienta de seguimiento | Justificación |
|---|---|---|---|
| Landing Page | Sitio estático en Vercel | Google Analytics 4 (`gtag.js`) con eventos personalizados | Es gratis y no requiere servidor propio |
| Web Application | Angular en Vercel | Google Analytics 4, mediante un servicio de analítica de Angular | Misma propiedad que la landing, para seguir al usuario desde la visita hasta el registro |
| Mobile Application | Flutter | Firebase Analytics (`firebase_analytics`) y Firebase Remote Config | El proyecto ya usa Firebase para distribuir la app (sección 7.2.1) |
| Web Services | Spring Boot en Dokploy | Registro en el contexto Analytics (base de datos del backend) | Es la fuente de verdad de alertas y notificaciones (sección 8.2.3) |

**Convenciones**

- Los nombres de evento van en `snake_case` con el formato `objeto_acción` (`alert_viewed`, `rule_saved`).
- Toda propiedad usa `snake_case` y un tipo fijo; los identificadores son siempre texto.
- **Identidad:** antes del registro se usa un `anonymous_id` (cookie en la landing); al completar `signup_completed` se enlaza con el `user_id`. El `user_id` es un UUID, nunca el correo.
- **Exposición:** el evento `experiment_exposure` se dispara una sola vez, la primera vez que el usuario ve la variante.
- **Privacidad:** no se envía ningún dato personal (nombre, correo, teléfono) en los eventos. La landing muestra un aviso de consentimiento de cookies y no activa el seguimiento hasta que el visitante acepta, en línea con la Ley N.º 29733, de Protección de Datos Personales.

**Propiedades comunes a todos los eventos**

| Propiedad | Tipo | Descripción |
|---|---|---|
| `platform` | texto | `landing`, `web`, `mobile` o `server` |
| `user_id` | texto | UUID de la cuenta; vacío antes del registro |
| `anonymous_id` | texto | Identificador anónimo del visitante |
| `segment` | texto | `facility_admin` o `home_user`, cuando se conoce |
| `plan` | texto | `free` o `premium` |
| `experiment_variants` | objeto | Variantes asignadas, por ejemplo `{"exp_01": "B", "exp_06": "A"}` |
| `app_version` | texto | Versión del sitio o de la aplicación |
| `timestamp` | fecha y hora | Momento del evento, en UTC |

**Eventos de la landing y de la aplicación web**

| ID | Evento | Se dispara cuando | Propiedades propias | Plataforma | Medida | Hip. |
|---|---|---|---|---|---|---|
| EV-01 | `experiment_exposure` | El visitante o usuario ve por primera vez la variante de un experimento | `experiment_id`, `variant` | Landing, web y móvil | Todas | Todas |
| EV-02 | `pricing_section_viewed` | La sección de precios del hero queda visible al menos un segundo | `variant`, `location` | Landing | M-10 | H-02 |
| EV-03 | `pricing_cta_clicked` | El visitante hace clic en el enlace a precios | `location` (`hero` o `pricing_page`) | Landing | M-10 | H-02 |
| EV-04 | `precision_section_viewed` | La sección "¿Qué tan preciso es Clair?" queda visible al menos un segundo | `variant` | Landing | M-16 | H-05 |
| EV-05 | `trust_survey_shown` | Se muestra la encuesta de confianza | `variant` | Landing | M-16 | H-05 |
| EV-06 | `trust_survey_answered` | El visitante responde la encuesta | `score` (1 a 5) | Landing | M-06, M-16 | H-05 |
| EV-07 | `signup_cta_clicked` | El visitante hace clic en un botón de registro | `cta_location` | Landing | M-02 | H-02, H-05 |
| EV-08 | `signup_started` | Se abre el formulario de registro | `source` | Web | M-02 | H-02, H-05 |
| EV-09 | `signup_completed` | La cuenta se crea con éxito | `source`, `segment` | Web y servidor | M-02, M-17 | H-02, H-05 |
| EV-10 | `alert_viewed` | El usuario ve el detalle de una alerta | `alert_id`, `severity`, `metric`, `has_recommendation` | Web y móvil | M-01 | H-01 |
| EV-11 | `recommendation_viewed` | La recomendación de la alerta queda visible | `alert_id`, `recommendation_id` | Web y móvil | M-01 | H-01 |
| EV-12 | `alert_action_done` | El usuario toca "Ya lo hice" | `alert_id`, `seconds_since_emitted` | Web y móvil | M-01, M-11 | H-01 |
| EV-13 | `alert_acknowledged` | El usuario reconoce la alerta (historia MA-US-22 del Capítulo III) | `alert_id`, `seconds_since_emitted` | Web y móvil | M-01, M-11 | H-01 |

**Eventos de la aplicación móvil**

| ID | Evento | Se dispara cuando | Propiedades propias | Medida | Hip. |
|---|---|---|---|---|---|
| EV-14 | `rule_creation_started` | El usuario abre el flujo para crear una regla | `entry_point`, `has_templates` | M-04, M-05 | H-04 |
| EV-15 | `rule_template_selected` | El usuario elige una plantilla | `template_id` | M-04 | H-04 |
| EV-16 | `rule_step_completed` | El usuario avanza un paso del flujo | `step_index` | M-04 | H-04 |
| EV-17 | `rule_validation_error` | El formulario muestra un error de validación | `field`, `error_type` | M-15 | H-04 |
| EV-18 | `rule_saved` | La regla se guarda con éxito | `rule_id`, `template_id`, `duration_ms` | M-04, M-05 | H-04 |
| EV-19 | `rule_creation_abandoned` | El usuario sale del flujo sin guardar | `last_step_index` | M-04 | H-04 |
| EV-20 | `push_permission_prompted` | La app pide permiso de notificaciones | — | M-14 | H-06 |
| EV-21 | `push_permission_result` | El usuario responde al permiso | `granted` (verdadero o falso) | M-14 | H-06 |
| EV-22 | `push_opened` | El usuario abre la aplicación desde una notificación | `notification_id`, `alert_id` | M-07 | H-06 |
| EV-23 | `push_disabled` | El usuario desactiva las notificaciones en los ajustes | — | M-14 | H-06 |
| EV-24 | `session_start` | Se inicia una sesión (evento automático de GA4 y Firebase) | — | M-07, M-08 | H-06 |

**Eventos del servidor** (fuente de verdad)

| ID | Evento | Se dispara cuando | Propiedades propias | Medida | Hip. |
|---|---|---|---|---|---|
| EV-25 | `alert_emitted` | El contexto Alerting emite una alerta | `alert_id`, `space_id`, `device_id`, `metric`, `severity`, `reading_at`, `emitted_at` | M-01, M-12 | H-01 |
| EV-26 | `alert_status_changed` | La alerta cambia a atendida o reconocida | `alert_id`, `status`, `via`, `changed_at` | M-01, M-11 | H-01 |
| EV-27 | `push_sent` | Notifications envía una notificación | `notification_id`, `alert_id` | M-13 | H-01, H-06 |
| EV-28 | `push_delivered` | FCM confirma la entrega | `notification_id` | M-13 | H-01, H-06 |
| EV-29 | `first_reading_received` | Se recibe la primera lectura de un dispositivo nuevo | `device_id`, `minutes_since_signup` | Tasa de activación y tiempo de instalación | — |

**Trazabilidad: cada medida con sus eventos**

| Medida | Numerador | Denominador |
|---|---|---|
| M-01 | EV-26 con `status` de atendida o reconocida dentro de 30 min (complementado por EV-12 y EV-13) | EV-25 |
| M-02 y M-17 | EV-09 con `experiment_exposure` en las 24 h previas | EV-01 únicos por visitante |
| M-04 | EV-18 | EV-14 |
| M-05 | `duration_ms` de EV-18 | — |
| M-06 | `score` de EV-06 | — |
| M-07 | EV-24 | Usuarios del grupo por semana |
| M-08 | Usuarios con EV-24 en la semana | Usuarios del grupo |
| M-13 | EV-28 | EV-27 |
| M-14 | Usuarios con EV-23 | Usuarios con push activado por defecto |

**H-03 no usa eventos de producción:** la interpretación correcta (M-03) se mide en la herramienta de la prueba de 5 segundos, porque se evalúa con participantes y no con usuarios reales.

**Verificación del plan antes de lanzar cada experimento**

1. **Prueba en entorno de pruebas** de cada evento con GA4 DebugView y Firebase DebugView, comprobando nombre, propiedades y tipo.
2. **Prueba automática** con Playwright (ya usado en la sección 6.1.3.2) que recorre la landing y la web y comprueba que los eventos esperados llegan al `dataLayer`.
3. **Conciliación con el backend:** antes de iniciar, se comparan los registros de EV-09 contra las cuentas realmente creadas, y los de EV-12 y EV-13 contra los estados de las alertas, hasta alcanzar el 95% de coincidencia (condición V-02).
4. **Monitoreo continuo:** el volumen diario de cada evento se vigila con las alertas del pipeline de monitoreo (sección 7.4); una caída de más de 20% frente al día anterior genera un aviso.
5. **Aviso de consentimiento:** se comprueba que ningún evento se envía antes de que el visitante acepte las cookies en la landing.

## 8.3. Experimentation

### 8.3.1. To-Be User Stories.

Las To-Be User Stories traducen las Experiment Cards de la sección 8.1.5 en cambios concretos de la landing page, la aplicación web, la aplicación móvil y los web services. Cada experimento tiene su propia épica (TB-EP-01 a TB-EP-06), de modo que la trazabilidad va de la pregunta del Question Backlog a la hipótesis de la sección 8.2.1 y de ahí a las historias que la hacen medible. Las historias describen las dos condiciones de la sección 8.2.4: la variante `A` mantiene el comportamiento actual (control) y la variante `B` incorpora el cambio (tratamiento). Así, ambas versiones conviven mientras dura la ventana del experimento.

La épica TB-EP-07 reúne las Technical Stories que asignan las variantes y registran los eventos del Tracking Plan de la sección 8.2.8; los nombres de eventos y sus identificadores (EV-xx) son los de ese plan, y ninguna historia introduce eventos ni medidas fuera de él. Las herramientas siguen lo decidido en la sección 8.2.6: la asignación por cuenta vive en el backend, EXP-04 usa Firebase Remote Config y la landing page asigna con una cookie. La épica TB-EP-08 recoge dos hallazgos de la auditoría recibida (sección 6.4.2) que no forman parte de un experimento, pero que apoyan la tasa de activación de la sección 8.2.2 sin tocar los flujos evaluados.

Los identificadores usan el prefijo `TB`, seguido del producto (`LP` landing page, `WA` aplicación web, `MA` aplicación móvil, `WS` web services) y del tipo (`US` User Story, `TS` Technical Story, `SP` Spike Story). En total son 24 historias: 12 User Stories, 10 Technical Stories y 2 Spike Stories.

**Épicas**

<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px;">
  <thead>
    <tr>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Epic ID</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Título</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Experimento / hipótesis / pregunta</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-01</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Alertas con recomendación accionable</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-01 / H-01 / Q-01</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero que cada alerta incluya una acción concreta según la métrica y la severidad, y poder registrar que la apliqué, para que pueda responder a un problema de calidad del aire sin interpretar valores técnicos.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-02</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Precio visible en la primera vista de la landing</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-02 / H-02 / Q-03</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Visitante, quiero conocer el costo del dispositivo y del plan desde la primera vista de la landing page, para que pueda decidir si me registro sin buscar el precio en otra sección.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-03</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Estado del aire con etiqueta de texto</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-03 / H-03 / Q-05</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero que el estado del aire se exprese con color, ícono y una etiqueta de texto, para que pueda entenderlo de un vistazo aunque no distinga los colores.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-04</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Plantillas de reglas en la aplicación móvil</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-04 / H-04 / Q-06</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario del segmento Home User, quiero crear una regla de alerta a partir de una plantilla, para que pueda configurar mis alertas en menos pasos y sin conocer los valores de cada métrica.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-05</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Evidencia de precisión del sensor</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-05 / H-05 / Q-04</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Visitante, quiero consultar cómo se verifica la precisión del sensor de Clair, para que pueda confiar en las mediciones antes de registrarme.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-06</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Notificaciones push activadas por defecto</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">EXP-06 / H-06 / Q-07</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario nuevo, quiero recibir las alertas en el celular desde el inicio, para que me entere de un problema de calidad del aire sin tener que abrir el panel web.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-07</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Asignación de variantes e instrumentación</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Condiciones de 8.2.4 y Tracking Plan de 8.2.8</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Desarrollador, quiero asignar las variantes de cada experimento, registrar los eventos del Tracking Plan y consultar los resultados por variante, para que el equipo pueda calcular las medidas de la sección 8.2.3 con datos confiables.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-08</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Mejoras derivadas de la auditoría recibida</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Hallazgos #6 y #9 de la sección 6.4.2</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero orientación al configurar umbrales y al empezar sin dispositivos, para que pueda dejar Clair funcionando sin ayuda externa.</td>
    </tr>
  </tbody>
</table>

<br>

**User Stories, Technical Stories y Spike Stories**

<!-- ========== HISTORIA TB-WS-TS-03 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-03</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asociar una recomendación a cada alerta según métrica y severidad</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero que el contexto Alerting asocie una recomendación a cada alerta según la métrica y la severidad, para que la aplicación web, la aplicación móvil y las notificaciones la presenten sin duplicar reglas de negocio.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Alerta con recomendación. Dado que el endpoint "/api/v1/alerts" está disponible y la cuenta tiene la variante `B` de EXP-01, cuando se envía una petición GET, entonces se recibe una respuesta con estado 200 y cada alerta incluye el objeto `recommendation` con `recommendation_id` y `text`.</li>
        <li>Escenario: Alerta del grupo control. Dado que la cuenta tiene la variante `A` de EXP-01, cuando se envía la petición GET a "/api/v1/alerts", entonces cada alerta incluye la métrica, el valor y la severidad, y no incluye el objeto `recommendation`.</li>
        <li>Escenario: Combinación sin recomendación. Dado que no existe una recomendación para la combinación de métrica y severidad de una alerta, cuando se responde a una cuenta con la variante `B`, entonces la alerta incluye la recomendación general de revisar el espacio y el servicio registra la combinación faltante en el log.</li>
        <li>Escenario: Recomendación estable durante la ventana. Dado que EXP-01 está en ejecución, cuando el equipo despliega otros cambios del backend, entonces los textos de las recomendaciones no cambian, como exige la condición V-06.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-04 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-04</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Registrar la acción del usuario ante una alerta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero registrar que el usuario aplicó la recomendación de una alerta a través de la API, para que la alerta cuente como atendida en la medida M-01.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Registrar acción. Dado que el endpoint "/api/v1/alerts/{alertId}/actions" está disponible y la alerta pertenece a la cuenta, cuando se envía una petición POST autenticada, entonces se recibe una respuesta con estado 201, la alerta pasa a atendida y el contexto Analytics registra `alert_status_changed` (EV-26) con `via` igual a `action`.</li>
        <li>Escenario: Acción repetida. Dado que la alerta ya tiene una acción registrada, cuando se envía nuevamente la petición POST, entonces se recibe una respuesta con estado 409 y no se registra un segundo evento.</li>
        <li>Escenario: Alerta de otra cuenta. Dado que la alerta no pertenece a la cuenta autenticada, cuando se envía la petición POST, entonces se recibe una respuesta con estado 404.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WA-US-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WA-US-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar la recomendación de una alerta y registrar la acción en la aplicación web</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero ver junto a cada alerta activa qué acción tomar y registrar que la apliqué, para que pueda responder al problema y dejar constancia de lo que hice.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que la cuenta tiene la variante `B` de EXP-01 y existe una alerta activa de CO₂, cuando el Usuario consulta la alerta, entonces el sistema presenta la métrica, el valor, la severidad y la recomendación de ventilar el espacio.</li>
        <li>Dado que la cuenta tiene la variante `A` de EXP-01, cuando el Usuario consulta una alerta activa, entonces el sistema presenta la métrica, el valor y la severidad sin recomendación.</li>
        <li>Dado que el Usuario de la variante `B` aplicó la recomendación, cuando registra la acción, entonces el sistema marca la alerta como atendida y registra `alert_action_done` (EV-12) con los segundos transcurridos desde la emisión.</li>
        <li>Dado que la recomendación queda visible para el Usuario, cuando el sistema la presenta, entonces el sistema registra `recommendation_viewed` (EV-11) con `alert_id` y `recommendation_id`.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar la recomendación de una alerta y registrar la acción en la aplicación móvil</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero ver en el celular qué acción tomar ante una alerta y registrar que la apliqué, para que pueda actuar desde donde esté.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que la cuenta tiene la variante `B` de EXP-01 y existe una alerta activa, cuando el Usuario consulta la alerta, entonces el sistema presenta la recomendación que corresponde a la métrica y la severidad.</li>
        <li>Dado que la cuenta tiene la variante `A` de EXP-01, cuando el Usuario consulta la alerta, entonces el sistema presenta la métrica, el valor y la severidad sin recomendación.</li>
        <li>Dado que el Usuario de la variante `B` registra que aplicó la recomendación, cuando el servicio confirma la acción, entonces el sistema muestra la alerta como atendida y registra `alert_action_done` (EV-12).</li>
        <li>Dado que el Usuario reconoce una alerta sin registrar una acción, cuando el servicio confirma el reconocimiento, entonces el sistema registra `alert_acknowledged` (EV-13), que también cuenta para M-01.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-02 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-02</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Recibir la recomendación en la notificación push de una alerta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero que la notificación push de una alerta incluya la acción recomendada, para que pueda actuar aunque no abra la aplicación.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que la cuenta tiene la variante `B` de EXP-01 y se emite una alerta en uno de sus espacios, cuando el sistema envía la notificación push, entonces la notificación incluye la métrica, el nombre del espacio y la recomendación.</li>
        <li>Dado que la cuenta tiene la variante `A` de EXP-01, cuando el sistema envía la notificación push de una alerta, entonces la notificación incluye la métrica, el nombre del espacio y el valor medido.</li>
        <li>Dado que el Usuario abre la aplicación desde la notificación, cuando la alerta queda visible, entonces el sistema registra `push_opened` (EV-22) con `notification_id` y `alert_id`.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-LP-TS-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-LP-TS-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asignar las variantes factoriales de la landing page</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero asignar a cada visitante una combinación de EXP-02 y EXP-05 con una cookie, para que ambos experimentos compartan el tráfico de la landing page en el diseño factorial 2×2 de la sección 8.2.4.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que un visitante acepta las cookies, cuando carga la landing page por primera vez, entonces el sitio crea un `anonymous_id` y asigna con hashes independientes una variante de EXP-02 y una de EXP-05, lo que produce una de las cuatro combinaciones.</li>
        <li>Dado que el visitante ya tiene una combinación asignada, cuando vuelve a la landing page, entonces el sitio presenta la misma combinación.</li>
        <li>Dado que el visitante ve por primera vez la variante de un experimento, cuando la condición se presenta, entonces el sitio registra `experiment_exposure` (EV-01) una sola vez por experimento.</li>
        <li>Dado que el visitante no acepta las cookies, cuando carga la landing page, entonces el sitio presenta la versión de control de ambos experimentos y no registra ningún evento, en línea con la Ley N.º 29733 citada en la sección 8.2.8.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-LP-US-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-LP-US-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Visitante</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Conocer el precio total desde la primera vista de la landing page</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante, quiero ver el precio del dispositivo y del plan Premium en la primera vista de la landing page, para que pueda estimar el costo de Clair antes de decidir si me registro.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante tiene la variante `B` de EXP-02, cuando carga la landing page, entonces la primera vista presenta el precio del dispositivo Clair Alpha, el plan Premium de S/ 29.90 al mes, el desglose entre pago único y pago mensual y la existencia del plan Free.</li>
        <li>Dado que el Visitante tiene la variante `A` de EXP-02, cuando carga la landing page, entonces la primera vista presenta la propuesta de valor actual sin precios.</li>
        <li>Dado que la información de precios queda visible al menos un segundo, cuando el sitio lo detecta, entonces el sitio registra `pricing_section_viewed` (EV-02) con la variante y la ubicación.</li>
        <li>Dado que el Visitante selecciona el enlace hacia la página de precios o hacia el registro, cuando el sitio lo procesa, entonces el sitio registra `pricing_cta_clicked` (EV-03) o `signup_cta_clicked` (EV-07) según corresponda.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-SP-02 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-SP-02</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-03</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Definir la herramienta de la prueba de 5 segundos</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero evaluar Maze, Lyssna y un formulario con imágenes para la prueba de 5 segundos de EXP-03, para que el equipo elija la opción que permite reclutar 90 participantes entre grupos con el presupuesto disponible.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que se revisan las tres opciones de la sección 8.2.6, cuando se comparan la asignación entre grupos, el límite de participantes del plan gratuito, el control del tiempo de exposición y la exportación de respuestas, entonces se presenta un documento con la opción elegida y su justificación.</li>
        <li>Dado que se eligió una opción, cuando se prepara una prueba piloto con tres personas del equipo, entonces la prueba muestra una sola versión por participante durante cinco segundos y exporta la respuesta de cada uno.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WA-US-02 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WA-US-02</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-03</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Ver el estado del aire con color, ícono y etiqueta en la aplicación web</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero que el estado del aire de cada espacio y dispositivo se exprese con color, ícono y la etiqueta Bueno, Moderado o Malo, para que pueda entenderlo sin depender solo del color.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el dispositivo tiene lecturas recientes y ninguna supera su umbral, cuando el Usuario consulta su estado, entonces el sistema presenta el nivel Bueno con su color, su ícono y su etiqueta.</li>
        <li>Dado que la evaluación más reciente del dispositivo tiene severidad LOW o WARNING, cuando el Usuario consulta su estado, entonces el sistema presenta el nivel Moderado; y si tiene severidad CRITICAL, entonces presenta el nivel Malo.</li>
        <li>Dado que el Usuario consulta el estado del aire en cualquier vista, cuando el sistema presenta el nivel, entonces el sistema ofrece una leyenda accesible que explica cada nivel y tiene un nombre legible por lectores de pantalla.</li>
        <li>Dado que el dispositivo no envía lecturas en los últimos 10 minutos, cuando el Usuario consulta su estado, entonces el sistema indica que el estado no está disponible y la hora de la última lectura.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-03 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-03</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-03</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Ver el estado del aire con color, ícono y etiqueta en la aplicación móvil</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero que el dashboard móvil muestre el estado del aire con color, ícono y etiqueta, para que pueda entenderlo de un vistazo incluso bajo luz solar directa.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario consulta el dashboard, cuando el sistema presenta el estado de cada espacio, entonces el sistema usa los mismos niveles, etiquetas e íconos que la aplicación web.</li>
        <li>Dado que el Usuario consulta la leyenda del estado, cuando el sistema la presenta, entonces el sistema explica qué significa cada nivel y qué acción general se sugiere.</li>
        <li>Dado que el equipo prepara el material de EXP-03, cuando captura la versión con etiqueta y la versión de control, entonces ambas capturas usan los mismos datos y solo difieren en la etiqueta y la leyenda.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-05 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-05</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-04</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar las plantillas de reglas de alerta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero obtener las plantillas de reglas a través de la API, para que la aplicación móvil precargue las métricas y los umbrales de cada plantilla.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Listar plantillas. Dado que el endpoint "/api/v1/rule-templates" está disponible, cuando se envía una petición GET autenticada, entonces se recibe una respuesta con estado 200 con las plantillas Oficina, Dormitorio y Local con público, cada una con sus métricas y valores de umbral.</li>
        <li>Escenario: Crear la regla desde una plantilla. Dado que el endpoint "/api/v1/devices/{deviceId}/thresholds" está disponible, cuando se envía una petición POST con los valores de una plantilla y el campo `template_id`, entonces se recibe una respuesta con estado 201 y el umbral queda asociado a la plantilla de origen.</li>
        <li>Escenario: Petición sin autenticación. Dado que el endpoint "/api/v1/rule-templates" está disponible, cuando se envía una petición GET sin token, entonces se recibe una respuesta con estado 401.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-04 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-04</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario del segmento Home User</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-04</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Crear una regla de alerta a partir de una plantilla</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario del segmento Home User, quiero elegir una plantilla al crear una regla de alerta, para que la regla quede configurada en menos pasos y pueda ajustarla si lo necesito.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario tiene la variante `B` de EXP-04 asignada por Firebase Remote Config, cuando inicia la creación de una regla, entonces el sistema ofrece las plantillas Oficina, Dormitorio y Local con público, y registra `rule_creation_started` (EV-14) con `has_templates` verdadero.</li>
        <li>Dado que el Usuario elige una plantilla, cuando el sistema la aplica, entonces el sistema precarga sus métricas y umbrales, permite modificarlos y registra `rule_template_selected` (EV-15).</li>
        <li>Dado que el Usuario tiene la variante `A` de EXP-04, cuando inicia la creación de una regla, entonces el sistema presenta el flujo actual de reglas personalizadas.</li>
        <li>Dado que el Usuario guarda la regla, cuando el servicio la confirma, entonces el sistema registra `rule_saved` (EV-18) con `duration_ms`; y si sale del flujo sin guardar, entonces registra `rule_creation_abandoned` (EV-19) con el último paso alcanzado.</li>
        <li>Dado que un valor ingresado no es válido, cuando el sistema valida el formulario, entonces el sistema indica el campo y el motivo, y registra `rule_validation_error` (EV-17).</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-SP-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-SP-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Definir el método de comparación del sensor con un equipo de referencia</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero definir cómo comparar las lecturas de Clair Alpha con un equipo de referencia durante 48 horas, para que la sección de precisión de EXP-05 publique evidencia verificable y no afirmaciones sin sustento.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que se investiga qué equipo de referencia puede conseguir el equipo para CO₂ y PM2.5, cuando se evalúan su disponibilidad, su certificado de calibración y su costo, entonces se presenta un documento con el equipo elegido o con la conclusión de que no hay uno disponible.</li>
        <li>Dado que existe un equipo de referencia, cuando se ejecuta una prueba piloto de 48 horas en un mismo espacio, entonces se documentan la diferencia promedio y la diferencia máxima entre ambos equipos para cada métrica.</li>
        <li>Dado que no se consigue un equipo de referencia, cuando se cierra el spike, entonces la historia TB-LP-US-02 se limita a la ficha técnica y al método de calibración, y el equipo lo comunica antes de lanzar EXP-05.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-LP-US-02 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-LP-US-02</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Visitante</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar la evidencia de precisión del sensor</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante, quiero consultar la ficha técnica de los sensores, el método de calibración y una comparación con un equipo de referencia, para que pueda evaluar si las mediciones de Clair son confiables.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante tiene la variante `B` de EXP-05, cuando recorre la landing page, entonces el sitio presenta la sección de precisión con la ficha técnica de los sensores, el método de calibración y la comparación documentada en TB-SP-01.</li>
        <li>Dado que el Visitante tiene la variante `A` de EXP-05, cuando recorre la landing page, entonces el sitio no presenta la sección de precisión.</li>
        <li>Dado que la sección de precisión queda visible al menos un segundo, cuando el sitio lo detecta, entonces el sitio registra `precision_section_viewed` (EV-04) con la variante.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-LP-US-03 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-LP-US-03</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Visitante</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Responder la encuesta de confianza en las mediciones</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante, quiero indicar cuánto confío en las mediciones de Clair, para que el equipo sepa si la información de la landing page genera confianza.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante aceptó las cookies y permanece 30 segundos en la landing page o llega al 50% de su recorrido, cuando se cumple la primera de esas condiciones, entonces el sitio presenta la pregunta "¿Confías en las mediciones de Clair?" con una escala de 1 a 5 y registra `trust_survey_shown` (EV-05).</li>
        <li>Dado que el Visitante responde la encuesta, cuando el sitio recibe la respuesta, entonces el sitio registra `trust_survey_answered` (EV-06) con el puntaje y no vuelve a presentar la encuesta a ese visitante.</li>
        <li>Dado que el Visitante cierra la encuesta sin responder, cuando vuelve a la landing page, entonces el sitio no presenta la encuesta otra vez.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-06 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-06</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-06</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asignar la cohorte de notificaciones al crear la cuenta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero asignar la variante de EXP-06 en el momento en que se crea una cuenta, para que el efecto de las notificaciones no se confunda con la semana de registro.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Asignar al registrarse. Dado que la ventana de reclutamiento de EXP-06 está abierta, cuando se confirma el registro de una cuenta, entonces el servicio asigna la variante `A` o `B` de EXP-06 y la guarda en el campo `experiment_variant` de la cuenta.</li>
        <li>Escenario: Notificaciones según la variante. Dado que la cuenta tiene la variante `B`, cuando se emite una alerta, entonces el contexto Notifications envía la notificación push; y si tiene la variante `A`, entonces la alerta queda disponible en el panel web sin notificación push.</li>
        <li>Escenario: Cuenta creada fuera de la ventana. Dado que la ventana de reclutamiento está cerrada, cuando se crea una cuenta, entonces el servicio no la incluye en EXP-06 y aplica la configuración de notificaciones vigente.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-05 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-05</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-06</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Recibir las alertas como notificaciones push desde el primer uso</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario nuevo, quiero que la aplicación active las notificaciones push al empezar, para que me entere de las alertas sin revisar el panel web.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que la cuenta tiene la variante `B` de EXP-06, cuando el Usuario abre la aplicación por primera vez, entonces el sistema solicita el permiso de notificaciones y registra `push_permission_prompted` (EV-20) y `push_permission_result` (EV-21).</li>
        <li>Dado que la cuenta tiene la variante `A` de EXP-06, cuando el Usuario abre la aplicación por primera vez, entonces el sistema no solicita el permiso y las alertas quedan disponibles en el panel web.</li>
        <li>Dado que el Usuario de cualquier variante quiere cambiar sus notificaciones, cuando las activa o desactiva en los ajustes, entonces el sistema respeta su elección y, si las desactiva, registra `push_disabled` (EV-23).</li>
        <li>Dado que el Usuario inicia una sesión en la aplicación, cuando la sesión comienza, entonces Firebase Analytics registra `session_start` (EV-24), que alimenta las medidas M-07 y M-08.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-07</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asignar la variante de un experimento por cuenta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero obtener la variante que el backend asigna a cada cuenta en EXP-01 y EXP-06, para que la aplicación web y la aplicación móvil presenten siempre la misma condición a la misma persona.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Obtener asignación. Dado que el endpoint "/api/v1/experiments/{experimentId}/assignment" está disponible y el experimento está activo, cuando se envía una petición GET autenticada, entonces se recibe una respuesta con estado 200 y el campo `variant` con el valor `A` (control) o `B` (tratamiento).</li>
        <li>Escenario: Asignación determinista. Dado que una cuenta ya tiene una variante asignada en un experimento, cuando se envía nuevamente la petición GET, entonces se recibe la misma variante y el campo `experiment_variant` de la cuenta en el contexto IAM no cambia.</li>
        <li>Escenario: Asignación independiente entre experimentos. Dado que la misma cuenta participa en EXP-01 y EXP-06, cuando se consulta la asignación de cada experimento, entonces cada variante sale de un hash distinto del identificador de la cuenta, como establece la sección 8.2.4.</li>
        <li>Escenario: Cuenta excluida. Dado que la cuenta pertenece al equipo o es de demostración, cuando se envía la petición GET, entonces se recibe la variante `A` y el campo `excluded` con valor verdadero, para que el análisis la descarte.</li>
        <li>Escenario: Experimento inexistente. Dado que no existe un experimento con el identificador indicado, cuando se envía la petición GET, entonces se recibe una respuesta con estado 404.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-02 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-02</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-07</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Registrar los eventos del servidor del Tracking Plan</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero que el contexto Analytics registre los eventos del servidor definidos en la sección 8.2.8, para que las medidas M-01, M-12 y M-13 se calculen desde la fuente de verdad del backend.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el contexto Alerting emite una alerta, cuando se completa la emisión, entonces el contexto Analytics registra el evento `alert_emitted` (EV-25) con `alert_id`, `space_id`, `device_id`, `metric`, `severity`, `reading_at` y `emitted_at`.</li>
        <li>Dado que una alerta pasa a atendida o reconocida, cuando el contexto Alerting guarda el cambio, entonces el contexto Analytics registra `alert_status_changed` (EV-26) con `status`, `via` y `changed_at`.</li>
        <li>Dado que el contexto Notifications envía una notificación push, cuando FCM confirma o no confirma la entrega, entonces el contexto Analytics registra `push_sent` (EV-27) y, si corresponde, `push_delivered` (EV-28).</li>
        <li>Dado que un dispositivo nuevo envía su primera lectura, cuando el contexto Evaluation la procesa, entonces el contexto Analytics registra `first_reading_received` (EV-29) con los minutos transcurridos desde el registro de la cuenta.</li>
        <li>Dado que se registra cualquier evento del servidor, cuando el contexto Analytics lo almacena, entonces el evento incluye las propiedades comunes de la sección 8.2.8 y no contiene nombre, correo ni teléfono del usuario.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WA-TS-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WA-TS-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-07</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Registrar los eventos de la aplicación web y atribuir el registro a la visita</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero que la aplicación web envíe a Google Analytics 4 los eventos del Tracking Plan y enlace el identificador anónimo con la cuenta al registrarse, para que la conversión a registro (M-02) se calcule desde la primera visita a la landing page.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que un visitante llega desde la landing page con un `anonymous_id`, cuando abre el formulario de registro, entonces la aplicación web registra `signup_started` (EV-08) con el `source` de la visita.</li>
        <li>Dado que la cuenta se crea con éxito, cuando el servicio confirma el registro, entonces la aplicación web registra `signup_completed` (EV-09) y enlaza el `anonymous_id` con el `user_id` de la cuenta.</li>
        <li>Dado que el usuario consulta una alerta, cuando el detalle queda disponible, entonces la aplicación web registra `alert_viewed` (EV-10) con `alert_id`, `severity`, `metric` y `has_recommendation`.</li>
        <li>Dado que el visitante no aceptó las cookies, cuando ocurre cualquiera de los eventos anteriores, entonces la aplicación web no envía ningún evento a Google Analytics 4.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-TS-01 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-TS-01</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-07</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Registrar los eventos de la aplicación móvil en Firebase Analytics</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero que la aplicación móvil registre en Firebase Analytics los eventos del Tracking Plan con la variante asignada, para que las medidas de EXP-01, EXP-04 y EXP-06 se calculen por grupo.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el usuario ve por primera vez una variante de un experimento, cuando la condición se presenta, entonces la aplicación registra `experiment_exposure` (EV-01) con `experiment_id` y `variant` una sola vez por experimento.</li>
        <li>Dado que se registra cualquier evento móvil, cuando Firebase Analytics lo recibe, entonces el evento incluye `platform` con valor `mobile`, el `user_id` y el objeto `experiment_variants` de la sección 8.2.8.</li>
        <li>Dado que el equipo prepara el lanzamiento de un experimento, cuando ejecuta la aplicación en el entorno de pruebas, entonces cada evento móvil del Tracking Plan aparece en Firebase DebugView con su nombre, sus propiedades y sus tipos.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WS-TS-07 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WS-TS-07</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Desarrollador</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-07</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar los resultados agregados por variante</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero consultar los conteos agregados de un experimento por variante, para que el equipo verifique el reparto (V-01), la completitud de eventos (V-02) y prepare el análisis de la sección 8.4.1 sin exportar datos personales.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Consultar resultados. Dado que el endpoint "/api/v1/experiments/{experimentId}/results" está disponible, cuando un usuario con rol administrador envía una petición GET, entonces se recibe una respuesta con estado 200 con la cantidad de unidades asignadas, expuestas y convertidas por variante.</li>
        <li>Escenario: Verificación del reparto. Dado que el experimento tiene unidades asignadas, cuando se consulta el resultado, entonces la respuesta incluye el valor p de la prueba χ² de desbalance de muestra definida en la condición V-01.</li>
        <li>Escenario: Usuario sin permisos. Dado que el endpoint está disponible, cuando un usuario sin rol administrador envía una petición GET, entonces se recibe una respuesta con estado 403.</li>
        <li>Escenario: Experimento inexistente. Dado que no existe un experimento con el identificador indicado, cuando se envía la petición GET, entonces se recibe una respuesta con estado 404.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-WA-US-03 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-WA-US-03</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Baja</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-08</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar valores de referencia al configurar un umbral en la aplicación web</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero conocer un valor de referencia para cada métrica al configurar un umbral en la aplicación web, para que pueda definir límites de alerta adecuados sin conocimientos técnicos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario configura un umbral de PM2.5, cuando el sistema presenta los datos de la métrica, entonces el sistema sugiere 15 µg/m³ e indica que corresponde a la guía de la Organización Mundial de la Salud para el promedio de 24 horas.</li>
        <li>Dado que el Usuario configura un umbral de CO₂, cuando el sistema presenta los datos de la métrica, entonces el sistema sugiere 1000 ppm como referencia de ventilación adecuada.</li>
        <li>Dado que el Usuario ingresa un valor distinto al sugerido, cuando guarda el umbral, entonces el sistema registra el valor ingresado.</li>
      </ul>
    </td>
  </tr>
</table>

<!-- ========== HISTORIA TB-MA-US-06 ========== -->
<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px; margin-bottom: 20px;">
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 15%;">Story ID</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 35%;">User</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 20%;">Priority</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; font-weight: bold; width: 30%;">Epic</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-MA-US-06</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Baja</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-08</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Seguir una guía de primeros pasos sin dispositivos vinculados</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario recién registrado, quiero que la aplicación me indique los pasos para vincular mi primer dispositivo, para que pueda empezar a monitorear sin ayuda externa.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario no tiene dispositivos vinculados, cuando consulta el dashboard, entonces el sistema informa que aún no hay dispositivos y presenta los pasos para crear un espacio y reclamar un dispositivo.</li>
        <li>Dado que el Usuario completa la vinculación y el dispositivo envía su primera lectura, cuando el backend la recibe, entonces se registra `first_reading_received` (EV-29), que alimenta la tasa de activación y el tiempo de instalación de la sección 8.2.2.</li>
        <li>Dado que el Usuario ya tiene dispositivos vinculados, cuando consulta el dashboard, entonces el sistema no presenta la guía de primeros pasos.</li>
      </ul>
    </td>
  </tr>
</table>

### 8.3.2. To-Be Product Backlog

El To-Be Product Backlog ordena las 24 historias de la sección 8.3.1 según el valor que aportan a responder las preguntas del Question Backlog (sección 8.1.4). La estimación usa la escala de story points 1, 2, 3, 5 y 8 del Capítulo III y suma 80 puntos. El orden sigue cuatro reglas:

1. **Primero la medición.** La asignación de variantes y los eventos del Tracking Plan (TB-EP-07) ocupan los primeros lugares, porque ningún experimento produce datos útiles sin ellos. Esto incluye la condición V-02, que exige que al menos el 95% de los eventos coincidan con el backend antes de iniciar.
2. **Después, cada experimento según la prioridad de su pregunta.** EXP-01 responde a Q-01, la pregunta de mayor puntaje, y sostiene la North Star Metric (alertas atendidas por espacio activo por semana). Junto a sus historias va el endpoint de resultados por variante, porque el tablero de salud de la sección 8.2.7 revisa el reparto entre grupos (V-01) desde el primer día.
3. **Los experimentos que comparten lanzamiento van juntos.** EXP-02 (Q-03, prioridad 2) y EXP-05 (Q-04) se ejecutan en el diseño factorial 2×2 de la landing page, así que sus historias, incluido el spike del equipo de referencia, se ordenan como un solo bloque. Les siguen EXP-03 (Q-05), EXP-04 (Q-06) y EXP-06 (Q-07), en el orden del Question Backlog.
4. **Al final, las mejoras de la auditoría.** Las dos historias de TB-EP-08 corrigen hallazgos de severidad 2 de la sección 6.4.2. No responden a una pregunta del backlog, y por eso no desplazan a ningún experimento.

| # Orden | User Story ID | Título | Descripción | Story Points ( 1 / 2 / 3 / 5 / 8 ) |
|---------|---------------|--------|-------------|------------------------------------|
| 1 | TB-WS-TS-01 | Asignar la variante de un experimento por cuenta | Como Desarrollador, quiero obtener la variante que el backend asigna a cada cuenta en EXP-01 y EXP-06, para que la aplicación web y la aplicación móvil presenten siempre la misma condición a la misma persona. | 5 |
| 2 | TB-WS-TS-02 | Registrar los eventos del servidor del Tracking Plan | Como Desarrollador, quiero que el contexto Analytics registre los eventos del servidor definidos en la sección 8.2.8, para que las medidas M-01, M-12 y M-13 se calculen desde la fuente de verdad del backend. | 5 |
| 3 | TB-WA-TS-01 | Registrar los eventos de la aplicación web y atribuir el registro a la visita | Como Desarrollador, quiero que la aplicación web envíe a Google Analytics 4 los eventos del Tracking Plan y enlace el identificador anónimo con la cuenta al registrarse, para que la conversión a registro (M-02) se calcule desde la primera visita a la landing page. | 3 |
| 4 | TB-MA-TS-01 | Registrar los eventos de la aplicación móvil en Firebase Analytics | Como Desarrollador, quiero que la aplicación móvil registre en Firebase Analytics los eventos del Tracking Plan con la variante asignada, para que las medidas de EXP-01, EXP-04 y EXP-06 se calculen por grupo. | 3 |
| 5 | TB-WS-TS-03 | Asociar una recomendación a cada alerta según métrica y severidad | Como Desarrollador, quiero que el contexto Alerting asocie una recomendación a cada alerta según la métrica y la severidad, para que la aplicación web, la aplicación móvil y las notificaciones la presenten sin duplicar reglas de negocio. | 5 |
| 6 | TB-WS-TS-04 | Registrar la acción del usuario ante una alerta | Como Desarrollador, quiero registrar que el usuario aplicó la recomendación de una alerta a través de la API, para que la alerta cuente como atendida en la medida M-01. | 3 |
| 7 | TB-WA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación web | Como Usuario, quiero ver junto a cada alerta activa qué acción tomar y registrar que la apliqué, para que pueda responder al problema y dejar constancia de lo que hice. | 3 |
| 8 | TB-MA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación móvil | Como Usuario, quiero ver en el celular qué acción tomar ante una alerta y registrar que la apliqué, para que pueda actuar desde donde esté. | 3 |
| 9 | TB-MA-US-02 | Recibir la recomendación en la notificación push de una alerta | Como Usuario, quiero que la notificación push de una alerta incluya la acción recomendada, para que pueda actuar aunque no abra la aplicación. | 3 |
| 10 | TB-WS-TS-07 | Consultar los resultados agregados por variante | Como Desarrollador, quiero consultar los conteos agregados de un experimento por variante, para que el equipo verifique el reparto (V-01), la completitud de eventos (V-02) y prepare el análisis de la sección 8.4.1 sin exportar datos personales. | 5 |
| 11 | TB-LP-TS-01 | Asignar las variantes factoriales de la landing page | Como Desarrollador, quiero asignar a cada visitante una combinación de EXP-02 y EXP-05 con una cookie, para que ambos experimentos compartan el tráfico de la landing page en el diseño factorial 2×2 de la sección 8.2.4. | 5 |
| 12 | TB-LP-US-01 | Conocer el precio total desde la primera vista de la landing page | Como Visitante, quiero ver el precio del dispositivo y del plan Premium en la primera vista de la landing page, para que pueda estimar el costo de Clair antes de decidir si me registro. | 2 |
| 13 | TB-SP-01 | Definir el método de comparación del sensor con un equipo de referencia | Como Desarrollador, quiero definir cómo comparar las lecturas de Clair Alpha con un equipo de referencia durante 48 horas, para que la sección de precisión de EXP-05 publique evidencia verificable y no afirmaciones sin sustento. | 3 |
| 14 | TB-LP-US-02 | Consultar la evidencia de precisión del sensor | Como Visitante, quiero consultar la ficha técnica de los sensores, el método de calibración y una comparación con un equipo de referencia, para que pueda evaluar si las mediciones de Clair son confiables. | 3 |
| 15 | TB-LP-US-03 | Responder la encuesta de confianza en las mediciones | Como Visitante, quiero indicar cuánto confío en las mediciones de Clair, para que el equipo sepa si la información de la landing page genera confianza. | 2 |
| 16 | TB-SP-02 | Definir la herramienta de la prueba de 5 segundos | Como Desarrollador, quiero evaluar Maze, Lyssna y un formulario con imágenes para la prueba de 5 segundos de EXP-03, para que el equipo elija la opción que permite reclutar 90 participantes entre grupos con el presupuesto disponible. | 2 |
| 17 | TB-WA-US-02 | Ver el estado del aire con color, ícono y etiqueta en la aplicación web | Como Usuario, quiero que el estado del aire de cada espacio y dispositivo se exprese con color, ícono y la etiqueta Bueno, Moderado o Malo, para que pueda entenderlo sin depender solo del color. | 3 |
| 18 | TB-MA-US-03 | Ver el estado del aire con color, ícono y etiqueta en la aplicación móvil | Como Usuario, quiero que el dashboard móvil muestre el estado del aire con color, ícono y etiqueta, para que pueda entenderlo de un vistazo incluso bajo luz solar directa. | 3 |
| 19 | TB-WS-TS-05 | Consultar las plantillas de reglas de alerta | Como Desarrollador, quiero obtener las plantillas de reglas a través de la API, para que la aplicación móvil precargue las métricas y los umbrales de cada plantilla. | 3 |
| 20 | TB-MA-US-04 | Crear una regla de alerta a partir de una plantilla | Como Usuario del segmento Home User, quiero elegir una plantilla al crear una regla de alerta, para que la regla quede configurada en menos pasos y pueda ajustarla si lo necesito. | 5 |
| 21 | TB-WS-TS-06 | Asignar la cohorte de notificaciones al crear la cuenta | Como Desarrollador, quiero asignar la variante de EXP-06 en el momento en que se crea una cuenta, para que el efecto de las notificaciones no se confunda con la semana de registro. | 3 |
| 22 | TB-MA-US-05 | Recibir las alertas como notificaciones push desde el primer uso | Como Usuario nuevo, quiero que la aplicación active las notificaciones push al empezar, para que me entere de las alertas sin revisar el panel web. | 3 |
| 23 | TB-WA-US-03 | Consultar valores de referencia al configurar un umbral en la aplicación web | Como Usuario, quiero conocer un valor de referencia para cada métrica al configurar un umbral en la aplicación web, para que pueda definir límites de alerta adecuados sin conocimientos técnicos. | 2 |
| 24 | TB-MA-US-06 | Seguir una guía de primeros pasos sin dispositivos vinculados | Como Usuario recién registrado, quiero que la aplicación me indique los pasos para vincular mi primer dispositivo, para que pueda empezar a monitorear sin ayuda externa. | 3 |

**Resumen por épica**

| Épica | Origen | Historias | Posiciones en el backlog | Story Points |
|---|---|---:|---|---:|
| TB-EP-07 Asignación de variantes e instrumentación | Condiciones de 8.2.4 y Tracking Plan de 8.2.8 | 5 | 1 a 4, 10 | 21 |
| TB-EP-01 Alertas con recomendación accionable | EXP-01 | 5 | 5 a 9 | 17 |
| TB-EP-02 Precio visible en la primera vista de la landing | EXP-02 | 2 | 11 a 12 | 7 |
| TB-EP-05 Evidencia de precisión del sensor | EXP-05 | 3 | 13 a 15 | 8 |
| TB-EP-03 Estado del aire con etiqueta de texto | EXP-03 | 3 | 16 a 18 | 8 |
| TB-EP-04 Plantillas de reglas en la aplicación móvil | EXP-04 | 2 | 19 a 20 | 8 |
| TB-EP-06 Notificaciones push activadas por defecto | EXP-06 | 2 | 21 a 22 | 6 |
| TB-EP-08 Mejoras derivadas de la auditoría recibida | Hallazgos #6 y #9 de la sección 6.4.2 | 2 | 23 a 24 | 5 |
| **Total** | | **24** | | **80** |

Las historias de una misma épica se entregan juntas, porque una variante incompleta rompería la condición V-06 (sin cambios en el flujo evaluado durante la ventana). Los Sprints To-Be de la sección 8.3.3.1 toman las historias en este orden.

### 8.3.3. Pipeline-supported, Experiment-Driven To-Be Software Platform Lifecycle

#### 8.3.3.1. To-Be Sprint Backlogs

Los Sprints To-Be toman las 24 historias del To-Be Product Backlog (sección 8.3.2) en su mismo orden y las descomponen en work items. El Sprint To-Be 1 cubre las posiciones 1 a 10 (38 story points) y el Sprint To-Be 2, las posiciones 11 a 24 (42 story points). Cada work item se estima en horas y tiene un responsable; los tasks generales, que no dependen de una historia, aseguran la condición V-02 antes de abrir la ventana de cada experimento.

El tablero del equipo está en Vikunja, el mismo de la sección 5.2.8. La captura muestra su estado actual: las tareas de pruebas, BDD y CI/CD figuran en Done y la actualización de Resend por el cambio de DNS, en To-Do. Los work items de esta sección se registrarán en ese tablero al iniciar cada Sprint To-Be.

<img src="https://i.imgur.com/KbqKXn0.png" alt="Kanban de Vikunja: tareas de implementación en Done y la actualización de Resend en To-Do">

**Sprint #: Sprint To-Be 1**

**Objetivo:** dejar lista la medición de los experimentos y entregar EXP-01 completo. Al cierre del Sprint, cada cuenta recibe una variante estable, los eventos del Tracking Plan llegan desde web, móvil y backend, y las alertas de la variante `B` muestran su recomendación en la web, en la app y en la notificación push.

| User Story Id | User Story Title | Work-Item Id | Work-Item Title | Description | Estimation (Hours) | Assigned To | Status |
|---|---|---|---|---|---:|---|---|
| TB-WS-TS-01 | Asignar la variante de un experimento por cuenta | TB-T01 | Modelar experimentos y variantes en IAM | Agregar la entidad del experimento y el campo `experiment_variant` de la cuenta, con su migración. | 5 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-WS-TS-01 | Asignar la variante de un experimento por cuenta | TB-T02 | Exponer la asignación por cuenta | Implementar GET `/api/v1/experiments/{experimentId}/assignment` con un hash por experimento y la exclusión de cuentas del equipo. | 6 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-WS-TS-02 | Registrar los eventos del servidor del Tracking Plan | TB-T03 | Registrar eventos de alertas en Analytics | Publicar `alert_emitted` y `alert_status_changed` desde Alerting hacia el contexto Analytics. | 6 | Dante Mateo Aleman Romano | To-do |
| TB-WS-TS-02 | Registrar los eventos del servidor del Tracking Plan | TB-T04 | Registrar eventos de push y de primera lectura | Registrar `push_sent`, `push_delivered` y `first_reading_received` con las propiedades comunes de 8.2.8. | 5 | Dante Mateo Aleman Romano | To-do |
| TB-WA-TS-01 | Registrar los eventos de la aplicación web y atribuir el registro a la visita | TB-T05 | Configurar Google Analytics 4 en la aplicación web | Crear el servicio de analítica de Angular con las propiedades comunes y el bloqueo de eventos sin consentimiento. | 5 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-WA-TS-01 | Registrar los eventos de la aplicación web y atribuir el registro a la visita | TB-T06 | Atribuir el registro a la visita | Enlazar el `anonymous_id` con el `user_id` y registrar `signup_started` y `signup_completed`. | 3 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-MA-TS-01 | Registrar los eventos de la aplicación móvil en Firebase Analytics | TB-T07 | Integrar Firebase Analytics en la app | Configurar `firebase_analytics` con las propiedades comunes y el evento `experiment_exposure`. | 5 | Iker Barturen | To-do |
| TB-MA-TS-01 | Registrar los eventos de la aplicación móvil en Firebase Analytics | TB-T08 | Verificar los eventos móviles | Comprobar en Firebase DebugView el nombre, las propiedades y los tipos de cada evento móvil. | 2 | Iker Barturen | To-do |
| TB-WS-TS-03 | Asociar una recomendación a cada alerta según métrica y severidad | TB-T09 | Definir el catálogo de recomendaciones | Redactar la recomendación de cada combinación de métrica y severidad, y la recomendación general. | 4 | Dante Mateo Aleman Romano | In-Process |
| TB-WS-TS-03 | Asociar una recomendación a cada alerta según métrica y severidad | TB-T10 | Incluir la recomendación en la API de alertas | Agregar el objeto `recommendation` a GET `/api/v1/alerts` solo para cuentas con la variante `B` de EXP-01. | 4 | Dante Mateo Aleman Romano | To-do |
| TB-WS-TS-04 | Registrar la acción del usuario ante una alerta | TB-T11 | Exponer el registro de acciones | Implementar POST `/api/v1/alerts/{alertId}/actions` con las respuestas 201, 404 y 409. | 5 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-WA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación web | TB-T12 | Presentar la recomendación en la alerta web | Mostrar la recomendación y el registro de la acción en el detalle de alerta según la variante. | 6 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-WA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación web | TB-T13 | Registrar los eventos de la alerta web | Enviar `recommendation_viewed` y `alert_action_done` con sus propiedades. | 2 | Luis Alonso Huaco Oliva | To-do |
| TB-MA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación móvil | TB-T14 | Presentar la recomendación en la alerta móvil | Mostrar la recomendación y el registro de la acción en la app según la variante. | 6 | Iker Barturen | To-do |
| TB-MA-US-01 | Consultar la recomendación de una alerta y registrar la acción en la aplicación móvil | TB-T15 | Registrar los eventos de la alerta móvil | Enviar `alert_action_done` y `alert_acknowledged` con sus propiedades. | 2 | Luis Alonso Huaco Oliva | To-do |
| TB-MA-US-02 | Recibir la recomendación en la notificación push de una alerta | TB-T16 | Incluir la recomendación en el push | Armar el contenido de la notificación en Notifications según la variante de EXP-01 y presentarlo en la app. | 6 | Iker Barturen | To-do |
| TB-MA-US-02 | Recibir la recomendación en la notificación push de una alerta | TB-T17 | Registrar la apertura desde el push | Enviar `push_opened` con `notification_id` y `alert_id`. | 2 | Iker Barturen | To-do |
| TB-WS-TS-07 | Consultar los resultados agregados por variante | TB-T18 | Exponer los resultados por variante | Implementar GET `/api/v1/experiments/{experimentId}/results` con conteos por variante, prueba χ² de V-01 y acceso solo para administradores. | 6 | Victor Nicolas Ortiz Alarcon | To-do |
| — | Task general del Sprint | TB-T19 | Automatizar la verificación de eventos web | Agregar a la suite de Playwright una prueba que compruebe que los eventos esperados llegan al `dataLayer`. | 4 | Luis Alonso Huaco Oliva | To-do |
| — | Task general del Sprint | TB-T20 | Conciliar eventos de EXP-01 con el backend | Comparar los eventos de cliente con los registros del backend hasta alcanzar el 95% de coincidencia de V-02. | 4 | Luis Alonso Huaco Oliva | To-do |

**Sprint #: Sprint To-Be 2**

**Objetivo:** lanzar los experimentos de la landing page, de comprensión del estado y de la aplicación móvil. Al cierre del Sprint, la landing page asigna las cuatro combinaciones del diseño factorial de EXP-02 y EXP-05, el indicador de estado con etiqueta está listo para la prueba de 5 segundos de EXP-03, la app ofrece plantillas de reglas (EXP-04) y asigna la cohorte de notificaciones al registrarse (EXP-06). Además, se incorporan las dos mejoras de la auditoría recibida.

| User Story Id | User Story Title | Work-Item Id | Work-Item Title | Description | Estimation (Hours) | Assigned To | Status |
|---|---|---|---|---|---:|---|---|
| TB-LP-TS-01 | Asignar las variantes factoriales de la landing page | TB-T21 | Asignar las combinaciones factoriales | Crear el `anonymous_id` en una cookie y asignar con hashes independientes las variantes de EXP-02 y EXP-05, solo con consentimiento. | 6 | Luis Alonso Huaco Oliva | To-do |
| TB-LP-TS-01 | Asignar las variantes factoriales de la landing page | TB-T22 | Registrar la exposición en la landing | Enviar `experiment_exposure` una vez por experimento y visitante. | 2 | Luis Alonso Huaco Oliva | To-do |
| TB-LP-US-01 | Conocer el precio total desde la primera vista de la landing page | TB-T23 | Construir el hero con precio | Presentar el precio del dispositivo, el plan Premium, el desglose y el plan Free en la variante `B` de EXP-02. | 4 | Luis Alonso Huaco Oliva | To-do |
| TB-LP-US-01 | Conocer el precio total desde la primera vista de la landing page | TB-T24 | Registrar los eventos de precio | Enviar `pricing_section_viewed`, `pricing_cta_clicked` y `signup_cta_clicked`. | 2 | Luis Alonso Huaco Oliva | To-do |
| TB-SP-01 | Definir el método de comparación del sensor con un equipo de referencia | TB-T25 | Evaluar el equipo de referencia | Comparar disponibilidad, certificado de calibración y costo de los equipos de referencia para CO₂ y PM2.5. | 4 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-SP-01 | Definir el método de comparación del sensor con un equipo de referencia | TB-T26 | Ejecutar la comparación piloto de 48 horas | Medir en un mismo espacio con Clair Alpha y el equipo de referencia, y documentar la diferencia promedio y máxima. | 6 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-LP-US-02 | Consultar la evidencia de precisión del sensor | TB-T27 | Construir la sección de precisión | Publicar la ficha técnica, el método de calibración y la comparación en la variante `B` de EXP-05. | 5 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-LP-US-02 | Consultar la evidencia de precisión del sensor | TB-T28 | Registrar la vista de la sección | Enviar `precision_section_viewed` con la variante. | 1 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-LP-US-03 | Responder la encuesta de confianza en las mediciones | TB-T29 | Construir la encuesta de confianza | Presentar la encuesta a los 30 segundos o al 50% del recorrido, una sola vez por visitante. | 4 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-LP-US-03 | Responder la encuesta de confianza en las mediciones | TB-T30 | Registrar los eventos de la encuesta | Enviar `trust_survey_shown` y `trust_survey_answered` con el puntaje. | 2 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-SP-02 | Definir la herramienta de la prueba de 5 segundos | TB-T31 | Elegir la herramienta de la prueba de 5 segundos | Comparar Maze, Lyssna y un formulario con imágenes, y ejecutar un piloto con tres personas del equipo. | 4 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-WA-US-02 | Ver el estado del aire con color, ícono y etiqueta en la aplicación web | TB-T32 | Construir el indicador de estado web | Mostrar color, ícono, etiqueta y leyenda accesible según la severidad de la evaluación más reciente. | 6 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-MA-US-03 | Ver el estado del aire con color, ícono y etiqueta en la aplicación móvil | TB-T33 | Construir el indicador de estado móvil | Aplicar los mismos niveles en el dashboard y preparar las capturas de ambas versiones para EXP-03. | 6 | Iker Barturen | To-do |
| TB-WS-TS-05 | Consultar las plantillas de reglas de alerta | TB-T34 | Exponer las plantillas de reglas | Implementar GET `/api/v1/rule-templates` y aceptar `template_id` al crear un umbral. | 6 | Dante Mateo Aleman Romano | To-do |
| TB-MA-US-04 | Crear una regla de alerta a partir de una plantilla | TB-T35 | Construir el flujo con plantillas | Ofrecer las plantillas en la variante `B` de EXP-04 leída desde Firebase Remote Config. | 8 | Luis Alonso Huaco Oliva | To-do |
| TB-MA-US-04 | Crear una regla de alerta a partir de una plantilla | TB-T36 | Registrar los eventos del flujo de reglas | Enviar los eventos EV-14 a EV-19 con `duration_ms` y el último paso alcanzado. | 3 | Iker Barturen | To-do |
| TB-WS-TS-06 | Asignar la cohorte de notificaciones al crear la cuenta | TB-T37 | Asignar EXP-06 al crear la cuenta | Asignar la variante al confirmar el registro y condicionar el envío de push a la variante `B`. | 5 | Dante Mateo Aleman Romano | To-do |
| TB-MA-US-05 | Recibir las alertas como notificaciones push desde el primer uso | TB-T38 | Solicitar el permiso de notificaciones según la variante | Pedir el permiso al primer uso en la variante `B` y respetar los cambios en los ajustes. | 5 | Iker Barturen | To-do |
| TB-MA-US-05 | Recibir las alertas como notificaciones push desde el primer uso | TB-T39 | Registrar los eventos de notificaciones | Enviar los eventos EV-20 a EV-23 y comprobar `session_start`. | 2 | Iker Barturen | To-do |
| TB-WA-US-03 | Consultar valores de referencia al configurar un umbral en la aplicación web | TB-T40 | Mostrar valores de referencia de umbrales | Sugerir 15 µg/m³ para PM2.5 y 1000 ppm para CO₂ al configurar un umbral en la web. | 3 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-MA-US-06 | Seguir una guía de primeros pasos sin dispositivos vinculados | TB-T41 | Construir la guía de primeros pasos | Presentar los pasos para crear un espacio y reclamar el primer dispositivo cuando la cuenta no tiene dispositivos. | 5 | Iker Barturen | To-do |
| — | Task general del Sprint | TB-T42 | Conciliar eventos de landing y app | Verificar V-02 para EXP-02, EXP-04, EXP-05 y EXP-06 antes de abrir sus ventanas. | 4 | Dante Mateo Aleman Romano | To-do |

**Carga por integrante**

| Integrante | Sprint To-Be 1 (horas) | Sprint To-Be 2 (horas) | Total |
|---|---:|---:|---:|
| Anderson Ricardo Ventosilla Trujillo | 14 | 19 | 33 |
| Dante Mateo Aleman Romano | 19 | 15 | 34 |
| Iker Barturen | 21 | 21 | 42 |
| Luis Alonso Huaco Oliva | 12 | 22 | 34 |
| Victor Nicolas Ortiz Alarcon | 22 | 16 | 38 |
| **Total** | **88** | **93** | **181** |

Ambos Sprints usan el pipeline del Capítulo VII: GitHub Actions verifica cada Pull Request, Dokploy recibe los despliegues del backend y de la aplicación web, y Vercel publica la landing page. Una historia solo pasa a Done cuando sus eventos superan las comprobaciones de identidad, consentimiento y conciliación del Tracking Plan (sección 8.2.8), porque una variante sin datos confiables no sirve para decidir.

#### 8.3.3.2. Implemented To-Be Landing Page Evidence

La landing page To-Be incorporará el precio total desde la primera vista, una explicación verificable de la precisión del sensor y los eventos necesarios para EXP-02 y EXP-05. Estos cambios todavía no están implementados en producción; la versión As-Is permanece disponible en https://site-beige-mu.vercel.app/ y no debe presentarse como evidencia de las variantes experimentales.

La evidencia se completará con capturas de ambas condiciones, la versión publicada y la comprobación de eventos después del Sprint correspondiente.

#### 8.3.3.3. Implemented To-Be Frontend-Web Application Evidence

La aplicación web To-Be mostrará etiquetas textuales accesibles para el estado del aire, recomendaciones accionables en las alertas y valores de referencia al configurar umbrales. La versión actual de https://clair-ui.vercel.app/ sigue siendo la experiencia As-Is y las variantes de EXP-01 y EXP-03 aún no están implementadas en producción.

La evidencia futura incluirá la pantalla de la variante, su asignación mediante feature flag y la verificación del evento correspondiente.

#### 8.3.3.4. Implemented To-Be Native-Mobile Application Evidence

La aplicación móvil To-Be incluirá el estado con texto e ícono, recomendaciones en notificaciones, registro de la acción tomada y una guía para vincular el primer dispositivo. No existe una URL pública de la compilación Flutter y estas historias todavía no están distribuidas a usuarios; por tanto, no se afirma que EXP-01, EXP-03, EXP-04 o EXP-06 estén en ejecución.

La evidencia se incorporará mediante una captura de la compilación Flutter, la versión distribuida y la comprobación de eventos en Firebase DebugView.

#### 8.3.3.5. Implemented To-Be RESTful API and/or Serverless Backend Evidence

El backend To-Be registrará eventos de producto, asignará variantes, asociará recomendaciones a las alertas y expondrá resultados agregados solo a administradores. La API As-Is permanece en https://clair-api.giks.net/; los endpoints y cambios del To-Be aún no están desplegados y no se presentan como funcionalidad disponible.

La evidencia incluirá la documentación OpenAPI, la ejecución de pruebas y la conciliación entre eventos y registros del backend exigida por V-02.

#### 8.3.3.6. Team Collaboration Insights

La evolución colaborativa del informe se encuentra trazada en `versions.md`, donde se conservan los bloques AV1, TB1 y A2 con sus aportes, commits y Pull Requests. La captura de analítica correspondiente al A2 se añadirá cuando el equipo obtenga la vista definitiva de GitHub y deberá coincidir con ese registro.

*Evidencia disponible: el historial de contribuciones del repositorio puede consultarse en [GitHub Contributors](https://github.com/bananawire/deis-report/graphs/contributors) y el detalle por entrega en `versions.md`. La captura de analítica del A2 se incorporará cuando el equipo obtenga la vista definitiva.*

### 8.3.4. To-Be Validation Interviews

#### 8.3.4.1. Diseño de Entrevistas.

Las entrevistas To-Be se realizarán después de publicar las variantes y reunir una primera ventana de exposición. Se convocarán entre tres y cinco participantes del segmento Facility Admin y entre tres y cinco del segmento Home User. Cada sesión solicitará interpretar el estado con y sin etiqueta de EXP-03, revisar una alerta con recomendación y explicar la acción que tomaría para EXP-01, y completar la creación de una regla con plantilla para EXP-04. Se registrarán éxito de tarea, tiempo, errores, comprensión, confianza y comentarios, junto con el consentimiento para la grabación.

El guion no se ejecutará antes del despliegue, porque mostrar únicamente diseños estáticos no permitiría contrastar la interacción real ni los eventos definidos en 8.2.8. A la fecha de este informe, las variantes no están en producción y las entrevistas To-Be no se han realizado.

#### 8.3.4.2. Registro de Entrevistas.

El registro permanece vacío porque todavía no se han ejecutado las entrevistas posteriores a los experimentos. No se incorporan nombres, capturas, tiempos ni testimonios sin una sesión real y su consentimiento. La única evidencia completada corresponde a las seis sesiones As-Is documentadas en la sección 6.3, que se conserva como línea cualitativa de referencia.

## 8.4. Experiment Aftermath & Analysis

### 8.4.1. Analysis and Interpretation of Results

Los experimentos de producción aún no cuentan con resultados: las variantes no están desplegadas y no se dispone de las muestras calculadas en 8.2.5. En particular, H-02 requiere alrededor de 21 920 visitantes únicos y H-06 requiere 224 usuarios nuevos. Ejecutar una ventana menor puede producir una señal exploratoria, pero no permite aceptar ni rechazar las hipótesis con la potencia acordada.

La evidencia disponible es cualitativa. Las seis sesiones de 6.3 alcanzaron una utilidad percibida promedio de 4.5/5, lo que apoya de forma direccional el criterio de utilidad del 70%, pero expresa intención declarada y no acción observada. Los seis participantes recomendarían Clair de forma explícita o implícita, aunque eso no equivale a la conversión del 60%. La comprensión del indicador basado solo en color permanece abierta por el problema heurístico 4, y tampoco se midió todavía el uso recurrente del 70%.

| Hipótesis | Resultado disponible | Decisión actual | Próximo paso |
|---|---|---|---|
| H-01 | Sin datos de producción sobre alertas atendidas; las entrevistas piden recomendaciones | No aceptar ni rechazar | Ejecutar EXP-01 y calcular M-01 por cuenta |
| H-02 | Sin datos de producción sobre conversión; existen dudas cualitativas sobre precio | No aceptar ni rechazar | Alcanzar la ventana de tráfico de EXP-02 y vigilar M-09 |
| H-03 | Sin datos experimentales; el uso exclusivo de color sigue como hallazgo | No aceptar ni rechazar | Ejecutar la prueba entre grupos de EXP-03 y medir M-03 |
| H-04 | Sin datos de producción sobre reglas completadas o tiempo | No aceptar ni rechazar | Ejecutar EXP-04 y analizar M-04 y M-05 conjuntamente |
| H-05 | Sin datos experimentales; cinco participantes pidieron evidencia de precisión | No aceptar ni rechazar | Ejecutar EXP-05 y medir M-06 sin deteriorar M-17 |
| H-06 | Sin datos de producción sobre sesiones o retención | No aceptar ni rechazar | Reclutar 224 usuarios y observar M-07 y M-08 |

### 8.4.2. Re-scored and Re-prioritized Question Backlog

La priorización se actualiza al cierre documental del A2. Como ningún experimento fue ejecutado, la incertidumbre se mantiene alta. La facilidad de Q-03 y Q-04 disminuye por el tráfico y las respuestas necesarias; Q-01 permanece primero por su impacto directo y porque aprovecha el sistema de alertas existente. Q-02 y Q-08 siguen diferidas hasta contar con uso sostenido.

| Prioridad | ID | Impacto | Incertidumbre | Facilidad | Puntaje | Razón de la nueva posición |
|---:|---|---:|---:|---:|---:|---|
| 1 | Q-01 | 5 | 5 | 4 | 14 | Responde al hallazgo de severidad 3 y mide una acción observable |
| 2 | Q-05 | 4 | 4 | 5 | 13 | Puede evaluarse sin depender del tráfico de producción |
| 3 | Q-06 | 4 | 4 | 4 | 12 | El flujo móvil existe, pero necesita instrumentación y usuarios |
| 4 | Q-03 | 4 | 5 | 2 | 11 | El efecto esperado exige más tráfico del disponible |
| 5 | Q-04 | 4 | 5 | 2 | 11 | Requiere evidencia técnica y suficientes respuestas a la encuesta |
| 6 | Q-07 | 4 | 4 | 3 | 11 | Necesita una cohorte nueva y tres semanas de observación |
| 7 | Q-10 | 4 | 3 | 3 | 10 | Puede medirse cuando existan dispositivos y cuentas nuevas |
| 8 | Q-02 | 5 | 4 | 1 | 10 | Se difiere hasta contar con alertas y acciones suficientes |
| 9 | Q-08 | 5 | 4 | 1 | 10 | Se difiere hasta que usuarios Free alcancen los límites del plan |
| 10 | Q-09 | 3 | 4 | 2 | 9 | Depende de demostrar primero el valor de la recomendación fija |

## 8.5. Continuous Learning

### 8.5.1. Shareback Session Artifacts: Learning Workflow

El ciclo de aprendizaje comenzará con una revisión diaria del tablero de salud del experimento para detectar desbalance, eventos incompletos y ruptura de guardrails. Cada semana, el equipo revisará la North Star y los KPIs por segmento sin detener anticipadamente los experimentos por resultados favorables. Al cierre de cada ventana se elaborará una lectura con tamaño del efecto, intervalo de confianza, condición de validez y decisión; las notas se conservarán en este informe y originarán la actualización del Question Backlog y del registro de versiones.

La primera sesión de shareback está programada después del segundo Sprint To-Be de 8.3.3.1 y todavía no ha ocurrido. Por ello, no se presentan actas ni decisiones como evidencia completada.

## 8.6. To-Be Software Platform Pre-launch

### 8.6.1. About-the-Product Intro Video

La sección 5.3 conserva el video As-Is About-the-Product de 46 segundos en https://bit.ly/4olR1cf. El video introductorio To-Be deberá mostrar los cambios validados e incluir un testimonio positivo autorizado de un participante; todavía no ha sido grabado y no existe un enlace adicional que pueda reportarse como evidencia.

### 8.6.2. Resumen usando Gees FrameWork

El equipo aplica un marco Goal-Question-Metric para mantener la trazabilidad entre el valor que espera generar, la pregunta que debe responder y la medida que sustenta la decisión. Este resumen no sustituye la ejecución experimental ni convierte los objetivos en resultados.

| Goal | Question | Metric |
|---|---|---|
| H-01: aumentar la respuesta útil ante alertas | ¿La recomendación accionable aumenta las alertas atendidas? | M-01, tasa de alertas atendidas |
| H-02: reducir incertidumbre comercial | ¿Mostrar el precio desde la primera vista aumenta el registro? | M-02, conversión a registro |
| H-03: hacer comprensible y accesible el estado | ¿El texto junto al color mejora la interpretación? | M-03, interpretación correcta |
| H-04: simplificar la configuración de alertas | ¿Las plantillas aumentan reglas completadas y reducen el tiempo? | M-04 y M-05, completitud y tiempo |
| H-05: sustentar la confianza en el sensor | ¿La evidencia de precisión aumenta la confianza? | M-06, confianza declarada |
| H-06: favorecer el uso recurrente | ¿Las notificaciones push aumentan las sesiones semanales? | M-07, sesiones semanales por usuario |

