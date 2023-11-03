# RIP

Para este ejemplo usaremos la siguiente topología.

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20200508.png)

Y configuraremos los dispositivos de la siguiente forma

## R1

    enable
    configure terminal
    interface e0/1
    ip address 9.0.0.1 255.255.255.0
    no shutdown
    interface e0/0
    ip address 10.0.0.1 255.255.255.0
    no shutdown

    !empezamos a configurar RIP
    router rip

    !usamos la versión 2
    version 2

    !definimos las redes conectadas a este router
    network 9.0.0.0
    network 10.0.0.0
    
    !guardamos la configuración
    do write

## R2

    enable
    configure terminal
    interface e0/1
    ip address 11.0.0.1 255.255.255.0
    no shutdown
    interface e0/0
    ip address 10.0.0.2 255.255.255.0
    no shutdown

    !empezamos a configurar RIP
    router rip

    !usamos la versión 2
    version 2

    !definimos las redes conectadas a este router
    network 10.0.0.0
    network 11.0.0.0
    
    !guardamos la configuración
    do write

Por último, con ponerle ips adecuadas a las VPCS ya se podrá tener ping a lo largo de la topología.

## Comandos para verificar la configuración

    show ip protocol
    show ip route
    show ip rip database
