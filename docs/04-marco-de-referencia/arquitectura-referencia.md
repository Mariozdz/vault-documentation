# Arquitectura de referencia

## Arquitectura de referencia

La arquitectura de referencia a proponer, define la organización y relación de los componentes necesarios para una implementación base automatizada de gestión segura de secretos en entornos de Kubernetes bajo el enfoque del modelo operativo de GitOps. Esta arquitectura busca integrar mecanismos de automatización declarativa, autenticación basada en indentidad y control de acceso granular de tal manera que se alinie a principios de Zero Trust.

Esta arquitectura busca abordar los principales desafios asociados a la gestión de secretos, principalmente en aplicativos y servicios web en distintos entornos como cloud o en premisas, donde existe la posibilidad de que credenciales o información sensible necesaria para su funcionamiento se vea expuesta. Por otro lado, tambien se puede hacer mención de abordaje a desafios como trazabilidad de cambios de configuración y controles de seguridad que deben ser consistentes en despliegues automatizados. Para lograr esto, el modelo propone una integración de herramientas de orquestación, automatización de infraestructura y gestión de secretos organizadas en distintas capas.

## Capas propuestas para la infraestructura

La arquitectura se estructura en cinco capas base, cada una responsable de un conjunto especifico de funciones dentro del sistema.

### Capa de orquestación.

La capa de orquestación constituye la base de la arquitectura propuesta y corresponde al entorno encargado de ejecutar y administrar las cargas de trabajo que conforman el sistema. Esta capa provee las capacidades necesarias para la gestión de recursos computacionales, el despliegue de aplicaciones y la administración de identidades dentro del clúster.

El componente de referencia para esta capa es Kubernetes, una plataforma de orquestación de contenedores ampliamente adoptada en entornos cloud-native y capaz de operar en diferentes contextos de infraestructura, incluyendo entornos locales, centros de datos y proveedores de nube pública.

Entre las principales responsabilidades de esta capa se encuentran:
<ul>
<li>Administración de recursos y workloads.</li>

<li>Gestión de identidades mediante ServiceAccounts (en caso de ser necesarias).</li>

<li>Aplicación de infraestructura declarativa.</li>

<li>Escalado automático de aplicaciones.</li>

<li>Aislamiento entre cargas de trabajo.</li>
</ul>
Si bien Kubernetes incluye mecanismos nativos para el manejo de secretos, estos no están diseñados para proporcionar un modelo completo de gestión segura de credenciales. Por esta razón, en la arquitectura propuesta se busca desacoplar la gestión de secretos del clúster, delegando dicha responsabilidad a un sistema especializado y limitando el rol de Kubernetes principalmente a la orquestación de recursos y ejecución de aplicaciones.

### Capa de automatización

La capa de automatización se encarga de gestionar el despliegue y la configuración de la infraestructura mediante un enfoque declarativo basado en principios GitOps. Esta capa permite que la configuración del sistema, las políticas y los recursos del clúster se gestionen como código, almacenándose en un repositorio versionado que actúa como fuente de verdad del sistema.

El componente de referencia para esta capa es Argo CD, una herramienta de entrega continua diseñada para Kubernetes que permite sincronizar automáticamente el estado definido en el repositorio con el estado real del clúster.

Las responsabilidades principales de esta capa incluyen:
<ul>
<li>Almacenamiento versionado de manifiestos de infraestructura.</li>

<li>Sincronización continua entre el estado deseado y el estado real del sistema.</li>

<li>Automatización del despliegue de componentes de la plataforma.</li>

<li>Trazabilidad y auditoría de cambios mediante control de versiones.</li>

<li>Reducción de intervención manual en procesos operativos.</li>
</ul>
La adopción del enfoque GitOps permite mejorar la trazabilidad de cambios, facilitar auditorías y reducir los errores asociados a configuraciones manuales, proporcionando un mecanismo estructurado para gestionar infraestructura, políticas y configuraciones de seguridad.

### Capa de red y seguridad de comunicación

La capa de red y seguridad de comunicación tiene como objetivo implementar mecanismos de control de tráfico y segmentación entre workloads, alineados con principios de seguridad basados en el modelo Zero Trust. Este enfoque establece que ningún componente dentro del sistema debe confiar implícitamente en otro, requiriendo controles explícitos de comunicación y autorización.

El componente de referencia para esta capa es Cilium, una solución de red basada en eBPF que permite implementar políticas de seguridad avanzadas para entornos Kubernetes.

Entre las responsabilidades principales de esta capa se encuentran:
<ul>

<li>Implementación de microsegmentación entre workloads.</li>

<li>Definición de políticas de red en múltiples niveles (L3, L4 y L7).</li>

<li>Control de comunicación basado en identidad.</li>

<li>Restricción del tráfico entre servicios según políticas definidas.</li>

<li>Cifrado del tráfico interno entre componentes del sistema.</li>
</ul>

