Volver al [principio](../README.md)

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
