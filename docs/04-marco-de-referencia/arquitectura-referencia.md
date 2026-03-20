# Arquitectura de referencia

## Arquitectura de referencia

La arquitectura de referencia propuesta define la organización y relación de los componentes necesarios para una implementación de un modelo automatizado de gestión segura de secretos en entornos de Kubernetes bajo el enfoque del modelo operativo de GitOps. Esta arquitectura busca integrar mecanismos de automatización declarativa, autenticación basada en indentidad y control de acceso granula, alineándose a principios de seguridad Zero Trust.

El modelo busca abordar los principales desafios asociados a la gestión de secretos, principalmente en aplicativos y servicios web en distintos entornos como cloud y on-premise, donde existe el riesgo de exposición de credenciales o información sensible necesaria para su funcionamiento. Asimismo, considera problemáticas como la falta de trazabilidad en los cambios de configuración y la necesidad de mantener los controles de seguridad consistentes en tornos altamente autommatizados.

Para lograr estos objetivos, el marco propone la integración de herramientas de orquestación, automatización de infraestructura, y gestión de secretos, organizadas en distintas capas funcionales.

Es importante destacar que esta arquitectura no se limita a una implementación especifica, sino que define un modelo generalizable que puede ser adaptado a distintos contextos organizacionales, independientemente de la infraestructura subyacente.

## Capas propuestas para la infraestructura

La arquitectura se estructura en cinco capas base, cada una responsable de un conjunto especifico de funciones dentro del sistema.

### Capa de orquestación.

La capa de orquestación constituye la base de la arquitectura propuesta y corresponde al entorno encargado de ejecutar y administrar las cargas de trabajo que conforman el sistema. Esta capa provee las capacidades necesarias para la gestión de recursos computacionales, el despliegue de aplicaciones y la administración de identidades dentro del clúster.

El marco de referencia establece el uso de una plataforma de orquestación cloud-native, siendo Kubernetes el componente de referencia debido a su capacidad para operar en distintos entornos de infraestructura, incluyendo entornos locales, centros de datos y proveedores de servicios en la nube.

Entre las principales responsabilidades de esta capa se encuentran:

<ul>
<li>Administración de recursos y workloads.</li>

<li>Gestión de identidades mediante componentes como ServiceAccounts</li>

<li>Aplicación de infraestructura declarativa.</li>

<li>Escalado automático de aplicaciones.</li>

<li>Aislamiento base entre cargas de trabajo.</li>
</ul>

Si bien Kubernetes incluye mecanismos nativos para el manejo de secretos, estos no están diseñados para proporcionar un modelo completo de gestión segura de credenciales. Por esta razón, el modelo propone desacoplat la gestión de secretos del clúster, delegando esta responsabilidad a un sistema especializado.

Este enfoque permite mantener la potabilidad del modelo, y facilita su adopción en distintos entornos organizaciones.

### Capa de automatización

La capa de automatización se encarga de gestionar el despliegue y la configuración de la infraestructura mediante un enfoque declarativo basado en principios GitOps. Esta capa permite que la configuración del sistema, las políticas y los recursos del clúster se gestionen como código, almacenándose en un repositorio versionado que actúa como fuente de verdad del sistema.

El marco de referencia propone el uso de herramientas como ArgoCD para implementar esta capa, permitiendo sincronizar de forma continua el estado definido en el repositorio con el estado real del clúster Kubernetes.

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

La capa de red y seguridad de comunicación tiene como objetivo implementar mecanismos de control de tráfico y segmentación entre workloads, alineados con principios de seguridad basados en el modelo Zero Trust. Este enfoque establece que ningún componente dentro del sistema debe confiar implícitamente en otro, requiriendo controles explícitos de comunicación entre componentes.

El marco propone la implementación de politicas de red que permitan definir reglas de comunicación basadas en identidad y contexto, incluyendo controles a nivel de capa 3 y 4 y, cuando sea posible, capa 7. Para ello, se consideran soluciones como Cilium, que permiten extender las capacidades nativas de Kubernetes.

Entre las responsabilidades principales de esta capa se encuentran:
<ul>

<li>Implementación de microsegmentación entre workloads.</li>

<li>Definición de políticas de red en múltiples niveles (L3, L4 y L7).</li>

<li>Control de comunicación basado en identidad.</li>

<li>Restricción del tráfico entre servicios según políticas definidas.</li>

<li>Cifrado del tráfico interno entre componentes del sistema.</li>
</ul>

Aunque Kubernetes incluye mecanismos básicos de políticas de red, estos pueden resultar limitados para entornos que requieren controles más granulares o mayor capacidad de escalabilidad. En este contexto, soluciones especializadas permiten fortaleces el modelo de seguridad de la plataforma.

