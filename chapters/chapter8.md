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

Las To-Be User Stories describen los cambios que Clair necesita para ejecutar los experimentos del Capítulo VIII. Cada épica parte de una de las hipótesis Lean UX de la sección 1.2.2.3 y de los hallazgos de la auditoría recibida en la sección 6.4.2, que mostraron que los usuarios ven los datos de calidad del aire pero no siempre saben qué significan ni qué hacer con ellos. Las User Stories de las épicas TB-EP-01 a TB-EP-04 definen el comportamiento de la condición experimental y, cuando corresponde, el de la condición de control, para que ambas versiones convivan durante el experimento. La épica TB-EP-05 reúne las Technical Stories y la Spike Story que permiten asignar variantes, registrar eventos y consultar resultados; sin ellas no habría datos para aceptar o rechazar ninguna hipótesis.

Los identificadores usan el prefijo `TB` para distinguirlos de las User Stories del Capítulo III, seguido del producto (`LP` landing page, `WA` aplicación web, `MA` aplicación móvil, `WS` web services) y del tipo (`US` User Story, `TS` Technical Story, `SP` Spike Story). Los nombres de eventos, como `alert_viewed` o `demo_requested`, se mantienen en inglés para respetar la convención de nomenclatura del código.

**Épicas**

<table style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif; font-size: 14px;">
  <thead>
    <tr>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Epic ID</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Título</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Hipótesis asociada</th>
      <th style="border: 1px solid #ccc; padding: 8px; background-color: #f2f2f2; text-align: left;">Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-01</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Comprensión del estado del aire en lenguaje claro</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Hipótesis 1 - comprensión</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero que Clair exprese el estado del aire con un nivel, una etiqueta textual y una explicación breve, para que pueda decidir si mi ambiente es seguro sin interpretar valores técnicos.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-02</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Alertas con recomendaciones accionables</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Hipótesis 2 - utilidad de las recomendaciones</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero que cada alerta incluya una acción concreta según la métrica y la gravedad, para que pueda responder a un problema de calidad del aire sin buscar información adicional.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-03</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Consulta recurrente y primeros pasos</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Hipótesis 3 - intención de uso</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Usuario, quiero recibir resúmenes periódicos y una guía para vincular mi primer dispositivo, para que pueda incorporar Clair a mi rutina con poco esfuerzo.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-04</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Conversión desde la landing page</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Hipótesis 4 - adopción</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Visitante, quiero conocer resultados concretos, el costo total de los planes y una forma directa de solicitar una demostración, para que pueda decidir si Clair se ajusta a mi establecimiento o a mi hogar.</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">TB-EP-05</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Instrumentación de experimentos</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Soporte transversal a las hipótesis 1 a 4</td>
      <td style="border: 1px solid #ccc; padding: 8px; vertical-align: top;">Como Desarrollador, quiero asignar variantes de experimento, registrar eventos de producto y consultar resultados por variante, para que el equipo pueda medir cada experimento con datos de uso reales.</td>
    </tr>
  </tbody>
</table>

<br>

