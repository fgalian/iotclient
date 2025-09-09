RELEASE 0.2.2
- Primera versión Alpha de pruebas
- Versión firmada digitalmente.
- Primeras versiones de script para automatizar compilacion y firma.


RELEASE 0.2.1
- Cambios menores.
- Primitivas para funciones de firma


Release 0.2.0
- Se añade modo debug para que muestre todo o nada por consola
- Se añaden iconos visuales al modo debug
- Se añade suscripción de atributos compartidos tanto de gateway como de dispositivos
- Se añade suscripción inicial para carga de valores iniciales
- Se cambia tiempo lecturas de NVS a atributo compartido


Release 0.1.6
- Corrección lectura de variables


Release 0.1.5
- Se añade variables para la velocidad del bus 485
- Se añade la posibilidad de cambiar el id de medidor y la velocidad (ojo, todos tienen que tener la misma)
- Se crea fichero de respuestas


Release 0.1.4
- Se optimizan variables para ahorrar memoria
- Se desactivan RPC temporales para pasar a nueva version
- Se añade bucle para leer todos los dispositivos


Release 0.1.3
- Se optimizan variables para ahorrar memoria
- Se añade RPC setConfig: Actualizar tiempo entre lecturas del bus
- Se añade primitiva de bucle para leer todos los dispositivos
- Se añade primitiva para enviar datos a TB


Release 0.1.2
- Se optimizan variables para ahorrar memoria
- Se ha conseguido leer 485 simulando un sensor con un Arduino mega 2560
- Se añaden los RPC setSensor, getSentor, getLAN y nuevos valores para getData
- En cuanto se detecta conexion a TB se elimina la tarea btTask para ahorrar recursos
- Se añade variable para controlar el tiempo que ha pasado entre lecturas del Bus


Release 0.1.1
- Se fusiona la tarea wifiTask y tbTask para ahorrar memoria
- Se optimizan variables para ahorrar memoria
- Se cambia diseño prototipo, ahora los pines para RS485 son 15, 16 y 4


Release 0.1.0
- Se añade manual de Hiking Tomzn
- Se añade codigo para leer Hiking
- Se modifica estructura Sensor y se añade id y tipo


Release 0.0.12
- Se cambian propiedades wifi. Al cabo de un tiempo se pierde la conexion
- Se hacen comprobaciones adicionales para comprobar la conexion con el servidor y poder reconectar.
- Se añade la función setSaldo para asignar los KWh de saldo
- Se cambia funcion addKWH por addSaldo
- Estudio completo para la viabilidad del cambio a Mogoose OS.


Release 0.0.11
- Se quita el ahorro de energía para que la wifi no se quede parada.
- Se envían y reciben mensajes RPC.
- Se ajusta el tamaño de la pila para evitar cuelgues al arrancar y al ejecutar funciones
- Implantación del protocolo modbus


Release 0.0.10
- Cambios de librerías


Release 0.0.9
- Cambios de librerías


Release 0.0.8
- Cambios de librerías


Release 0.0.7
- Limpieza de código antiguo.
- Eliminación de tarea principal; ahora solo tareas concurrentes.
- Conexión exitosa a ThingsBoard.
- Configuración del cliente como gateway de dispositivos.
- Creación de estructura para almacenar 32 dispositivos ampliable a 250
- Anuncio de los dispositivos activos a ThingsBoard.


Release 0.0.6
- Se añaden primitivas para el uso de mqtt
- Se organiza el código


Release 0.0.5
- Se añade el comando reboot
- Se añade un botón a modo de prueba que al pulsarlo envía mensaje


Release 0.0.4
- Soporte OTA (Over-The-Air update) correctamente.
