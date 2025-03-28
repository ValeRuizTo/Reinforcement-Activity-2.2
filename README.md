# Reinforcement-Activity-2.2
## Valentina Ruiz, Tomas Barrios, Darek Aljuri, Rafael Salcedo
# Wiki del Proyecto IoT para Máquinas Expendedoras

## Resumen del Diseño
En este proyecto, diseñamos y validamos un componente de conectividad para nuestra aplicación IoT enfocada en máquinas expendedoras. Nuestro objetivo es mejorar la gestión y monitoreo de las máquinas mediante sensores que midan el peso del producto, la temperatura de las bebidas y las variaciones de voltaje. Estos datos permiten optimizar la reposición de productos, garantizar la calidad de las bebidas y prevenir daños por picos de energía.

Además, implementamos un **tablero de control** que recibe datos en tiempo real desde los sensores a través de sockets UDP. Este tablero permite visualizar información clave sobre el estado de la máquina expendedora y genera alertas en caso de eventos críticos, facilitando la supervisión y el mantenimiento preventivo.

## Tipo de Red
Seleccionamos **Wi-Fi** como la red principal debido a su accesibilidad y compatibilidad con múltiples dispositivos IoT. Esta elección se basa en la existencia de una infraestructura de red estable en el entorno de las máquinas expendedoras, lo que permite la conexión directa de nuestros dispositivos al punto de acceso.

## Protocolos Utilizados
### MQTT (Message Queuing Telemetry Transport)
- Protocolo ligero y eficiente, ideal para la comunicación entre dispositivos IoT.
- Facilita la transmisión de datos en tiempo real con un consumo mínimo de ancho de banda.
- Se utilizará para el envío de datos desde los sensores al servidor central.

### HTTP
- Utilizado para la comunicación con la interfaz web.
- Permite la visualización remota de los datos recopilados por los sensores.

### UDP (User Datagram Protocol)
- Se implementará para la comunicación rápida y eficiente con el tablero de control.
- Ideal para la transmisión de datos en redes locales sin necesidad de establecer una conexión permanente.

## Sensores y Proceso de Sensado
Para lograr una correcta recolección de datos, los sensores están conectados a un **Single Board Computer (SBC Board)**, que procesa la información y la envía al servidor. 

### Razón por la que no se utilizó un Microcontrolador (MCU)
Inicialmente, consideramos el uso de un **MCU Board**, pero lo descartamos debido a limitaciones en la implementación del protocolo MQTT. Los microcontroladores, aunque eficientes para tareas específicas de sensado, requieren librerías y configuraciones adicionales para soportar MQTT, lo que complicaba la implementación en nuestro caso. En cambio, el **SBC Board** proporciona mayor capacidad de procesamiento y compatibilidad con herramientas necesarias para la comunicación IoT, incluyendo soporte nativo para MQTT.

### Sensores Implementados y Funcionamiento
- **Sensor de Peso (simulado con potenciómetro):** Se encarga de medir el peso de los productos dentro de la máquina expendedora. La lectura del sensor se compara con valores anteriores para determinar si hubo consumo y garantizar que se realice la reposición adecuada.
- **Sensor de Voltaje (simulado con potenciómetro):** Detecta fluctuaciones en la corriente eléctrica. Si hay una caída o un pico de voltaje, el sistema lo registra y envía una alerta al servidor para que los técnicos puedan actuar a tiempo.
- **Sensor de Temperatura (DS18B20):** Controla la temperatura de las bebidas calientes, asegurando que se mantengan dentro de un rango adecuado antes de ser dispensadas. Si la temperatura no está en el umbral correcto, se puede generar una alerta para mantenimiento.

### Single Board Computer (SBC Board)
- El SBC Board lee periódicamente los valores de los sensores.
- Procesa los datos para identificar patrones anómalos.
- Utiliza Wi-Fi para enviar la información al servidor central mediante MQTT.
- Puede recibir comandos desde el servidor en caso de ajustes necesarios.

## Comunicación con el Tablero de Control
Para una supervisión eficiente, el sistema incluye un **tablero de control** que muestra en tiempo real los datos de los sensores y envía alertas cuando sea necesario. 

