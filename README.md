# Raspberry Pi 5 - Setup Guide
### Getting Started
> [!IMPORTANT]
> Para este proyecto se necesita algunos componentes:
> - Raspberry Pi 5 *(Modelo de 8GB recomendado)* [🔗](https://amzn.eu/d/8PSWlGE)
> - Fuente de alimentación Raspberry Pi 27W [🔗](https://amzn.eu/d/5KuvbUQ)
> - Tarjeta microSD 128GB *(capacidad variable)* [🔗](https://amzn.eu/d/2EA1wH9)
> - (Opcional) Caja para Raspberry Pi 5 NVMe [🔗](https://amzn.eu/d/1gozBP4)
> - (Opcional) SSD NVMe M.2 500GB  *(capacidad variable)* [🔗](https://amzn.eu/d/a8RKGx0)

> [!NOTE]
> Cabe destacar que tanto el modelo de 8GB, como el SSD NVMe son opcionales, pero recomendados para un mejor rendimiento y duarabilidad.
> 
> La caja para Raspberry Pi 5 NVMe es opcional, pero recomendada para una mejor refrigeración y protección del SSD NVMe.

### Instalación de Raspberry Pi OS
Para comenzar con la instalación de Raspberry Pi OS, instalaremos Raspberry Pi Imager en nuestro sistema operativo. Para ello, accedemos a la [página oficial](https://www.raspberrypi.org/software/)   de Raspberry Pi Imager y descargamos el programa según nuestro sistema operativo.

<details>
<summary>Configuración Imagen Raspberry Pi OS</summary>
<br>

1. Seleccionamos la opción de **"Choose Device"**  y elegimos la opción de Raspberry Pi 5.
2. Seleccionamos la opción de **"Choose OS"** y elegimos la opción de Raspberry Pi OS. (Raspberry Pi OS [Con interfaz gráfica] o Raspberry Pi OS Lite [Sin interfaz gráfica]) en este caso seleccionaremos la versión con interfaz gráfica.
    - En el caso de tener una raspberry pi 5 de 8GB, se recomienda instalar la versión de 64 bits.
    - En el caso de tener una raspberry pi 5 de 4GB, se recomienda instalar la versión de 32 bits.
3. Seleccionamos la opción de **"Choose Storage"** y elegimos la tarjeta microSD que vamos a utilizar.
4. Antes de finalizar la instalar, editaremos los ajustes predeterminados del sistema operativo.

<img src="/img/personalizarOS-general.png" alt="Texto alternativo" width="49%" />
<img src="/img/personalizarSO-servicios.png" alt="Texto alternativo" width="49%" />

5. Finalmente, guardamos la configuración, aplicamos los ajustes y comenzamos la instalación.
</details>

<details>
<summary>Acceder a la Raspberry Pi</summary>
<br>
Tras conectar la Raspberry Pi a la corriente y a la red mediante un cable ethernet, accederemos a la Raspberry Pi mediante SSH.

1. Para ello, abriremos una terminal y ejecutaremos el siguiente comando para optener la dirección IP de la Raspberry Pi.
```bash
ping -4 raspberrypi.local
```
2. Una vez obtenida la dirección IP, accederemos mediante **SSH** con el siguiente comando.
```bash
ssh usuario@ipRaspberry
# Confirmamos la conexión con "yes" y escribimos la contraseña que hemos configurado en la instalación.
```
</details>
<details>
<summary>Configurar parámetros de la Raspberry Pi</summary>
<br>

- Para abrir la configuración de la Raspberry Pi, ejecutaremos el siguiente comando.
```bash
sudo raspi-config
```
 Y aplicaremos los siguientes ajustes:
```bash
1. APARTADO [6 Advanced Options] > [A1 Expand Filesystem] > FINISH
2. APARTADO [1 System Options] > [S5 Boot / Auto Login] > [B1 Desktop / CLI] > [B4 Desktop Autologin] > FINISH
3. APARTADO [3 Interface Options] > [I2 VNC] > [YES] > FINISH
4. APARTADO [2 Display Options] > [D3 VNC resolution] > [1280x720] > FINISH
5. APARTADO [5 Localisation Options] > [L1 Locale] > [es_ES.UTF-8 UTF-8] > [es_ES.UTF-8] > [OK] > [es_ES.UTF-8] > [OK] > [es_ES.UTF-8] > [OK]
6. APARTADO [5 Localisation Options] > [L2 Timezone] > [Europe] > [Madrid] > FINISH
7. APARTADO [5 Keyboard] > ENTER
8. APARTADO [5 WLAN Country] > [ES Spain] > FINISH
------------------------------------------------------------------------------------------------------------------------------------------------
FINISH > REBOOT
```
```bash
ssh usuario@ipRaspberry # Iniciamos de nuevo sesión por SSH
```
</details>

Vamos a configurar una IP estática para la Raspberry Pi, para ello, ejecutaremos el siguiente comando.
```bash
sudo nmtui
```


<details>
<summary>Modificaremos la configuración de la conexión</summary>
<br>

Seleccionamos la opción de **"Edit a connection"** y seleccionamos la conexión de **"Wired connection 1"**.
- **Dirección IP:** *Puedes poner la que quieras, pero asegúrate de que no esté en uso y fuera del rango de direcciones IP asignadas por el router.*
- **Máscara de red:** *Pondremos la máscara "**/24**"*
- **Puerta de enlace:** *Pondremos la que se encuentra detrás de nuestro router.*
- **DNS:** *Pondremos la de Google "**8.8.8.8**" y "**8.8.4.4**"*

<img src="/img/ipManual.png" alt="Texto alternativo" width="100%" />

Finalmente, seleccionamos la opción de **"Save"** y **"Quit"**, y reiniciamos la Raspberry Pi para aplicar los cambios.
```bash
sudo reboot
ssh usuario@ipRaspberry # Iniciamos de nuevo sesión por SSH con la nueva ip estática
```
</details>

**Actualizamos** el sistema operativo con los siguientes comandos. (Se recomienda realizar este tipo de actualizaciones cada cierto tiempo)
```bash
sudo apt update
sudo apt full-upgrade
```
## Instalación de Servicios mediante Docker
Para instalar cualquier servicio en la Raspberry Pi 5, usaremos `docker`. Ya que es una herramienta que nos permite instalar servicios de forma rápida, sencilla y segura. [*documentación oficial*](https://docs.docker.com/engine/install/debian/)
### Instalación de Docker
Pen primer lugar instalaremos docker y docker-compose en la Raspberry Pi 5.
```bash
sudo curl -fsSL https://get.docker.com/ -o get-docker.sh
sudo sh get-docker.sh
```
Añadir nuestro usuario al grupo Docker y reiniciar la Raspberry Pi para aplicar los cambios.
```bash
sudo usermod -aG docker ${USER}
sudo reboot
```
*Ejecutar un contenedor de prueba:*

`docker run hello-world`   -- Creamos un contenedor de prueba para comprobar que docker está instalado correctamente.

`docker ps -a` -- Listamos los contenedores que tenemos en ejecución y comprobamos que el contenedor de prueba se ha ejecutado correctamente.

<details>
<summary style="font-size: 1.3em;">Instalar Portainer para gestionar Docker mediante una interfaz gráfica.</summary>
<br>
Crear volumen Docker que contendrá los datos gestionados por el servidor Portainer.

```bash
docker volume create portainer_data
```
Descargar e instalar contenedor Portainer.
```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
Ver contenedores instalados: `docker ps`

Finalmente, para acceder a Portainer, abriremos el navegador y accederemos mediante la siguiente URL: `https://[IP de tu Raspberry Pi]:9443`
</details>

## Servicios PI5
> [!Services]
> - Instalar Pi-Hole (Servidor DNS) [🔗](https://youtu.be/hXs9Cmzg1bY?si=Ny3Gx1x02Oh1uB3a&t=204)
> - Instalar WireGuard (VPN) [🔗](https://youtu.be/hXs9Cmzg1bY?si=Ny3Gx1x02Oh1uB3a&t=204)
> - Instalar DuckDNS (DNS Dinámico) [🔗](https://youtu.be/hXs9Cmzg1bY?si=JswBKuOG0TYUQhYc&t=635)