### Capa de gestión de secretos

La capa de gestión de secretos tiene como propósito centralizar el ciclo de vida de credenciales y secretos utilizados por las aplicaciones, desacoplando su almacenamiento y administración del clúster Kubernetes.

El marco de referencia propone la incorporación de un sistema especializado para la gestión de secretos, como OpenBao, el cual permite almacenar, generar y distribuir credenciales de manera segura.

Entre las responsabilidades de esta capa se encuentran:
<ul>

<li>Gestión centralizada de secretos y credenciales.</li>

<li>Distribución segura de secretos mediante API.</li>

<li>Auditoría de accesos a información sensible.</li>

<li>Registro de actividad relacionada con el uso de secretos.</li>

<li>Revocación y rotación controlada de credenciales.</li>
</ul>

La adopción de este modelo permite reducir la persistencia de credenciales dentro del clúster, y minimizar el uso del recurso nativo Secret de Kubernetes para información sensible. De esta forma, se promueve un enfoque en el cual los secretos se obtienen dinamicamente bajo demanda.

Este enfoque es aplicable a distintos entornos organizacionales, y permite adaptar el modelo a diferentes herramientas sin afectar la estructura general de la arquitectura.

### Capa de identidad y autenticación

La capa de identidad y autenticación define los mecanismos mediante los cuales los distintos componentes del sistema establecen relaciones de confianza y acceden a los recursos protegidos. En el modelo propuesto, la identidad constituye el elemento central para la aplicación de controles de seguridad, en alineación con los principios del enfoque Zero Trust.

El marco establece el uso de identidades asociadas a los workloads, como los ServiceAccounts de Kubernetes, las cuales permiten autenticar aplicaciones dentro del clúster y establecer relaciones de confianza con otros componentes del sistema.

En particular, el modelo enfatiza el uso de mecanismos de autenticación fuerte basados en certificados digitales para el acceso al gestor de secretos. Este enfoque permite implementar esquemas de autenticación mutua (mTLS), en los cuales tanto el cliente como el servicio validan su identidad, garantizando un canal seguro y verificable para la obtención de credenciales.

Adicionalmente, la identidad puede ser utilizada como base para la definición de politicas de red en la capa de comunicación, permitiendo reforzar el modelo Zero Trust mediante controles de acceso basados en identidad entre workloads. No obstante, en el contexto de este marco, el uso principal de la identidad se orienta a la autenticación y autorización en el acceso a secretos.

Entre las responsabilidades de esta caoa se encuentran:

<ul>
<li>Autenticación de workloads mediante identidades del clúster.</li>

<li>Asociación de políticas de acceso con identidades específicas.</li>

<li>Implementación de controles basados en mínimo privilegio.</li>

<li>Establecimiento de relaciones de confianza entre aplicaciones y el gestor de secretos.</li>
</ul>

Este enfoque permite asegurar que el acceso a recursos sensibles se realice de forma controlada, verificable y alineada a practicas modernas de seguridad basadas en identidad.

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

El funcionamiento de esta arquitectura se basa en el flujo de interacción entre sus componentes, desde la definición declarativa de la infraestructura hasta el acceso controlado a secretos por parte de las aplicaciones.

En primer lugar, la configuración de la infraestructura se define de forma declarativa en un repositorio de Git, el cual actúa como fuente de verdad del sistema. En este repositorio se almacenan los manifiestos y configuraciones necesarias para desplegar los distintos componentes de la plataforma.

El motor de GitOps monitorea continuamente el repositorio y sincroniza el estado deseado con el clúster Kubernetes. A través de este proceso, se despliegan y mantienen actualizados los componentes de la arquitectura.

Una vez desplegado el sistema, las aplicaciones que requieren acceso a secretos se autentican contra el gestor de secretos utilizando mecanismos basados en identidad. El gestor valida la identidad de la aplicación y, en función de las politicas ocnfiguradas, genera un token que permite acceder únicamente a los secretos autorizados.

Este modelo permite evitar el almacenamiento de credenciales sensibles en repositorios de código, archivos de configuración o recursos del clúster, reduciendo significativamente el riesgo de exposición.

## Beneficios

Entre los principales beneficios del modelo propuesto se encuentran:


<ul>
<li>Automatizacion del despliegue de infraestructura</li>
<li>Replicabilidad del entorno en distintos contextos organizacionales</li>
<li>Trazabilidad de cambios en configuración del sistema</li>
<li>Trazabilidad en el acceso y uso de secretos</li>
<li>Gestión centralizada y segura de credenciales</li>
<li>Control de acceso basado en identidad y principio de mínimo privilegio</li>
<li>Reducción de la complejidad en el diseño de soluciones seguras</li>
</ul>