**User Stories, Technical Stories y Spike Stories**

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
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Ver el estado del aire en lenguaje claro en la aplicación web</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero ver el estado de la calidad del aire de cada dispositivo como un nivel con etiqueta textual y una explicación breve, para que pueda entender si el ambiente es seguro sin interpretar valores técnicos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario pertenece al grupo experimental y consulta un dispositivo con lecturas recientes, cuando el sistema calcula el estado del aire, entonces el sistema presenta el nivel (Bueno, Moderado o Crítico), su etiqueta textual y una explicación de una oración sobre su significado.</li>
        <li>Dado que el Usuario pertenece al grupo de control, cuando consulta el mismo dispositivo, entonces el sistema presenta los valores numéricos de cada métrica sin la explicación en lenguaje claro.</li>
        <li>Dado que el sistema recibe una nueva lectura que cambia el nivel del dispositivo, cuando el Usuario mantiene abierta la consulta, entonces el sistema actualiza el nivel, la etiqueta y la explicación sin requerir una nueva consulta.</li>
        <li>Dado que el dispositivo no reporta lecturas en los últimos 10 minutos, cuando el Usuario consulta su estado, entonces el sistema indica que el estado no está disponible y muestra la hora de la última lectura recibida.</li>
        <li>Dado que el sistema presenta el estado del aire al Usuario, cuando la información queda disponible, entonces el sistema registra el evento air_status_viewed con la variante asignada.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Ver el estado del aire en lenguaje claro en la aplicación móvil</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero ver en la aplicación móvil el estado del aire de mis espacios como un nivel con etiqueta textual y una explicación breve, para que pueda entender la situación desde el celular en pocos segundos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario pertenece al grupo experimental y tiene dispositivos con lecturas recientes, cuando consulta el dashboard, entonces el sistema presenta para cada espacio el nivel, su etiqueta textual y una explicación de una oración.</li>
        <li>Dado que el Usuario pertenece al grupo de control, cuando consulta el dashboard, entonces el sistema presenta los valores numéricos de cada métrica sin la explicación en lenguaje claro.</li>
        <li>Dado que el nivel de un espacio es Crítico, cuando el sistema presenta el estado, entonces el sistema distingue el nivel mediante la etiqueta textual y un ícono, además del color.</li>
        <li>Dado que el sistema presenta el estado del aire al Usuario, cuando la información queda disponible, entonces el sistema registra el evento air_status_viewed con la plataforma móvil y la variante asignada.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-01</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar valores de referencia al configurar un umbral</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero conocer un valor de referencia sugerido para cada métrica al configurar un umbral, para que pueda definir límites de alerta adecuados sin conocimientos técnicos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario inicia la configuración de un umbral de PM2.5, cuando el sistema presenta los datos de la métrica, entonces el sistema sugiere 15 µg/m³ como valor de referencia e indica que corresponde a la guía de la Organización Mundial de la Salud para el promedio de 24 horas.</li>
        <li>Dado que el Usuario inicia la configuración de un umbral de CO₂, cuando el sistema presenta los datos de la métrica, entonces el sistema sugiere 1000 ppm como valor de referencia de ventilación adecuada.</li>
        <li>Dado que el Usuario acepta el valor sugerido, cuando guarda el umbral, entonces el sistema registra el umbral y el evento threshold_suggestion_accepted.</li>
        <li>Dado que el Usuario ingresa un valor distinto al sugerido, cuando guarda el umbral, entonces el sistema registra el valor ingresado y el evento threshold_suggestion_modified.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asociar una recomendación a cada alerta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero que el servicio de alertas asocie una recomendación a cada alerta según la métrica y la gravedad, para que las aplicaciones web y móvil la presenten sin duplicar reglas de negocio.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Consultar alerta con recomendación. Dado que el endpoint "/api/v1/alerts" está disponible y el usuario pertenece al grupo experimental, cuando se envía una petición GET, entonces se recibe una respuesta con estado 200 y cada alerta incluye los campos `recommendationCode` y `recommendationText`.</li>
        <li>Escenario: Combinación sin recomendación configurada. Dado que no existe una recomendación para la combinación de métrica y gravedad de una alerta, cuando se envía una petición GET a "/api/v1/alerts", entonces la alerta incluye la recomendación general `REVIEW_SPACE` y el servicio registra la combinación faltante en el log.</li>
        <li>Escenario: Usuario del grupo de control. Dado que el usuario pertenece al grupo de control, cuando se envía una petición GET a "/api/v1/alerts", entonces se recibe una respuesta con estado 200 y las alertas no incluyen los campos de recomendación.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Recibir una recomendación junto a la alerta en la aplicación web</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero que cada alerta activa explique el riesgo y sugiera una acción concreta, para que pueda responder al problema sin conocer los valores técnicos de cada métrica.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario pertenece al grupo experimental y existe una alerta activa de CO₂, cuando consulta sus alertas activas, entonces el sistema presenta una explicación breve del riesgo y la acción recomendada de ventilar el espacio.</li>
        <li>Dado que el Usuario pertenece al grupo experimental y existe una alerta activa de PM2.5, cuando consulta sus alertas activas, entonces el sistema presenta una explicación breve del riesgo y la acción recomendada correspondiente a esa métrica.</li>
        <li>Dado que el Usuario pertenece al grupo de control, cuando consulta sus alertas activas, entonces el sistema presenta la métrica, el valor y la gravedad sin recomendación.</li>
        <li>Dado que el sistema presenta una alerta al Usuario, cuando la información queda disponible, entonces el sistema registra el evento alert_viewed con la variante asignada.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Recibir notificaciones push con recomendación</td>
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
        <li>Dado que el Usuario pertenece al grupo experimental y se genera una alerta en uno de sus espacios, cuando el sistema envía la notificación push, entonces la notificación incluye la métrica, el nombre del espacio y la acción recomendada.</li>
        <li>Dado que el Usuario pertenece al grupo de control y se genera una alerta, cuando el sistema envía la notificación push, entonces la notificación incluye la métrica, el nombre del espacio y el valor medido.</li>
        <li>Dado que el Usuario recibe una notificación push de alerta, cuando la abre, entonces el sistema registra el evento alert_notification_opened con la variante asignada y el tiempo transcurrido desde el envío.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-02</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Indicar la acción tomada ante una alerta</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero indicar qué hice después de recibir una alerta, para que Clair conserve un historial de mis acciones y pueda evaluar la utilidad de sus recomendaciones.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que existe una alerta activa, cuando el Usuario indica que aplicó la recomendación, que realizó otra acción o que no realizó ninguna, entonces el sistema registra la respuesta con la fecha y la hora.</li>
        <li>Dado que el Usuario registró una acción, cuando la métrica vuelve a un nivel normal dentro de los 30 minutos siguientes, entonces el sistema marca la alerta como resuelta después de una acción del Usuario.</li>
        <li>Dado que el Usuario registra una respuesta, cuando el sistema la almacena, entonces el sistema registra el evento alert_action_reported con el tipo de respuesta y la variante asignada.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Usuario</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-03</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Recibir un resumen semanal de la calidad del aire</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario, quiero recibir cada semana un resumen del estado del aire de mis espacios, para que pueda revisar su evolución sin consultar la aplicación todos los días.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario tiene al menos un dispositivo con lecturas en los últimos 7 días, cuando llega el lunes a las 08:00 en hora de Lima, entonces el sistema envía una notificación push con el porcentaje del tiempo en nivel Bueno, la cantidad de alertas y el espacio con más alertas.</li>
        <li>Dado que el Usuario no tiene lecturas en los últimos 7 días, cuando llega el horario del resumen, entonces el sistema envía un aviso de que sus dispositivos no reportan datos.</li>
        <li>Dado que el Usuario desactivó el resumen semanal en sus preferencias, cuando llega el horario del resumen, entonces el sistema no envía la notificación.</li>
        <li>Dado que el Usuario abre el resumen semanal, cuando el sistema presenta el detalle, entonces el sistema registra el evento weekly_summary_opened.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-03</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Seguir una guía de primeros pasos sin dispositivos vinculados</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Usuario recién registrado, quiero que la aplicación me indique los pasos para vincular mi primer dispositivo, para que pueda empezar a monitorear sin buscar ayuda externa.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Usuario no tiene dispositivos vinculados, cuando consulta el dashboard, entonces el sistema informa que aún no existen dispositivos y presenta los pasos para crear un espacio y reclamar un dispositivo.</li>
        <li>Dado que el Usuario completa el reclamo de su primer dispositivo, cuando el sistema confirma la vinculación, entonces el sistema registra el evento first_device_claimed con el tiempo transcurrido desde el registro de la cuenta.</li>
        <li>Dado que el Usuario ya tiene dispositivos vinculados, cuando consulta el dashboard, entonces el sistema no presenta la guía de primeros pasos.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Visitante del segmento administradores</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-04</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Conocer resultados de establecimientos que usan Clair</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante del segmento administradores, quiero conocer resultados concretos y testimonios de establecimientos que usan Clair, para que pueda confiar en que la solución produce mejoras reales.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante accede a la sección de resultados, cuando el sitio presenta la información, entonces el sitio muestra al menos dos resultados con el tipo de establecimiento, la métrica que mejoró y el periodo de medición.</li>
        <li>Dado que el sitio publica un testimonio, cuando el Visitante lo consulta, entonces el testimonio corresponde a una persona que autorizó por escrito el uso de su nombre y de su opinión.</li>
        <li>Dado que el Visitante llega a la sección de resultados, cuando la sección se presenta, entonces el sitio registra el evento results_section_viewed.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Visitante del segmento administradores</td>
    <td style="border: 1px solid #ccc; padding: 8px;">Alta</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-04</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Solicitar una demostración de Clair</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante del segmento administradores, quiero solicitar una demostración de Clair dejando mis datos de contacto, para que pueda evaluar el producto en mi establecimiento antes de contratarlo.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante ingresa su nombre, correo electrónico y tipo de establecimiento, cuando envía la solicitud, entonces el sitio registra la solicitud y confirma que el equipo comercial lo contactará en un plazo de dos días hábiles.</li>
        <li>Dado que el Visitante ingresa un correo electrónico con formato inválido, cuando envía la solicitud, entonces el sitio indica el error y no registra la solicitud.</li>
        <li>Dado que el Visitante envía una solicitud válida, cuando el sitio la registra, entonces el sitio registra el evento demo_requested con la variante del llamado a la acción que vio el Visitante.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-04</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Conocer qué incluye cada plan y el costo inicial total</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Visitante, quiero conocer qué incluye cada plan y cuánto pagaré en total al empezar, para que pueda comparar las opciones sin dudas sobre costos ocultos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que el Visitante consulta los planes, cuando el sitio presenta cada opción, entonces el sitio indica si el plan incluye el dispositivo Clair Alpha o si este se adquiere por separado.</li>
        <li>Dado que el Visitante consulta un plan, cuando el sitio presenta el precio, entonces el sitio muestra el costo inicial total, compuesto por el dispositivo y el primer mes de suscripción.</li>
        <li>Dado que el Visitante selecciona un plan, cuando el sitio registra la selección, entonces el sitio registra el evento plan_selected con el nombre del plan.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Investigar herramientas de feature flags y analítica de producto</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero evaluar herramientas de feature flags y analítica de producto compatibles con Angular, Flutter y Spring Boot, para elegir la que permita asignar variantes y medir eventos con el menor costo de integración.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Dado que se realiza la investigación de herramientas como PostHog, GrowthBook y Firebase Remote Config con Google Analytics 4, cuando se evalúan la disponibilidad de SDK para Angular, Flutter y Java, la asignación estable de variantes por usuario, la exportación de eventos, el costo del plan gratuito y el tratamiento de datos personales, entonces se presenta un documento comparativo con la herramienta recomendada.</li>
        <li>Dado que se eligió una herramienta, cuando se construye un prototipo mínimo, entonces el prototipo asigna una variante a un usuario de prueba y registra un evento desde la aplicación web y desde la aplicación móvil.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Registrar eventos de producto</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero enviar eventos de producto a un endpoint del API, para que el equipo cuente con datos de uso para analizar los experimentos.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Registrar evento exitosamente. Dado que el endpoint "/api/v1/analytics/events" está disponible, cuando se envía una petición POST autenticada con los campos `eventName`, `occurredAt`, `platform` y `variant`, entonces se recibe una respuesta con estado 202.</li>
        <li>Escenario: Evento sin nombre. Dado que el endpoint "/api/v1/analytics/events" está disponible, cuando se envía una petición POST sin el campo `eventName`, entonces se recibe una respuesta con estado 400.</li>
        <li>Escenario: Petición sin autenticación. Dado que el endpoint "/api/v1/analytics/events" está disponible, cuando se envía una petición POST sin token, entonces se recibe una respuesta con estado 401.</li>
        <li>Escenario: Protección de datos personales. Dado que se registra un evento, cuando el servicio lo almacena, entonces el evento conserva un identificador seudonimizado del usuario y no almacena su nombre ni su correo electrónico.</li>
      </ul>
    </td>
  </tr>
