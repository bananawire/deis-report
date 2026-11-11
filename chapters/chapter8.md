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

