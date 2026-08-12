Volver al [principio](../README.md)


**RELEASE 0.8.8**
- Restaurar la secuencia correcta de conexión Wi-Fi, Bluetooth y MQTT.
- Mantener Bluetooth activo mientras no exista conexión Wi-Fi.
- Iniciar MQTT únicamente después de establecer la conexión de red.
- Mantener operativa la lectura RS-485 durante los reintentos de conexión.
- Retirar las versiones 0.8.6 y 0.8.7 debido a sus errores en la secuencia de conexión.
- Establecer la versión 0.8.8 como firmware recomendado para instalación y actualización.
- Se borra la versión 0.8.7 y 0.8.6
- Se vuelve a dar soporte a A1


**RELEASE 0.8.7 MED**
Migrar BTesp32 de Bluedroid a NimBLE  
- Sustituir la pila Bluedroid por NimBLE-Arduino.
- Mantener los UUID y el protocolo BLE existentes.
- Conservar la autenticación y el manejador de comandos.
- Anunciar el nombre configurado y el UUID del servicio.
- Iniciar explícitamente el servidor GATT y el advertising.
- Detener BLE cuando el firmware confirma la conexión Wi-Fi.
- Reducir significativamente el uso de flash en ESP32 clásico.


**RELEASE 0.8.6 MED**
No abierta al público
- 20 tests reales que verifican comportamiento observable del código
- Validaciones de host, puerto, URL de provision, credenciales y NVS
- Tests de JSON parsing con ArduinoJson 7.x
- Tests de operaciones FakeNVS (guardado y recuperación de valores)
- 100% de tests passing
- 45 fallos documentados en 4 categorías de prioridad
- 18 fallos corregidos (40% del total)
- Plan de acción definido por prioridades
- DD-001: Credenciales por defecto admin/admin para Bluetooth y Telnet
- Justificación técnica y mitigaciones de seguridad documentadas


**RELEASE 0.8.5 MED (RELEASE CANDIDATE 2)** 
- Mantener las nuevas imágenes OTA pendientes de validación durante 300 segundos
- Supervisar las tareas Modbus y publicación mediante watchdog de 30 segundos
- Confirmar el firmware cuando ambas tareas permanecen activas
- Ejecutar rollback si una tarea se bloquea o la firma no es válida
- Permitir la validación sin conexión WiFi o MQTT
- Continuar el arranque offline tras 10 segundos sin WiFi
- Calcular dinámicamente el tamaño real de la imagen para verificar su firma
- Hacer obligatorio el firmado en build.sh
- Eliminar el parámetro de compilación para generar firmware sin firmar



**RELEASE 0.8.4 MED**
- Se corrige la recuperación inicial de tiempoLecturas y tiempoEnvios desde los atributos compartidos de ThingsBoard.
- La petición de atributos utiliza ahora el formato sharedKeys esperado por ThingsBoard.
- Se añade la suscripción a v1/devices/me/attributes/response/+.
- Se comprueba el resultado de la publicación de la petición inicial.
- Se validan el tipo y los límites de tiempoLecturas y tiempoEnvios antes de aplicarlos.
- Los intervalos se almacenan como variables atómicas para compartirlos correctamente entre las tareas MQTT y Modbus.
- setSensor permite guardar latitude y longitude, conjuntamente o por separado.
- Se validan los rangos de latitud y longitud antes de escribirlos.
- Las coordenadas se guardan en NVS mediante LAT_n y LON_n.



**RELEASE 0.8.3 MED**
- Se añade una consola Telnet en el puerto 23 con autenticación, control de sesión y comandos JSON.
- El equipo permanece activo si falla el aprovisionamiento para permitir su recuperación mediante Telnet.
- Se añaden los comandos getNVS y setNVS para consultar y modificar valores NVS desde Telnet, Bluetooth y RPC.
- Se corrige la lectura de los parámetros pagina y variable en getNVS/setNVS.
- setURL elimina el token MQTT anterior para forzar un nuevo aprovisionamiento tras reiniciar.
- getData muestra el servidor y puerto MQTT utilizados realmente en la conexión.
- Se actualiza el tamaño del firmware firmado para la versión 0.8.3.
- Se amplía la documentación de la API con los nuevos comandos.
- Se incorpora la auditoría técnica de la versión 0.8.2.


