# Cliente de Gestión y Monitoreo IoT

## 📄 Descripción
Este proyecto implementa el firmware del cliente para acceder a la plataforma comercial de recolección, procesamiento y visualización de datos de dispositivos IoT.
El firmware se distribuye al cliente final, quien se conecta directamente a la plataforma para enviar y recibir datos en tiempo real desde sensores y equipos, aplicar reglas de procesamiento y visualizar la información en paneles interactivos, facilitando el análisis y la toma de decisiones.

## ✨ Características principales
- **Conexión segura de dispositivos** mediante protocolos estándar (MQTT, HTTP, CoAP).
- **Procesamiento de datos en tiempo real** con generación de alertas.
- **Visualización personalizada** mediante paneles y widgets configurables.
- **Automatización de eventos** a través de reglas y flujos lógicos.
- **Gestión centralizada** de dispositivos, usuarios y permisos.

## 🚀 Casos de uso
- Monitorización industrial y mantenimiento predictivo.
- Seguimiento de variables medioambientales.
- Gestión inteligente de edificios y ciudades.
- Control y seguimiento de flotas.
- Manejo y control de plantas y actividad industrial.
- Control y gestión de salud y seguridad doméstica.


# 🔄 Cómo actualizar nuestro dispositivo
El sistema ThinkSIoT permite mantener su dispositivo siempre al día mediante un mecanismo de **actualización de firmware remota (OTA, Over-The-Air)**.  
Este proceso garantiza que su equipo disponga de las **últimas mejoras, correcciones de seguridad y nuevas funcionalidades** sin necesidad de conectarlo físicamente al ordenador.

---

## 🧩 ¿En qué consiste una actualización?

Una actualización de firmware reemplaza el software interno del dispositivo (firmware) por una versión más reciente.  
Durante el proceso, el nuevo archivo se descarga directamente desde el servidor y se instala de forma segura en la memoria del ESP32.

Las actualizaciones pueden incluir:
- **Corrección de errores y mejoras de estabilidad.**
- **Nuevas funciones o compatibilidad con sensores adicionales.**
- **Optimizaciones de rendimiento y ahorro energético.**
- **Actualizaciones de seguridad y protocolos de comunicación.**

---

## ⚙️ Cómo realizar la actualización

La actualización se realiza desde el **Panel de Control de ThinkSIoT**, en el apartado de gestión de dispositivos.  
Dentro de la ficha del equipo encontrará la opción **“Actualizar Firmware”**, que permite ejecutar remotamente el proceso OTA.

Para iniciar la actualización manualmente, también puede enviarse un comando desde la consola o desde la propia plataforma con la siguiente sintaxis:

## HARDWARE A1
```
updateFirmware {"version":"https://github.com/fgalian/iotclient/raw/refs/heads/main/firmware/protoA1/FW-0.4.5.bin"}
```

## HARDWARE A2
```
updateFirmware {"version":"https://github.com/fgalian/iotclient/raw/refs/heads/main/firmware/protoA2/FW-0.4.5.bin"}
```

> 💡 **Nota:**  
> - El campo `version` debe contener la **URL directa** al archivo `.bin` del firmware que desea instalar.  
> - El dispositivo descargará el archivo, verificará su integridad y procederá automáticamente con la instalación.  
> - Durante el proceso, el dispositivo se **reiniciará** para aplicar los cambios.
> - Por motivos de seguridad, las versiones mas antiguas se irán retirando. En este caso se han retirado las versiones anteriores a la 0.3.0


## ✅ Recomendaciones antes de actualizar
- Asegúrese de que el dispositivo esté **conectado a la red Wi-Fi** y con buena señal.  
- No interrumpa la alimentación eléctrica durante el proceso.  
- Verifique que la versión que va a instalar sea **compatible con su modelo de dispositivo**.

Una vez completada la actualización, el dispositivo reiniciará automáticamente y se reconectará a la plataforma ThinkSIoT con la nueva versión activa.

## Versiones de firmware disponibles
Firmware [PROTO A1](firmware/RELEASES.md) para más detalles.
Firmware [PROTO A2](firmware/RELEASES.md) para más detalles.

---


## 🧩 Compatibilidad entre versiones de Firmware y Hardware

La siguiente tabla muestra la compatibilidad entre las versiones actuales de **firmware** y los modelos de **hardware** del sistema **ThinkSIoT**.

| Firmware ↓ / Hardware → | PROTO A1 | PROTO A2 |
|--------------------------|:---------:|:---------:|:---------:|
| **FW-0.4.4 y anteriores** | [✅](firmware/protoA1/) | ❌|
| **FW-0.4.5 ** | [✅](firmware/protoA1) | [✅](firmware/protoA2) |

---

### 🔎 Leyenda

| Símbolo | Descripción |
|:--------:|-------------|
| ✅ | **Totalmente compatible** — probado y estable. |
| ⚠️ | **Parcialmente compatible** — requiere ajustes, configuración adicional o perdida de algunas características. |
| ❌ | **No compatible** — no se recomienda su uso. |
| ⏳ | **No probado** — en pruebas y pendiente de verificación. |



💡 **Recomendación:**  
Utilice siempre la versión de firmware más reciente (actualmente **FW-0.4.5**) para garantizar el mejor rendimiento, compatibilidad y soporte técnico.


---

## Manual de instalación
En el siguiente [enlace](manuales/instalacion.md) podrá obtener la versión actualizada del manual de intalación del cliente y su sincronización con la plataforma