### Uso de Sockets UDP
- Se emplea **UDP (User Datagram Protocol)** para la transmisión de datos al tablero de control debido a su baja latencia y eficiencia en entornos de red local.
- El SBC Board envía paquetes de datos a una dirección IP específica en la red, donde el tablero de control está ejecutando un servicio que recibe y procesa la información.
- Como UDP no requiere confirmación de recepción, se implementa un mecanismo de actualización periódica para asegurar que la información se refresque constantemente.

## Proceso de Validación
### Uso de Cisco Packet Tracer
Para validar nuestra conectividad, seguimos estos pasos en Cisco Packet Tracer:

1. **Configuración de la Simulación:** Creación de un proyecto en Cisco Packet Tracer con los dispositivos IoT requeridos.
2. **Implementación del Diseño:** Conexión de los dispositivos según nuestro plan, asegurando que la configuración de red sea correcta.
3. **Pruebas de Conectividad:** Evaluación de la comunicación entre dispositivos mediante la simulación de transmisión de datos.

### Descripción del Circuito en Cisco Packet Tracer
El siguiente diagrama representa la implementación de nuestra solución IoT en Cisco Packet Tracer:

![.](imagenesWiki/circuito.png)

**Componentes del Circuito:**
- **Servidor (Server-PT)**: Responsable del procesamiento y almacenamiento de los datos recibidos desde los sensores.
- **Home Gateway (SLC100)**: Punto de acceso Wi-Fi que conecta todos los dispositivos IoT con el servidor.
- **Tablet-PC**: Representa la interfaz de usuario para el monitoreo remoto de los datos.
- **SBC Board (Control0)**: Dispositivo que recibe datos de los sensores, los procesa y los envía al servidor mediante MQTT.
- **Sensores:**
  - **Sensor de Temperatura (IoT2)**: Mide la temperatura de las bebidas y envía datos al SBC Board.
  - **Potenciómetros (IoT0, IoT1)**: Simulan los valores de peso y voltaje debido a la falta de sensores específicos en Packet Tracer.
    
### Simulación en Cisco Packet Tracer y funcionamiento
A continuación, se presenta una captura de la simulación en Cisco Packet Tracer:

![.](imagenesWiki/mqtt.png)

####  Flujo de Datos en la Red IoT  

1. **Los sensores recogen datos**  
   - El **sensor de temperatura (IoT2)** mide la temperatura de la máquina expendedora.  
   - Los **potenciómetros (IoT0 e IoT1)** simulan sensores de peso y voltaje, registrando cambios en los productos disponibles y en la corriente eléctrica.  
   - Estos sensores están conectados a un **SBC Board (Control0)**, que actúa como controlador.  

2. **Transmisión de datos mediante MQTT**  
   - El SBC Board **publica** los datos de los sensores utilizando el **protocolo MQTT** a través de la **puerta de enlace Wi-Fi (Home Gateway - SLC100)**.  
   - La puerta de enlace envía estos datos al **servidor central (Server-PT)**, que actúa como el **broker MQTT**.  
   - El **broker MQTT** recibe los datos y los **distribuye** a los dispositivos suscriptores, como la **Tablet-PC**, que visualiza la información en tiempo real.  

3. **Interacción con la Tablet-PC**  
   - La **Tablet-PC (Tablet PC0)** está suscrita a los tópicos MQTT del servidor, por lo que **recibe actualizaciones** cuando los sensores detectan cambios.  
   - Si la temperatura de la máquina es demasiado baja o alta, o si hay fluctuaciones de voltaje peligrosas, la tablet **muestra alertas** para que los técnicos puedan intervenir.  

4. **Transmisión de eventos y control del sistema**  
   - Cuando el SBC Board detecta eventos críticos, como un cambio brusco en el voltaje, puede enviar una alerta utilizando **mensajes MQTT o paquetes TCP/UDP**.  
   - El servidor puede responder enviando comandos al SBC Board para **activar medidas correctivas**, como apagar el sistema o enviar una notificación de mantenimiento.  

### Formato de los Mensajes MQTT
La Tablet-PC muestra mensajes en formato JSON, que es el estándar en MQTT para el intercambio de datos. Los mensajes tienen la siguiente estructura:

          {
            "topic": "ControlIA0",
            "payload": "¡ALERTA! La variable A0 cambió su valor drásticamente de 0 a 1023"
          }

***Explicación del mensaje:***

- "topic" → Define la categoría o canal donde se publica el mensaje. En este caso, "ControlIA0", que representa un sensor o grupo de sensores.

