# Dolibarr on Docker

Imagen Docker para Dolibarr ERP & CRM suite web de código abierto.

Dolibarr es un software moderno para gestionar la actividad de tu organización (contactos, presupuestos, facturas, pedidos, stocks, agenda, RRHH, informes de gastos, contabilidad, ecm, fabricación, ...).

> [More information](https://github.com/dolibarr/dolibarr)


## Available versions/tags on Docker

See https://hub.docker.com/r/dolibarr/dolibarr/tags

*Very old Dolibarr versions may not be updated on docker hub, but you can always get them as standard zip package from Dolibarr official web site*


## Supported architectures

Linux x86-64 (`amd64`) and ARMv8 64-bit (`arm64v8`).


## How to run this image ?
## ¿Cómo ejecutar esta imagen?

Esta imagen está basada en el [repositorio oficial de PHP](https://hub.docker.com/_/php/) y el [repositorio oficial de Dolibarr](https://github.com/Dolibarr/dolibarr). Se construye usando las herramientas guardadas en el [repositorio de construcción Docker de Dolibarr](https://github.com/Dolibarr/dolibarr-docker).

Esta imagen no contiene base de datos, por lo que necesitas enlazarla con un contenedor de base de datos. Veamos cómo usar [Docker Compose](https://docs.docker.com/compose/) para integrarla con [MariaDB](https://hub.docker.com/_/mariadb/) (también puedes usar [MySQL](https://hub.docker.com/_/mysql/) si lo prefieres):

Si quieres tener una base de datos persistente y archivos de Dolibarr después de un reinicio o actualización, primero debes crear los directorios `/home/dolibarr_mariadb`, `/home/dolibarr_documents` y `/home/dolibarr_custom` en tu host para almacenar los archivos persistentes, respectivamente, de la base de datos, de los documentos de Dolibarr y de los módulos externos instalados.

`mkdir /home/dolibarr_mariadb /home/dolibarr_documents /home/dolibarr_custom;`

Luego, crea un archivo `docker-compose.yml` como el siguiente:

This image is based on the [official PHP repository](https://hub.docker.com/_/php/) and the [official Dolibarr repository](https://github.com/Dolibarr/dolibarr). It is build
using the tools saved in the [Dolibarr docker build repository](https://github.com/Dolibarr/dolibarr-docker). 

This image does not contains database, so you need to link it with a database container. Let's see how to use [Docker Compose](https://docs.docker.com/compose/) to integrate it with [MariaDB](https://hub.docker.com/_/mariadb/) (you can also use [MySQL](https://hub.docker.com/_/mysql/) if you prefer):

If you want to have a persistent database and Dolibarr data files after a reboot or upgrade, you must first
create the directories `/home/dolibarr_mariadb`, `/home/dolibarr_documents` and `/home/dolibarr_custom` on your host to store persistent files, respectively, of the database, of the Dolibarr document files and of the installed external Dolibarr modules.

`mkdir /home/dolibarr_mariadb /home/dolibarr_documents /home/dolibarr_custom;`

Then, create a `docker-compose.yml` file as following:

```yaml
# Edit this file then run 
# docker-compose up -d
# docker-compose logs

services:
    mariadb:
        image: mariadb:latest
        environment:
            MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD:-root}
            MYSQL_DATABASE: ${MYSQL_DATABASE:-dolidb}
            MYSQL_USER: ${MYSQL_USER:-dolidbuser}
            MYSQL_PASSWORD: ${MYSQL_PASSWORD:-dolidbpass}

        volumes:
            - /home/dolibarr_mariadb:/var/lib/mysql

    web:
        # Choose the version of image to install

        # Dolibarr en Docker

        Imagen Docker para Dolibarr ERP & CRM, suite web de código abierto.

        Dolibarr es un software moderno para gestionar la actividad de tu organización (contactos, presupuestos, facturas, pedidos, stocks, agenda, RRHH, informes de gastos, contabilidad, ECM, fabricación, ...).

        > [Más información](https://github.com/dolibarr/dolibarr)
            DOLI_CRON_KEY: ${DOLI_CRON_KEY:-mycronsecurekey}

        ## Versiones/tags disponibles en Docker

        Consulta https://hub.docker.com/r/dolibarr/dolibarr/tags

        *Las versiones muy antiguas de Dolibarr pueden no estar actualizadas en Docker Hub, pero siempre puedes obtenerlas como paquete zip estándar desde el sitio oficial de Dolibarr.*
            - "80:80"

        ## Arquitecturas soportadas

        Linux x86-64 (`amd64`) y ARMv8 64-bit (`arm64v8`).
            - /home/dolibarr_documents:/var/www/documents

        ## ¿Cómo ejecutar esta imagen?

        Esta imagen está basada en el [repositorio oficial de PHP](https://hub.docker.com/_/php/) y el [repositorio oficial de Dolibarr](https://github.com/Dolibarr/dolibarr). Se construye usando las herramientas guardadas en el [repositorio de construcción Docker de Dolibarr](https://github.com/Dolibarr/dolibarr-docker).

        Esta imagen no contiene base de datos, por lo que necesitas enlazarla con un contenedor de base de datos. Veamos cómo usar [Docker Compose](https://docs.docker.com/compose/) para integrarla con [MariaDB](https://hub.docker.com/_/mariadb/) (también puedes usar [MySQL](https://hub.docker.com/_/mysql/) si lo prefieres):

        Si quieres tener una base de datos persistente y archivos de Dolibarr después de un reinicio o actualización, primero debes crear los directorios `/home/dolibarr_mariadb`, `/home/dolibarr_documents` y `/home/dolibarr_custom` en tu host para almacenar los archivos persistentes, respectivamente, de la base de datos, de los documentos de Dolibarr y de los módulos externos instalados.

        `mkdir /home/dolibarr_mariadb /home/dolibarr_documents /home/dolibarr_custom;`

        Luego, crea un archivo `docker-compose.yml` como el siguiente:
Si tienes problemas con la instalación y necesitas eliminar el archivo `install.lock` desde Windows usando PowerShell y Docker Compose, puedes ejecutar los siguientes comandos:

```powershell

        Luego, construye y ejecuta todos los servicios (usa -d para ejecutarlos en segundo plano):

        `sudo docker-compose up -d`

        Si el comando "docker-compose" no está disponible, puedes reemplazarlo por "docker compose".

        Puedes verificar que los contenedores web y mariadb están activos y ver los logs con:

        `sudo docker-compose ps`
        `sudo docker-compose logs`

        Cuando el log muestre que el inicio está completo (deberías ver el mensaje "You can connect to your Dolibarr web application..."), accede a http://0.0.0.0 para iniciar la instalación de Dolibarr. El primer usuario administrador es admin/admin (si no cambiaste el valor por defecto en el archivo docker-compose.yml).

        Nota: Si el puerto 80 del host ya está en uso, puedes reemplazar "80:80" por "xx:80", donde xx es un puerto libre en el host. Podrás acceder a Dolibarr usando la URL http://0.0.0.0:xx
accounting                 banque    doctemplates  expensereport  holiday     migration_error.html  salaries
backup-before-upgrade.sql  bom       don           facture        margin      product               users

        ## Ejemplo de comandos PowerShell para eliminar install.lock y reiniciar contenedores

        Si tienes problemas con la instalación y necesitas eliminar el archivo `install.lock` desde Windows usando PowerShell y Docker Compose, puedes ejecutar los siguientes comandos:
 ✔ Container dolibarr-docker-cron-1     Started                                                               10.8s 
 ✔ Container dolibarr-docker-mariadb-1  Started                                                                1.1s 
 ✔ Container dolibarr-docker-web-1      Started                                                                2.5s 

        Después de esto, accede nuevamente a `http://localhost:81/` y sigue el asistente de instalación para crear las tablas y finalizar la configuración.
```

        Otros ejemplos:

        Puedes encontrar otros ejemplos de archivos docker-compose.yml para usos avanzados en el directorio `examples`, como:
         - [Dolibarr con cron (para el módulo de tareas programadas)](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-cron/)
         - [Dolibarr con certificado letsencrypt](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-certbot/)
         - [Dolibarr con servidor mysql](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-mysql/)
         - [Dolibarr con proxy reverso Traefik](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-rp-traefik/)
         - [Dolibarr con secrets](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-secrets/)
 - [Running Dolibarr with the cron (for Scheduled Tasks module)](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-cron/)
 - [Running Dolibarr with a letsencrypt certificate](https://github.com/Dolibarr/dolibarr-docker/tree/main/examples/with-certbot/)


        ## Actualización de versión de Dolibarr y migración de la base de datos

        Advertencia: Solo los datos almacenados en los directorios persistentes (ver la sección "volumes" de tu docker-compose.yml) no se perderán tras una actualización de los contenedores.

        Elimina el archivo `install.lock` ubicado dentro del volumen del contenedor `/var/www/documents` usando alguno de estos métodos:

        `sudo docker exec nombre_del_contenedor_web bash -c "rm -f /var/www/documents/install.lock"`

        o

        `sudo docker exec -it nombre_del_contenedor_web bash`
        `rm -f /var/www/documents/install.lock; exit`

        o si el directorio de documentos está configurado como directorio persistente, puedes hacerlo desde el host:

        `rm -f /home/dolibarr_documents/install.lock`

        Luego descarga la versión actualizada de los contenedores y reinícialos:

        `sudo docker-compose pull`
        `sudo docker-compose up -d`
        `sudo docker-compose logs`

        Asegúrate de que la variable de entorno `DOLI_INSTALL_AUTO` en tu docker-compose.yml esté en `1` para que la base de datos se migre automáticamente a la nueva versión, o puedes preferir usar el método estándar de actualización de Dolibarr a través de la interfaz web accediendo a la página /install.

`sudo docker-compose logs`

        ## Resumen de variables de entorno

        Puedes usar las siguientes variables para una mejor personalización de tu archivo docker-compose:


## Environment variables summary

        Algunas variables de entorno son compatibles con el comportamiento de docker secrets, solo agrega el sufijo `_FILE` al nombre de la variable y apunta al archivo que contiene el valor.
        Variables compatibles con docker secrets:

        * `DOLI_INSTANCE_UNIQUE_ID` => `DOLI_INSTANCE_UNIQUE_ID_FILE`
        * `DOLI_DB_USER` => `DOLI_DB_USER_FILE`
        * `DOLI_DB_PASSWORD` => `DOLI_DB_PASSWORD_FILE`
        * `DOLI_ADMIN_LOGIN` => `DOLI_ADMIN_LOGIN_FILE`
        * `DOLI_ADMIN_PASSWORD` => `DOLI_ADMIN_PASSWORD_FILE`
        * `DOLI_CRON_KEY` => `DOLI_CRON_KEY_FILE`
        * `DOLI_CRON_USER` => `DOLI_CRON_USER_FILE`
| **DOLI_DB_HOST**                | *mariadb*                      | Host name of the MariaDB/MySQL server
| **DOLI_DB_HOST_PORT**           | *3306*                         | Host port of the MariaDB/MySQL server

        ## Configuración avanzada

        ### Agregar scripts personalizados post-despliegue y antes de iniciar Apache

        Es posible ejecutar archivos personalizados `*.sh`, `*.sql` y/o `*.php` al final del despliegue o antes de iniciar Apache, montando volúmenes.
        Para scripts que se ejecutan durante el despliegue, monta el volumen en `/var/www/scripts/docker-init.d`.
        Para scripts que se ejecutan antes de iniciar Apache, monta el volumen en `/var/www/scripts/before-starting.d`.

        ```
        \docker-init.d
        |- custom_script.sql
        |- custom_script.php
        |- custom_script.sh
        ```

        Ejemplo de cómo montar los volúmenes en el archivo compose:

        ```yaml
        services:
            mariadb:
                image: mariadb:latest
                environment:
                    MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD:-root}
                    MYSQL_DATABASE: ${MYSQL_DATABASE:-dolidb}
                    MYSQL_USER: ${MYSQL_USER:-dolidbuser}
                    MYSQL_PASSWORD: ${MYSQL_PASSWORD:-dolidbpass}

            web:
                # Elige la versión de la imagen a instalar
                # dolibarr/dolibarr:latest (la última versión estable)
                # dolibarr/dolibarr:develop
                # dolibarr/dolibarr:x.y.z
                image: dolibarr/dolibarr
                environment:
                    DOLI_INIT_DEMO: ${DOLI_INIT_DEMO:-0}
                    DOLI_DB_HOST: ${DOLI_DB_HOST:-mariadb}
                    DOLI_DB_NAME: ${DOLI_DB_NAME:-dolidb}
                    DOLI_DB_USER: ${DOLI_DB_USER:-dolidbuser}
                    DOLI_DB_PASSWORD: ${DOLI_DB_PASSWORD:-dolidbpass}
                    DOLI_URL_ROOT: "${DOLI_URL_ROOT:-http://0.0.0.0}"
                    DOLI_ADMIN_LOGIN: "${DOLI_ADMIN_LOGIN:-admin}"
                    DOLI_ADMIN_PASSWORD: "${DOLI_ADMIN_PASSWORD:-admin}"
                    DOLI_CRON: ${DOLI_CRON:-0}
                    DOLI_CRON_KEY: ${DOLI_CRON_KEY:-mycronsecurekey}
                    WWW_USER_ID: ${WWW_USER_ID:-1000}
                    WWW_GROUP_ID: ${WWW_GROUP_ID:-1000}
                volumes:
                  - volume-scripts:/var/www/scripts/docker-init.d
                  - before-starting-scripts:/var/www/scripts/before-starting.d
                ports:
                    - "80:80"
                links:
                    - mariadb
        ```
\docker-init.d
|- custom_script.sql

        ### Ajuste de la configuración de Apache

        #### ServerName

        Si ejecutas `apache2ctl configtest` dentro del contenedor, probablemente verás un mensaje como:
        > AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using x.y.z.w Set the 'ServerName' directive globally to suppress this message

        Solución sencilla: crea un archivo de texto con el contenido:

        `ServerName dolibarr.example.com`

        Punto de montaje: `/etc/apache2/conf-enabled/servername.conf`

        Solo lectura: sí, móntalo como solo lectura con `:ro`
            MYSQL_PASSWORD: ${MYSQL_PASSWORD:-dolidbpass}

        #### ¿Ejecutas Dolibarr detrás de un proxy?

        Si quieres que Dolibarr o los logs del contenedor muestren la IP original y no solo la IP del proxy, debes crear dos archivos de texto:

        *remoteip.load*
        Este archivo carga el módulo remoteip de Apache: https://httpd.apache.org/docs/current/mod/mod_remoteip.html

        Contenido: `LoadModule remoteip_module /usr/lib/apache2/modules/mod_remoteip.so`

        Punto de montaje: `/etc/apache2/mods-enabled/remoteip.load`

        Solo lectura: sí, móntalo como solo lectura con `:ro`

        *remoteip.conf*
        Este archivo contiene la configuración de remoteip y también debe montarse como solo lectura dentro del contenedor. El contenido depende de tu proxy y del tipo de cabecera que utilice. Quizás debas habilitar el protocolo proxy, más información en https://httpd.apache.org/docs/current/mod/mod_remoteip.html

        Ejemplo de contenido: `RemoteIPHeader X-Forwarded-For`

        Punto de montaje: `/etc/apache2/mods-enabled/remoteip.conf`
            WWW_GROUP_ID: ${WWW_GROUP_ID:-1000}
        volumes :

        ### Soporte para PostgreSQL

        Estableciendo `DOLI_DB_TYPE` en `pgsql` puedes ejecutar Dolibarr con una base de datos PostgreSQL.
        Cuando se usa `pgsql`, Dolibarr debe instalarse manualmente en la primera ejecución:
         - Accede a `http://0.0.0.0/install`;
         - Sigue el asistente de instalación;
         - Agrega el archivo `install.lock` dentro del volumen del contenedor `/var/www/html/documents` (ejemplo: `docker-compose exec services-data_dolibarr_1 /bin/bash -c "touch /var/www/html/documents/install.lock"`).

        En este modo, para actualizar la versión es obligatorio usar la interfaz web:
         - Elimina el archivo `install.lock` (ejemplo: `docker-compose exec services-data_dolibarr_1 /bin/bash -c "rm -f /var/www/html/documents/install.lock"`).
         - Accede a `http://0.0.0.0/install`;
         - Actualiza la base de datos;
         - Agrega nuevamente el archivo `install.lock` dentro del volumen del contenedor `/var/www/html/documents` (ejemplo: `docker-compose exec services-data_dolibarr_1 /bin/bash -c "touch /var/www/html/documents/install.lock"`).
If you run apache2ctl configtest inside the container you'll probably get a message like this:
> AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using x.y.z.w Set the 'ServerName' directive globally to suppress this message

        ## Solución de problemas

        Si obtienes el error "urllib3.exceptions.URLSchemeUnknown: Not supported URL scheme http+docker" durante docker-compose, prueba actualizar o degradar el paquete pip:
        `pip install requests==2.31.0`

Mountpoint: "/etc/apache2/conf-enabled/servername.conf"

read-only: Yes, mount it read only with :ro 

#### Running your dolibarr behind a proxy?

If you want Dolibarr or the logs from the dolibarr container to reveal the original IP address and not just the proxy's IP address you should create 2 text files:

*remoteip.load*
This file will load the apache module remoteip https://httpd.apache.org/docs/current/mod/mod_remoteip.html

Contents: "LoadModule remoteip_module /usr/lib/apache2/modules/mod_remoteip.so"

Mountpoint: "/etc/apache2/mods-enabled/remoteip.load"

read-only: Yes, mount it read only with :ro 

*remoteip.conf*
This file will contain the configuration for remoteip and should also be bind mounted read-only inside the container. Content will depend on your proxy and which kind of header it uses. You may perhaps also enable the proxy protocol, read more at https://httpd.apache.org/docs/current/mod/mod_remoteip.html

Example content: "RemoteIPHeader X-Forwarded-For"

Mountpoint: "/etc/apache2/mods-enabled/remoteip.conf"


### Support for PostgreSQL

Setting `DOLI_DB_TYPE` to `pgsql` enable Dolibarr to run with a PostgreSQL database.
When set to use `pgsql`, Dolibarr must be installed manually on it's first execution:
 - Browse to `http://0.0.0.0/install`;
 - Follow the installation setup;
 - Add `install.lock` inside the container volume `/var/www/html/documents` (ex `docker-compose exec services-data_dolibarr_1 /bin/bash -c "touch /var/www/html/documents/install.lock"`).

When setup this way, to upgrade version the use of the web interface is mandatory:
 - Remove the `install.lock` file (ex `docker-compose exec services-data_dolibarr_1 /bin/bash -c "rm -f /var/www/html/documents/install.lock"`).
 - Browse to `http://0.0.0.0/install`;
 - Upgrade DB;
 - Add `install.lock` inside the container volume `/var/www/html/documents` (ex `docker-compose exec services-data_dolibarr_1 /bin/bash -c "touch /var/www/html/documents/install.lock"`).

 
## Trouble shooting

If you get error "urllib3.exceptions.URLSchemeUnknown: Not supported URL scheme http+docker" during docker-compose, try to upgrade or downgrade the pip package:
pip install requests==2.31.0
