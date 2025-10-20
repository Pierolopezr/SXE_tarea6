# SXE_tarea6

# Nivel 1

## Crear un fichero `docker-compose.yml` con los servicios requeridos

Por medio de intellij, creo el archivo `docker-compose.yml` que define los siguientes servicios:

- **prestashop-app**: servicio de PrestaShop
- **prestashop-db**: servicio de base de datos MySQL
- **prestashop-phpmyadmin**: servicio de phpMyAdmin para gestionar la base de datos

### Dentro del archivo `docker-compose.yml` colocamos los siguientes datos para el funcionamiento de los servicios mencionados.
Estos datos, como lo indica el nivel uno, colocaremos un usuario y contraseña escritos. 
Posteriormente, añadimos los puertos a cada uno, 8080 y 8081.

```yaml
services:
  # Servicio de base de datos MySQL
  prestashop-db:
    image: mysql:5.7
    container_name: prestashop-db
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: hola123Piero
      MYSQL_DATABASE: prestashop
      MYSQL_USER: prestashop
      MYSQL_PASSWORD: hola123Piero
    volumes:
      - mysql_data:/var/lib/mysql

  # Servicio de PrestaShop
  prestashop-app:
    image: prestashop/prestashop:latest
    container_name: prestashop-app
    restart: unless-stopped
    environment:
      DB_SERVER: prestashop-db
      DB_NAME: prestashop
      DB_USER: prestashop
      DB_PASSWORD: hola123Piero
    ports:
      - "8080:80"
    volumes:
      - prestashop_data:/var/www/html
    depends_on:
      - prestashop-db

  # Servicio de phpMyAdmin
  prestashop-phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: prestashop-phpmyadmin
    restart: unless-stopped
    environment:
      PMA_HOST: prestashop-db
      MYSQL_ROOT_PASSWORD: hola123Piero
    ports:
      - "8081:80"
    depends_on:
      - prestashop-db

volumes:
  mysql_data:
  prestashop_data:

```
Configurar dependencias y variables de entorno
Se ha utilizado depends_on para asegurar que PrestaShop y phpMyAdmin no se inicien hasta que la base de datos esté lista.

Las variables de entorno (MYSQL_*, DB_*, PMA_*) están definidas directamente en el archivo.

Para iniciar todos los servicios, se ejecuta:
'docker-compose up'

Se recomienda no usar -d para ver los logs en tiempo real y detectar errores durante el arranque.

Estructura del fichero

services: Define los tres contenedores necesarios.
image: Es la imagen oficial usada por cada servicio.
environment: Configura las credenciales y parámetros de conexión.
ports: Conecta los servicios con el navegador mediante puertos locales.
volumes: Garantiza la persistencia de datos aunque se borren los contenedores.
depends_on: Establece el orden de arranque entre servicios.
container_name: Facilita la identificación de cada contenedor.

PrestaShop — Asistente de instalación
Al acceder por primera vez a http://localhost:8080, aparece el asistente de instalación a lo cual:
crearemos una cuenta hasta que nos aparezca la pantalla de bienvenida.

PrestaShop — Configuración de base de datos
Se introducen los siguientes datos:

Servidor: prestashop-db
Base de datos: prestashop
Usuario: prestashop
Contraseña: hola123Piero

PrestaShop — Panel de administración
Una vez completada la instalación, se accede al backend desde el enlace generado (ej. http://localhost:8080/Piero123):

PrestaShop — Vista de la tienda
La tienda está disponible en http://localhost:8080:


phpMyAdmin — Tablas de la base de datos
Se accede a http://localhost:8081 con:

Usuario: root
Contraseña: hola123Piero

Dentro de la base de datos prestashop, se visualizan las tablas creadas (ps_cart, ps_customer, ps_orders, etc.).


<img width="1181" height="930" alt="Captura de pantalla 2025-10-19 115211" src="https://github.com/user-attachments/assets/aed9f8cf-2ac8-4ade-a270-a6052d33ad82" />
<img width="1276" height="908" alt="Captura de pantalla 2025-10-19 115158" src="https://github.com/user-attachments/assets/e4426b06-2c3c-488a-ae5d-9a18746d003c" />
<img width="492" height="462" alt="Captura de pantalla 2025-10-19 124101" src="https://github.com/user-attachments/assets/26f555e2-5561-43a4-bc25-3abe6da18872" />
<img width="1479" height="927" alt="Captura de pantalla 2025-10-19 124005" src="https://github.com/user-attachments/assets/823bbece-c51b-4c75-9982-20deb88989ab" />
<img width="1200" height="623" alt="Captura de pantalla 2025-10-19 123910" src="https://github.com/user-attachments/assets/b40c0e0a-05be-4585-966e-5936ef296a32" />
<img width="1635" height="1100" alt="Captura de pantalla 2025-10-19 121132" src="https://github.com/user-attachments/assets/37295ea9-de10-43c6-9a2a-fdb23c26e2ce" />
<img width="1648" height="1115" alt="Captura de pantalla 2025-10-19 120732" src="https://github.com/user-attachments/assets/b03d8cc7-ca9b-44f2-b6d9-f7dbcb10c799" />
<img width="1296" height="1128" alt="Captura de pantalla 2025-10-19 120330" src="https://github.com/user-attachments/assets/7db1c21d-d1d5-4ff5-ae54-6bca5d6abf68" />
<img width="1634" height="1127" alt="Captura de pantalla 2025-10-19 115501" src="https://github.com/user-attachments/assets/8b831267-d04d-4381-90ad-9f835fca2748" />
