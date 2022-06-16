# Instalación y configuración de ngnix


Esta práctica consiste en instalar y configurar el servidor web nginx, y además, establecer dos "dominios" o sitios web bajo nuestro localhost con dos HTML diferentes. Las páginas HTML que he utilizado son:

 - [Ant Colony](https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/ant_colony.html) *de Christopher Powroznik*.
 - [Fishies](https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/fishies.html) *de William Chung*.

>Estas páginas HTML, han sido sacadas de https://onehtmlpagechallenge.com/

# Instalación de nginx

Para poder instalar nginx en linux, *el SO que estoy usando para la práctica*, deberemos abrir la terminal y ejecutar el siguiente comando: `apt-get install nginx`. Este comando empezará a descargar e instalar nginx.
Para comprobar que ngnix se ha instalado correctamente procedemos a escribir `localhost` en nuestro navegador:

![image](https://user-images.githubusercontent.com/91749310/174076508-ee2ef56e-d1df-4ab9-9ff6-008f5baa5c1d.png)

Como podemos ver, ngnix se ha instalado correctamente.

# Sitios web en localhost

## Creación de sitios web

A continuación, crearemos dos dominios para poder usar las dos páginas HTML, para ello usaremos el comando `cd /etc/nginx/sites-available` para situarnos en ese directorio y poder copiar la configuración por defecto, o *default*. 

Para poder copiar dicha configuración (*debemos asegurarnos de estar en el directorio sites-available*) utilizamos el comando `sudo cp default xavieruno` y `sudo cp default xavierdos`. Con esto copiaremos el archivo *default* dos veces, *una vez por cada dominio*.

![image](https://user-images.githubusercontent.com/91749310/174088866-6f385b6e-83d2-483a-8d6e-ea9b1318042e.png)

## Edición de la configuración de  sitios web

Una vez ya tengamos las dos configuraciones copiadas debermos editarlas para ponerles un nombre de dominio personalizado, entre otras cosas. Para ello deberemos editar las configuraciones con `sudo vim xavieruno`.
Esto nos abrirá el editor *vim* y nos aparecerá esto:

![image](https://user-images.githubusercontent.com/91749310/174079369-093dbc17-c931-4963-861b-b9713e0045cc.png)

Lo que nos interesa cambiar en el archivo de configuración es:

 - Quitar *default_server* de las dos primeras líneas *listen*.
 - Cambiar la línea de *root* a `root /var/www/xavieruno;`
 - Cambiar el *_* de *server_name* a `server_name xavieruno.sistemas.com;`

![image](https://user-images.githubusercontent.com/91749310/174080664-7c8557cb-09cf-4ced-ba55-10e4953addd0.png)
*Archivo de configuración editado*

Una vez hayamos terminado de editar el documento, presionamos la tecla *ESC* y escribimos `:x` y el damos a *Enter*. Esto nos guardará el archivo y nos sacará del editor *vim*.

Realizamos el mismo proceso pero con *xavierdos*.

## Habilitar sitio web

Una vez tengamos la configuración creada deberemos habilitar el sitio web creando un *enlace simbólico* en el directorio sites-enabled; para ello deberemos situarnos primero en *sites-enabled* con el comando `cd /etc/nginx/sites-enabled` y a continuación usaremos el comando `sudo ln -s /etc/nginx/sites-available/xavieruno` para crear dicho enlace y habilitar el sitio web.

![image](https://user-images.githubusercontent.com/91749310/174088605-2b5d455a-323a-4b6d-8b24-d496d8a3c3bb.png)

Realizamos el mismo proceso pero con *xavierdos* y recargamos nginx para que todos se aplique correctamente con el comando `sudo nginx -s reload`.

Para que los dominios especificados en la configuración de los sitios web redirijan a nuestro localhost deberemos editar el archivo *hosts* que se encuentra en `/etc/hosts` con el comando `sudo nano /etc/hosts`.

![image](https://user-images.githubusercontent.com/91749310/174083179-847d36e5-7cd0-46b1-887c-568ba5c18821.png)
Deberemos añadir las dos siguientes líneas:

    127.0.0.1 xavieruno.sistemas.com xavieruno
    127.0.0.1 xavierdos.sistemas.com xavierdos
La dirección *127.0.0.1* es nuestro localhost e indica a que dirección se redirije *xavieruno.sistemas.com*, el cual es el nombre del dominio personalizado, y xavieruno al final, es el alias.

Guardamos el archivo y salimos.

## Creación de los directorios de los sitios web

A continuación, crearemos el directorio para cada sitio web donde irán los archivos HTML. Para ello, usamos el comando `cd /var/www` para situarnos en la ruta donde crearemos los directorios con los comandos `sudo mkdir xavieruno` y  `sudo mkdir xavierdos`. 

A continuación, crearemos los archivos HTML situándonos en *xavieruno* y usando el comando `sudo vim index.html` y se nos abrirá el editor *vim*, en mi caso he copiado el HTML de [Ant Colony](https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/ant_colony.html) y lo he pegado en el index.html. Guardamos, cerramos y repetimos el mismo proceso con *xavierdos* pero con el HTML de [Fishies](https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/fishies.html).

## Comprobación

Para comprobar si los sitios web funcionan, nos dirigimos a nuestro navegador y escribimos `xavieruno.sistemas.com` y `xavierdos.sistemas.com`:

![image](https://user-images.githubusercontent.com/91749310/174087219-61a06c09-7cca-459b-b193-9b9d1b4b56f2.png)*xavieruno.sistemas.com*

![image](https://user-images.githubusercontent.com/91749310/174087144-95cd7ce6-1ebc-459a-b4c6-e31f2e4164c9.png)
*xavierdos.sistemas.com*

# Conclusiones
He tenido que repetir esta práctica bastantes veces porque al principio lo estuve intentando hacer en Windows 10, mientras estábamos en clase, pero como en Windows por algún motivo que desconozco está hecho de manera distinta no fui capaz de hacer la práctica. Esta vez, la he hecho con Linux y he sido capaz de realizarla, aunque tarde.

# Anexos
https://onehtmlpagechallenge.com/

 - https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/ant_colony.html
 - https://github.com/Metroxe/one-html-page-challenge/blob/master/entries/fishies.html

###  Xavier Borrás Mercant - Sistemas Informáticos
