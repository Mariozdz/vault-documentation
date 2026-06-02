# Conectividad privada con Nebula

## Propósito de la sección

Nebula se incorpora como una tecnología de conectividad privada que permite comunicar entornos distribuidos mediante una red overlay cifrada. En el contexto de una arquitectura orientada a Zero Trust, su función es reducir la necesidad de exponer servicios sensibles de forma pública y permitir que solo nodos autorizados puedan establecer comunicación entre sí.

Esta sección presenta los fundamentos conceptuales de Nebula, su forma general de operación y las razones por las cuales puede utilizarse como una capa complementaria dentro de una arquitectura segura para la gestión de secretos.


## ¿Qué es Nebula?

Nebula es una herramienta de red overlay que permite conectar hosts ubicados en distintas redes físicas o lógicas mediante túneles cifrados. Cada nodo que participa en la red Nebula posee una identidad criptográfica representada por un certificado emitido por una autoridad certificadora propia de Nebula.

A diferencia de una red tradicional donde la confianza suele depender de la ubicación dentro de una red privada, Nebula permite que la comunicación se base en identidades verificables. Esto resulta relevante para arquitecturas Zero Trust, donde no se debe asumir confianza únicamente por pertenecer a una red interna.

Cada participante de la red Nebula normalmente cuenta con:

- Un certificado emitido por la autoridad certificadora de Nebula.
- Una dirección IP dentro de la red overlay.
- Una configuración local con lighthouses, reglas de firewall y parámetros de conectividad.
- Una identidad lógica que puede incluir nombre, grupos y subredes autorizadas.

## Componentes principales

### Autoridad certificadora de Nebula

La autoridad certificadora de Nebula es responsable de emitir los certificados utilizados por los nodos de la red overlay. Esta CA representa la raíz de confianza de la red Nebula.

Todo nodo que desee participar en la red debe contar con un certificado válido emitido por esta CA. Por esta razón, la clave privada de la CA debe protegerse cuidadosamente y no debe almacenarse en repositorios Git ni distribuirse junto con los manifiestos de despliegue.

---

### Certificados de nodo

Cada nodo de Nebula utiliza un certificado propio. Este certificado identifica al nodo dentro de la red overlay y permite aplicar controles de comunicación basados en identidad.

Un certificado de Nebula puede contener información como:


- Nombre del nodo
- Dirección IP dentro de la red overlay
- Grupos asociados
- Subredes permitidas
- Vigencia del certificado


Estos atributos pueden utilizarse posteriormente para aplicar reglas de firewall basadas en identidad. Por ejemplo, se puede permitir que únicamente los nodos pertenecientes al grupo `client` se conecten al puerto `8200` de un gateway asociado a Vault.


### Lighthouse

El lighthouse es un nodo utilizado para facilitar el descubrimiento entre participantes de la red Nebula. Su función principal es permitir que los nodos conozcan cómo alcanzarse entre sí, especialmente cuando se encuentran detrás de NAT o en redes diferentes.

El lighthouse no reemplaza a un proxy de aplicación ni expone directamente los servicios internos. Su función es ayudar a que los nodos Nebula establezcan conectividad entre ellos (o funcionar como puente de comunicación en caso de ser utilizado como "relay").

En una arquitectura típica, el lighthouse se ubica en una máquina con dirección pública estable, como una VM en la nube.

### Red overlay

La red overlay es la red lógica privada creada por Nebula. Cada nodo recibe una IP privada dentro de esta red, independiente de la red física donde se encuentre.

Por ejemplo:


- Lighthouse:     10.10.0.1
- Vault Gateway:  10.10.0.10
- Client Gateway: 10.10.0.20

Aunque estos nodos estén ubicados en redes diferentes, Nebula permite que se comuniquen a través de la red overlay usando túneles cifrados.


### Firewall de Nebula

Nebula incluye reglas de firewall que permiten controlar qué tráfico puede entrar o salir de cada nodo. Estas reglas pueden basarse en elementos como:


- Host
- Grupo
- Puerto
- Protocolo
- CIDR

Esto permite aplicar controles de mínimo privilegio. En lugar de permitir conectividad general entre todos los nodos, se pueden definir reglas específicas para permitir únicamente los flujos necesarios.

Ejemplo conceptual:

```yaml
firewall:
  inbound:
    - port: 8200
      proto: tcp
      group: client
```

Esta regla representa la idea de permitir conexiones TCP al puerto `8200` únicamente desde nodos que pertenezcan al grupo `client`.

## Funcionamiento general

