# 🐢 Turtlesim en Ros2

### Paquete Turtlesim
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

<p align="center">
  <img width="407" height="431" alt="image" src="https://github.com/user-attachments/assets/68d04ae4-ff61-4850-9ba4-552346262e0b" />
</p>


Para controlar el movimiento del robot tortuga se ejecuta la instrucción: 

```bash
ros2 run turtlesim turtle_teleop_key 
```

El nodo turtle_teleop_key, permite controlar el movimiento de la tortuga mediante el uso de las teclas del teclado.

<p align="center">
   <img width="408" height="442" alt="image" src="https://github.com/user-attachments/assets/392ae704-a852-409c-8224-463c64d7025e" />
</p>


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

<p align="center">
   <img width="403" height="433" alt="image" src="https://github.com/user-attachments/assets/4898217e-ce36-4995-a88d-4051c58c6640" />
</p>


Para conocer los **nodos** disponibles, se utiliza el siguiente comando:

```bash
ros2 node list
> /turtlesim
```

Para evidenciar los **tópicos** disponibles, se usa el comando:

```bash
ros2 topic list 
> /parameter_events
  /rosout
  /turtle1/cmd_vel
  /turtle1/color_sensor
  /turtle1/pose
```

Para obtener la lista de **servicios** activos, se utiliza la instrucción:

```bash
ros2 service list
> /clear
  /kill
  /reset
  /spawn
  /turtle1/set_pen
  /turtle1/teleport_absolute
  /turtle1/teleport_relative
  /turtlesim/describe_parameters
  /turtlesim/get_parameter_types
  /turtlesim/get_parameters
  /turtlesim/list_parameters
  /turtlesim/set_parameters
  /turtlesim/set_parameters_atomically
```

También es posible evidenciar la lista de **acciones** disponibles en el ecosistema:

```bash
ros2 action list 
> /turtle1/rotate_absolute
```

La forma de obtener información del tópico asociado, es de la siguiente  manera:

```bash
ros2 topic info <topic>
ros2 topic info /turtle1/cmd_vel 
> Type: geometry_msgs/msg/Twist
  Publisher count: 0
  Subscription count: 1
```

Para conocer información del nodo a trabajar, se utiliza el comando:


```bash
ros2 node info <node>
ros2 node info /turtlesim
> /turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:
```





