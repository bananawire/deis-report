# PartI: As-Is Software Project

# Capítulo I: Introducción

## 1.1. Startup Profile

### 1.1.1. Descripción de la Startup

En Bananawire, creemos firmemente que respirar aire limpio no debería ser un privilegio ni una incógnita, sino una garantía para las personas. Al observar y transitar los espacios comerciales cerrados de Lima Metropolitana, hemos identificado una problemática invisible, pero de profundo impacto: la calidad del aire interior suele ser una variable ignorada y descuidada. Nuestro proyecto nace del deseo genuino de proteger la salud de nuestra comunidad frente a los riesgos que representa esta amenaza silenciosa. Nuestro propósito es visibilizar lo invisible, empoderar a las personas para que puedan tomar decisiones conscientes sobre los lugares que habitan y frecuentan.

Para materializar este compromiso con nuestra ciudad, hemos desarrollado **Clair**. Más que una herramienta tecnológica, Clair es un sistema integral de monitoreo diseñado para cuidar de las personas.

- **Misión:** Despertar una conciencia colectiva y fomentar el cuidado activo del aire en los espacios que compartimos a diario, democratizando el acceso a la información para proteger la salud y elevar la calidad de vida de nuestra comunidad.

- **Visión:** Convertirnos en la plataforma líder y el principal motor de cambio en el monitoreo de la calidad del aire interior en el Perú, impulsando una transformación hacia un futuro más saludable y consciente.

### 1.1.2. Perfiles de integrantes del equipo

| Foto del estudiante | Nombres y apellidos | Código de estudiante | Descripción |
|------------------------------------------------------------------------------------------------------|-----------------------------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="../assets/members/U202319963.jpg" alt="Dante Mateo Aleman Romano" width="100"> | Dante Mateo Aleman Romano | u202319963 | Desarrollador de 20 años y estudiante de Ingeniería de Software, apasionado por Linux. Me encanta crear servicios, configurar máquinas y profundizar en prácticas de seguridad. |
| <img src="../assets/members/u202319025.jpeg" alt="Iker Barturen" width="100"> | Barturen, Iker | u202319025 | Tiene 21 años. Disfruta escuchar música, ver películas y compartir tiempo con sus amigos. En el futuro le gustaría viajar y seguir creciendo en el ámbito personal y profesional. Le interesa aprender nuevos idiomas y mejorar sus habilidades de comunicación. |
| <img src="../assets/members/u202417743.jpeg" alt="Luis Alonso Huaco Oliva" width="100"> | Huaco Oliva, Luis Alonso | u202417743 | Tiene 22 años. Le gustan el fútbol, la fotografía y probar nuevos restaurantes. Entre sus planes está viajar por el Perú y emprender un proyecto propio. Le gustaría aprender cocina, administración y técnicas para organizar mejor su tiempo. |
| <img src="../assets/members/u202312899.jpeg" alt="Victor Nicolas Ortiz Alarcon" width="100"> | Ortiz Alarcon, Victor Nicolas | u202312899 | Tiene 20 años. Le interesan los deportes, la lectura y escuchar podcasts sobre temas variados. A futuro quiere continuar sus estudios y alcanzar mayor independencia personal. Le gustaría aprender a tocar un instrumento y profundizar en finanzas personales. |
| <img src="../assets/members/u202319095.jpeg" alt="Anderson Ricardo Ventosilla Trujillo" width="100"> | Ventosilla Trujillo, Anderson Ricardo | u202319095 | Tiene 21 años. Disfruta los videojuegos, el cine y pasar tiempo con su familia. Sus planes a futuro incluyen viajar, adquirir nuevas experiencias y formar un negocio. Le gustaría aprender sobre emprendimiento, cocina y comunicación en público. |

## 1.2. Solution Profile

### 1.2.1. Antecedentes y problemática

En Lima Metropolitana, las personas permanecen durante varias horas en espacios interiores como tiendas, oficinas y viviendas, donde la calidad del aire puede verse afectada por la acumulación de dióxido de carbono, partículas y una ventilación insuficiente. Sin embargo, estas condiciones no siempre son visibles ni generan una respuesta inmediata, por lo que suelen pasar desapercibidas hasta que aparecen molestias, fatiga o síntomas respiratorios.

Actualmente, los administradores de establecimientos suelen tomar decisiones sobre la ventilación a partir de percepciones subjetivas o medidas reactivas, como abrir puertas o encender ventiladores. Del mismo modo, las personas preocupadas por el aire de su hogar no suelen contar con dispositivos especializados para conocer el estado real del ambiente. Esta ausencia de indicadores objetivos dificulta saber cuándo existe un riesgo y qué acción resulta más conveniente.

