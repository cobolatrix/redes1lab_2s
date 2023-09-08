# EtherChannel

## Topologia a realizar

![Alt text](img/Captura%20de%20pantalla%202023-03-09%20225638.png)

### Configurando Port-channel 1 (PAGP)

#### S1

    configure terminal
    interface range f0/3-4
    channel-group 1 mode desirable
    no shutdown

#### S3

    configure terminal
    interface range f0/3-4
    channel-group 1 mode auto
    no shutdown

### Configurando Port-channel 2 (LACP)

#### S1

    configure terminal
    interface range f0/1-2
    channel-group 2 mode active
    no shutdown

#### S2

    configure terminal
    interface range f0/1-2
    channel-group 2 mode passive
    no shutdown

### Verificando la configuración

#### S1

    show etherchannel summary
    show pagp neighbor
    show lacp neighbor

