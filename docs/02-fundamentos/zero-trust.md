# Zero Trust

El modelo de seguridad Zero Trust surge como una evolución de los enfoques tradicionales basados en perímetros de red, en los cuales se asumía que los componentes internos de un sistema eran confiables por defecto. Sin embargo, el incremento en la complejidad de los sistemas distribuidos, el uso de entornos cloud y la proliferación de amenazas internas han evidenciado las limitaciones de este modelo.

En este contexto, Zero Trust propone un cambio de paradigma en el cual ningún usuario, dispositivo o servicio es considerado confiable de forma implícita, independientemente de su ubicación dentro o fuera de la red. Este enfoque establece que todas las solicitudes de acceso deben ser verificadas de manera continua antes de permitir el acceso a recursos protegidos, en concordancia con lo establecido en NIST SP 800-207.

## Principios fundamentales de Zero Trust

De acuerdo con lo definido en NIST SP 800-207, el modelo Zero Trust se basa en una serie de principios fundamentales que guían la protección de los recursos dentro de una organización.

En primer lugar, todos los recursos deben considerarse como potencialmente expuestos, lo que implica que no se debe asumir confianza en función de la ubicación de red. En segundo lugar, todas las comunicaciones deben ser autenticadas y autorizadas de forma explícita, mediante mecanismos de verificación de identidad y control de acceso.

Asimismo, el acceso a los recursos debe otorgarse bajo el principio de mínimo privilegio, limitando las acciones permitidas a lo estrictamente necesario para cada entidad. Este acceso no debe ser estático, sino dinámico y basado en múltiples factores, incluyendo la identidad, el contexto y el comportamiento observado.

Finalmente, el modelo establece la necesidad de monitorear continuamente el estado de los sistemas y las interacciones entre componentes, con el objetivo de detectar anomalías y responder de forma oportuna ante posibles incidentes de seguridad  (sección 2 - Zero Trust Basics).

## Componentes de la arquitectura Zero Trust

El estándar NIST SP 800-207 define una arquitectura lógica compuesta por varios componentes que permiten implementar el modelo Zero Trust de manera estructurada dentro de un sistema.

En el núcleo de esta arquitectura se encuentran el Policy Engine (PE), el Policy Administrator (PA) y el Policy Enforcement Point (PEP), los cuales operan de forma coordinada para evaluar, decidir y aplicar el acceso a los recursos.

El Policy Engine (PE) es responsable de tomar la decisión final sobre si una entidad puede acceder a un recurso. Para ello, utiliza políticas definidas a nivel organizacional y múltiples fuentes de información, tales como estado del sistema, contexto de la solicitud y datos provenientes de sistemas externos. Estas entradas son evaluadas mediante un proceso lógico que determina si el acceso debe ser autorizado, denegado o revocado. Asimismo, el PE registra las decisiones tomadas, contribuyendo a la trazabilidad del sistema.

El Policy Administrator (PA) actúa como el componente encargado de ejecutar las decisiones definidas por el Policy Engine. En particular, establece o interrumpe los canales de comunicación entre los sujetos y los recursos, mediante la configuración de los puntos de control correspondientes. Además, es responsable de generar credenciales o tokens de sesión necesarios para acceder a los recursos autorizados. Su operación depende directamente de las decisiones del PE, y su comunicación con los puntos de enforcement se realiza a través del plano de control.

Por su parte, el Policy Enforcement Point (PEP) es el componente encargado de aplicar las decisiones de acceso en los puntos donde se produce la interacción entre sujetos y recursos. Este elemento controla el establecimiento, monitoreo y terminación de las conexiones, actuando como un intermediario que asegura que solo las solicitudes autorizadas puedan progresar. Dependiendo de la implementación, el PEP puede estar distribuido entre el cliente, el recurso o un componente intermedio que funcione como punto de control de acceso.

Además de estos componentes centrales, la arquitectura Zero Trust incorpora diversas fuentes de información que alimentan el proceso de toma de decisiones. Estas fuentes incluyen sistemas de monitoreo continuo del estado de los activos, sistemas de gestión de identidades, infraestructuras de clave pública (PKI), registros de actividad de red y sistemas de inteligencia de amenazas. La integración de estas fuentes permite evaluar el contexto de cada solicitud de acceso de forma dinámica y ajustar las decisiones en función del estado actual del sistema.

Este modelo introduce una separación clara entre la toma de decisiones y su ejecución, lo que permite aplicar políticas de acceso de manera consistente, adaptable y centralizada en distintos componentes del sistema (sección 3 - Logical Components of Zero Trust Architecture ).

