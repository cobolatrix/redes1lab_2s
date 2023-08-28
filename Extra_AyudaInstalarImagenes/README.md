# Instalación de imagenes externas al PNETLab

Paso 1: Descargar y descomprimir las imagenes que pasó el ingeniero: https://drive.google.com/file/d/1LUh24wPFQ8CnORf2I-AfsP5kW1LMIscE/view?usp=sharing

Paso 2: Iniciar la máquina virtual en la que está el PNETLab.

Paso 3: Descargar e instalar algún software para realizar conexión usando el protocolo SFTP, por ejemplo en Windows recomiendo Filezilla: https://filezilla-project.org/download.php?type=client

Paso 4: Seleccionar las imagenes a instalar, como detalle extra si siguieron la instalación de imagenes vistas en la clase 2 ya tienen instaladas las de la carpeta IOL.

![Alt text](<img/Captura de pantalla 2023-08-28 112513.png>)

Paso 5: Loguearse a la máquina virtual que contiene el PNETLab usando el software SFTP, usando las credenciales para conectarse por SSH.

![Alt text](<img/Captura de pantalla 2023-08-28 112804.png>)

Paso 6: En el cliente SFTP, en la parte de sitio remoto navegar a la siguiente dirección:

    /opt/unetlab/addons/qemu

Ahí se deberán arrastrar y soltar las imagenes a instalar (menos las de IOL porque estas ya están instaladas).

![Alt text](<img/Captura de pantalla 2023-08-28 113002.png>)


Cuando se obtenga este mensaje ya estará terminada la transferencia.

![Alt text](<img/Captura de pantalla 2023-08-28 113024.png>)

Paso 7: En nuestro PNETLab debemos ir a "System", "System Setting" y le damos clic al botón "Fix Permission".

![Alt text](<img/Captura de pantalla 2023-08-28 113128.png>)

![Alt text](<img/Captura de pantalla 2023-08-28 113230.png>)

Paso 8: Las imagenes ya están listas para ser usadas.

Nota: Si al iniciar el dispositivo de las imagenes este se enciende y se apaga tocará que activar la virtualización, la opción que dice "Virtualize Intel VT-x...", es todo un tema aparte por lo complicado que se puede poner.

![Alt text](<img/Captura de pantalla 2023-08-28 115054.png>)
