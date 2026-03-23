# GitOps

GitOps es una práctica de DevOps que utiliza Git como la única fuente de verdad donde se almacena el estado de la configuración deseada del despliegue. El enfoque principal de este proceso es la automatización de operaciones a partir del contenido de los repositorios de Git. 

A diferencia de herramientas o plataformas específicas, GitOps se define como un conjunto de principios y prácticas orientadas a la automatización de la infraestructura, utilizando flujos de trabajo ya conocidos en el desarrollo de software, como control de versiones, revisión de cambios y despliegues automatizados.

## Principios de GitOps

El enfoque GitOps se fundamenta en un conjunto de principios que permiten gestionar infraestructura de forma consistente, auditable y automatizada:

- Infraestructura declarativa: El estado deseado del sistema se define mediante archivos de configuración almacenados en un repositorio Git, lo que permite versionar y auditar los cambios realizados.

- Git como fuente de verdad: Toda la configuración relevante del sistema se mantiene en el repositorio, garantizando consistencia entre entornos y facilitando la trazabilidad de cambios.

- Automatización mediante reconciliación continua: Un sistema automatizado se encarga de comparar el estado actual del entorno con el estado definido en Git, aplicando los cambios necesarios para mantener la coherencia.

Reconciliación continua del estado del sistema: Agentes de software observan continuamente el estado actual del sistema y lo comparan con el estado deseado definido en el repositorio Git, aplicando automáticamente los cambios necesarios para mantener la coherencia entre ambos estados.

## Principales componentes de GitOps

Los tres principales componentes de GitOps son:

-	Infraestructura declarativa: el estado deseado de un sistema se define como código, el cual es almacenado en un repositorio de Git, lo que permite tener control y auditoria sobre las versiones de este.
-	PRs o MRs: los Pull Request y/o Merge Request son los principales mecanismos para la aplicación de cambios y actualización de la infraestructura, siendo este también el apartado donde los equipos pueden colaborar mediante la revisión y retroalimentación que conllevan a la aprobación o rechazo de los cambios propuestos.
-	CI/CD: GitOps automatiza las actualizaciones de infraestructura utilizando un flujo de trabajo de Git que implementa integración continua (CI) y entrega continua (CD). Cuando nuevas actualizaciones al código son incluidas, el pipeline de CI/CD se encarga de aplicar los cambios al ambiente donde se encuentra desplegada dicha infraestructura.


## GitOps workflow

Un flujo de trabajo de GitOps se define como un enfoque sistemático y controlado para la gestión de infraestructura y aplicaciones, en el cual un repositorio Git actúa como la única fuente de verdad del estado deseado del sistema. Este modelo permite gestionar tanto la configuración de la infraestructura como el despliegue de aplicaciones mediante procesos versionados, auditables y automatizados.

El flujo de GitOps se construye sobre un conjunto de componentes fundamentales que interactúan para garantizar la consistencia entre el estado deseado y el estado real del sistema:

1.	Repositorio de Git: el repositorio Git actúa como la fuente de verdad del sistema, almacenando tanto el código de la aplicación como la configuración de la infraestructura. Este enfoque permite mantener un historial completo de cambios, facilitando la trazabilidad, auditoría y control de versiones a lo largo del ciclo de vida del software.

2.	Entrega Continua (CD) Pipeline: el pipeline de integración continua se encarga de validar los cambios realizados en el repositorio mediante procesos automatizados de construcción y pruebas. Este componente garantiza que las modificaciones cumplan con los estándares definidos antes de ser integradas al estado deseado del sistema.


3.	Herramienta de despliegue de aplicaciones: A diferencia de los modelos tradicionales de entrega continua, en GitOps el despliegue se realiza mediante un mecanismo de reconciliación continua. Un agente dentro del clúster observa el repositorio Git y compara el estado deseado con el estado actual del sistema, aplicando automáticamente los cambios necesarios para mantener la coherencia. Este enfoque reduce la necesidad de intervención manual y evita el uso de mecanismos push hacia el clúster, promoviendo un modelo más seguro y controlado.

4.	El sistema de monitoreo permite observar el estado de las aplicaciones y la infraestructura en tiempo real, proporcionando información relevante sobre su desempeño y funcionamiento. Esta retroalimentación es fundamental para la detección de fallos, validación de despliegues y toma de decisiones por parte de los equipos de desarrollo y operación.

## El desafío de la gestión de secretos en GitOps

Un principio fundamental de GitOps establece que toda la configuración del sistema debe estar versionada en un repositorio Git, el cual actúa como fuente de verdad del estado deseado. Sin embargo, este principio introduce desafíos significativos en la gestión de información sensible.

El almacenamiento directo de datos confidenciales, como claves API, credenciales de bases de datos o certificados privados, en repositorios Git —incluso cuando estos son privados— representa un riesgo considerable de seguridad. Esta práctica puede derivar en lo que se conoce como expansión de secretos, donde la información sensible se encuentra distribuida en múltiples ubicaciones, dificultando su control, auditoría y protección.

En este contexto, diversos autores y organizaciones han señalado que una vez que un secreto ha sido almacenado en texto plano o en un formato fácilmente reversible dentro de un repositorio, debe considerarse comprometido y proceder a su inmediata revocación [4].

Para abordar esta problemática, han surgido distintas estrategias que permiten integrar la gestión de secretos dentro de entornos GitOps sin comprometer la seguridad. Estas estrategias pueden agruparse en dos enfoques principales:

- Almacenamiento de secretos cifrados en Git: Los secretos se almacenan en el repositorio en forma cifrada, utilizando herramientas especializadas que permiten su descifrado únicamente en tiempo de ejecución o despliegue.

- Uso de referencias a secretos externos: En lugar de almacenar los secretos directamente en el repositorio, se incluyen referencias a un sistema externo de gestión de secretos, donde las credenciales se almacenan de forma segura y son recuperadas dinámicamente por las aplicaciones.


Ambos enfoques buscan mitigar los riesgos asociados al almacenamiento de información sensible en repositorios, siendo el segundo especialmente relevante en arquitecturas que priorizan la separación entre configuración e información confidencial.

## Referencias

**OpenGitOps.**  
*OpenGitOps Principles.*  
Disponible en: [Ver principios](https://opengitops.dev/)

**IBM.**  
*What is GitOps?* IBM Think Blog, 2025.  
Disponible en: [Leer artículo](https://www.ibm.com/think/topics/gitops)

**GitLab.**  
*GitOps.* GitLab Topics, 2025.  
Disponible en: [Ver documentación](https://about.gitlab.com/topics/gitops/)

**Vaibhav, V.**  
*Scaling GitOps in the enterprise: Secure secrets, policy as code, and multi-cluster strategies.* DEV Community.  
Disponible en: [Leer artículo](https://dev.to/vaib/scaling-gitops-in-the-enterprise-secure-secrets-policy-as-code-and-multi-cluster-strategies-6hb)