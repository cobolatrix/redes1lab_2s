# VLSM y FLSM

Utilizaremos la siguiente información para la aplicación de ambos tipos de subnetteo.

ID de red = 192.168.0.0
Máscara de subred = 255.255.255.255

Las subredes están definidas como en la siguiente imagen:

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20193250.png)


## VLSM

Primeramente reordenaremos nuestras subredes dependiendo del número de equipos, de mayor a menor.

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20193641.png)

Luego, calcularemos la máscara de subred que pueda contener la cantidad de equipos que vamos a utilizar. (Acá puede variar un poco si dentro de estos equipos está contado o no el que funcionará como gateway predeterminado, para propositos de este ejemplo asumiremos que si).

También calcularemos el wildcard, el wildcard es la resta entre el host y 255.255.255.255, por lo que wildcard de por ejemplo la máscara de subred 255.255.255.252 sería 0.0.0.3.

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20194635.png)

Por ejemplo, para la VLAN de Ventas necesitamos 25 equipos, si revisamos la tabla vemos que con una máscara de subred /27 tenemos 30 hosts, por lo cual esta nos funcionará bien. Repetimos este procedimiento para todas las subredes.

El resultado queda así:

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20195032.png)

Con esta información ya podemos llenar la información de nuestras subredes, teniendo en cuenta que:

* Primera IP = ID de red + 1
* Broadcast = ID de red + Wildcard
* Última IP = Broadcast - 1
* Siguiente ID de red = Broadcast + 1

Por lo que nuestra tabla final quedaría así:

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20195401.png)

## FLSM

A diferencia del VLSM acá no es necesario ordenar, solo tenemos que tener en cuenta la cantidad de equipos de la subred más grande, determinamos la máscara de subred adecuada para este y se la aplicamos a todas las subredes.

Con el mismo ejemplo, vemos que la VLAN de Ventas pide 25 equipos, la máscara de subred adecuada para esto sería 255.255.255.224 así que se la aplicamos a todas las subredes, al final quedaría así.

![Alt text](img/Captura%20de%20pantalla%202023-04-22%20195835.png)