- "payload" → Contiene la información transmitida. Aquí se reporta que la variable "A0" sufrió un cambio brusco en su valor
  
![.](imagenesWiki/mqtt2.jpg)

***Análisis de los Mensajes Recibidos***
- El sensor A0 pasó de 0 a 1023, lo que indica un cambio súbito en su medición.

- Luego, la variable A1 cambió de 0 a 534, lo que podría significar un ajuste en otro sensor.

- Finalmente, A0 cambió nuevamente de 1023 a 558, indicando otra variación significativa.
- 
### Protocolos Utilizados en la Simulación  

####  MQTT (Message Queuing Telemetry Transport)  
 **Función:** Permite la comunicación eficiente entre dispositivos IoT y el servidor.  

- **Publicadores:** Los sensores transmiten datos al servidor.  
- **Broker MQTT:** El servidor recibe y distribuye los datos.  
- **Suscriptores:** La tablet y otros dispositivos reciben actualizaciones.  

 **Ventajas:**  
- Consumo bajo de ancho de banda.  
- Eficiencia en la transmisión de datos en redes IoT.  
- Comunicación basada en eventos (solo se envían datos cuando hay cambios).  


####  TCP (Transmission Control Protocol)  
 **Función:** Se usa para la comunicación confiable entre el servidor y los dispositivos IoT.  

- **Se usa cuando es necesario asegurar que los datos lleguen correctamente.**  
- **Requiere una conexión establecida antes de la transmisión de datos.**  

 **Ventajas:**  
- Garantiza que los mensajes lleguen sin errores y en orden.  
- Es útil para la configuración de dispositivos y transmisión de comandos críticos.  

#### 🟣 UDP (User Datagram Protocol)  
 **Función:** Se usa para la comunicación rápida con el tablero de control.  

- **No establece una conexión permanente, sino que envía datos de manera inmediata.**  
- **El SBC Board transmite datos directamente a la dirección IP del servidor sin esperar confirmación.**  

 **Ventajas:**  
- Baja latencia y transmisión rápida.  
- Ideal para monitoreo en tiempo real.  



###  Resumen del Funcionamiento de la Red  

- **Sensores** → Recogen datos y los envían al SBC Board.  
- **SBC Board (Control0)** → Publica datos mediante MQTT a través del Home Gateway.  
- **Home Gateway (SLC100)** → Transmite los datos al servidor central.  
- **Servidor (Server-PT)** → Actúa como el broker MQTT y distribuye los datos.  
- **Tablet-PC** → Se suscribe a los datos y permite monitorear el sistema en tiempo real.  

Con esta arquitectura, logramos una red eficiente para la gestión y monitoreo de las máquinas expendedoras, asegurando un control óptimo y la prevención de fallos en el sistema. 


### Desafíos y Soluciones
- **Configuración de MQTT:** Inicialmente tuvimos dificultades en la configuración del broker MQTT dentro de Cisco Packet Tracer. Solucionamos esto verificando las conexiones y utilizando tópicos adecuados para la transmisión de datos.
- **Retrasos en la Transmisión de Datos:** Para evitar latencias, optimizamos los parámetros de los sensores y configuramos adecuadamente el tiempo de actualización de los datos.
- **Simulación de Sensores:** Dado que Cisco Packet Tracer no tiene sensores de peso y voltaje, usamos potenciómetros para representar sus valores en la simulación.

## Imágenes de la Simulación en Cisco Packet Tracer
A continuación, se presentan imágenes de la simulación realizada en Cisco Packet Tracer:

![Diagrama de Conexión de Dispositivos](ruta_de_la_imagen)

![Configuración del Broker MQTT](ruta_de_la_imagen)

![Prueba de Comunicación entre Sensores y Servidor](ruta_de_la_imagen)

## Conclusión
Este proyecto demuestra la importancia del IoT en la optimización de máquinas expendedoras. A través de una red eficiente y protocolos adecuados, logramos implementar un sistema de monitoreo en tiempo real que mejora la gestión de inventario, asegura la calidad del producto y previene daños por fallas eléctricas. 

Nuestro enfoque en Wi-Fi y MQTT garantiza una comunicación estable y eficiente, mientras que la integración de UDP permite un monitoreo rápido desde el tablero de control. Con este sistema, buscamos mejorar la operatividad de las máquinas expendedoras y facilitar su mantenimiento preventivo.


