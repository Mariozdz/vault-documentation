## Alineación con estandares y buenas practicas.

| Elemento del marco               | Capa del modelo      | Estándar relacionado | Descripción         |
| -------------------------------- | -------------------- | -------------------- |-------------------- |
| Infraestructura declarativa      | Automatización       | OpenGitOps           | Un sistema administrado por GitOps debe tener expresado su estado deseado de manera declarativa |
| Control de identidad             | Identidad            | NIST Zero Trust Architecture 800-207     | Utilizar la identidad de los actores como componente clave de la creación de políticas |
| Gestión centralizada de secretos | Gestión de secretos  | NIST CSF             |
| Segmentación de red              | Red y seguridad      | NIST Zero Trust Architecture 800-207        |Separar usuarios o grupos de recursos en una unica red segmentada y protegida por un componente de seguridad             |
| Control de acceso granular       | Identidad / secretos | NIST Zero Trust Architecture 800-207 y CIS Kubernetes       | ZT busca prevenir el acceso no autorizado a datos y servicios, junto con una aplicación del control de acceso lo más granular posible.           |
| Trazabilidad de cambios          | Automatización       | OpenGitOps           |El estado deseado es almacenado de una manera que refuerza la inmutabilidad, el control de versiones y conserva un historial de versiones completo.           | 
| Protección de secretos           | Gestión de secretos  | OWASP Kubernetes     |Las aplicaciones que se ejecutan en clústeres de Kubernetes necesitan acceso a secretos para su funcionamiento, y es importante garantizar que estos secretos se gestionen de forma segura.           |
