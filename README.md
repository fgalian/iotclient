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


## 🔄 Cómo actualizar su dispositivo
El sistema ThinksIoT permite mantener su dispositivo siempre al día mediante un mecanismo de **actualización de firmware remota (OTA, Over-The-Air)**.  
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

La actualización se realiza desde el **Panel de Control de ThinksIoT**, en el apartado de gestión de dispositivos.  
Dentro de la ficha del equipo encontrará la opción **“Actualizar Firmware”**, que permite ejecutar remotamente el proceso OTA.

Para iniciar la actualización manualmente, también puede enviarse un comando desde la consola o desde la propia plataforma con la siguiente sintaxis:

## HARDWARE PROTO A1
```
updateFirmware {"version":"https://github.com/fgalian/iotclient/raw/refs/heads/main/firmware/FW-PROTOA1-0.9.3.bin"}
```

## HARDWARE A2
```
updateFirmware {"version":"https://github.com/fgalian/iotclient/raw/refs/heads/main/firmware/FW-A2-0.9.3.bin"}
```

## HARDWARE A3
```
updateFirmware {"version":"https://github.com/fgalian/iotclient/raw/refs/heads/main/firmware/FW-A3-0.9.3.bin"}
```



> 💡 **Nota:**  
> - El campo `version` debe contener la **URL directa** al archivo `.bin` del firmware que desea instalar.  
> - El dispositivo descargará el archivo, verificará su integridad y procederá automáticamente con la instalación.  
> - Durante el proceso, el dispositivo se **reiniciará** para aplicar los cambios.
> - Las versiones más antiguas se irán retirando. En este caso se han retirado las versiones anteriores a la 0.8.19


## 🆕 Novedades de la versión 0.9.3

La versión **0.9.3** está disponible para los tres modelos de hardware (PROTO A1, A2 y A3) y sustituye a la 0.9.2 como versión recomendada. Incluye todas las mejoras de la 0.9.2 (identidad única del gateway, hostname WiFi y nombre Bluetooth unificado) y añade los siguientes cambios:

- **Coordenadas de los medidores como configuración local**: la latitud y la longitud de cada medidor se fijan en el propio gateway con el comando `setSensor` (campos `latitude` y `longitude`) y se guardan en su memoria NVS, igual que el nombre o la energía contratada. El equipo ya no solicita ni acepta estas coordenadas a través de los atributos compartidos de ThingsBoard.
- **Menos tráfico y memoria en MQTT**: al anunciar cada dispositivo hijo ya no se envía la petición `v1/gateway/attributes/request` (192 bytes menos por anuncio) y se eliminan las suscripciones a `v1/gateway/attributes` y `v1/gateway/attributes/response`, junto con el buffer de 512 bytes asociado en el callback de recepción.
- **`getData` más compacto**: la respuesta usa ahora las claves `fwOK` y `objetos` en lugar de `firmwareValido` y `objetosSensor`.
- **Diagnóstico del bus RS-485**: la explicación de la cesión del mutex del bus (`FALLOS_PARA_CEDER_BUS`) se refiere al número real de reintentos por lectura (`MAX_TRY`, definido en `Sensor.cpp`). Sin cambios de comportamiento.
- **API actualizada**: la documentación de la API se entrega como `API_0.9.3.txt`, sincronizada con el firmware.

> ⚠️ **Cambios incompatibles respecto a la 0.9.2**
> - `getData` ya no publica las claves `firmwareValido` ni `objetosSensor`; ahora publica `fwOK` y `objetos`. Deben actualizarse los paneles, scripts y reglas que lean las claves antiguas.
> - Las coordenadas de los dispositivos hijos ya no se toman de los atributos compartidos de ThingsBoard: hay que enviarlas con `setSensor` (`latitude`/`longitude`), que las persiste en el propio equipo.

## ✅ Recomendaciones antes de actualizar
- Asegúrese de que el dispositivo esté **conectado a la red Wi-Fi** y con buena señal.  
- No interrumpa la alimentación eléctrica durante el proceso.  
- Verifique que la versión que va a instalar sea **compatible con su modelo de dispositivo**.

Una vez completada la actualización, el dispositivo reiniciará automáticamente y se reconectará a la plataforma ThinksIoT con la nueva versión activa.

## Versiones de firmware disponibles
[Todo el firmware disponible](firmware/RELEASES.md) para más detalles.  

---


## 🧩 Compatibilidad entre versiones de Firmware y Hardware

La siguiente tabla muestra la compatibilidad entre las versiones actuales de **firmware** y los modelos de **hardware** del sistema **ThinksIoT**.

| Firmware ↓ / Hardware → | PROTO A1 | A2 | A3 |
|-------------------------|:--------:|:--:|:--:|
| **FW-0.4.4 y anteriores** | [✅](firmware/) | ❌ | ❌ |
| **FW-Ax-0.9.3** | [✅](firmware/FW-PROTOA1-0.9.3.bin) | [✅](firmware/FW-A2-0.9.3.bin) | [✅](firmware/FW-A3-0.9.3.bin) |
---

### 🔎 Leyenda

| Símbolo | Descripción |
|:--------:|-------------|
| ✅ | **Totalmente compatible** — probado y estable. |
| ⚠️ | **Parcialmente compatible** — requiere ajustes, configuración adicional o pérdida de algunas características. |
| ❌ | **No compatible** — no se recomienda su uso. |
| ⏳ | **No probado** — en pruebas y pendiente de verificación. |



💡 **Recomendación:**  
Utilice siempre la versión de firmware más reciente de su gama para garantizar el mejor rendimiento, compatibilidad y soporte técnico: **FW-0.9.3**.


---

## Manual de instalación
En el siguiente [enlace](manuales/instalacion.md) podrá obtener la versión actualizada del manual de instalación del cliente y su sincronización con la plataforma

