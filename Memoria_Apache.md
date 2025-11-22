# Instalación y configuración de Apache
Resumen:
Palabras clave:
Índice:
### Introducción
El trabajo a realizar de tanto instalar como configurar el servidor web Apache se ha desarrollado en una clase del módulo 
de DAW del CFGS 2º DAW del instituto I.E.S. Juan Bosco, ubicado en Alcázar de San Juan, España.

Como se ha comentado, el entorno usado es Apache, un servidor web que nació en 1995 por un grupo de desarrolladores que decidió continuar trabajando sobre el código del servidor NCSA HTTPd, que era el más popular en aquellos tiempos aunque había dejado de actualizarse. Su nombre proviene tanto de una referencia a la tribu nativa americana Apache como del juego de palabras "a patchy server" que quiere decir "un servidor lleno de parches" ya que inicialmente estaba hecho a partir de “parches” del servidor NCSA.

El servidos web Apache sirve para hacer que los sitios web funcionen. Recibe solicitudes HTTP o HTTPS, las procesa y finalmente devuelve una respuesta, es decir, hace de intermedario.

Posibles alternativas son:
* Nginx:
    * Ligero y eficiente.
    * Maneja muchas conexiones simultáneas con pocos recursos.
    * Ideal como proxy inverso, balanceador de carga y servidor de caché.
    * Consume menos memoria que Apache.
* LiteSpeed:
    * Servidor web comercial.
    * Compatible con configuraciones Apache.
    * Rápido con PHP.
    * Incluye funciones integradas de seguridad y caché.
* Caddy:
    * Servidor web moderno.
    * Fácil de configurar.
    * Incluye HTTPS automático.
    * Ligero y multiplataforma.
* Microsoft IIS:
    * Integración nativa con el ecosistema Windows.
    * Administración gráfica intuitiva.
* Tomcat:
    * Especializado en Java.
* Node.js:
    * No es un servidor web tradicional, pero puede servir contenido HTTP y manejar webs dinámicas.
    * Ideal para aplicaciones en tiempo real.
    * Gran rendimiento en I/O.
* Cherokee:
    * Open source.
    * Fácil de usar.
    * Fácil de configurar.
    * Soporta balanceo, autenticación y proxy.

La motivación detrás de este trabajo es llevar a cabo la práctica propuesta para el módulo la cual es conseguir un intermediario que sería Apache, que nos permita conectar el cliente con el servidor.
### Cuerpo
1. Instalación:

   **1.1.** Actualizar el sistema mediante los comandos `sudo apt update` y `sudo apt upgrade -y`
   ![Actualizar el sistema](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/1.png)
   
   **1.2.** Instalar Apache mediante el comando `sudo apt install apache2 -y`
   ![Instalar Apache](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/2.png)
   
   **1.3.** Verificar la instalación mediante el comando `hostname -I`
   ![Verificar la instalación](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/3.png)
   
   **1.4.** Configurar el usuario y grupo de Apache mediante el comando `sudo nano /etc/apache2/envvars`
   ![Configurar el usuario y grupo de Apache](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/4.png)
   
   **1.5.** Configurar el directorio raíz mediante el comando `sudo nano /etc/apache2/apache2.conf` y dejarlo como
   
      `<Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
       </Directory>`
   ![Configurar el directorio raíz #1](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/5.png)
   ![Configurar el directorio raíz #2](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/6.png)
   
   **1.6.** Habilitar módulos de Apache mediante los comandos `sudo a2enmod headers` y `sudo a2enmod rewrite`
   ![Habilitar módulos de Apache](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/7.png)
   
   **1.7.** Establecer propiedades del directorio de documentos mediante el comando `sudo chown -R $USER:$USER /var/www/html`
   ![Establecer propiedades del directorio de documentos](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/8.png)
   
   **1.8.** Reiniciar Apache mediante el comando `sudo systemctl restart apache2`
   ![Reiniciar Apache](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/9.png)
   
   **1.9.** Compobación de que la instalación fue exitosa
   ![Compobación de que la instalación fue exitosa](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/10.png)

2. Configuración:

   **2.1.** Crear una carpeta para nuestra página web mediante el comando `sudo mkdir /var/www/gci/`
   ![Crear una carpeta para nuestra página web](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/11.png)
   
   **2.2.** Crear un archivo HTML en la carpeta anteriormente creada mediante los comandos `cd /var/www/gci/` y `sudo nano index.html`
   ![Crear un archivo HTML en la carpeta anteriormente creada](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/12.png)
   
   **2.3.** Escribir el siguiente código en el archivo HTML
   ![Escribir código en el archivo HTML](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/13.png)
   
   **2.4.** Configurar el archivo de configuración del host virtual mediante el comando `cd /etc/apache2/sites-available/`
   ![Configurar el archivo de configuración del host virtual](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/14.png)
   
   **2.5.** Como Apache venía con un archivo VirtualHost predeterminado, usamos ese como base. Aquí se usa gci.conf para que coincida con el nombre de nuestro subdominio. Hacerlo mediante el comando `sudo cp 000-default.conf gci.conf`
   ![Coincidir el host con el nombre de nuestro subdominio](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/15.png)
   
   **2.6.** Editar el archivo de configuración mediante el comando `sudo nano gci.conf`
   ![Editar el archivo de configuración #1](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/16.png)
   
   **2.7.** Colocar nuestro correo electrónico en ServerAdmin para que los usuarios puedan contactarnos en caso de que Apache experimente algún error, que la directiva DocumentRoot apunte al directorio donde están alojados los archivos de nuestro sitio y por último, como el archivo predeterminado no incluye una directiva ServerName, tendremos que añadirla y definirla agregando una línea concreta debajo de la última directiva:
   ![Editar el archivo de configuración #2](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/17.png)
   
   **2.8.** Activar el archivo de configuración del host virtual mediante el comando `sudo a2ensite gci.conf`
   ![Activar el archivo de configuración del host virtual](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/18.png)
   
   **2.9.** Recargar Apache mediante el comando `service apache2 reload`
   ![Recargar Apache](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/19.png)

   **2.10.** Poner nuestro nombre de host en el navegador e identificarse
   ![Poner nuestro nombre de host en el navegador e identificarse](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/20.png)

   **2.11.** Nos da error por lo que hay que hacer un cambio
   ![Nos da error por lo que hay que hacer un cambio](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/21.png)

   **2.12.** Mediante el comando `sudo nano /etc/hosts` añadimos la línea `127.0.0.1 gci.example.com`
   ![Editar /etc/hosts #1](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/22.png)
   ![Editar /etc/hosts #2](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/23.png)

   **2.13.** Volvemos a comprobar la página en el navegador y ahora ya sí va
   ![Volvemos a comprobar la página en el navegador y ahora ya sí va](https://github.com/JavierMoralesSimon/apacheIntroduccionYConfiguracion/blob/main/Capturas/24.png)

### Conclusión

### Bibliografía
Instalación de Apache: https://foro.puntocomunica.com/viewtopic.php?t=312
Configuración de Apache: https://ubuntu.com/tutorials/install-and-configure-apache#1-overview
ChatGPT: https://chatgpt.com/
