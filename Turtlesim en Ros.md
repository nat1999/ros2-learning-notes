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


```bash
ros2 run turtlesim turtle_teleop_key  
```

El nodo turtle_teleop_key, permite controlar el movimiento de la tortuga mediante el uso de las teclas del teclado.

