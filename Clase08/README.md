# Configurando nuestro primer router

Usaremos la imagen **i86bi_LinuxL3-AdvEnterpriseK9-M2_157_3_May_2018.bin** la cual pueden descargar con el ishare2 como se vio en la clase 2.

Y luego lo configuramos de esta manera.

![Alt text](img/Captura%20de%20pantalla%202023-03-17%20100036.png)

# Creando rutas estáticas

    ip route [red de destino] [máscara de subred] [siguiente salto]

Donde:
* Red de destino: El id de la red a la que queremos llegar
* Máscara de subred: La máscara de subred de la red de destino
* Siguiente salto: La dirección ip que se encuentra afuera de nuestro router que nos ayudará a llegar al lugar al que queremos ir.

# Topología a implementar

![Alt text](img/Captura%20de%20pantalla%202023-03-17%20130404.png)

Es importante tener definidas nuestras redes, en este ejemplo tenemos 4 redes, las 2 que están conectadas con el switch y la vpc y las 2 que se usan para comunicación entre routers.

Una vez definido eso podemos empezar a trabajar, por simplicidad asumiremos que la puerta de enlace predeterminada de cada red será la ip terminada en 1 y la ip de la vpc de cada red será la terminada en 2.

En las redes definidas entre routers asignaremos las ips de la siguiente forma.

| Router | Interfaz | IP | Máscada de subred
| --- | --- | --- | --- |
| R3 | e0/1 | 10.0.0.1 | 255.255.255.0
| R3 | e0/0 | 11.0.0.1 | 255.255.255.252
| R1 | e0/0 | 11.0.0.2 | 255.255.255.252
| R1 | e0/1 | 192.167.0.1 | 255.255.255.252
| R2 | e0/1 | 192.167.0.2 | 255.255.255.252
| R2 | e0/0 | 192.168.0.1 | 255.255.255.0

## R3

    configure terminal
    
    !configuramos la primera interfaz, la puerta de enlace predeterminada
    interface e0/1
    ip address 10.0.0.1 255.255.255.0
    no shutdown

    !configuramos el primer enlace entre routers
    interface e0/0
    ip address 11.0.0.1 255.255.255.252
    no shutdown

    !configuramos las rutas estáticas
    !hacia 11.0.0.0
    ip route 11.0.0.0 255.255.255.252 11.0.0.2
    !hacia 192.167.0.0
    ip route 192.167.0.0 255.255.255.252 11.0.0.2
    !hacia 192.168.0.0
    ip route 192.168.0.0 255.255.255.0 11.0.0.2

## R1

    configure terminal

    !configuramos el segundo enlace entre routers
    interface e0/0
    ip address 11.0.0.2 255.255.255.252
    no shutdown

    !configuramos el tercer enlace entre routers
    interface e0/1
    ip address 192.167.0.1 255.255.255.252
    no shutdown

    !configuramos las rutas estáticas
    !hacia 10.0.0.0
    ip route 10.0.0.0 255.255.255.0 11.0.0.1
    !hacia 11.0.0.0
    ip route 11.0.0.0 255.255.255.252 11.0.0.1

    !estas dos posiblemente no van, pero tampoco afectan
    !hacia 192.167.0.0
    ip route 192.167.0.0 255.255.255.252 192.167.0.2
    !hacia 192.168.0.0
    ip route 192.168.0.0 255.255.255.0 192.167.0.2

## R2

    configure terminal
    
    !configuramos el cuarto enlace entre routers
    interface e0/0
    ip address 192.167.0.2 255.255.255.252
    no shutdown

    !configuramos la última interfaz, la otra puerta de enlace predeterminada
    interface e0/1
    ip address 192.168.0.1 255.255.255.0
    no shutdown

    !configuramos las rutas estáticas
    !hacia 10.0.0.0
    ip route 10.0.0.0 255.255.255.0 192.167.0.1
    !hacia 11.0.0.0
    ip route 11.0.0.0 255.255.255.252 192.167.0.1
    !hacia 192.167.0.0
     ip route 192.167.0.0 255.255.255.252 192.167.0.1

## Comprobando la configuración

    show ip route
    show running-config | section ip route


