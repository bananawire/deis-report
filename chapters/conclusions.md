# Conclusiones

Durante el ciclo AV1, el equipo Bananawire consolidó las bases del proyecto Clair mediante el desarrollo articulado de los cinco capítulos del informe —Introducción, Requirements Elicitation & Analysis, Requirements Specification, Product Design y Product Implementation—, respaldado por un flujo de colaboración que registró 58 commits, 17 pull requests mergeados y 23 hitos documentados en el registro de versiones; en concreto, la fase de Requirements Elicitation evidenció que aproximadamente el 67% de los administradores consultados carece de protocolos formales de calidad del aire interior y cerca del 100% de los hogares no utiliza dispositivos especializados de monitoreo, lo cual valida empíricamente la problemática identificada en el Capítulo I y sustenta las decisiones de diseño adoptadas en los capítulos posteriores; como consecuencia, la arquitectura DDD propuesta —con seis Bounded Contexts (IAM, Billing, Device Management, Air Quality Evaluation, Alerting y Analytics)—, la documentación de la API REST y los wireframes, mock-ups y prototipos web y móvil se constituyen en productos consistentes que articulan problema, solución y entrega técnica de manera trazable.

En términos de gestión, la distribución de responsabilidades entre los cinco integrantes —Dante Mateo Aleman Romano como arquitecto líder y responsable de la estructura general del informe; Iker Barturen como líder de UX/UI web y móvil; Luis Alonso Huaco Oliva como conductor de la investigación de usuarios y la construcción del product backlog; Victor Nicolas Ortiz Alarcon como responsable del Capítulo I y del proceso Lean UX; y Anderson Ricardo Ventosilla Trujillo como integrante de soporte transversal— permitió cubrir integralmente las dimensiones de producto, investigación, diseño e implementación; en consecuencia, los hallazgos de las entrevistas, las hipótesis Lean UX y las decisiones arquitectónicas están alineadas entre sí, lo que reduce el riesgo de incoherencia entre la problemática validada, la solución propuesta y la implementación desarrollada en el Capítulo V.

# Conclusiones y recomendaciones.

A partir del trabajo realizado en el ciclo AV1, el equipo Bananawire concluye que el proyecto Clair constituye una solución técnicamente viable, socialmente pertinente y comercialmente sostenible para el monitoreo de la calidad del aire interior en Lima Metropolitana; en concreto, la arquitectura DDD con microservicios, el modelo SaaS documentado en el Acuerdo de Servicio y la estrategia de despliegue definida en el Capítulo V permiten sostener el crecimiento orgánico del producto sin requerir rediseños estructurales; como consecuencia, las hipótesis Lean UX —80% de comprensión de alertas, 70% de utilidad percibida, 70% de intención de uso recurrente y 60% de intención de adopción— se convierten en los criterios de éxito sobre los cuales se evaluará empíricamente el impacto de la solución en las fases siguientes.

Como recomendaciones para los próximos ciclos del proyecto, el equipo Bananawire identifica cuatro líneas prioritarias de acción; en primer lugar, ejecutar las entrevistas de validación con usuarios finales utilizando los prototipos web y móvil ya construidos, con el propósito de medir cuantitativamente las hipótesis formuladas y ajustar la experiencia de usuario según los hallazgos; en segundo lugar, completar la implementación de los Bounded Contexts pendientes del lado del edge y del embedded service, asegurando la trazabilidad de las mediciones IoT hacia la plataforma; en tercer lugar, instrumentar el pipeline de Continuous Integration y Continuous Deployment definido en el Capítulo VII, con el fin de reducir el ciclo de retroalimentación entre commits, pruebas automatizadas y despliegue productivo; finalmente, en cuarto lugar, formalizar el modelo de monitoreo y alertas definido en el Capítulo VII a través de prácticas de Continuous Monitoring que permitan operar el servicio en producción con observabilidad sobre los indicadores ambientales y sobre el comportamiento de los usuarios.

# Video App Validation

Validation Interviews Video: https://bit.ly/4xI4vDB

# Video About-the-Team.

About the Product: https://bit.ly/4olR1cf

# Bibliografía

American Society of Heating, Refrigerating and Air-Conditioning Engineers. (2022). *Position document on indoor carbon dioxide*. ASHRAE. https://www.ashrae.org/file%20library/about/position%20documents/pd-on-indoor-carbon-dioxide-english.pdf

Asociación Automotriz del Perú. (2024, 15 de agosto). *Contaminación del aire en Perú triplica el límite recomendado por la OMS*. ProActivo. https://proactivo.com.pe/contaminacion-del-aire-en-peru-triplica-el-limite-recomendado-por-la-oms/

IQAir. (2024). *World air quality report 2023*. IQAir. https://www.iqair.com/world-air-quality-report

Organización Mundial de la Salud. (2021). *WHO global air quality guidelines: Particulate matter (PM2.5 and PM10), ozone, nitrogen dioxide, sulfur dioxide and carbon monoxide*. World Health Organization. https://iris.who.int/handle/10665/344167

Airly. (s. f.). *Air quality monitoring in the UK, EU, and worldwide*. https://airly.org/en/

Kaiterra. (s. f.). *Soluciones de monitoreo de la calidad del aire para edificios saludables y sostenibles*. https://www.kaiterra.com/es/

IQAir. (s. f.). *Información sobre la calidad del aire en todo el mundo*. https://www.iqair.com/es/

Balestrieri, E., De Vito, L., Lamonaca, F., Picariello, F., Rapuano, S., & Tudosa, I. (2018). Research challenges in Measurement for Internet of Things systems. *Acta IMEKO*, *7*(4), 14-23. https://doi.org/10.21014/acta_imeko.v7i4.675

Cirkit Designer. (s. f.). *Online circuit design and prototyping platform for IoT projects*. https://app.cirkitdesigner.com


# Anexos

- Entrevistas: https://goo.su/KKwEhz4
- Big Picture Event Storming: https://bit.ly/3QwYkAS
- Candidate Context Discovery: https://imgur.com/a/OX5FnV6
- Backlog en Trello: https://sl1nk.com/r2diehi
- Diagramas C4: https://bit.ly/48eogr9
- Diagramas de Clases: https://bit.ly/48eogr9

- Landing Page: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/site
- Web Services: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/clair-core
- Frontend Web Applications: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/clair-ui
- Mobile Application: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/mobile
- Edge Station: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/edge
- Embedded Application: https://github.com/Vanana-Desarrollo-de-Soluciones-IOT/embedded

- Execution Evidence Web: https://413rsr4.s.gy/W0C0gD
- Execution Evidence Mobile: https://413rsr4.s.gy/r0nBbK
- Prototype Web App Navigation Video: https://bit.ly/3Q84l7g
- Prototype Mobile App Navigation Video: https://bit.ly/43bBBh7
- About the Product: https://bit.ly/4olR1cf
- Validation Interviews Video: https://bit.ly/4xI4vDB

