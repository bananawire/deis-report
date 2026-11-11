# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

### 8.1.1. As-Is Summary.

### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims.

### 8.1.3. Experiment-Ready Questions.

### 8.1.4. Question Backlog.

### 8.1.5. Experiment Cards.

## 8.2. Experiment Design

### 8.2.1. Hypotheses.

### 8.2.2. Domain Business Metrics

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

