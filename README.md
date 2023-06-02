🚀 Aplicación Slim Framework 4 PHP + MySQL con despliegue automático.
==============================

## 📝 Introducción
El principal objetivo de este repositorio es poder desplegar de forma automática nuestra aplicación PHP Slim Framework 4 en un servidor en la nube. En esta ocación vamos a utilizar la versión gratuita de Railway, que nos permite vincular nuestro repositorio de github con la plataforma, poder desplegar automáticamente nuesto código y quedar disponible en la web.

## 1⃣ Forkear proyecto
Como primer paso, debemos hacer un fork de este proyecto desde el boton ubicado en la parte superior derecha de la pagina del repositorio.

## 2⃣ Subimos nuestro código (opcional si agregan código)
Una vez forkeado, clonamos el repo con `git clone <url del repo>` y agregamos nuestro codigo PHP (SLIM Framework).
Luego comiteamos y pusheamos los cambios.

```sh
git add .
git commit -m "first commit"
git push -u origin main
```

## 3⃣ Creamos y configuramos la aplicación en el servidor remoto

Para poder desplegar nuestro código en un servidor remoto, necesitamos una plataforma que nos permita gestionar uno. Para ello, nos dirigimos a la página de Railway https://railway.app/, iniciamos sesión con nuestra cuenta de Github.

![Railway2](https://i.ibb.co/XSj7ppS/railway-2.png)

Railway al iniciar sesión nos muestra su dashboard, aquí haremos clic en **Deploy from Github repo**

![Railway1](https://i.ibb.co/q9570sL/railway-1.png)

En esta sección buscamos por el nombre de nuestro repo forkeado. Ej.: **slim-php**

![Railway3](https://i.ibb.co/Yf2Fnx6/railway-3.png)

Una vez hecho esto, va a comenzar a clonar y desplegar nuestro repositorio en el servidor remoto. Este paso puede demorar unos minutos.

![Railway4](https://i.ibb.co/XxsR518/railway-4.png)

Una vez que termine vamos a poder ir a la sección **Settings** y elegir la rama de github que queremos deplegar con nuestra aplicación, en nuestro caso `main`. De esta forma, cada vez que se haga una modificación a esta rama, Railway va actualizar automáticamente la aplicación.

![Railway5](https://i.ibb.co/CVk5fLR/railway-5.png)

En esa misma sección podemos verificar si el depliegue se hizo con exito y la url para acceder en **Domains**. 

https://slim-php-deployment-production.up.railway.app/

Accedemos a la URL de la app desplegada y si todo funcionó correctamente veremos el siguiente mensaje:

``` {"method":"GET","msg":"Bienvenido a SlimFramework 2023"} ```

## 4️⃣ Crear y configurar la base de datos MySQL 

Abre [dev.new](https://dev.new/) y elige "**Provisionar MySQL**".

![01-railway-mysql](https://user-images.githubusercontent.com/12433465/224468181-60f51bbe-0105-4874-bdae-568d0b3fc587.png)

Después de configurar la base de datos, haz clic en **"MySQL"** a la izquierda y luego elige **"Connect"**.

![02-connect-to-database](https://user-images.githubusercontent.com/12433465/224468219-6d90581a-a0fc-4caa-95c2-d55cf373c264.png)

### Copia y pega el comando del cliente de MySQL

Tu propia contraseña se incluirá en lugar de `xxxx`.

```plaintext
mysql -hcontainers-us-west-8.railway.app -uroot -xxxx --port 7551 --protocol=TCP railway
```

(es necesario descargar MySQL)

Ejecuta los siguientes comandos SQL para crear una tabla de prueba con datos iniciales.

```plaintext
-- Estructura de tabla para la tabla `usuarios`
CREATE TABLE `usuarios` (
`id` int(11) NOT NULL,
`usuario` varchar(250) COLLATE utf8_unicode_ci NOT NULL,
`clave` varchar(250) COLLATE utf8_unicode_ci NOT NULL,
`fechaBaja` date DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

-- Volcado de datos para la tabla `usuarios`
INSERT INTO `usuarios` (`id`, `usuario`, `clave`, `fechaBaja`) VALUES
(1, 'franco', 'Hsu23sDsjseWs', NULL),
(2, 'pedro', 'dasdqsdw2sd23', NULL),
(3, 'jorge', 'sda2s2f332f2', NULL);

-- Indices de la tabla `usuarios`
ALTER TABLE `usuarios` ADD PRIMARY KEY (`id`);
```

## Requisitos para correr localmente

- Instalar PHP o XAMPP (https://www.php.net/downloads.php o https://www.apachefriends.org/es/download.html)
- Instalar Composer desde https://getcomposer.org/download/ o por medio de CLI:

```sh
php -r "copy('//getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
```

## Correr localmente via XAMPP

- Copiar proyecto dentro de la carpeta htdocs

```sh
C:\xampp\htdocs\
```
- Acceder por linea de comandos a la carpeta del proyecto y luego instalar Slim framework via Compose

```sh
cd C:\xampp\htdocs\<ruta-del-repo-clonado>
composer update
```
- En el archivo index.php agregar la siguiente linea debajo de `AppFactory::create();`

```sh
// Set base path
$app->setBasePath('/app');
```
- Abrir desde http://localhost/app ó http://localhost:8080/app (depende del puerto configurado en el panel del XAMPP)

## Correr localmente via PHP

- Acceder por linea de comandos a la carpeta del proyecto y luego instalar Slim framework via Compose

```sh
cd C:\<ruta-del-repo-clonado>
composer update
php -S localhost:666 -t app
```

- Abrir desde http://localhost:666/

## Archivo .env localmente

Crear dentro de la carpeta `/app/` el archivo `.env` tomando de referencia `.env.example`

Agregamos los siguientes datos Clave -> Valor:

```sh
MYSQL_HOST=remotemysql.com (campo "Server" de los datos que guardamos al crear la base en remotemysql.com)
MYSQL_PORT=3306 (campo "Port" de los datos que guardamos al crear la base en remotemysql.com)
MYSQL_USER=elcNx8VTCx (campo "Username" de los datos que guardamos al crear la base en remotemysql.com)
MYSQL_PASS=1234 (campo "Password" de los datos que guardamos al crear la base en remotemysql.com)
MYSQL_DB=elcNx8VTCx (campo "Database Name" de los datos que guardamos al crear la base en remotemysql.com)
```

## Ayuda
Cualquier duda o consulta por el canal de slack

### 2022 - UTN FRA
