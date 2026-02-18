# Configuración Básica de un Router (Cisco CLI)

Guía práctica de configuración inicial de un router mediante interfaz **CLI**, incluyendo:

* **Configuración de interfaces**
* **Asignación de direcciones IP**
* **Activación de interfaces**
* **Persistencia de configuración**
* **Enrutamiento estático**

---

## 1. Acceso al Router

Nos dirigimos al **Router** y accedemos a la pestaña **CLI**.

![Acceso CLI](/img/router-cli-1.png)
![CLI inicial](/img/router-cli-2.png)

---

## 2. Configuración Inicial del Dispositivo

```cisco
enable                          # Entra al modo privilegiado (prompt #)
configure terminal              # Entra al modo de configuración global
hostname <NOMBRE_DEL_EQUIPO>    # Asigna un nombre único al dispositivo
interface <NOMBRE_INTERFAZ>     # Ej: gigabitEthernet 0/0
