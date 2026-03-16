# Implementación de politicas de red

## Rol de Cilium en la arquitectura

Dentro de la arquitectura implementada, Cilium se utiliza como componente encargado de gestionar la conectividad y aplicar controles de seguridad sobre la comunicación entre workloads dentro del clúster Kubernetes. A diferencia del modelo de red tradicional, donde los servicios pueden comunicarse libremente dentro del clúster, Cilium permite definir políticas explícitas que regulan qué componentes pueden intercambiar tráfico.

El uso de Cilium permite implementar mecanismos de microsegmentación que limitan la comunicación entre servicios únicamente a los flujos necesarios para la operación del sistema. Este enfoque reduce la superficie de ataque del entorno y se alinea con los principios de seguridad del modelo Zero Trust, en el cual ninguna comunicación se considera confiable por defecto.

## Funcionamiento de las políticas de red

Las políticas de red definidas mediante Cilium permiten controlar el tráfico entre workloads utilizando etiquetas asociadas a los recursos de Kubernetes. Estas etiquetas actúan como identificadores de identidad para los distintos componentes del sistema y permiten definir reglas que determinan qué servicios pueden comunicarse entre sí.

A diferencia de los mecanismos tradicionales basados únicamente en direcciones IP, Cilium permite aplicar políticas basadas en identidad, lo que facilita la gestión de reglas incluso cuando los pods cambian dinámicamente dentro del clúster.

En el modelo implementado, las políticas de red siguen un enfoque de **deny-by-default**, en el cual las comunicaciones entre workloads se bloquean por defecto y únicamente se habilitan aquellas que se definen explícitamente mediante políticas.

## Definición de políticas de red

Las políticas de red se definieron utilizando los recursos proporcionados por Cilium (CDRs) para controlar el tráfico entre los distintos componentes desplegados en el clúster. Estas políticas permiten especificar qué servicios pueden comunicarse entre sí y bajo qué condiciones.

En particular, se definieron reglas que restringen el acceso al gestor de secretos únicamente a los componentes autorizados, evitando que otros componentes del sistema puedan interactuar con este servicio.

Por esto mismo la comunicación entre algún elemento o aplicativo dentro del clúster y el gestor de secretos se vería de la siguiente forma: 

```mermaid
flowchart LR

App["Aplicación"]
Cilium["Cilium Network Policy"]
Bao["Vault/OpenBao"]

App --> Cilium
Cilium --> Bao
```

## Modelo de seguridad aplicado

El modelo de seguridad implementado combina mecanismos de control de acceso a secretos con políticas de red que restringen la comunicación entre servicios. De esta forma, incluso si un componente obtiene credenciales válidas, su capacidad de interactuar con otros servicios del sistema se encuentra limitada por las políticas de red definidas.

En particular, las políticas implementadas se enfocan en:

- Restringir el acceso al gestor de secretos únicamente a workloads autorizados
- Limitar la comunicación entre aplicaciones dentro del clúster
- Evitar el acceso directo a servicios críticos desde componentes no autorizados

## Ejemplo de política de acceso al gestor de secretos

A continuación se muestra un ejemplo simplificado de una política de red utilizada para permitir que una aplicación específica se comunique con el gestor de secretos.

```yaml
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
  name: allow-ingress-from-curl-app
  namespace: vault
spec:
  endpointSelector:
    matchLabels:
      app.kubernetes.io/name: vault/openbao
  ingress:
    - fromEndpoints:
        - matchLabels:
            k8s:io.kubernetes.pod.namespace: curl-app
            app: curl-app
      toPorts:
        - ports:
            - port: "8200"
              protocol: TCP
```

Esta política permite que únicamente los pods identificados con la etiqueta `curl-app` (aplicativo de prueba dentro del clúster) puedan establecer comunicación con el servicio del gestor de secretos a través del puerto correspondiente. De esta manera, se evita que otros workloads dentro del clúster puedan interactuar con el sistema de gestión de secretos.

Otro ejemplo más restrictivo es la aplicación de políticas de capa 7 como se muestra en la siguiente definición:

```yaml
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
  name: allow-post-to-vault-openbao
  namespace: vault
spec:
  endpointSelector:
    matchLabels:
      app.kubernetes.io/name: vault/openbao

  ingress:
    - fromEndpoints:
        - matchLabels:
            app: curl-app

      toPorts:
        - ports:
            - port: "8200"
              protocol: TCP
          rules:
            http:
              - method: "POST"
```

Esta política no solo restringe el acceso de los pods identificados con la etiqueta `curl-app` a un puerto y protocolo específico, sino que ahora también restringe el método http al que puede acceder, por lo que en este caso la aplicación solo podrá realizar solicitudes POST al puerto 8200, lo que en el caso de vault/openbao significa que no puede acceder a los endpoint para solicitar secretos (GET /v1/secret/data) pero si al login (POST /v1/auth/kubernetes/login).

## Consideraciones de seguridad

Durante la definición de políticas de red se tomaron en cuenta los siguientes principios:

- Restricción explícita de comunicaciones entre servicios

- Aplicación de microsegmentación entre componentes dentro del clúster

- Limitación del acceso al gestor de secretos

- Reducción del movimiento lateral dentro del clúster

- Alineación con principios Zero Trust

- La incorporación de estas políticas permite complementar los mecanismos de autenticación y autorización implementados en el gestor de secretos, en especial la aplicación de políticas L7 sobre la API expuesta por vault.