</table>

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
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Asignar la variante de un experimento a cada usuario</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero obtener la variante de experimento asignada a un usuario, para que las aplicaciones presenten la condición de control o la experimental de forma consistente.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Obtener asignación. Dado que el endpoint "/api/v1/experiments/{experimentKey}/assignment" está disponible y el experimento está activo, cuando se envía una petición GET autenticada, entonces se recibe una respuesta con estado 200 y el campo `variant` con el valor `control` o `experimental`.</li>
        <li>Escenario: Asignación estable. Dado que un usuario ya tiene una variante asignada, cuando se envía nuevamente la petición GET, entonces se recibe la misma variante.</li>
        <li>Escenario: Experimento inactivo. Dado que el experimento no está activo, cuando se envía la petición GET, entonces se recibe una respuesta con estado 200 y el campo `variant` con el valor `control`.</li>
        <li>Escenario: Exclusión entre experimentos del mismo tema. Dado que el usuario participa en otro experimento activo sobre el mismo tema, cuando se envía la petición GET, entonces se recibe la variante `control` y el campo `excluded` con valor verdadero.</li>
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
    <td style="border: 1px solid #ccc; padding: 8px;">Media</td>
    <td style="border: 1px solid #ccc; padding: 8px;">TB-EP-05</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold; width: 15%;">Title</td>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa;" colspan="3">Consultar resultados agregados por variante</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Description</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">Como Desarrollador, quiero consultar los resultados agregados de un experimento por variante, para que el equipo pueda comparar las condiciones sin exportar los eventos manualmente.</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px; background-color: #fafafa; font-weight: bold;" colspan="4">Acceptance Criteria</td>
  </tr>
  <tr>
    <td style="border: 1px solid #ccc; padding: 8px;" colspan="4">
      <ul style="margin: 0; padding-left: 20px;">
        <li>Escenario: Consultar resultados. Dado que el endpoint "/api/v1/experiments/{experimentKey}/results" está disponible, cuando un usuario con rol administrador envía una petición GET, entonces se recibe una respuesta con estado 200 con la cantidad de usuarios expuestos, la cantidad de conversiones y la tasa de conversión de cada variante.</li>
        <li>Escenario: Usuario sin permisos. Dado que el endpoint está disponible, cuando un usuario sin rol administrador envía una petición GET, entonces se recibe una respuesta con estado 403.</li>
        <li>Escenario: Experimento inexistente. Dado que no existe un experimento con la clave indicada, cuando se envía la petición GET, entonces se recibe una respuesta con estado 404.</li>
      </ul>
    </td>
  </tr>
