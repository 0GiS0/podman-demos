# Podman 🦭 vs. Docker 🐳

¡Hola developer 👋🏻! Este repositorio contiene las demos mostradas durante mi vídeo [12. Docker 🐳 vs. Podman 🦭](https://youtu.be/Mc_kAf0UkmY?si=eyxE8kOE2byJUDCq).

![Podman vs Docker](docs/images/Docker%20vs%20Podman.png)

En este repo puedes encontrar algunos ejemplo de cómo puedes comprobar que trabajar con Podman es casi igual que trabajar con Docker.

Si quieres ver estos ejemplos en acción puedes ver el vídeo en mi canal de YouTube relacionado con estos ejemplos:

[PLAVEHOLDER VIDEO]

## Cómo ejecutar tu primer contenedor

En Podman, al igual que en Docker, podemos ejecutar contenedores utilizando los mismos parámetros que en `docker run`:

```bash
podman run --name web -d -p 8080:80 nginx 
```

Este comando descargará la imagen de nginx de Docker Hub y la ejecutará en un contenedor, exactamente igual que si lo hiciéramos con Docker.

## Construir tus propias imágenes

Para construir tus propias imágenes, puedes hacerlo con un Containerfile, que es exactamente igual que un Dockerfile, pero con otro nombre.

```bash
podman build -t solarsystem:v1 .
podman run --name solar -d -p 8081:80 solarsystem:v1
```

## Podman Compose

Podman Compose es una herramienta que permite definir y ejecutar aplicaciones multi-contenedor con Podman, utilizando un archivo YAML para definir las configuraciones de los servicios. Es una alternativa a Docker Compose. El archivo de configuración es exactamente igual que el de Docker Compose compose.yml.

```bash
podman compose up
```

## Crear un pod

Como has podido ver, hasta ahora hemos estado trabajando con contenedores sueltos. Pero en Podman, al igual que en Kubernetes, se trabaja con el concepto de Pod, que es un grupo de contenedores que comparten un mismo espacio de red y volúmenes.

```bash
# Crear el pod
podman pod create --name wordpress -p 8082:80 -p 3306:3306

# Ejecutar el contenedor de MySQL dentro del pod
podman run -d --pod wordpress \
--name mysql \
-e MYSQL_ROOT_PASSWORD=Password1234! \
-e MYSQL_DATABASE=wordpress \
-e MYSQL_USER=wordpress \
-e MYSQL_PASSWORD=Password1234! \
mysql

# Ejecutar el contenedor de WordPress dentro del pod
podman run -d --pod wordpress \
--name wordpress \
-e WORDPRESS_DB_HOST=mysql \
-e WORDPRESS_DB_USER=wordpress \
-e WORDPRESS_DB_PASSWORD=Password1234! \
wordpress
```

```bash
podman pod ps
```

## Utilizar un manifiesto de Kubernetes para crear pods

Y ya por último, también es posible crear Pods de Podman utilizando manifiestos de Kubernetes:

```bash
podman play kube --publish 8085:80 pod.yaml
```

¡Nos vemos 👋🏻!
