# Configuración Básica de un Router (Cisco CLI)

Guía práctica de configuración inicial de un router mediante interfaz **CLI**, incluyendo:

* **Configuración de interfaces**
* **Asignación de direcciones IP**
* **Activación de interfaces**
* **Persistencia de configuración**
* **Enrutamiento estático**

---
# Nos basaremos en el siguiente ejemplo para realizar esta práctica:

![Paso 1: Configuración inicial](/02-redes/img/r2.png)


## Acceso al Router

Nos dirigimos al **Router** y accedemos a la pestaña **CLI**.

![Paso 1: Configuración inicial](/02-redes/img/r1.png)

---

## Configuración Inicial del Dispositivo

```cisco
enable                          # Entra al modo privilegiado (prompt #)
configure terminal              # Entra al modo de configuración global
hostname <NOMBRE_DEL_EQUIPO>    # Asigna un nombre único al dispositivo
interface <NOMBRE_INTERFAZ>     # Ej: gigabitEthernet 0/0
```

## Configuración de IP y Activación
Es vital que la dirección IP del gateway coincida con la configuración de los dispositivos finales.

```cisco
ip address <IP> <MASCARA>       # Ej: 192.168.10.1 255.255.255.0
no shutdown                     # Levanta la interfaz (la activa)
```

## Guardado de Configuración
Para evitar perder los cambios tras un reinicio, guardamos en la NVRAM:

```cisco
write memory                    # Comando abreviado (wr)
# O también:
copy running-config startup-config
```

![Paso 1: Configuración inicial](/02-redes/img/r3.png)

## Enrutamiento Estático
Nota: En redes WAN, el router solo conoce sus redes directamente conectadas. Para alcanzar redes remotas, debemos definir rutas.

```cisco
configure terminal
# Formato: ip route <RED_DESTINO> <MASCARA> <SIGUIENTE_SALTO>
ip route 10.1.1.0 255.255.255.0 209.165.200.226
end
write memory
```
![Paso 1: Configuración inicial](/02-redes/img/r5.png)

Recuerda que el enrutamiento debe configurarse en ida y vuelta para que haya comunicación bidireccional.





