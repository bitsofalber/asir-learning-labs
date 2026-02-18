#  Configuración básica de un Router (Cisco CLI)

Guía práctica de configuración inicial de un router mediante interfaz **CLI**, incluyendo:

- Configuración de interfaces
- Asiganción de dirección IP
- Activación de interfaces
- Guardado de configuración
- Enrutamiento estático

---

##  Acceso al Router

Nos dirigimos al **Router** y accedemos a la pestaña **CLI**.

![Acceso CLI](/img/router-cli-1.png)  
![CLI inicial](/img/router-cli-2.png)

---

##  Configuración inicial del dispositivo

```bash
enable                               # Entra al modo privilegiado (prompt #)
configure terminal                  # Entra al modo de configuración global
hostname <NOMBRE_DEL_EQUIPO>        # Asigna un nombre único al dispositivo
interface <NOMBRE_INTERFAZ>         # Cambiamos a la interfaz que queramos modificar Ej: gigabitEthernet 0/0```

Ahora tenemos que configurar la dirección IP del gateway que tiene que coincidir y ser la misma que tienen los dispositivos conectados a esa interfaz de red.

```bash
ip address <IP> <MASCARA>      # Le asignamos la IP que consideremos y su máscara Ej: 192.168.10.1 255.255.255.0```

Y después de hacer esta configuración viene una paso muy importante que es levantar toda esta configuración.

```bash
no shutdown         # Levantamos toda la configuración.
write memory        # Guardamos los ajustes fuera de la memoria volatil.
runing-config startup-config  # Tambien sirve para guardar los ajustes.```

*Si  tuvieramos que configurar una red WAN , no basta solo con configurar los routers y sus interfaces. Ya que el router no tiene información mas allá de lo que tiene conectado directamente.*
Deberemos configurar la configuración del ***enrutamiento.***
En este caso vamos a realizar el enrutamiento estático.

```bash
# Dentro del router.
configure terminal
ip router <DIRECCIÓN_DESTINO> <MÁSCARA> <SIGUIENTE_SALTO> # Ej: 10.1.1.0 255.255.255.0 20
9.165.200.226
end
write memory```

*Recordar que hay que hacer una configuración por cada interfaz de red a la que queramos llegar.*

*Y lo tenemos que hacer en ambas direcciones.*