</table>

### 8.3.2. To-Be Product Backlog

El To-Be Product Backlog ordena las 16 historias de la sección 8.3.1 según el valor que aportan a la validación de las hipótesis. Los primeros lugares los ocupan la Spike Story y las Technical Stories de instrumentación, porque ningún experimento puede medirse si antes no existen la asignación de variantes y el registro de eventos. Les siguen las historias de alertas con recomendación (TB-EP-02), que responden a uno de los hallazgos de severidad 3 de la auditoría y a la hipótesis con la métrica de éxito más directa, junto con las historias de comprensión del estado del aire (TB-EP-01). Después se ubican las historias de la landing page (TB-EP-04); la de resultados y testimonios queda al final de ese grupo porque requiere resultados reales y testimonios autorizados antes de publicarse. La guía de primeros pasos, el resumen semanal, la consulta de resultados por variante y los valores de referencia de umbrales cierran el backlog, ya que mejoran el análisis o la experiencia, pero no bloquean el inicio de los experimentos. La estimación usa la escala 1, 2, 3, 5 y 8 del Capítulo III y suma 54 story points.

| # Orden | User Story ID | Título | Descripción | Story Points ( 1 / 2 / 3 / 5 / 8 ) |
|---------|---------------|--------|-------------|------------------------------------|
| 1 | TB-SP-01 | Investigar herramientas de feature flags y analítica de producto | Como Desarrollador, quiero evaluar herramientas de feature flags y analítica de producto compatibles con Angular, Flutter y Spring Boot, para elegir la que permita asignar variantes y medir eventos con el menor costo de integración. | 3 |
| 2 | TB-WS-TS-02 | Registrar eventos de producto | Como Desarrollador, quiero enviar eventos de producto a un endpoint del API, para que el equipo cuente con datos de uso para analizar los experimentos. | 5 |
| 3 | TB-WS-TS-03 | Asignar la variante de un experimento a cada usuario | Como Desarrollador, quiero obtener la variante de experimento asignada a un usuario, para que las aplicaciones presenten la condición de control o la experimental de forma consistente. | 5 |
| 4 | TB-WS-TS-01 | Asociar una recomendación a cada alerta | Como Desarrollador, quiero que el servicio de alertas asocie una recomendación a cada alerta según la métrica y la gravedad, para que las aplicaciones web y móvil la presenten sin duplicar reglas de negocio. | 5 |
| 5 | TB-WA-US-03 | Recibir una recomendación junto a la alerta en la aplicación web | Como Usuario, quiero que cada alerta activa explique el riesgo y sugiera una acción concreta, para que pueda responder al problema sin conocer los valores técnicos de cada métrica. | 3 |
| 6 | TB-MA-US-02 | Recibir notificaciones push con recomendación | Como Usuario, quiero que la notificación push de una alerta incluya la acción recomendada, para que pueda actuar aunque no abra la aplicación. | 5 |
| 7 | TB-WA-US-01 | Ver el estado del aire en lenguaje claro en la aplicación web | Como Usuario, quiero ver el estado de la calidad del aire de cada dispositivo como un nivel con etiqueta textual y una explicación breve, para que pueda entender si el ambiente es seguro sin interpretar valores técnicos. | 3 |
| 8 | TB-MA-US-01 | Ver el estado del aire en lenguaje claro en la aplicación móvil | Como Usuario, quiero ver en la aplicación móvil el estado del aire de mis espacios como un nivel con etiqueta textual y una explicación breve, para que pueda entender la situación desde el celular en pocos segundos. | 3 |
| 9 | TB-MA-US-03 | Indicar la acción tomada ante una alerta | Como Usuario, quiero indicar qué hice después de recibir una alerta, para que Clair conserve un historial de mis acciones y pueda evaluar la utilidad de sus recomendaciones. | 2 |
| 10 | TB-LP-US-02 | Solicitar una demostración de Clair | Como Visitante del segmento administradores, quiero solicitar una demostración de Clair dejando mis datos de contacto, para que pueda evaluar el producto en mi establecimiento antes de contratarlo. | 3 |
| 11 | TB-LP-US-03 | Conocer qué incluye cada plan y el costo inicial total | Como Visitante, quiero conocer qué incluye cada plan y cuánto pagaré en total al empezar, para que pueda comparar las opciones sin dudas sobre costos ocultos. | 2 |
| 12 | TB-LP-US-01 | Conocer resultados de establecimientos que usan Clair | Como Visitante del segmento administradores, quiero conocer resultados concretos y testimonios de establecimientos que usan Clair, para que pueda confiar en que la solución produce mejoras reales. | 2 |
| 13 | TB-MA-US-05 | Seguir una guía de primeros pasos sin dispositivos vinculados | Como Usuario recién registrado, quiero que la aplicación me indique los pasos para vincular mi primer dispositivo, para que pueda empezar a monitorear sin buscar ayuda externa. | 3 |
| 14 | TB-MA-US-04 | Recibir un resumen semanal de la calidad del aire | Como Usuario, quiero recibir cada semana un resumen del estado del aire de mis espacios, para que pueda revisar su evolución sin consultar la aplicación todos los días. | 5 |
| 15 | TB-WS-TS-04 | Consultar resultados agregados por variante | Como Desarrollador, quiero consultar los resultados agregados de un experimento por variante, para que el equipo pueda comparar las condiciones sin exportar los eventos manualmente. | 3 |
| 16 | TB-WA-US-02 | Consultar valores de referencia al configurar un umbral | Como Usuario, quiero conocer un valor de referencia sugerido para cada métrica al configurar un umbral, para que pueda definir límites de alerta adecuados sin conocimientos técnicos. | 2 |

