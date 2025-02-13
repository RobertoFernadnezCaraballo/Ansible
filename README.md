1️⃣ Habilitar la autenticación en Apache

Edita (o crea) un archivo .htaccess en el directorio que quieres proteger, por ejemplo:

sudo nano /var/www/html/protegido/.htaccess

Agrega estas líneas:

AuthType Basic
AuthName "Acceso Restringido"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user

2️⃣ Crear usuarios y contraseñas

Ahora, crea un usuario con htpasswd:

sudo htpasswd -c /etc/apache2/.htpasswd usuario1

Esto te pedirá una contraseña para usuario1 y la guardará en /etc/apache2/.htpasswd.

Si quieres agregar más usuarios (sin sobrescribir):

sudo htpasswd /etc/apache2/.htpasswd usuario2

3️⃣ Habilitar .htaccess en Apache

Asegúrate de que Apache permita el uso de .htaccess. Edita el archivo de configuración del sitio web:

sudo nano /etc/apache2/sites-available/000-default.conf

Busca la línea:

<Directory /var/www/html>

Y asegúrate de que AllowOverride esté en All:

<Directory /var/www/html>
    AllowOverride All
</Directory>

Guarda y cierra el archivo.
4️⃣ Reiniciar Apache

Aplica los cambios reiniciando Apache:

sudo systemctl restart apache2

5️⃣ Prueba el acceso

Ahora, cuando accedas a http://tu-servidor/protegido, Apache te pedirá usuario y contraseña.

Si no te lo pide, revisa los logs de Apache:

sudo tail -f /var/log/apache2/error.log