**RELEASE 0.8.2**
- Se añade almacenamiento persistente de latitud y longitud para cada sensor.
- Las coordenadas se guardan en NVS mediante las claves LAT_<id> y LON_<id>.
- getSensor devuelve los campos latitude y longitude.
- deleteSensor elimina también las coordenadas guardadas.
- Al anunciar un sensor se solicitan sus atributos compartidos latitude y longitude a ThingsBoard.
- Se añade la suscripción a las respuestas de atributos de los dispositivos gateway.
- Las coordenadas recibidas desde ThingsBoard se actualizan en el sensor y se guardan en NVS.
- Se añade el comando deleteToken.
- deleteToken elimina únicamente el token MQTT y reinicia el equipo para volver a aprovisionarlo.
- La respuesta de deleteToken se envía antes de ejecutar el reinicio.
- Se centralizan los valores fallback de MQTT y aprovisionamiento en variables globales.
- Se añaden al fallback la clave y el secreto de aprovisionamiento.
- Los valores fallback pasan a utilizarse únicamente en RAM, sin sobrescribir automáticamente la configuración guardada en NVS.
- El aprovisionamiento utiliza el fallback completo cuando la configuración MQTT, la URL o las credenciales no son válidas.
- Después de 100 intentos fallidos de conexión MQTT ya no se elimina el token ni se reinicia el equipo.
- Tras 100 fallos se intenta obtener un token temporal mediante el servidor de aprovisionamiento fallback.
- El token fallback es efímero y no se guarda en NVS.
- La conexión al servidor MQTT fallback tampoco modifica la configuración persistente.
- Se cambia el mensaje de setWifi para indicar que el reinicio debe realizarse manualmente.
- Se documenta el uso de setURL con host, puerto, URL y credenciales de aprovisionamiento.
- Se deshabilita temporalmente setApagado y su declaración pública.
- Se deshabilitan los campos dinámicos C, P_prev y last_ms del sensor.
- Se deshabilita la variable usarCorreccionPF.
- Se comenta temporalmente la configuración de pines de la placa RELAYX2.
- Se comenta la declaración de setNombre en comandos.h.


**RELEASE 0.8.1**
Restaura la configuración de Serial2 de 8E1 a 8N1.
Permite enviar las credenciales de aprovisionamiento durante la configuración inicial.
La versión 0.8.0 no llega a publicarse por ser defectuosa.


**RELEASE 0.7.7**
- Sustituye el formato antiguo byte1/byte2 de setRAW por tipos u16, i16, u32, float y words.
- Añade escrituras Modbus 0x06 para una palabra y 0x10 para varias palabras.
- Permite escribir valores float de 32 bits, necesarios para el DDS665.
- Protege las operaciones RAW con el mutex compartido del bus RS485.
- Expone la instancia global node desde modbus.h.
- Configura el puerto RS485 del DDS6619/DDS665 como 9600 8E1.
- Añade trazas de éxito y error para diagnosticar las escrituras.
- Evita que el wrapper RPC sobrescriba el resultado real de setRAW.
- Añade la plantilla de lectura del DDS665 en medidores.h.
- Documenta en API_MEDIDORES los registros y ejemplos para DDS238/DDS238R y DDS665.
- Documenta el cambio de dirección del DDS665 usando el registro 0x0008 y un valor float.
- Corrige la documentación del cálculo del nuevo ID en los medidores Hiking.
- Verifica la compilación para la placa A2.


**RELEASE 0.7.5 MED (Release Candidate 1) **
- Evita que un sensor pueda quedar en modo prepago si su plantilla no define el campo R1.
- Cambia el valor por defecto de prepago a false.
- Al aplicar el tipo de medidor, fuerza y persiste prepago=false cuando no hay R1.
- Versión RC1


**RELEASE 0.7.4 MED**
- La anterior release funciona bien pero getData daba error.


**RELEASE 0.7.3 MED**
- Problemas con la gestion de la url de provisionamiento


**RELEASE 0.7.2 MED**
- Se añade URL de aprovisionamiento configurable en NVS mediante CONFIG/provisionUrl
- Si no existe CONFIG/provisionUrl, se usa la URL de aprovisionamiento por defecto
- Si CONFIG/provisionUrl no existe o está vacía, se guarda automáticamente la URL por defecto en NVS
- El comando setURL permite cambiar el servidor MQTT y opcionalmente la URL de aprovisionamiento
- Se mantiene compatibilidad con equipos antiguos que no tenían guardada la URL de aprovisionamiento en NVS


**RELEASE 0.7.1**
Versión de transición, no abierta al público


**RELEASE 0.7.0**
Versión de transición, no abierta al público


**RELEASE 0.6.7 NFC y MED**
- Se elimina el cambio de nombre de GW
- Se borra gran parte del código comentado para redes moviles y eth
- Se eliminan versiones 0.6.6 y 0.6.5