En el contexto de esta investigación, estos componentes se materializan a través de mecanismos de autenticación, políticas de acceso y sistemas de gestión de secretos, los cuales implementan de forma práctica las funciones del PE, PA y PEP dentro del entorno Kubernetes

## Zero Trust en entornos cloud-native

El estándar NIST SP 800-207 describe diversos escenarios de despliegue en los cuales el modelo Zero Trust resulta especialmente relevante, destacando entornos distribuidos, multi-cloud y con acceso remoto como contextos naturales para su adopción.

Estos escenarios comparten una característica común: la imposibilidad de definir un perímetro de red claro y confiable. En organizaciones con múltiples ubicaciones, usuarios remotos o servicios desplegados en diferentes proveedores de nube, el tráfico no necesariamente fluye a través de la infraestructura central de la organización, lo que limita la efectividad de los modelos tradicionales basados en perímetro.

En particular, los entornos multi-cloud y cloud-to-cloud introducen la necesidad de establecer comunicaciones directas entre servicios distribuidos, evitando el enrutamiento innecesario a través de redes centrales. En este contexto, el modelo Zero Trust propone ubicar puntos de control de acceso (PEP) cerca de los recursos y servicios, permitiendo aplicar políticas de seguridad de manera consistente sin importar la ubicación física de los componentes.

Asimismo, el modelo contempla escenarios donde múltiples entidades, incluyendo usuarios externos o sistemas de terceros, requieren acceso limitado a recursos organizacionales. En estos casos, Zero Trust permite definir políticas granulares que restringen el acceso únicamente a los recursos necesarios, evitando la exposición innecesaria de otros componentes del sistema.

Estos principios resultan altamente aplicables a entornos cloud-native, como Kubernetes, donde los servicios se despliegan de forma distribuida y las interacciones entre workloads son dinámicas. En este tipo de arquitecturas, no es viable confiar en mecanismos de segmentación tradicionales basados en red, lo que hace necesario adoptar modelos basados en identidad y políticas de acceso explícitas.

De esta manera, Zero Trust proporciona un enfoque adecuado para controlar la comunicación entre servicios, asegurando que cada interacción sea autenticada, autorizada y monitoreada, independientemente de la ubicación del recurso o del origen de la solicitud. Este modelo se alinea con las necesidades de seguridad en arquitecturas modernas, donde la flexibilidad, escalabilidad y distribución de los sistemas requieren mecanismos de control más adaptativos y contextuales (sección 4. Deployment Scenarios/Use Cases).

## Relación con la gestión de secretos e identidad

Uno de los elementos clave para la implementación efectiva de Zero Trust es la gestión de identidades y credenciales. En este contexto, los sistemas de gestión de secretos desempeñan un rol fundamental al permitir la emisión, distribución y control de credenciales utilizadas por los distintos componentes del sistema.

El uso de mecanismos de autenticación basados en identidad, como certificados o tokens dinámicos, asegura que únicamente entidades autorizadas puedan acceder a recursos sensibles. Asimismo, la aplicación de políticas de acceso centralizadas facilita la implementación del principio de mínimo privilegio y la rotación controlada de credenciales ( sección 5.3 Stolen Credentials/Insider Threat).

## Relevancia dentro del contexto de la investigación

El modelo Zero Trust constituye un elemento central dentro del marco de referencia propuesto en esta investigación, ya que define los principios sobre los cuales se construyen los mecanismos de autenticación, autorización y control de acceso en la arquitectura.

En particular, este enfoque se refleja en la separación entre identidad y red, la utilización de mecanismos de autenticación fuerte para workloads, clientes externos y la aplicación de políticas de acceso granulares tanto en el gestor de secretos como a nivel de red dentro del entorno de Kubernetes. Este modelo permite que el acceso a los recursos no dependa de la ubicación dentro de la red, sino de la verificación continua de la identidad y del contexto de cada solicitud.

De esta manera, Zero Trust proporciona la base conceptual que permite integrar de forma coherente la automatización de infraestructura, la gestión de secretos y los controles de seguridad en entornos Kubernetes, alineando los componentes del sistema con un modelo de seguridad basado en identidad y definición de políticas [2].

## Referencias

1. National Institute of Standards and Technology (NIST). Zero Trust Architecture (NIST Special Publication 800-207). 2020. Disponible en: https://doi.org/10.6028/NIST.SP.800-207
2. A Zero Trust Architecture Model for Access Control in Cloud-Native Applications in Multi-Location Environments (NIST SP 800-207A). 2023.
Disponible en: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207A.pdf