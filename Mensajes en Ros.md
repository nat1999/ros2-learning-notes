# Mensajes en Ros2
Los mensajes, son estructura de datos que son utilizados para el intercambio de datos e información entre nodos. Los mensajes son archivos que se encuentran definidos con la extensión .msg.

## Comandos relacionados con los mensajes:
- `<ros2 topic echo <topic_name>>:` Permite visualizar los mensajes publicados  en tiempo real.
- `<ros2 interface show <package>/<type>>:`Para examinar la estructura de un mensaje. Permite conocer los campos y tipos de datos que contiene. 

## Ejemplo:
​
```bash

ros2 interface show geometry_msgs/msg/Twist

>  Vector3  linear
	float64 x
	float64 y
	float64 z
   Vector3  angular
	float64 x
	float64 y
	float64 z
```
### Mensajes más utilizados 
- `<std_msgs/String>:` El mensaje se utiliza para transmitir información en forma de texto o cadena de texto. 
sensor_msgs/LaserScan: Representa los datos de escaneo láser. Contiene información sobre las mediciones de distancia y la intensidad de los puntos obtenidos por un escáner láser.
nav_msgs/Odometry: Contiene los datos de odometría, como la posición y la orientación de un robot en un entorno. Presenta la información sobre la posición (x, y, z) y la orientación (cuaternión) del robot.
sensor_msgs/Image: Se utiliza para representar imágenes. Contiene información sobre el ancho, alto, codificación de la imagen y los datos de píxeles.
geometry_msgs/Twist: Representa una velocidad lineal y angular en un sistema de coordenadas tridimensional. Se utiliza para controlar el movimiento de un robot. 