**RELEASE 0.6.6 NFC y MED**
- Solo se borra el token si es rechazado por el servicor
- Posibilidad de cambiar el nombre del GW
- Se borra gran parte del código comentado para redes moviles y eth
- Los codigos de apertura y reset se pueden escoger y guardar en NVS
- Al cambiar la wifi ahora resetea el esp32


**RELEASE 0.6.5 NFC y MED**
- Ahora solo borra el token si realmente es rechazado por el servidor.


**RELEASE 0.6.4 NFC y MED**
- Los led inicialmente pensados para TX y RX ahora se usan para  
  comprobar el estado de la RED y el cliente MQTT
- Se comenta gran parte del código para eth y gsm
- En siguiente versión se eliminará.
- Si no consigue conectar con el token actual a MQTT lo borra en 100 intentos


**RELEASE 0.6.3 NFC**
- Reparación versión 0.6.2. La anterior se elimina


**RELEASE 0.6.2**
- Se implementa borrado por teclado en proyecto NFC


**RELEASE 0.6.1**
- Se añade pushTarjeta como comando en NFC


**RELEASE 0.6.0**
- Se elimina el soporte de las versiones 0.4.*
- Se activa la posibilidad de apagar el medidor por medio del operador independiente de la programación
- Versión inicial del proyecto NFC, totalmente compatible con A2 y en verificación de PROTOA1
- Se añade el id del lector en cada lectura (NFC)


**RELEASE 0.5.1**
Atención, al actualizar a esta versión desde 0.4.7 o anterior, se pierde la conexion al servidor.
- Proto A2 Se activan led de envío y recepción
- Se añade el comando resetConfig para dejar de fábrica el Gateway


**RELEASE 0.5.0**
- Atención, al actualizar a esta versión desde otra anterior, se puede perder la conexion al servidor.
- El servidor TB ya no está incrustado en el código.


**RESEASE 0.4.7**
- Se activa W para la potencia en todos los medidores
- Se añade visualización correcta de Kwh en DDS6619
- Se reorganiza el código


**RELEASE 0.4.6**
- En el Hiking Tomzn DDS238 se elimina Wh porque no lo muestra bien


**RELEASE 0.4.5**
- Se añade compatibilidad con la placa PROTO A2
- Se añade la posibilidad de leer holding registers o input registers en los medidores
- Se añade compatibilidad con medidor DDS6619-39


**RELEASE 0.4.4**
- Al contratar nueva energía, se elimina el retardo en la reconexión
- Se añade el set y get prepago a los comandos
- Se añade el medidor DDS238 y DDS238R de forma separada
- Se añade prepago a las variables no volatiles
- Se modifica plantilla de DDS238 y DDS238R para que manden W/h totales. Antes mandaba Kw/h totales
- Ahora se puede apagar un medidor simplemente indicando que su potencia contratada es 0


**RELEASE 0.4.3**
- DeleteSensor "desanuncia" los sensores borrados
- Despues de un tiempo prudencial sin poder conectar con un sensor, este se pone en modo inactivo
- Se cambia la programación de BT clasico a BT BLE para poder ser ejecutado desde WEB
- Se crea primitiva de web para poder conectar y emparejar sensores.


**RELEASE 0.4.2**
- Se añade deleteSensor para poder borrar sensores en tiempo de ejecución
- Se modifica y se hace funcionar por fin el sistema de añadir sensores en tiempo real
- Se agregan las primitivas para poner un sensor en modo prepago o postpago


**RELEASE 0.4.1**
- Token, servidor, puerto los recoge de momento de la NVS
- Se crean las primitivas para el aprovisionamiento automático


**RELEASE 0.4.0**
- Funcionamiento del corte por curva
- Funcionamiento del corte por exceso de energía
- Se envía potencia contratada y energía contratada
- Reconexión programada
- Se elimina el sistema de cola y ahora envía el último estado del sensor
- Se añade el mapeo de rpc enviados a hijos hacia el gateway.


**RELEASE 0.3.6**
- Firmware versión 0.3.6 del cliente ESP32.
- Los atributos se leen directamente desde la plantilla sin depender del código.


**RELEASE 0.3.5**
- Nuevo sistema de plantillas para leer los valores de los medidores
- Ahora se lee un rango dinámico de registros


**RELEASE 0.3.4**
- La lectura y escribura de la NVS es ahora un singleton.


**RELEASE 0.3.3**
- Se añaden los datos de los registros de lectura de un medidor como variables para poder añadir mas modelos
- Si la firma no es válida, sólo bloquea modbus.
- Optimización tareas


**RELEASE 0.3.2**
- Versión no válida, se elimina del historial.

