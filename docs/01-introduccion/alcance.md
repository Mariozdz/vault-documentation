# Alcance de la investigación

La presente investigación se enfoca en el diseño, implementación y validación de un marco de referencia orientado a la gestión segura y automatizada de la infraestructura necesaria para el acceso a secretos en entornos Kubernetes, bajo un enfoque basado en GitOps y principios de seguridad Zero Trust.

El alcance del trabajo comprende el análisis de riesgos asociados al manejo de credenciales en entornos cloud-native, la evaluación de herramientas y tecnologías relevantes, así como la definición de un modelo que integre prácticas de automatización de infraestructura, control de acceso basado en identidad y gestión centralizada de secretos.

A diferencia de enfoques centrados exclusivamente en aplicaciones desplegadas dentro del clúster, el modelo propuesto considera también escenarios en los cuales aplicaciones externas pueden consumir secretos mediante el uso del API del gestor de secretos. Esto permite ampliar la aplicabilidad del marco a arquitecturas distribuidas donde los servicios no se encuentran necesariamente alojados dentro de Kubernetes, pero requieren acceso seguro a credenciales.

La automatización planteada en esta investigación se enfoca en la gestión declarativa de la infraestructura, la configuración de los componentes de seguridad y la definición de políticas de acceso, más que en la automatización interna del ciclo de vida de los secretos. En este sentido, el marco busca establecer las condiciones necesarias para un acceso seguro y controlado a secretos, delegando la gestión específica de los mismos al sistema especializado utilizado.

Como parte de la investigación, se desarrolla una implementación práctica del marco de referencia en un entorno controlado, utilizando herramientas de código abierto. Esta implementación tiene como propósito demostrar la viabilidad técnica del modelo, así como evaluar su capacidad para mejorar la automatización, seguridad y replicabilidad en distintos escenarios de consumo de secretos.

El estudio se limita al contexto de arquitecturas basadas en Kubernetes como plataforma de orquestación, así como a la integración con un gestor de secretos accesible mediante API. No se abordan en profundidad otros aspectos de seguridad como la protección de endpoints, seguridad a nivel de código o análisis de vulnerabilidades en aplicaciones.

Asimismo, la investigación no contempla la comparación exhaustiva entre todas las herramientas disponibles en el mercado, sino que se centra en un conjunto representativo de tecnologías que permiten demostrar la aplicabilidad del modelo propuesto.

Finalmente, los resultados obtenidos corresponden a un entorno de implementación específico, por lo que su generalización dependerá de factores como la infraestructura disponible, el nivel de madurez tecnológica y los requerimientos particulares de cada organización.