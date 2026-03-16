# Entorno de implementación

La implementación basada en el marco y arquitectura de referencia se realizó en un entorno de Kubernetes utilizado como plataforma de ejecución para los componentes de automatización, seguridad y gestión de secretos. Este entorno tuvo como propósito servir como escenario de validación técnica del modelo, permitiendo comprobar su viabilidad de implementación y su capacidad para implementar prácticas de GitOps, gestión de secretos y controles alineados con principios de Zero Trust.

Sobre el clúster se despliegan los componentes principales de la solución, entre los cuales se encuentran el motor de GitOps, el gestor de secretos, los mecanismos de emisión de certificados y los recursos necesarios para la operatividad general del sistema.

## Principales componentes

Entre los principales componentes incluidos en esta implementación se encuentran:


| Elemento            | Descripción     |
| ------------------- | --------------- |
| Plataforma base     | Kubernetes      |
| Automatización      | Argo CD         |
| Gestión de secretos | OpenBao o Vault |
| Certificados        | cert-manager    |
| Red y seguridad     | Cilium          |
| Fuente de verdad    | Repositorio Git |

## Consideraciones de diseño

Durante la implementación del entorno se priorizan los siguientes principios:

- Separación entre infraestructura y gestión de secretos, ya sea dentro del mismo clúster o en relación a componentes externos.

- Uso de infraestructura declarativa como medio de automatización.

- Control de acceso basado en identidad

- Mínimo privilegio en el acceso tanto a componentes como secretos

- Trazabilidad completa de cambios mediante control de versiones en el repositorio git.

Estas decisiones permiten que el entorno implementado funcione como un caso de estudio representativo para validar el marco de referencia propuesto.