**RELEASE 0.3.1**
- Se almacena potencia contratada en la NVS
- Se almacena consumo contratado en la NVS
- Se crea nueva curva de disparo basada en media de consumo y deuda de consumo
- Se tiene en cuenta la energía reactiva para la deuda de consumo
- Se tiene en cuenta la energía contratada para el corte


**RELEASE 0.3.0**
- Cambios en el sistema de suscripcion para que se detecte que no hay conexion
- Se añade el nombre del ESP
- Se añade token a prefs
- Se divide el trabajo en 2 tareas principales que corren en nucleos distintos. Una tarea lee el bus y la otra tarea envía los datos al broker.
- Se añade conexion a ethernet, wifi y gsm


**RELEASE 0.2.3**
- Primitiva que calcula curva de disparo
- Se añade funcion setRAW para enviar comandos en bruto a un cliente
- Se eliminan funciones no usadas y se optimiza el código


**RELEASE 0.2.2**
- Primera versión Alpha de pruebas
- Versión firmada digitalmente.
- Primeras versiones de script para automatizar compilacion y firma.


**RELEASE 0.2.1**
- Cambios menores.
- Primitivas para funciones de firma


**RELEASE 0.2.0**
- Se añade modo debug para que muestre todo o nada por consola
- Se añaden iconos visuales al modo debug
- Se añade suscripción de atributos compartidos tanto de gateway como de dispositivos
- Se añade suscripción inicial para carga de valores iniciales
- Se cambia tiempo lecturas de NVS a atributo compartido


**RELEASE 0.1.6**
- Corrección lectura de variables


**RELEASE 0.1.5**
- Se añade variables para la velocidad del bus 485
- Se añade la posibilidad de cambiar el id de medidor y la velocidad (ojo, todos tienen que tener la misma)
- Se crea fichero de respuestas


**RELEASE 0.1.4**
- Se optimizan variables para ahorrar memoria
- Se desactivan RPC temporales para pasar a nueva version
- Se añade bucle para leer todos los dispositivos


**RELEASE 0.1.3**
- Se optimizan variables para ahorrar memoria
- Se añade RPC setConfig: Actualizar tiempo entre lecturas del bus
- Se añade primitiva de bucle para leer todos los dispositivos
- Se añade primitiva para enviar datos a TB


**RELEASE 0.1.2**
- Se optimizan variables para ahorrar memoria
- Se ha conseguido leer 485 simulando un sensor con un Arduino mega 2560
- Se añaden los RPC setSensor, getSentor, getLAN y nuevos valores para getData
- En cuanto se detecta conexion a TB se elimina la tarea btTask para ahorrar recursos
- Se añade variable para controlar el tiempo que ha pasado entre lecturas del Bus


**RELEASE 0.1.1**
- Se fusiona la tarea wifiTask y tbTask para ahorrar memoria
- Se optimizan variables para ahorrar memoria
- Se cambia diseño prototipo, ahora los pines para RS485 son 15, 16 y 4


**RELEASE 0.1.0**
- Se añade manual de Hiking Tomzn
- Se añade codigo para leer Hiking
- Se modifica estructura Sensor y se añade id y tipo


**RELEASE 0.0.12**
- Se cambian propiedades wifi. Al cabo de un tiempo se pierde la conexion
- Se hacen comprobaciones adicionales para comprobar la conexion con el servidor y poder reconectar.
- Se añade la función setSaldo para asignar los KWh de saldo
- Se cambia funcion addKWH por addSaldo
- Estudio completo para la viabilidad del cambio a Mogoose OS.


**RELEASE 0.0.11**
- Se quita el ahorro de energía para que la wifi no se quede parada.
- Se envían y reciben mensajes RPC.
- Se ajusta el tamaño de la pila para evitar cuelgues al arrancar y al ejecutar funciones
- Implantación del protocolo modbus


**RELEASE 0.0.10**
- Cambios de librerías


**RELEASE 0.0.9**
- Cambios de librerías


**RELEASE 0.0.8**
- Cambios de librerías


**RELEASE 0.0.7**
- Limpieza de código antiguo.
- Eliminación de tarea principal; ahora solo tareas concurrentes.
- Conexión exitosa a ThingsBoard.
- Configuración del cliente como gateway de dispositivos.
- Creación de estructura para almacenar 32 dispositivos ampliable a 250
- Anuncio de los dispositivos activos a ThingsBoard.


**RELEASE 0.0.6**
- Se añaden primitivas para el uso de mqtt
- Se organiza el código


**RELEASE 0.0.5**
- Se añade el comando reboot
- Se añade un botón a modo de prueba que al pulsarlo envía mensaje


**RELEASE 0.0.4**
- Soporte OTA (Over-The-Air update) correctamente.

Volver al [principio](../../README.md)
