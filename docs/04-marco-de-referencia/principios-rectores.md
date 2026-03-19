# Principios rectores

El marco de referencia se fundamenta en un conjutno de principios que guían el diseño, implementación y operación de la plataforma propuesta.Estos principios aseguran coherencia entre los componentes de la arquitectura y establecen criterios para la toma de decisiones técnicas.

## Infraestructura declarativa

La infraestructura y configuración del sistema deben definirse de manera declarativa, permitiendo representar el estado deseado mediante archivos versionados.

## Git como fuente de verdad

El repositorio de Git actúa como fuente única de verdad para la configuración del sistema, garantizando la intervención manual y minimizando errores operativos.

## Separación de secretos y configuración

La información sensible no debe almacenarse junto con la configuración del sistema, sino gestionarse mediante mecanismos especializados.

## Identidad como base de seguridad

El acceso a recursos debe basarse en identidades verificables, evitando la confianza implícita basada en la red o ubicación.

## Principio del minimo privilegio

Cada componente debe tener acceso unicamente a recursos necesarios para su funcionamiento.

## Trazabilidad y auditoria

Todas las acciones relevantes del sistema deben poder ser registradas y auditadas.

