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

## Sensores y Simulación en Cisco Packet Tracer
Dado que Cisco Packet Tracer no cuenta con sensores específicos para peso y voltaje, utilizaremos **potenciómetros** para simular estos valores. También emplearemos el **sensor de temperatura DS18B20** para monitorear la temperatura de las bebidas.

### Sensores Implementados
- **Sensor de Peso (simulado con potenciómetro):** Permite determinar el consumo de productos y verificar la correcta reposición.
- **Sensor de Voltaje (simulado con potenciómetro):** Detecta cambios bruscos en el suministro eléctrico y registra eventos de picos de voltaje.
- **Sensor de Temperatura (DS18B20):** Garantiza que las bebidas calientes se sirvan a la temperatura adecuada.

## Proceso de Validación
### Uso de Cisco Packet Tracer
Para validar nuestra conectividad, seguimos estos pasos en Cisco Packet Tracer:

1. **Configuración de la Simulación:** Creación de un proyecto en Cisco Packet Tracer con los dispositivos IoT requeridos.
2. **Implementación del Diseño:** Conexión de los dispositivos según nuestro plan, asegurando que la configuración de red sea correcta.
3. **Pruebas de Conectividad:** Evaluación de la comunicación entre dispositivos mediante la simulación de transmisión de datos.

### Desafíos y Soluciones
- **Configuración de MQTT:** Inicialmente tuvimos dificultades en la configuración del broker MQTT dentro de Cisco Packet Tracer. Solucionamos esto verificando las conexiones y utilizando tópicos adecuados para la transmisión de datos.
- **Retrasos en la Transmisión de Datos:** Para evitar latencias, optimizamos los parámetros de los sensores y configuramos adecuadamente el tiempo de actualización de los datos.

## Video de Presentación
Preparamos un video de 5 minutos que muestra:
- **Explicación del Diseño:** Descripción de los sensores utilizados y su funcionalidad.
- **Demostración de Validación:** Conexión y pruebas de comunicación en Cisco Packet Tracer.
- **Conclusiones y Futuras Mejoras:** Posibles mejoras y aprendizajes obtenidos.

## Conclusión
Este proyecto demuestra la importancia del IoT en la optimización de máquinas expendedoras. A través de una red eficiente y protocolos adecuados, logramos implementar un sistema de monitoreo en tiempo real que mejora la gestión de inventario, asegura la calidad del producto y previene daños por fallas eléctricas. 

Nuestro enfoque en Wi-Fi y MQTT garantiza una comunicación estable y eficiente, mientras que la integración de UDP permite un monitoreo rápido desde el tablero de control. Con este sistema, buscamos mejorar la operatividad de las máquinas expendedoras y facilitar su mantenimiento preventivo.
```

