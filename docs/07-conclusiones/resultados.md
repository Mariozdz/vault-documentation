# Resultados 


1. Se identificaron herramientas compatibles con los principios de gestión segura de secretos, automatización, control de acceso basado en identidad y aplicación de conceptos Zero Trust. A partir de este análisis se seleccionaron Gitops con ArgoCD como medio de gestión y automatización de recursos, OpenBao para la gestión centralizada de secretos, Nebula para la conectividad privada entre entornos y mecanismos Zero Trust para limitar el acceso mediante identidad, certificados y políticas de red con Cilium.

2. Se implementó una versión base de la arquitectura propuesta, integrando OpenBao como servicio de gestión de secretos, certificados para autenticación, controles de red basados en Cilium y conectividad privada para acceso al gestor de secretos mediante Nebula. Esta implementación permitió comprobar la integración inicial entre los componentes principales y establecer una base funcional para escenarios posteriores de validación. 

3. La arquitectura fue adaptada al caso de uso de identidad digital del TEC, considerando la necesidad de proteger secretos, certificados y canales de comunicación en arquitectura de componentes distribuidos. Esta adaptación permitió demostrar que el marco puede ser contextualizado a un entorno real con cambios mínimos que no se salen del marco propuesto, aunque la evaluación formal de seguridad, desempeño y operación queda como una fase posterior. 
