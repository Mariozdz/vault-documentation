# Kubernetes como plataforma de orquestación

Kubernetes es una plataforma de código abierto diseñada para automatizar el despliegue, escalado y operación de aplicaciones contenerizadas. Proporciona un modelo declarativo que permite definir el estado deseado del sistema, el cual es mantenido mediante mecanismos de control que garantizan la coherencia entre el estado actual y el definido por el usuario.

Esta capacidad permite gestionar sistemas distribuidos de forma resiliente, facilitando la recuperación ante fallos, el balanceo de carga y la automatización de operaciones.

## Arquitectura general de Kubernetes

La arquitectura de Kubernetes se compone de dos elementos principales:

- Plano de control (Control Plane): responsable de la gestión global del clúster, incluyendo la administración del estado, la planificación de workloads y la exposición del API del sistema.

- Nodos de trabajo (Worker Nodes): encargados de ejecutar las aplicaciones contenerizadas mediante la gestión de pods y contenedores.

Este modelo permite separar la lógica de control de la ejecución de aplicaciones, facilitando la escalabilidad y el manejo de entornos distribuidos.

## Componentes fundamentales

Kubernetes se compone de diversos elementos que permiten gestionar aplicaciones y recursos dentro del clúster. Entre los más relevantes se encuentran:

- **Pods**: es un grupo de una o más contenedores, con almacenamiento compartido y recursos de red, y una especificación sobre cómo ejecutar los contenedores.

- **Deployments**: En un Deployment, se describe el estado deseado, y el Deployment Controller modifica el estado actual al estado deseado a un ritmo controlado. Se pueden definir Deployments para crear nuevos conjuntos de réplicas o para eliminar Deployments existentes y adoptar todos sus recursos con nuevos Deployments.

- **Services**: es un método para exponer una aplicación de red que se ejecuta como uno o más Pods en su clúster.

- **ConfigMaps y Secrets**: Un configmap es un objeto de la API utilizado para almacenar datos no confidenciales en el formato clave-valor. Por otro lado, los objetos de tipo Secret en Kubernetes te permiten almacenar y administrar información confidencial, como contraseñas, tokens OAuth y llaves ssh. Poniendo esta información en un Secret es más seguro y más flexible que ponerlo en la definición de un Pod o en un container image.

- **ServiceAccounts**: Una ServiceAccount es un tipo de cuenta no humana que, en Kubernetes, proporciona una identidad distintiva dentro del clúster. Los Pods de la aplicación, los componentes del sistema y las entidades dentro y fuera del clúster pueden usar las credenciales de una ServiceAccount específica para identificarse como dicha cuenta.

- **RBAC (Role-Based Access Control)**: el control de acceso basado en roles (RBAC, por sus siglas en inglés) es un método para regular el acceso a los recursos informáticos o de red en función de las tareas que desempeñan los usuarios individuales dentro de su organización.

Estos componentes permiten modelar tanto la ejecución de aplicaciones como su configuración y control de acceso.

## Modelo declarativo y estado deseado

Kubernetes adopta un modelo declarativo basado en la definición del estado deseado (desired state), en el cual los usuarios especifican cómo debe comportarse el sistema mediante archivos de configuración, comúnmente en formato YAML o JSON.

A diferencia del enfoque imperativo, donde los cambios se realizan mediante comandos directos, el modelo declarativo permite:

- Versionar la configuración del sistema

- Mantener trazabilidad de cambios

- Reproducir entornos de forma consistente

- Automatizar la gestión de infraestructura

Este enfoque se encuentra estrechamente relacionado con prácticas como Infraestructura como Código (IaC) y GitOps, donde el estado del sistema es gestionado mediante repositorios de control de versiones.

## Seguridad y gestión de secretos en Kubernetes

Kubernetes incluye mecanismos nativos para la gestión de información sensible a través del recurso Secret, el cual permite almacenar datos como credenciales, tokens o certificados. Sin embargo, este mecanismo presenta limitaciones importantes desde el punto de vista de seguridad.

Entre las principales limitaciones se encuentran:

- Almacenamiento de secretos codificados en Base64, lo cual no constituye cifrado seguro por sí mismo

- Dependencia de configuraciones de acceso (RBAC) que pueden ser mal implementadas

- Exposición de secretos a workloads con permisos amplios

- Ausencia de mecanismos avanzados de rotación y revocación

- Capacidades limitadas de auditoría

Estas limitaciones hacen que, en entornos con altos requerimientos de seguridad, el uso de mecanismos nativos resulte insuficiente.

## Desafíos de seguridad en entornos Kubernetes

El uso de Kubernetes en entornos distribuidos introduce múltiples desafíos relacionados con la seguridad, entre los cuales destacan:

- gestión distribuida de credenciales

- Control de acceso entre servicios

- Exposición de información sensible en configuraciones

- Dificultad para aplicar el principio de mínimo privilegio

- Necesidad de establecer mecanismos de identidad entre workloads

En particular, la gestión de secretos se presenta como un problema crítico, ya que las aplicaciones requieren acceso a credenciales para su funcionamiento, pero su almacenamiento y distribución deben realizarse de forma segura.

## Referencias

**Kubernetes.**  
*Kubernetes Documentation.*  
Disponible en: [Ver documentación](https://kubernetes.io/)

