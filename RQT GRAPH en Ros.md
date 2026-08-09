# 🦿rqt_graph Ros2

rqt, es una herramienta que permite visualizar las conexiones y la comunicación entre los nodos(grafo de comunicación entre nodos) de un sistema robótico. Permite realizar operaciones como el llamar un servicio y el verificar los diferentes tópicos y nodos asociados.


# 🦾 Para instalar el rqt

### 1. Se actualiza la lista de paquetes disponibles.

```bash
sudo apt upgrade 
```

### 2. Se instala el paquete con la siguiente instrucción:

```bash
sudo apt install ros-<distro>-<package>
```

- <distro>: La distribución de Ros2 como por ejemplo: Fox y humble. 
- <package>: Es el nombre del paquete.

```bash
sudo apt install ros-humble-rqt
```

### Visualizador de nodos y tópicos
Se ejecuta el nodo turtlesim_node que se encuentra en el paquete turtlesim:

```bash
ros2 run turtlesim turtlesim_node
```
<img width="467" height="509" alt="image" src="https://github.com/user-attachments/assets/1494e630-34f4-49a0-a378-bb4c73cdbeb7" />

El nodo turtle_teleop_key que se encuentra ubicado en el paquete turtlesim. Este nodo, permite el movimiento y desplazamiento del robot en el entorno virtual. 
