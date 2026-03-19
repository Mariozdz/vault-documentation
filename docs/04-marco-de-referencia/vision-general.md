# Visión general

El presente marco de referencia tiene como objetivo establecer un conjunto estructurado de lineamientos, componentes y procesos para la gestión segura de secretos en entornos de Kubernetes bajo un enfoque de GitOps. Este modelo busca abordar limitaciones existentes en la gestión tradicional de credenciales dentro de plataformas y aplicativos que necesitan manipular información sensible para su funcionamiento, proponiendo una arquitectura que integra automatización, control de acceso basado en identidad y prácticas de seguridad alineadas con el modelo de Zero Trust.

El marco se orienta en la implementación de una plataforma de gestión de secretos basada en la declaratividad y el versionamiento, permitiendo que tanto la configuración del sistema como las politicas de seguridad sean administradas como código. En dicho contexto, se promueve la separación entre la definición de infraestructura y la gestión de información sensible, reduciendo la exposición de secretos y mejorando la trazabilidad de cambios.

El modelo propuesto se fundamenta en la integración de multiples capas funcionales que incluyen la orquestación, automatización, seguridad de red, identidad y gestión de secretos. Asi mismo, permitiendo la separación de responsabilidades y facilitar la implementación progresiva del sistema en distintos contextos organizacionales. 

## Alcance del marco

El marco de referencia está dirigido a organizaciones que operen con metodos tradicionales o poco seguros para la gestión de secretos en cualquier tipo de entorno con un enfoque primario en Kubernetes y que requieran mejorar la gestión de los mismos, la automatización de despliegues y la aplicación de controles de seguridad. Su aplicación es relevante en escenarios deonde se busca reducir la interveción manual, aumentar la trazabilidad y adoptar principios de seguridad basados en identidad.


## Alineación con estandares y buenas practicas.

El diseño del marco se alinea con diversos estándares y prácticas reconocidas en la industria. En particular:

- Los principios de GitOps fundamentan la gestión declarativa y versionada de la infraestructura para una mejor administración de recursos y su debida auditoria.
- El modelo de Zero Trust orienta la implementación de controles basados en identidad y verificación explicita, espcialmente toda aquella identidad criptografica. 
- Las recomendaciones de seguridad para Kubernetes permiten identificar riesgos en la metodologia tradicional de manejo de secreos en ambientes cloud native como Kubernetes.
- Las prácticas de gestión de secretos establecen la necesidad de centralizar y controlar el acceso a credenciales sensibles.

Estas definiciones permiten sustentar el modelo propuesto en enfoques ampliamente aceptados, fortaleciendo su validez conceptual y aplicabilidad práctica.

</br>
**Tabla 1. Alineación con estandares**

| Elemento del marco               | Capa del modelo      | Estándar relacionado | Descripción         |
| :--------------------------------: | :--------------------: | :--------------------: | :--------------------: |
| Infraestructura declarativa      | Automatización       | OpenGitOps           | *Un sistema administrado por GitOps debe tener expresado su estado deseado de manera declarativa* |
| Control de identidad             | Identidad            | NIST Zero Trust Architecture 800-207     | *Utilizar la identidad de los actores como componente clave de la creación de políticas* |
| Gestión centralizada de secretos | Gestión de secretos  | NIST CSF             |
| Segmentación de red              | Red y seguridad      | NIST Zero Trust Architecture 800-207        |*Separar usuarios o grupos de recursos en una unica red segmentada y protegida por un componente de seguridad*            |
| Control de acceso granular       | Identidad / secretos | NIST Zero Trust Architecture 800-207 y CIS Kubernetes       | *ZT busca prevenir el acceso no autorizado a datos y servicios, junto con una aplicación del control de acceso lo más granular posible.*           |
| Trazabilidad de cambios          | Automatización       | OpenGitOps           |*El estado deseado es almacenado de una manera que refuerza la inmutabilidad, el control de versiones y conserva un historial de versiones completo.*           | 
| Protección de secretos           | Gestión de secretos  | OWASP Kubernetes     |*Las aplicaciones que se ejecutan en clústeres de Kubernetes necesitan acceso a secretos para su funcionamiento, y es importante garantizar que estos secretos se gestionen de forma segura.*           |