### 8.3.3. Pipeline-supported, Experiment-Driven To-Be Software Platform Lifecycle

#### 8.3.3.1. To-Be Sprint Backlogs

El primer Sprint To-Be tiene como objetivo habilitar la medición de los experimentos y entregar la recomendación accionable asociada a las alertas de mayor severidad. El trabajo comienza con la investigación de herramientas, continúa con la asignación estable de variantes y el registro de eventos, y termina con la presentación coherente de la recomendación en web, móvil y notificaciones. Esas historias todavía no están en el tablero ni desplegadas. La captura que sí existe es el Kanban actual de Vikunja, el mismo de la sección 5.2.8: las tareas de pruebas, BDD y CI/CD figuran en Done, y la única tarea en To-Do es actualizar Resend por el cambio de DNS. Doing está vacío. Ese tablero no sustituye el Sprint Backlog To-Be; muestra el punto del que sale.

<img src="https://i.imgur.com/KbqKXn0.png" alt="Kanban de Vikunja: tareas de implementación en Done y la actualización de Resend en To-Do">

| User Story | Work item | Estimación (horas) | Responsable | Estado |
|---|---|---:|---|---|
| TB-SP-01 | Comparar herramientas de feature flags y analítica compatibles con Angular, Flutter y Spring Boot | 6 | Anderson Ricardo Ventosilla Trujillo | In-Process |
| TB-WS-TS-02 | Diseñar y construir el endpoint de eventos de producto con validación de propiedades | 12 | Dante Mateo Aleman Romano | To-do |
| TB-WS-TS-03 | Implementar la asignación determinista de variantes por cuenta | 10 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-WS-TS-01 | Asociar recomendaciones por métrica y severidad en el contexto Alerting | 12 | Dante Mateo Aleman Romano | In-Process |
| TB-WA-US-03 | Mostrar el riesgo y la recomendación en el detalle de alerta web | 8 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-MA-US-02 | Incluir la recomendación en la notificación push móvil | 10 | Iker Barturen | To-do |