El análisis exploratorio de entrevistas realizado en el proyecto evidencia que aproximadamente el 67% de los administradores consultados no cuenta con un protocolo técnico formal ni con indicadores objetivos para verificar la calidad del aire. En el segmento residencial, cerca del 100% de las personas entrevistadas indicó que no utiliza dispositivos especializados para monitorear el aire en casa. Además, ambos segmentos valoran una solución que presente la información de manera simple, mediante colores, notificaciones y recomendaciones accionables.

Frente a esta problemática surge **Clair**, una solución de monitoreo de calidad del aire interior orientada a convertir datos ambientales en información comprensible y útil. Su propósito es ayudar a los usuarios a identificar cambios en el ambiente, comprender su posible impacto y actuar oportunamente, sin exigir conocimientos técnicos avanzados. El alcance inicial se concentra en espacios comerciales cerrados y hogares de Lima Metropolitana, considerando las necesidades de administradores y personas preocupadas por el bienestar respiratorio de sus familias.

En su primera versión, Clair se enfocará en registrar indicadores ambientales relevantes, mostrar su estado mediante una interfaz clara y emitir alertas o recomendaciones cuando se detecten condiciones que requieran atención. La solución busca apoyar la toma de decisiones, pero no reemplaza una evaluación médica ni una inspección técnica especializada. Tampoco pretende diagnosticar enfermedades o garantizar por sí sola la calidad total del aire; su valor está en ofrecer información oportuna que permita adoptar medidas preventivas y verificar sus resultados.

Los hallazgos también muestran que la adopción depende de que la solución sea fácil de usar, económicamente accesible y capaz de demostrar resultados concretos. Los administradores necesitan saber cuándo actuar sin interpretar datos técnicos complejos, mientras que las personas en el hogar buscan prevenir molestias respiratorias y recibir indicaciones claras. Por ello, la problemática no se limita a la falta de sensores, sino también a la dificultad de transformar las mediciones en decisiones cotidianas que los usuarios puedan comprender y aplicar.

### 1.2.2. Lean UX Process.

#### 1.2.2.1. Lean UX Problem Statements.

**Administradores de establecimientos públicos y privados:** Los administradores necesitan conocer de manera rápida y comprensible el estado del aire interior de sus locales porque actualmente toman decisiones de ventilación basadas principalmente en percepciones, sin indicadores objetivos ni protocolos formales. Esta situación puede afectar el bienestar de clientes y colaboradores y dificultar la gestión oportuna del establecimiento.

**Personas preocupadas por la calidad del aire en el hogar:** Las personas necesitan identificar si el ambiente de su vivienda presenta condiciones que requieren atención porque no suelen contar con dispositivos especializados y no tienen una forma clara de interpretar el estado del aire. Esta falta de información limita la prevención de molestias respiratorias y la adopción de medidas correctivas.

**Problema común:** Ambos segmentos necesitan transformar mediciones ambientales en información sencilla, accesible y accionable. Las soluciones que solo muestran datos técnicos no resuelven completamente la necesidad, ya que los usuarios también requieren saber cuándo actuar y qué medidas preventivas pueden aplicar.

#### 1.2.2.2. Lean UX Assumptions.

Partimos de los siguientes supuestos, que deberán ser validados mediante prototipos, entrevistas y pruebas de uso:

- Los administradores de establecimientos revisarán periódicamente el estado del aire si la información se presenta de forma rápida y visual.
- Las personas preocupadas por la calidad del aire en el hogar valorarán una herramienta que les permita detectar cambios ambientales antes de que aparezcan molestias persistentes.
- Los usuarios confiarán más en Clair cuando las alertas incluyan una explicación breve y una recomendación concreta, en lugar de mostrar únicamente valores numéricos.
- La facilidad de instalación, el precio accesible y la posibilidad de consultar la información desde el celular serán condiciones importantes para la adopción.
- La evidencia de mejoras en el bienestar o en la gestión del establecimiento aumentará la disposición de los usuarios a continuar utilizando y recomendar la solución.

#### 1.2.2.3. Lean UX Hypothesis Statements.

Validaremos las siguientes hipótesis mediante pruebas con prototipos y sesiones de uso:

- **Hipótesis 1 - comprensión:** Creemos que los administradores y las personas preocupadas por el aire en el hogar comprenderán el estado ambiental con mayor rapidez cuando Clair utilice colores, alertas y lenguaje claro. Tendremos éxito si al menos el 80% de los participantes interpreta correctamente el estado mostrado y selecciona una acción adecuada.
- **Hipótesis 2 - utilidad de las recomendaciones:** Creemos que los usuarios considerarán más útil una alerta acompañada de una recomendación concreta que una alerta compuesta solo por valores técnicos. Tendremos éxito si al menos el 70% de los participantes identifica la recomendación como útil y puede explicar qué acción realizaría.
- **Hipótesis 3 - intención de uso:** Creemos que una consulta desde el celular y una instalación sencilla aumentarán la intención de utilizar Clair de forma recurrente. Tendremos éxito si al menos el 70% de los participantes declara que consultaría la solución semanalmente o ante una alerta.
- **Hipótesis 4 - adopción:** Creemos que demostrar resultados concretos y mantener un precio accesible reducirá las principales barreras de adopción. Tendremos éxito si al menos el 60% de los participantes manifiesta intención de probar o recomendar Clair después de conocer su funcionamiento y propuesta de valor.

