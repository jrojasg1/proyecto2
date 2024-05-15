## Proyecto 2

En esta ocasión, llevamos a cabo la implementación de una aplicación WordPress en un entorno altamente disponible utilizando tecnologías de contenedorización y gestión de clústeres. Nuestro objetivo principal fue garantizar la disponibilidad y escalabilidad de la aplicación, así como optimizar la gestión de recursos.

### Tecnologías Utilizadas

- **WordPress**: Plataforma de gestión de contenido (CMS) ampliamente utilizada, elegida como base para nuestra aplicación web.
- **Kubernetes**: servicio EKS para automatizar la implementación, escalado y gestión de aplicaciones en contenedores.
- **Nginx**: Servidor web y proxy inverso utilizado como balanceador de carga para distribuir el tráfico de manera eficiente entre los nodos del clúster Kubernetes.
- **Amazon Elastic File System (EFS)**: Sistema de archivos en red utilizado para almacenar los archivos estáticos y dinámicos de WordPress, garantizando la persistencia de los datos y facilitando su acceso desde múltiples instancias.
- **Amazon Relational Database Service (RDS)**: Servicio administrado de bases de datos relacionales utilizado para alojar la base de datos MySQL de WordPress, garantizando la escalabilidad, la alta disponibilidad y la gestión simplificada de la base de datos.

### Objetivos del Proyecto

- **Alta Disponibilidad**: Implementar la aplicación WordPress en un entorno altamente disponible para garantizar la disponibilidad continua del servicio, minimizando así el tiempo de inactividad y mejorando la experiencia del usuario.
- **Escalabilidad**: Configurar el clúster Kubernetes para escalar automáticamente los recursos según la demanda de la aplicación, permitiendo manejar picos de tráfico sin comprometer el rendimiento.
- **Gestión Simplificada**: Utilizar servicios administrados de AWS como EFS y RDS para minimizar la carga operativa en la gestión de infraestructura, permitiendo al equipo centrarse en el desarrollo y la mejora continua de la aplicación.

## Archivos de Configuración

Las configuraciones necesarias para el despliegue de cada componente se encuentran detalladas en los siguientes archivos YAML:

- `issuer.yaml`: Configuración del certificado SSL/TLS para el balanceador de carga.
- `lb.yaml`: Configuración del balanceador de carga Nginx.
- `nfs.yaml`: Configuración del sistema de archivos en red (NFS).
- `wordpress.yaml`: Configuración de la aplicación WordPress.

## Prerrequisitos

Antes de comenzar con la implementación, es necesario contar con ciertos prerrequisitos:

1. **Instalación de kubectl**: Se requiere instalar desde la CLI de AWS, kubectl, utilizando el siguiente comando:

```bash
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.29.3/2024-04-19/bin/linux/amd64/kubectl
```

2. **Instalación de helm**: 

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
3. **Instalación  del controlador de Ingress Nginx**:para configurar el balanceador de carga Nginx, se necesita instalar el controlador de Ingress Nginx. Esto se puede lograr con los siguientes comandos:

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx
```


## Ejecución de servicios:

```bash
kubectl apply -f nfs.yaml
kubectl apply -f wordpress.yaml
kubectl apply -f issuer.yaml
kubectl apply -f lb.yaml
```