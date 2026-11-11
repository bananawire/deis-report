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

### 8.2.4. Conditions.

### 8.2.5. Scale Calculations and Decisions.

### 8.2.6. Methods Selection.

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection.

### 8.2.8. Web and Mobile Tracking Plan.

### 8.3. Experimentation

### 8.3.1. To-Be User Stories.

### 8.3.2. To-Be Product Backlog

### 8.3.3. Pipeline-supported, Experiment-Driven To-Be Software Platform Lifecycle

#### 8.3.3.1. To-Be Sprint Backlogs

#### 8.3.3.2. Implemented To-Be Landing Page Evidence

#### 8.3.3.3. Implemented To-Be Frontend-Web Application Evidence

#### 8.3.3.4. Implemented To-Be Native-Mobile Application Evidence

#### 8.3.3.5. Implemented To-Be RESTful API and/or Serverless Backend Evidence

#### 8.3.3.6. Team Collaboration Insights

### 8.3.4. To-Be Validation Interviews

#### 8.3.4.1. Diseño de Entrevistas.

#### 8.3.4.2. Registro de Entrevistas.

## 8.4. Experiment Aftermath & Analysis

### 8.4.1. Analysis and Interpretation of Results

### 8.4.2. Re-scored and Re-prioritized Question Backlog

## 8.5. Continuous Learning

### 8.5.1. Shareback Session Artifacts: Learning Workflow

## 8.6. To-Be Software Platform Pre-launch

### 8.6.1. About-the-Product Intro Video

### 8.6.2. Resumen usando Gees FrameWork

