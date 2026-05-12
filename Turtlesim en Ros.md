### 🐢 Turtlesim en Ros2

# Paquete Turtlesim
El paquete Turtlesim, es una herramienta que presenta una simulación gráfica en un entorno virtual, con el objetivo de poder simular el movimiento y el comportamiento del robot tortuga. 

Para instalar el paquete turtlesim se utiliza el siguiente comando:

```bash
sudo apt install ros-humble-turtlesim
```

Para analizar los paquetes relacionados al turtlesim se ejecuta el comando: 

```bash
ros2 pkg executables turtlesim
> turtlesim draw_square
> turtlesim mimic
> turtlesim turtle_teleop_key
> turtlesim turtlesim_node 
```

Para ejecutar nodos en Ros2

```bash
ros2 run [Paquete] [Nodo]
```

### Ejemplo

Para ejecutar el nodo turtlesim_node que se encuentra en el paquete turtlesim, se usa el siguiente comando:

```bash
ros2 run turtlesim turtlesim_node 
```
El nodo turtlesim_node muestra una ventana de simulación del robot tortuga.

<img width="407" height="431" alt="image" src="https://github.com/user-attachments/assets/68d04ae4-ff61-4850-9ba4-552346262e0b" />

Para controlar el movimiento del robot tortuga se ejecuta la instrucción: 

<img width="408" height="442" alt="image" src="https://github.com/user-attachments/assets/392ae704-a852-409c-8224-463c64d7025e" />

Para visualizar comandos de velocidad lineal y angular se utiliza la siguiente instrucción:

```bash
ros2 topic echo <topic_name>
```

El tópico asociado es /turtle1/cmd_vel

```bash
ros2 topic echo /turtle1/cmd_vel

linear:
  x: -2.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0
---
linear:
  x: 0.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: -2.0
---
linear:
  x: 0.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: -2.0
---
linear:
  x: -2.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0
---
```