El segundo Sprint To-Be tiene como objetivo mejorar la comprensión del estado del aire, transparentar precio y precisión en la landing page, simplificar la creación de reglas y verificar que la instrumentación produzca datos conciliables con el backend. No tiene tablero propio: las historias de la tabla siguiente siguen en To-do y no aparecen en la captura de Vikunja.

| User Story | Work item | Estimación (horas) | Responsable | Estado |
|---|---|---:|---|---|
| TB-WA-US-01 / TB-MA-US-01 | Incorporar etiqueta textual, ícono y leyenda accesible al estado del aire | 12 | Iker Barturen | To-do |
| TB-LP-US-03 | Mostrar planes y costo inicial total sin costos ocultos | 8 | Luis Alonso Huaco Oliva | To-do |
| TB-LP-US-01 | Preparar el espacio para evidencia verificable de precisión y testimonios autorizados | 8 | Victor Nicolas Ortiz Alarcon | To-do |
| TB-MA-US-05 | Preparar la guía de vinculación del primer dispositivo | 8 | Iker Barturen | To-do |
| EXP-04 | Construir y medir las plantillas de reglas "Oficina", "Dormitorio" y "Local con público" | 10 | Luis Alonso Huaco Oliva | To-do |
| TB-WA-US-02 | Mostrar valores de referencia al configurar umbrales | 6 | Anderson Ricardo Ventosilla Trujillo | To-do |
| TB-WS-TS-04 | Consultar resultados agregados por variante y verificar la conciliación de eventos | 10 | Dante Mateo Aleman Romano | To-do |