Aunque Kubernetes incluye mecanismos básicos de políticas de red, estos pueden resultar limitados para entornos que requieren controles más granulares o mayor capacidad de escalabilidad. En este contexto, soluciones como Cilium permiten extender las capacidades de seguridad del clúster, proporcionando un modelo más robusto para el control de comunicaciones internas.

### Capa de gestión de secretos

La capa de gestión de secretos tiene como propósito centralizar el ciclo de vida de credenciales y secretos utilizados por las aplicaciones, desacoplando su almacenamiento y administración del clúster Kubernetes.

El componente de referencia utilizado en esta capa es OpenBao, un sistema de gestión de secretos de código abierto que permite almacenar, generar y distribuir credenciales de manera segura.

Entre las responsabilidades de esta capa se encuentran:
<ul>

<li>Gestión centralizada de secretos y credenciales.</li>

<li>Distribución segura de secretos mediante API.</li>

<li>Auditoría de accesos a información sensible.</li>

<li>Registro de actividad relacionada con el uso de secretos.</li>

<li>Revocación y rotación controlada de credenciales.</li>
</ul>
La incorporación de un gestor de secretos externo permite reducir la persistencia de credenciales dentro del clúster y minimizar el uso del recurso nativo Secret de Kubernetes para información sensible. De esta forma, se promueve un modelo en el cual los secretos se obtienen dinámicamente bajo demanda, reduciendo el riesgo de exposición de credenciales.

### Capa de identidad y autenticación

La capa de identidad y autenticación define los mecanismos mediante los cuales los distintos componentes del sistema establecen relaciones de confianza y acceden a los recursos protegidos. Esta capa permite implementar controles de acceso basados en identidad y aplicar el principio de mínimo privilegio en la interacción entre aplicaciones y sistemas de gestión de secretos.

El mecanismo principal considerado en esta capa es el uso de ServiceAccounts de Kubernetes, los cuales permiten identificar workloads dentro del clúster y asociarlos con políticas de acceso específicas.

Las responsabilidades de esta capa incluyen:
<ul>
<li>Autenticación de workloads mediante identidades del clúster.</li>

<li>Asociación de políticas de acceso con identidades específicas.</li>

<li>Implementación de controles basados en mínimo privilegio.</li>

<li>Establecimiento de relaciones de confianza entre aplicaciones y el gestor de secretos.</li>
</ul>

Dependiendo del contexto de implementación, este modelo puede complementarse con otros mecanismos de autenticación, como proveedores de identidad externos o protocolos de federación de identidades.

## Principales componentes de referencia

| Componente   | Función                                                 |
| ------------ | ------------------------------------------------------- |
| Kubernetes   | Plataforma de ejecución para contenedores y servicios   |
| Git          | Fuente de verdad para la configuración declarativa      |
| Argo CD      | Motor GitOps encargado de sincronizar el estado deseado |
| Vault        | Gestor centralizado de secretos                         |
| cert-manager | Emisión y renovación automática de certificados         |
| Aplicaciones | Consumidores de secretos gestionados por Vault          |

## Flujo de interación entre los componentes

El funcionamiento de esta arquitectura se basa en el flujo de interacción entre los distintos componentes, desde su implementación automatizada general hasta el acceso y administración segura de la infraestuctura para manejo de secretos.

Como base de la implementación de esta arquitectura, toda configuración y recurso necesario de la infraestructura se define de forma declarativa en un repositorio de Git. Dicho respositorio actúa como la fuente de verdad del sistema al almacenar manifiestos y configuraciones necesarias para desplegar los distintos componentes de la plataforma.

Argo CD (o el motor GitOps de preferencia) monitorea constantemente el repositorio git, sincronizando el estado deseado con el cluster de Kubernetes. A travez de este proceso, se despliegan, gestiónan y mantienen actualizados componentes como Vault, Cert-Manager y Cilium.

Una ves se termina el despliegue del sistema, cualquier aplicación que requiera acceso a secretos se autentica con Vault utilizando identidades, en este caso especifico, mediante certificados y mTls integrado como cert auth para Vault. Estos certificados usualmente son asociados a politicas y restricciones de espcio en el gestor de secretos, por lo que al recibir una solicitud, Vault valida la identidad y permisos generado un token que permite el acceso unicamente a los secretos a los que está autorizado.

Este modelo permite evitar el almacenamiento de credenciales sensibles en repositorios de código, archivos de configuración e incluso dentro de el recurso nativo Secret de Kubernetes, reduciendo significativamente el riesgo de la exposición y acceso no deseado a los secretos.

## Beneficios

Entre algunos de los beneficios que se buscan aportar mediante la implementación de esta arquitectura en relación a operación y seguridad se encuentran:

<ul>
<li>Automatizacion del despliegue de infraestructura</li>
<li>Replicabilidad del entorno en distintos contextos organizacionales</li>
<li>Trazabilidad de cambios en configuración del sistema</li>
<li>Trazabilidad de manipulación de secretos</li>
<li>Gestión centralizada y segura de secretos</li>
<li>Control de acceso a secretos basado en identidad y mínimo privilegio</li>
<li>Reducción en la curva de aprendizaje o diseño base</li>
</ul>