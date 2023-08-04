# Instalando imagenes de dispositivos usando ishare2

Emplearemos la herramienta ishare2 para instalar las imagenes de los dispositivos que se usarán en el laboratorio.

ishare2: https://github.com/ishare2-org/ishare2-cli

Los dispositivos a emplear serán:

- Switch de capa 3 (que también funcionará en la capa 2): i86bi_linux_l2-adventerprisek9-ms.SSA.high_iron_20190423.bin
- Router: i86bi_LinuxL3-AdvEnterpriseK9-M2_157_3_May_2018.bin

Para instalar ishare2 recomiendo copiar y correr este comando, esto debido a que la guia de instalación del repositorio oficial está desactualizada:

    wget -O /usr/sbin/ishare2 https://raw.githubusercontent.com/ishare2-org/ishare2-cli/main/ishare2 > /dev/null 2>&1 && chmod +x /usr/sbin/ishare2 && ishare2

Luego, usando el comando ishare2 search <nombre de la imagen> podremos encontrar los dispositivos a usar, por ejemplo:

    ishare2 search i86bi_linux_l2-adventerprisek9-ms.SSA.high_iron_20190423.bin

El comando nos dirá si lo encontró, su id y también nos dará un ejemplo del comando usado para descargar la imagen en nuestra máquina virtual, en el caso de los dispositivos que usaremos en el laboratorio los comandos serían al 04/08/2023:

    ishare2 pull bin 6
    ishare2 pull bin 19

Al ejecutar los comandos y si no hay ningún problema con la descarga, los dispositivos ya deberían quedar disponibles para usarlos en nuestro PNETLab.

# Instalación de Wireshark

Wireshark será el programa que utilizaremos para capturar paquetes a lo largo del curso, puede ser descargado de acá: https://www.wireshark.org/

Es importante que al momento de instalarlo marquemos la opción en "Tool" que dice sshdump como se ve en la imagen.

![Alt text](<img/Captura de pantalla 2023-08-04 134322.png>)

Para el desarrollo del laboratorio pueden usar el Wireshak instalado en su sistema operativo o el interno del PNETLab, la instalación y uso de este segundo se explicará en el laboratorio.

