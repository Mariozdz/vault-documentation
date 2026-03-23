# Contexto regional y relevancia del problema

## Transformación digital en América Latina

En los últimos años, América Latina ha experimentado un crecimiento sostenido en la adopción de tecnologías digitales, particularmente en el uso de servicios cloud, arquitecturas basadas en microservicios y plataformas de orquestación como Kubernetes. Este proceso de transformación digital ha sido impulsado tanto por organizaciones privadas como por instituciones públicas, con el objetivo de mejorar la escalabilidad, disponibilidad y eficiencia de los sistemas tecnológicos.

Sin embargo, este crecimiento ha traído consigo un incremento significativo en la complejidad de los entornos tecnológicos. La distribución de servicios, la comunicación entre múltiples componentes y la necesidad de gestionar identidades y credenciales de forma dinámica introducen nuevos desafíos en materia de seguridad.

## Incremento de amenazas y desafíos de seguridad

Paralelamente, diversos estudios han evidenciado que América Latina se ha consolidado como una de las regiones más afectadas por incidentes de ciberseguridad a nivel global, a pesar de presentar niveles de preparación relativamente bajos en comparación con otras regiones. Este fenómeno se ve acentuado por el alto nivel de conectividad digital, que incrementa significativamente la superficie de ataque disponible [a].

En este contexto, el crecimiento en la adopción de arquitecturas basadas en APIs y servicios distribuidos ha ampliado considerablemente los vectores de ataque. Las APIs, al ser un componente fundamental en la comunicación entre aplicaciones, se han convertido en un objetivo prioritario para los atacantes, quienes buscan explotar vulnerabilidades para acceder a datos sensibles o interrumpir servicios críticos [b].

De acuerdo con reportes recientes, la región ha experimentado un incremento significativo en ataques dirigidos a aplicaciones web y APIs, pasando de cientos de miles de incidentes a miles de millones en un corto periodo de tiempo, lo que evidencia una rápida evolución en la sofisticación y escala de las amenazas [b].

Este tipo de ataques puede derivar en brechas de datos, interrupciones del servicio, pérdidas financieras y daños reputacionales, afectando tanto a organizaciones privadas como a entidades gubernamentales que dependen de sistemas interconectados para su operación (Akamai, 2024).

Adicionalmente, el informe de ciberseguridad 2025 del Banco Interamericano de Desarrollo y la Organización de los Estados Americanos señala que la región enfrenta desafíos estructurales relacionados con la madurez en seguridad, incluyendo limitaciones en recursos, talento especializado y coordinación entre sectores [c].

Esta combinación de mayor dependencia tecnológica, aumento en la exposición de servicios y limitaciones en la implementación de controles de seguridad adecuados dificulta la protección efectiva de los sistemas frente a amenazas cada vez más sofisticadas.

## Seguridad en el despliegue de aplicaciones en Kubernetes

El despliegue de aplicaciones web distribuidas en entornos basados en Kubernetes se ha convertido en una práctica común para organizaciones que buscan escalabilidad, eficiencia y alta disponibilidad. Sin embargo, la gestión de la seguridad en estos entornos continúa siendo un desafío crítico, particularmente en lo relacionado con la administración de secretos y credenciales necesarios para el funcionamiento y la comunicación entre los componentes desplegados.

Si bien existen soluciones avanzadas y servicios externos ofrecidos por proveedores cloud, estos suelen implicar costos elevados, mayor complejidad operativa y dependencia tecnológica de terceros. Esta situación puede representar una barrera para organizaciones en desarrollo, instituciones públicas o pequeñas y medianas empresas que buscan implementar servicios seguros sin incurrir en altos costos o dependencia externa.

Como resultado, dichas organizaciones pueden optar por mecanismos alternativos que no cumplen con buenas prácticas de seguridad, como el almacenamiento de credenciales en archivos de configuración o repositorios de código, lo que incrementa el riesgo de exposición de información sensible y limita la adopción de modelos de seguridad modernos.

