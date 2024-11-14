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

[!TIP]
    - **Nombre de Host:** `raspberrypi`
    - **Usuario:** `pi`
    - **Contraseña:** `raspberry`
    - **Habilitar SSH:** `Activado`
    - **Habilitar VNC:** `Activado`
    - **Idioma:** `Español`
    - **Zona Horaria:** `Madrid`
    - **Teclado:** `Español`
    - **Wi-Fi:** `Nombre de la red Wi-Fi`
    - **Contraseña Wi-Fi:** `Contraseña de la red Wi-Fi`


</details>
