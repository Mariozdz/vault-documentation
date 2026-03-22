# Networking y eBPF

La capa de red, encargada de gestionar la comunicación entre los distintos sistemas de un entorno, tanto interno como externo, puede constituirse como un vector de ataque crítico en escenarios donde se manipula información sensible. Esta condición expone la necesidad de implementar medidas de seguridad como firewalls, proxies, políticas de red y listas de control de acceso, las cuales, si bien contribuyen a la protección del sistema, pueden introducir una carga adicional que impacta su rendimiento.

Este impacto se vuelve más evidente en entornos distribuidos que requieren escalabilidad, comunicación en tiempo real y procesamiento de grandes volúmenes de información, donde la aplicación de múltiples controles de seguridad puede afectar la eficiencia operativa. En este contexto, surge la necesidad de establecer un equilibrio entre seguridad y optimización del rendimiento.

Ante este escenario, el uso de tecnologías como eBPF, en conjunto con soluciones de red como Cilium, permite abordar estas limitaciones al integrar capacidades de observabilidad, gestión de comunicaciones y aplicación de controles de seguridad de manera más eficiente, reduciendo la dependencia de mecanismos tradicionales y mejorando el desempeño general del sistema.

## Concepto general de eBPF

eBPF es una tecnología del kernel de Linux que permite ejecutar programas de forma segura dentro del sistema operativo sin necesidad de modificar su código fuente. Estos programas se ejecutan en puntos específicos del kernel, lo que permite interceptar, analizar y modificar el comportamiento de distintos subsistemas, incluyendo el procesamiento de paquetes de red.

A diferencia de enfoques tradicionales, eBPF habilita la implementación de lógica personalizada directamente en el kernel, reduciendo la necesidad de componentes intermedios y mejorando el rendimiento de las operaciones de red y seguridad.

## Funcionamiento a alto nivel

El funcionamiento de eBPF se basa en la ejecución de pequeños programas que son cargados en el kernel y validados previamente para garantizar su seguridad. Estos programas pueden ser asociados a distintos eventos del sistema, como la recepción de paquetes de red, llamadas al sistema o eventos de ejecución de procesos.

Una vez cargados, los programas eBPF son capaces de:

- inspeccionar paquetes de red en tiempo real  
- aplicar reglas de filtrado o redirección  
- recolectar métricas de tráfico  
- implementar controles de seguridad basados en comportamiento  

Este modelo permite trasladar parte de la lógica de red y seguridad desde el espacio de usuario hacia el kernel, mejorando la eficiencia y reduciendo la latencia en el procesamiento de datos.

## Aplicaciones en entornos Kubernetes

En Kubernetes, eBPF se ha convertido en una tecnología clave para habilitar soluciones avanzadas de networking y seguridad. Su uso facilita superar algunas limitaciones de los modelos tradicionales basados en iptables o reglas estáticas, facilitando la implementación de políticas dinámicas y contextuales.

Entre sus principales aplicaciones en este tipo de entornos se encuentran:

- implementación de redes definidas por software con mayor eficiencia  
- aplicación de políticas de red más granulares  
- observabilidad del tráfico entre servicios  
- detección de comportamientos anómalos  
- control de acceso basado en identidad  

Estas capacidades resultan especialmente relevantes en arquitecturas distribuidas donde múltiples servicios interactúan de forma dinámica.

## Relación con seguridad y Zero Trust

El modelo Zero Trust establece que ningún componente dentro del sistema debe ser considerado confiable por defecto, requiriendo verificación continua de identidad y control explícito de las comunicaciones. En este contexto, eBPF facilita la implementación de mecanismos de control más estrictos sobre el tráfico de red, facilitando la aplicación de políticas que restringen la comunicación únicamente a los flujos autorizados.

La capacidad de aplicar controles a nivel de kernel permite definir políticas basadas no solo en direcciones IP o puertos, sino también en la identidad de los workloads, lo que fortalece la seguridad del sistema y reduce la superficie de ataque.

## Uso en soluciones como Cilium

Cilium es una solución de red para Kubernetes que utiliza eBPF como base tecnológica para implementar conectividad, seguridad y observabilidad de manera integrada. A diferencia de enfoques tradicionales basados en iptables o proxies intermedios, Cilium procesa el tráfico directamente en el kernel, lo que habilita un modelo más eficiente y flexible para la gestión de comunicaciones entre workloads.

Una de las principales ventajas de este enfoque es la capacidad de aplicar políticas de red a diferentes niveles (L3, L4 y L7) de manera más granular, incluyendo controles basados en identidad de los workloads. Esto hace posible restringir la comunicación entre servicios de forma precisa, alineándose con principios de mínimo privilegio y modelos de seguridad Zero Trust.

Desde el punto de vista de la observabilidad, el uso de eBPF permite inspeccionar el tráfico de red en tiempo real sin necesidad de instrumentar las aplicaciones o introducir componentes adicionales en la ruta de comunicación. Esto facilita la recopilación de métricas detalladas sobre el comportamiento de los servicios, incluyendo patrones de tráfico, latencias y relaciones entre componentes, lo que resulta clave para la detección de anomalías y el análisis de incidentes.

En términos de seguridad, la capacidad de aplicar controles directamente en el kernel contribuye a reducir la superficie de ataque y limitar el movimiento lateral dentro del clúster. La combinación de segmentación basada en identidad, políticas de red avanzadas y monitoreo continuo del tráfico fortalece la protección de los servicios y de la información que estos intercambian.

Adicionalmente, el enfoque basado en eBPF contribuye a mejorar el rendimiento del sistema al reducir la dependencia de mecanismos tradicionales que requieren múltiples saltos o procesamiento en espacio de usuario. Al ejecutarse directamente en el kernel, las operaciones de red pueden realizarse con menor latencia y menor sobrecarga, lo cual resulta especialmente relevante en entornos que requieren procesamiento en tiempo real o manejo de grandes volúmenes de tráfico.

Estas características posicionan a Cilium como una solución adecuada para entornos Kubernetes que demandan altos niveles de seguridad, visibilidad y eficiencia, permitiendo implementar controles de red avanzados sin comprometer el rendimiento del sistema, además resultan especialmente relevantes dentro del marco de referencia propuesto, donde la capa de red y seguridad requiere mecanismos eficientes para aplicar controles de comunicación alineados con principios Zero Trust sin afectar el rendimiento del sistema.

## Relevancia dentro del contexto de la investigación

Si bien eBPF no constituye el elemento central del modelo propuesto en esta investigación, su inclusión como fundamento técnico resulta relevante debido a su rol como tecnología habilitadora en la implementación de controles de red avanzados. En particular, permite soportar las capacidades de segmentación y control de tráfico requeridas por la arquitectura de referencia, contribuyendo a la aplicación de principios Zero Trust en la comunicación entre componentes.

De esta manera, eBPF actúa como un facilitador tecnológico que fortalece la capa de red y seguridad, complementando los mecanismos de autenticación, autorización y gestión de secretos definidos en el marco de referencia.

## Referencias

1. eBPF Foundation. "What is eBPF?" Disponible en: https://ebpf.io/what-is-ebpf/
2. eBPF Documentation. "Linux eBPF documentation". Disponible en: https://docs.ebpf.io/linux/
3. Cilium. "Zero Trust Networking with Cilium". Disponible en: https://cilium.io/outcomes/zero-trust/