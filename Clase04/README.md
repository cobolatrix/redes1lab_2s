# Comandos básicos de IOS

Al conectarnos al dispositivo nos puede salir una pantalla así.

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20191017.png)

Si notamos después del nombre predeterminado del dispositivo se muestra un ">", el cual indica que nos encontramos en modo EXEC de usuario.

En este modo tendremos acceso a un número límitado de comandos, para ver los comandos disponibles podemos presionar "?" y nos saldrá un listado de todos los comandos disponibles.

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20191248.png)

Entre estos se encuentran por ejemplo "ping" y "enable". El ping ya lo conocemos pero el enable es el comando que nos permite subir de nivel y entrar a modo EXEC privilegiado, el cual nos permitirá indagar más en la configuración del dispositivo.

Al utilizar el comando enable si nos damos cuenta el ">" cambió a "#", esto nos indica que estamos en modo EXEC privilegiado, para salir de este modo y volver al modo EXEC de usuario podemos usar el comando "exit".

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20191442.png)

Dentro del modo EXEC privilegiado también hay una larga lista de comandos disponibles para su uso, en este modo tenemos 2 comandos importantes, "show running-config", el cual nos muestra la configuración del dispositivo y "copy running-config startup-config" que guarda la configuración del mismo, también podemos usar el comando "write" para guardar la configuración del dispositivo.

Pero en este modo no podemos realizar la configuración del dispositivo, por lo que para realizar esto necesitaremos usar el comando "configure terminal". Esto pondrá al dispositivo en el modo de configuración global.

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20191752.png)

En este modo podremos configurar completamente nuestro dispositivo, para salir del modo podemos usar "exit", "end" o ctrl+Z.

Para poderle cambiar el nombre a nuestro dispositivo podemos usar el comando "hostname <nombre>", por ejemplo:

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20192111.png)

Para poder configurar las interfaces de nuestro dispositivo usamos el comando "interface <nombre_interfaz> <numero>", por ejemplo:

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20191944.png)

Dentro de este modo podemos controlar todo lo referente a la interfaz dada, por ejemplo apagarla o encenderla usando "shutdown" y "no shutdown".

También desde el modo de configuración global podremos usar los comandos del modo EXEC privilegiado, para hacerlo tenemos que anteponer "do" al comando, por ejemplo "do write".

# Creación de VLANS

Para crear una VLAN usaremos este comando desde el modo de configuración global: "VLAN <numero>", por ejemplo "VLAN 10", luego podremos asignarle un nombre a la misma usando name, por ejemplo "name CONTABILIDAD".

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20192551.png)

# Configuración de modo troncal

Para configurar el modo troncal necesitamos acceder a la interfaz que queremos configurar en dicho modo y usar los comandos:

    interface ethernet 0/0
    switchport trunk encapsulation dot1q
    switchport mode trunk

# Configuración de modo acceso

Para configurar el modo acceso necesitamos acceder a la interfaz que queremos configurar en dicho modo y usar los comandos:

    interface ethernet 0/1
    switchport mode access
    switchport access vlan 10

# Verificación de la configuración

Para ver las VLANS del dispositivo usamos el comando "show VLAN"

![Alt text](img/Captura%20de%20pantalla%202023-02-16%20192736.png)

Para ver el estado del modo troncal en el dispositivo usamos el comando "show interfaces trunk"

 ![Alt text](img/Captura%20de%20pantalla%202023-02-16%20195411.png)

 Para ver los puertos en modo acceso y su vlan asignada usamos el comando "show vlan"
 
 ![Alt text](img/Captura%20de%20pantalla%202023-02-16%20200339.png)

 # Ejemplo completo

    ! esto es un comentario
    enable
    configure terminal
    hostname SW1

    ! creando y definiendo las vlans
    vlan 10
    name CONTABILIDAD
    vlan 20
    name ADMINISTRACION
    vlan 99
    name NATIVA
    exit

    ! configurando el modo troncal
    interface ethernet 0/0
    switchport trunk encapsulation dot1q
    switchport mode trunk

    ! cambiando la vlan nativa
    switchport trunk native vlan 99

    ! restringiendo las vlan que se pasarán en modo troncal
    switchport trunk allowed vlan 10,20,99,1002-1005

    ! configurando el modo acceso
    interface ethernet 0/1
    switchport mode access
    switchport access vlan 10

    interface ethernet 0/2
    switchport mode access
    switchport access vlan 20

    ! guardando la configuracion
    do write
    end
