# Secretos

Un secreto es una credencial digital integrada en una aplicación o servicio que permite a usuarios no humanos comunicarse con un servicio, base de datos, aplicación u otro recurso informático, y realizar acciones en él. Las claves secretas ayudan a las organizaciones a reforzar su seguridad, garantizando que solo los usuarios autorizados tengan acceso a datos y sistemas confidenciales.

- Contraseñas
- Certificados
- LLaves ssh
- Api Keys
- Llaves de cifrado
- Secretos arbitrarios
- Tokens de autenticación
- Strings de conexión

Estos elementos son fundamentales para el funcionamiento de aplicaciones modernas, ya que permiten establecer mecanismos de confianza entre servicios y proteger el acceso a recursos críticos.

## Importancia de la gestión de secretos

En los entornos tecnológicos actuales, las organizaciones utilizan cada vez más identidades no humanas —como Service Accounts, pipelines CI/CD, contenedores, microservicios y herramientas de automatización— para ejecutar procesos críticos.

Estas entidades requieren credenciales o secretos para autenticarse y acceder a recursos organizacionales, frecuentemente con privilegios elevados. Debido a esto, se convierten en objetivos de alto valor para actores maliciosos, ya que su compromiso puede permitir el acceso a información sensible o la manipulación de sistemas críticos.

En este contexto, la gestión de secretos es fundamental para garantizar la seguridad de los sistemas. Los mecanismos especializados permiten controlar, proteger y auditar las credenciales a lo largo de su ciclo de vida, reduciendo el riesgo de accesos no autorizados y exposición de información sensible, al mismo tiempo que habilitan la automatización segura en entornos distribuidos.

## Problemas comunes en la gestión de secretos

A pesar de su importancia, la gestión de secretos presenta múltiples desafíos, especialmente en entornos DevOps y cloud-native:

- Almacenamiento en texto plano: credenciales directamente en código fuente, archivos de configuración y por ende incluso en repositorios de Git.

- Distribución insegura: transferencia de secretos en texto plano mediante herramientas poco seguras o no ideales como chats, git, email, etc.

- Falta de rotación: muchas veces los secretos se mantienen durante mucho tiempo y no existe proceso o consideración para la rotación de los mismos.

- Acceso excesivo: falta de configuración adecuada basada en mínimo privilegio, exponiendo secretos de manera innecesaria.

- Ausencia de trazabilidad: dificultad para definir información relevante como tiempos de creación, modificación, versiones, usos y accesos.

- Aumento de secretos: con el continuo crecimiento de sistemas, aumenta la necesidad de generación y uso de secretos que podrían extenderse continuamente por numerosas partes aisladas del sistema. Esta distribución puede ser riesgosa principalmente en sistema con secciones privadas y públicas, ya que dichos secretos podrían terminar siendo accesibles por identidades no autorizadas.

Estos problemas aumentan la superficie de ataque y dificultan la aplicación de controles de seguridad efectivos.

## Gestión de secretos en entornos Kubernetes

En entornos Kubernetes, los secretos se gestionan comúnmente mediante el recurso nativo Secret, el cual permite almacenar información sensible dentro del clúster. Sin embargo, este mecanismo presenta limitaciones en términos de seguridad, control de acceso, gestión del ciclo de la vida y gran parte de los problemas descritos en la sección anterior.

Además, en este tipo de entornos declarativos que pueden ser administrados mediante prácticas como GitOps, el manejo de secretos se vuelve aún más importante y complejo, debido a la necesidad de mantener configuraciones versionadas en repositorios Git, lo que incrementa el riesgo de exposición de credenciales.

## Enfoques para la gestión de secretos

Para abordar los desafíos asociados a la gestión de secretos, se han desarrollado distintos enfoques que buscan mejorar la seguridad y el control sobre la información sensible:

### Gestión de secretos mediante sistemas externos

### Almacenamiento de secretos cifrados

## Relación con la problemática de investigación

## Referencias

1. https://www.ibm.com/think/topics/secrets-management

