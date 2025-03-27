# Reinforcement-Activity-2.2
## Valentina Ruiz, Tomas Barrios, Darek Aljuri, Rafael Salcedo
# Wiki del Proyecto IoT para Máquinas Expendedoras

## Resumen del Diseño
En este proyecto, diseñamos y validamos un componente de conectividad para nuestra aplicación IoT enfocada en máquinas expendedoras. Nuestro objetivo es mejorar la gestión y monitoreo de las máquinas mediante sensores que midan el peso del producto, la temperatura de las bebidas y las variaciones de voltaje. Estos datos permiten optimizar la reposición de productos, garantizar la calidad de las bebidas y prevenir daños por picos de energía.

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
Para lograr una correcta recolección de datos, los sensores están conectados a un **microcontrolador (MCU Board)**, que procesa la información y la envía al servidor. 

### Sensores Implementados y Funcionamiento
- **Sensor de Peso (simulado con potenciómetro):** Se encarga de medir el peso de los productos dentro de la máquina expendedora. La lectura del sensor se compara con valores anteriores para determinar si hubo consumo y garantizar que se realice la reposición adecuada.
- **Sensor de Voltaje (simulado con potenciómetro):** Detecta fluctuaciones en la corriente eléctrica. Si hay una caída o un pico de voltaje, el sistema lo registra y envía una alerta al servidor para que los técnicos puedan actuar a tiempo.
- **Sensor de Temperatura (DS18B20):** Controla la temperatura de las bebidas calientes, asegurando que se mantengan dentro de un rango adecuado antes de ser dispensadas. Si la temperatura no está en el umbral correcto, se puede generar una alerta para mantenimiento.

### Microcontrolador (MCU Board)
- El microcontrolador lee periódicamente los valores de los sensores.
- Procesa los datos para identificar patrones anómalos.
- Utiliza Wi-Fi para enviar la información al servidor central mediante MQTT.
- Puede recibir comandos desde el servidor en caso de ajustes necesarios.

## Comunicación con el Tablero de Control
Para una supervisión eficiente, el sistema incluye un **tablero de control** que muestra en tiempo real los datos de los sensores y envía alertas cuando sea necesario. 

### Uso de Sockets UDP
- Se emplea **UDP (User Datagram Protocol)** para la transmisión de datos al tablero de control debido a su baja latencia y eficiencia en entornos de red local.
- El microcontrolador envía paquetes de datos a una dirección IP específica en la red, donde el tablero de control está ejecutando un servicio que recibe y procesa la información.
- Como UDP no requiere confirmación de recepción, se implementa un mecanismo de actualización periódica para asegurar que la información se refresque constantemente.

## Proceso de Validación
### Uso de Cisco Packet Tracer
Para validar nuestra conectividad, seguimos estos pasos en Cisco Packet Tracer:

1. **Configuración de la Simulación:** Creación de un proyecto en Cisco Packet Tracer con los dispositivos IoT requeridos.
2. **Implementación del Diseño:** Conexión de los dispositivos según nuestro plan, asegurando que la configuración de red sea correcta.
3. **Pruebas de Conectividad:** Evaluación de la comunicación entre dispositivos mediante la simulación de transmisión de datos.

### Desafíos y Soluciones
- **Configuración de MQTT:** Inicialmente tuvimos dificultades en la configuración del broker MQTT dentro de Cisco Packet Tracer. Solucionamos esto verificando las conexiones y utilizando tópicos adecuados para la transmisión de datos.
- **Retrasos en la Transmisión de Datos:** Para evitar latencias, optimizamos los parámetros de los sensores y configuramos adecuadamente el tiempo de actualización de los datos.
- **Simulación de Sensores:** Dado que Cisco Packet Tracer no tiene sensores de peso y voltaje, usamos potenciómetros para representar sus valores en la simulación.

## Conclusión
Este proyecto demuestra la importancia del IoT en la optimización de máquinas expendedoras. A través de una red eficiente y protocolos adecuados, logramos implementar un sistema de monitoreo en tiempo real que mejora la gestión de inventario, asegura la calidad del producto y previene daños por fallas eléctricas. 

Nuestro enfoque en Wi-Fi y MQTT garantiza una comunicación estable y eficiente, mientras que la integración de UDP permite un monitoreo rápido desde el tablero de control. Con este sistema, buscamos mejorar la operatividad de las máquinas expendedoras y facilitar su mantenimiento preventivo.

