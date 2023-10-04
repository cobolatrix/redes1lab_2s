# Ruteo InterVLAN

## Usando un router

Para lograr el ruteo intervlan con un router emplearemos subinterfaces, las cuales pueden ser creadas con el siguiente comando:

Asumiendo que le crearemos subinterfaces a la interfaz Ethernet 0/0

    interface Ethernet 0/0.<numero de vlan>
    encapsulation dot1q <numero de vlan>

    interface Ethernet 0/0.10
    encapsulation dot1q 10

Con esto ya estará creada la subinterfaz, luego tendremos que asignarle una IP como estamos acostumbrados.

![Alt text](img/Captura%20de%20pantalla%202023-04-12%20152346.png)

### R1

    enable
    configure terminal
    hostname R1
    interface Ethernet 0/0
    no shutdown
    interface Ethernet 0/0.10
    encapsulation dot1q 10
    ip address 192.168.1.1 255.255.255.0
    interface Ethernet 0/0.20
    encapsulation dot1q 20
    ip address 192.168.2.1 255.255.255.0
    do write

### SW

Este se configura como siempre, creandole las VLANS y asignando los tipos de puertos, tanto los que van en modo acceso como los que van en modo troncal.

## Usando un switch de capa 3

Para lograr el ruteo intervlan con un switch de capa 3 emplearemos interfaces virtuales, por ejemplo para crear una interfaz virtual para la vlan 10 usaremos el comando:

    interface vlan 10

Dentro de esta configuración le asignaremos ip como estamos acostumbrados y es importante encender la interfaz con "no shutdown", también hay que recordar habilitar el ruteo IP en nuestro router para que pueda hacer el enrutamiento, esto se logra con el comando (en modo de configuración):

    ip routing

![Alt text](img/Captura%20de%20pantalla%202023-04-12%20154948.png)

### ESW

    enable
    configure terminal
    hostname ESW
    vlan 10
    name GERENCIA
    vlan 20
    name IT
    interface e0/0
    switchport trunk encapsulation dot1q
    switchport mode trunk
    interface vlan 10
    ip address 192.168.1.1 255.255.255.0
    no shutdown
    interface vlan 20
    ip address 192.168.2.1 255.255.255.0
    no shutdown
    exit
    ip routing
    do write

### SW

Podemos aprovechar VTP y configurar las vlans desde ESW o podemos hacerlo acá, todo lo demás es igual al SW del ejemplo anterior.