El funcionamiento general de Nebula puede resumirse de la siguiente manera:

1. Se crea una autoridad certificadora de Nebula.
2. Se emiten certificados para cada nodo participante.
3. Se configura un lighthouse con dirección alcanzable.
4. Los nodos se conectan al lighthouse para descubrirse.
5. Nebula establece túneles cifrados entre nodos autorizados.
6. Las reglas de firewall definen qué comunicación está permitida.
7. El tráfico fluye por la red overlay sin exponer directamente los servicios internos.

## Relación con Zero Trust

Nebula se alinea con los principios de Zero Trust porque evita asumir que la red interna es automáticamente confiable. En su lugar, cada nodo debe demostrar su identidad mediante un certificado válido.

Dentro de este enfoque:

- La identidad del nodo se verifica criptográficamente.
- La comunicación se limita mediante reglas explícitas.
- La pertenencia a la red overlay no implica acceso total.
- Los servicios internos pueden mantenerse sin exposición pública directa.
- Las reglas pueden modelarse bajo el principio de mínimo privilegio.

Nebula no reemplaza otros controles de seguridad como TLS de aplicación, autenticación, autorización o políticas de red dentro de Kubernetes. Más bien, funciona como una capa adicional de conectividad privada y control de acceso entre entornos.

## ¿Por qué utilizar Nebula?

Nebula se propone como alternativa para habilitar comunicación privada entre entornos sin exponer públicamente servicios sensibles. En el contexto de una arquitectura de gestión de secretos, esto resulta importante porque Vault suele contener información crítica y debe reducirse su superficie de exposición.

En lugar de publicar Vault mediante un Ingress público, Nebula permite crear un canal privado entre consumidores autorizados y el entorno donde Vault se encuentra desplegado.

Sus principales ventajas son:

- Permite conectividad privada entre redes distintas.
- Utiliza certificados como base de identidad.
- Reduce la necesidad de exposición pública de servicios sensibles.
- Permite reglas de acceso basadas en host, grupo, puerto y protocolo.
- Puede operar en entornos híbridos, locales o cloud.
- Se adapta a escenarios multi-cluster.
- Complementa controles Zero Trust existentes en Kubernetes.


## Diferencia frente a exponer servicios públicamente

Una opción común para acceder a servicios dentro de Kubernetes es publicarlos mediante Ingress, LoadBalancer o NodePort. Sin embargo, para servicios sensibles como Vault, esta decisión puede aumentar la superficie de ataque y requerir controles adicionales.

Nebula permite una alternativa donde el servicio se mantiene interno y solo se habilita acceso mediante la red overlay.

## Rol dentro de una arquitectura de gestión de secretos

En una arquitectura orientada a la gestión segura de secretos, Nebula no cumple la función de almacenar, emitir o rotar secretos. Su función es proporcionar una ruta de conectividad privada entre los consumidores autorizados y el sistema encargado de gestionar los secretos.

Por tanto, Nebula se ubica en la capa de conectividad segura entre entornos, mientras que Vault mantiene la responsabilidad sobre la gestión de secretos, autenticación, autorización, políticas y auditoría.

| Capa | Componente | Responsabilidad |
|---|---|---|
| Gestión de secretos | Vault | Almacenar, controlar y auditar el acceso a secretos |
| Identidad de aplicación | Certificados / Vault auth | Autenticar consumidores |
| Confianza interna | cert-manager / trust-manager | Emitir y distribuir certificados y CA bundles |
| Red interna del cluster | Cilium | Aplicar políticas de red y segmentación |
| Conectividad entre entornos | Nebula | Crear túneles privados cifrados entre nodos o gateways |
| Automatización | GitOps / Argo CD | Mantener configuración versionada y reproducible |


## Consideraciones de seguridad

El uso de Nebula debe acompañarse de buenas prácticas operativas y de seguridad:

- La clave privada de la CA de Nebula debe resguardarse fuera del repositorio.
- Los certificados de nodo deben tener una vigencia controlada.
- Las reglas de firewall deben seguir el principio de mínimo privilegio.
- El lighthouse debe exponer únicamente los puertos necesarios.
- La conectividad Nebula no debe reemplazar la autenticación propia de los servicios.
- Los servicios sensibles deben mantener TLS, autenticación y autorización a nivel de aplicación.

Nebula debe entenderse como una capa complementaria, no como el único mecanismo de protección.


## Referencias 
**Nebula**  
*Nebula: Open source overlay networking*  
Disponible en: [Ver documentación](https://nebula.defined.net/docs/)
