# Configurando mi primer switch de capa 3 

Agregamos el dispositivo como se ve a continuación:

![Alt text](img/Captura%20de%20pantalla%202023-03-02%20233513.png)

![Alt text](img/Captura%20de%20pantalla%202023-03-02%20233614.png)

![Alt text](img/Captura%20de%20pantalla%202023-03-03%20111617.png)

## Configurando STP

En modo de ejecución privilegiada

    show spanning-tree

![Alt text](img/Captura%20de%20pantalla%202023-03-03%20111958.png)

En esta captura podemos ver el tipo de protocolo habilitado, en este caso "protocol ieee" equivale al spanning tree normal.

También se nos indica que la raíz está en este switch con la línea "This bridge is the root".

Se ve un listado de interfaces, en el cual se puede ver su rol (Role), estado (Sts) y costo (Cost). Esta información es importante a la hora de poder describir el funcionamiento del STP. 

Un rol Root implica que se trata de la conexión hacia el switch raíz, un rol Desg se trata de una conexión que si bien no es para la raíz el algoritmo determinó que no representa un riesgo de loop y por lo tanto la información también puede pasar y un rol Altn es el de la reserva, se encuentra en modo bloqueo pero se activa si el puerto raíz o el puerto designado fallan.

La parte más importante es el estado, un puerto en estado LIS está escuchando y aprendiendo la topología de la red, un puerto en estado FWD va a permitir el paso de la información y por último un puerto en estado BLK no permitirá la transmisión de datos.

Para ver en mas detalle la información también podemos usar

    show spanning-tree detail

Y para ver los puertos bloqueados podemos usar

    show spanning-tree blockedports

Ingresamos a modo de configuración del switch

    configure terminal

Y luego tenemos los siguientes comandos disponibles

    spanning-tree mode pvst
    spanning-tree mode rapid-pvst
    spanning-tree mode mst

Estos tres comandos sirven para definir el modo en el que operará nuestro STP.

El "root" de nuestro STP puede ser definido de la siguiente manera

    spanning-tree vlan <vlan o lista de vlans> root primary

Con esto lograremos definir al switch como raíz y además indicarle las vlans con las que trabajará.

## Consideraciones proyecto 1

Recuerden que para su proyecto los pasos serían:

<ol>
<li>Hacer la topología</li>
<li>Elegir switch raiz y servidor vtp</li>
<li>Configurar vlans</li>
<li>Configurar enlaces en modo troncal y acceso</li>
<li>Configurar stp</li>
</ol>