Ante este escenario, surge la necesidad de diseñar e implementar un modelo de seguridad automatizado, basado en tecnologías como GitOps y herramientas como ArgoCD, que permita integrar soluciones open source para la gestión segura de secretos. Este enfoque busca garantizar tanto la facilidad de implementación de la infraestructura como la correcta administración, transmisión y auditoría de credenciales.


## Gestión de secretos como punto crítico

Uno de los aspectos más críticos dentro de este contexto es la gestión de credenciales y secretos. En muchos casos, las organizaciones continúan utilizando mecanismos tradicionales, como el almacenamiento de credenciales en archivos de configuración, variables de entorno o repositorios de código, lo que incrementa el riesgo de exposición de información sensible.

Asimismo, la falta de controles centralizados dificulta la aplicación de prácticas como la rotación de credenciales, la auditoría de accesos y la implementación de políticas de mínimo privilegio, lo que incrementa la superficie de ataque en sistemas distribuidos.

## Limitaciones en la adopción de controles avanzados

Adicionalmente, factores como la limitada disponibilidad de recursos, la complejidad de las herramientas de seguridad avanzadas y la falta de especialización técnica en algunas organizaciones de la región pueden dificultar la adopción de modelos de seguridad más robustos.

Esta situación es especialmente relevante en instituciones públicas, pequeñas y medianas empresas, donde la implementación de soluciones de seguridad suele competir con otras prioridades operativas y presupuestarias.

Estas limitaciones evidencian la necesidad de soluciones que reduzcan la complejidad técnica y operativa de la seguridad, facilitando su adopción en organizaciones con distintos niveles de madurez.

## Necesidad de enfoques adaptativos y automatizados

En este contexto, se hace evidente la necesidad de contar con enfoques que permitan fortalecer la seguridad de los sistemas sin introducir una complejidad excesiva en su implementación y operación. Modelos como Zero Trust, junto con el uso de tecnologías que faciliten la automatización y la gestión centralizada de credenciales, ofrecen una alternativa viable para abordar estos desafíos.

Estos enfoques permiten mejorar el control de acceso, la trazabilidad y la protección de la información sensible en entornos distribuidos, alineándose con las necesidades actuales de seguridad en arquitecturas modernas.

## Relevancia para la investigación propuesta

De esta manera, el desarrollo de un marco de referencia orientado a la gestión automatizada y segura de secretos en entornos Kubernetes no solo responde a una necesidad técnica, sino también a un contexto regional donde la adopción de prácticas de seguridad avanzadas aún presenta oportunidades de mejora.

Este enfoque busca reducir la brecha existente entre la complejidad de los sistemas actuales y la capacidad de las organizaciones para gestionarlos de forma segura, promoviendo soluciones replicables, accesibles y alineadas con estándares modernos de seguridad.

## Referencias

**Renzullo Narváez, J. A., & Hall, M. M.**  
*Cybersecurity Developments in Latin America: Problems, Models, and Cooperation Channels.*  
DigiTraL Policy Study No. 7/2025, GIGA, 2025.  
Disponible en: [Ver documento](https://pure.giga-hamburg.de/ws/files/54047533/DigiTraL-08-Renzullo-Hall.pdf)

**Akamai Technologies.**  
*API Cyberattacks: A Growing Threat for Organizations in Latin America.* 2024.  
Disponible en: [Leer artículo](https://www.akamai.com/blog/security/api-cyberattacks-growing-threat-organizations-latin-america)

**Inter-American Development Bank (IDB) & Organization of American States (OAS).**  
*2025 Cybersecurity Report: Vulnerability and Maturity Challenges to Bridging the Gaps in Latin America and the Caribbean.* 2025.  
Disponible en: [Ver informe](https://publications.iadb.org/en/publications/english/viewer/2025-Cybersecurity-Report-Vulnerability-and-Maturity-Challenges-to-Bridging-the-Gaps-in-Latin-America-and-the-Caribbean.pdf)