#### 1.2.2.4. Lean UX Canvas.

| Elemento | Definición inicial |
|---|---|
| **Usuarios y clientes** | Administradores de establecimientos públicos y privados, y personas preocupadas por la calidad del aire en el hogar. |
| **Problemas y necesidades** | Falta de indicadores objetivos, dificultad para interpretar datos ambientales y ausencia de recomendaciones claras para actuar. |
| **Resultados esperados** | Mejorar la comprensión del estado del aire, facilitar decisiones preventivas y aumentar la sensación de control sobre el ambiente interior. |
| **Propuesta de valor** | Clair convierte mediciones ambientales en información visual, comprensible y accionable mediante alertas y recomendaciones oportunas. |
| **Solución propuesta** | Dispositivo y plataforma de monitoreo que registran indicadores relevantes, muestran su estado desde el celular y orientan al usuario sobre posibles acciones. |
| **Canales** | Aplicación móvil o interfaz web, comunicación digital, demostraciones del producto y recomendación de usuarios o administradores. |
| **Métricas de aprendizaje** | Porcentaje de usuarios que interpreta correctamente una alerta, utilidad percibida de las recomendaciones, frecuencia de consulta e intención de prueba o recomendación. |
| **Riesgos y supuestos críticos** | Precio poco accesible, instalación compleja, exceso de información técnica, baja confianza en las mediciones o recomendaciones que no se adapten al contexto del usuario. |
| **Experimentos iniciales** | Pruebas de comprensión de alertas, entrevistas de seguimiento, prototipo navegable y comparación entre alertas técnicas y alertas con recomendaciones. |

## 1.3. Segmentos objetivo.

Clair se orienta inicialmente a dos segmentos que enfrentan dificultades para conocer y gestionar la calidad del aire en espacios interiores:

1. **Administradores de establecimientos públicos y privados:** Personas responsables de tiendas y otros locales comerciales cerrados, especialmente en zonas urbanas de Lima Metropolitana. Necesitan supervisar las condiciones del ambiente para proteger el bienestar de clientes y colaboradores y mantener una operación adecuada.
2. **Personas preocupadas por la calidad del aire en el hogar:** Adultos que desean conocer el estado del aire de su vivienda y tomar medidas preventivas frente a alergias, rinitis, fatiga u otras molestias asociadas al ambiente interior. El segmento incluye principalmente usuarios que consultan información desde el celular y valoran recomendaciones fáciles de comprender.

Los segmentos se representan mediante dos personas de usuario que sintetizan los hallazgos de las entrevistas. **María Moreira** representa a los administradores de establecimientos: busca proteger a clientes y colaboradores, pero enfrenta falta de información técnica y soluciones difíciles de usar. **Lara Alemán** representa a las personas preocupadas por el aire en el hogar: desea prevenir problemas respiratorios y necesita interpretar el estado ambiental sin recurrir a conocimientos especializados. Ambas personas valoran información clara, alertas oportunas y acciones concretas.

### Necesidades y barreras por segmento

| Segmento | Necesidades principales | Barreras de adopción |
|---|---|---|
| Administradores de establecimientos públicos y privados | Medir el aire en tiempo real, recibir alertas fáciles de interpretar, saber cuándo ventilar y contar con evidencia para mejorar el bienestar de clientes y colaboradores. | Precio elevado, instalación compleja, falta de tiempo para revisar datos y desconfianza frente a mediciones que no se traduzcan en acciones concretas. |
| Personas preocupadas por la calidad del aire en el hogar | Conocer el estado del ambiente desde el celular, prevenir molestias respiratorias, recibir recomendaciones sencillas y verificar si las medidas aplicadas producen mejoras. | Costo del dispositivo, exceso de información técnica, baja percepción de riesgo hasta que aparecen síntomas y dudas sobre la precisión de las mediciones. |

### Actores relacionados con los segmentos

- **Usuario principal en establecimientos:** el administrador consulta el estado del aire, interpreta las alertas y decide acciones como mejorar la ventilación o revisar el ambiente del local.
- **Usuario principal en el hogar:** la persona responsable del bienestar del hogar consulta las mediciones, identifica cambios en el ambiente y aplica medidas preventivas según las recomendaciones.
- **Beneficiarios indirectos:** clientes, colaboradores y familiares se benefician de ambientes interiores mejor gestionados, aunque no sean quienes consulten directamente la plataforma.
- **Actores de soporte y validación:** el equipo de Bananawire mantiene la solución y analiza los resultados de las pruebas, mientras que profesionales de salud o especialistas ambientales pueden aportar criterios para interpretar los indicadores y las recomendaciones.