Ambos Sprints utilizarán el pipeline existente del Capítulo VII: GitHub Actions verificará cada Pull Request, Dokploy recibirá los despliegues del backend y de la aplicación web, y Vercel publicará la landing page. La recolección se realizará según el plan de seguimiento de la sección 8.2.8; por ello, ninguna historia se considerará terminada mientras sus eventos no superen las comprobaciones de identidad, consentimiento y conciliación definidas en ese plan.

#### 8.3.3.2. Implemented To-Be Landing Page Evidence

La landing page To-Be incorporará el precio total desde la primera vista, una explicación verificable de la precisión del sensor y los eventos necesarios para EXP-02 y EXP-05. Estos cambios todavía no están implementados en producción; la versión As-Is permanece disponible en https://site-beige-mu.vercel.app/ y no debe presentarse como evidencia de las variantes experimentales.

La evidencia se completará con capturas de ambas condiciones, la versión publicada y la comprobación de eventos después del Sprint correspondiente.

*Evidencia pendiente: las capturas de ambas variantes de la landing page y la verificación de eventos se incorporarán tras el Sprint To-Be correspondiente.*

#### 8.3.3.3. Implemented To-Be Frontend-Web Application Evidence

La aplicación web To-Be mostrará etiquetas textuales accesibles para el estado del aire, recomendaciones accionables en las alertas y valores de referencia al configurar umbrales. La versión actual de https://clair-ui.vercel.app/ sigue siendo la experiencia As-Is y las variantes de EXP-01 y EXP-03 aún no están implementadas en producción.

