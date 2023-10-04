# Configurando HSRP

Tendremos 2 routers, llamados R1 y R2

![Alt text](img/Captura%20de%20pantalla%202023-03-24%20132418.png)

## Configurando a R1

    enable
    configure terminal
    !le definimos su nombre
    hostname R1

    !configuramos la interfaz
    interface Ethernet 0/0
    ip address 10.0.0.2 255.255.255.0
    no shutdown

    !usamos la version 2 de HSRP
    standby version 2

    !definimos su id de grupo HSRP y la dirección ip virtual del gateway
    standby 21 ip 10.0.0.1
    
    !también le definimos su prioridad
    standby 21 priority 109

    !configuramos el preempt, que sirve para que recupere la prioridad una se recupere la comunicación
    standby 21 preempt

    !guardamos
    do write


## Configurando a R2

    enable
    configure terminal
    hostname R2
    interface Ethernet 0/0
    ip address 10.0.0.3 255.255.255.0
    no shutdown
    standby version 2
    standby 21 ip 10.0.0.1
    do write

## Verificando la configuración

    show standby
    show standby brief

# Configurando GLBP

Tendremos de nuevo dos routers, R3 y R4

![Alt text](img/Captura%20de%20pantalla%202023-03-24%20132451.png)

## Configurando a R3

    enable
    configure terminal
    hostname R3
    interface Ethernet 0/0
    ip address 192.168.0.2 255.255.255.0
    no shutdown
    glbp 7 ip 192.168.0.1
    glbp 7 preempt
    glbp 7 priority 150
    glbp 7 load-balancing round-robin
    do write

## Configurando a R4

    enable
    configure terminal
    hostname R4
    interface Ethernet 0/0
    ip address 192.168.0.3
    no shutdown
    glbp 7 ip 192.168.0.1
    glbp 7 load-balancing round-robin
    do write

## Verificando la configuración

    show glbp brief






