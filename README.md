# WordPress Development Starter

Esta es una plantilla para crear un entorno de desarrollo en WordPress con la ayuda de Docker.

**Advertencia:** Esta plantilla está probada con un sistema operativo linux y el tutorial de instalación y los comandos también.

## Instalación

Comenzamos modificando el archivo `Dockerfile` en la ruta `/build/wp-web/Dockerfile` donde añadiremos primero la etiqueta de la versión que quieras utilizar y por último el nombre de usuario de tu pc.

```Dockerfile
# Ejemplo: 6-php8.3-apache
FROM wordpress:<your_tag>
# Ejemplo: albertodsosa
RUN useradd <your_pc_user>
```
A continuación modificaremos el archivo `docker-compose.yml` que está en la ruta raíz. Como principal modificación para este archivo añadiremos el nombre de usuario de nuestro pc a la declaración de las variables de entorno `APACHE_RUN_USER` y `APACHE_RUN_GROUP`.

Algo que no es estrictamente necesario si no están en uso es modificar las ips de la red, así que echa un vistazo a la utilización de ips privadas en tu pc y modificarlas si están en uso. Puedes comprobarlo con este comando `ip addr`.

Otra cosa a tener en cuenta es que si prefieres que los contenedores se inicien automáticamente cuando enciendas el pc descomenta la variable `restart: always`.

-----------------------------------

Antes de ejecutar los comandos para activar los contenedores es recomendable ya que le estamos asignando ips a los contenedores que apunten a un host interno en nuestra máquina. Para ello nos dirigimos a nuestra consola y en el archivo `hosts` que se encuera en la ruta `/etc/` añadimos nuestros hosts por ejemplo de esta forma:

```bash
27.0.0.1       localhost
127.0.1.1      albertodsosa-laptop
172.18.0.10    wp-desktop.test
172.18.0.11    wp-phpmyadmin.test
172.18.0.12    wp-mariadb.test

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

¡Perfecto! Ahora estamos listos para iniciar nuestros contenedores. Vé a la consola y en la raíz donde se encuentra el archivo `docker-compose.yml` ejecuta el comando `docker compose up`. Si es la primera vez que lo haces con esto bastará para que docker se encargue de todo. Luego si quieres modificar algo en el archivo `Dockerfile` asegúrate de ejecutar primero `docker compose build` y luego `docker compose up`. Si modificas algo en el `docker-compose.yml` como una variable de entorno por ejemplo con `docker compose up` es suficiente.
