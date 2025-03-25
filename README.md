# Reinforcement-Activity-2.2
## Valentina Ruiz, Tomas Barrios, Darek Aljuri, Rafael Salcedo
## Resumen del Diseño
En este proyecto, diseñamos y validamos un componente de conectividad para nuestra aplicación IoT. Consideramos diversos tipos de redes y protocolos para garantizar una comunicación eficiente entre dispositivos.

### Tipo de Red
Seleccionamos **Wi-Fi** como la red principal debido a su accesibilidad y compatibilidad con múltiples dispositivos IoT. También exploramos **Ethernet** como una opción de conexión confiable para ciertos dispositivos fijos.

### Protocolos Utilizados
- **MQTT (Message Queuing Telemetry Transport)**: Protocolo ligero y eficiente para la comunicación entre dispositivos IoT, ideal para enviar y recibir datos de sensores en tiempo real.
- **HTTP**: Utilizado para la comunicación con la interfaz web, permitiendo la visualización remota de los datos.

## Proceso de Validación

### Uso de Cisco Packet Tracer
Para validar nuestra conectividad, seguimos estos pasos en **Cisco Packet Tracer**:
1. **Configuración de la Simulación**: Creación de un proyecto en Cisco Packet Tracer con los dispositivos IoT requeridos.
2. **Implementación del Diseño**: Conexión de los dispositivos según nuestro plan, asegurando que la configuración de red sea correcta.
3. **Pruebas de Conectividad**: Evaluación de la comunicación entre dispositivos mediante la simulación de transmisión de datos.

### Desafíos y Soluciones
- **Configuración de MQTT**: Encontramos dificultades en la configuración del protocolo en Cisco Packet Tracer. Lo resolvimos asegurando que los dispositivos estuvieran correctamente conectados al **broker MQTT** y que se usaran los tópicos adecuados.
- **Retrasos en la Transmisión de Datos**: Optimizamos los parámetros de los sensores para garantizar actualizaciones en tiempo real sin sobrecargar la red.