La evidencia futura incluirá la pantalla de la variante, su asignación mediante feature flag y la verificación del evento correspondiente.

*Evidencia pendiente: la captura de la variante, su feature flag y la verificación del evento se incorporarán tras el Sprint To-Be correspondiente.*

#### 8.3.3.4. Implemented To-Be Native-Mobile Application Evidence

La aplicación móvil To-Be incluirá el estado con texto e ícono, recomendaciones en notificaciones, registro de la acción tomada y una guía para vincular el primer dispositivo. No existe una URL pública de la compilación Flutter y estas historias todavía no están distribuidas a usuarios; por tanto, no se afirma que EXP-01, EXP-03, EXP-04 o EXP-06 estén en ejecución.

La evidencia se incorporará mediante una captura de la compilación Flutter, la versión distribuida y la comprobación de eventos en Firebase DebugView.

*Evidencia pendiente: la captura de la compilación Flutter, la versión distribuida y los eventos en Firebase DebugView se incorporarán tras el Sprint To-Be correspondiente.*

#### 8.3.3.5. Implemented To-Be RESTful API and/or Serverless Backend Evidence

El backend To-Be registrará eventos de producto, asignará variantes, asociará recomendaciones a las alertas y expondrá resultados agregados solo a administradores. La API As-Is permanece en https://clair-api.giks.net/; los endpoints y cambios del To-Be aún no están desplegados y no se presentan como funcionalidad disponible.

La evidencia pendiente incluirá la documentación OpenAPI, la ejecución de pruebas y la conciliación entre eventos y registros del backend exigida por V-02.

*Evidencia pendiente: la documentación OpenAPI, la ejecución de pruebas y la conciliación de eventos se incorporarán tras el Sprint To-Be correspondiente.*

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

*Evidencia pendiente: los artefactos se incorporarán tras la primera sesión de shareback, programada después del segundo Sprint To-Be.*

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

