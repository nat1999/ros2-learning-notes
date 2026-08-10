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

1. <distro>: La distribución de Ros2 como por ejemplo: Fox y humble. 
2. <package>: Es el nombre del paquete.

```bash
sudo apt install ros-humble-rqt
```

### Visualizador de nodos y tópicos
Se ejecuta el nodo turtlesim_node que se encuentra en el paquete turtlesim:

```bash
ros2 run turtlesim turtlesim_node
```

<p align="center">
<img width="467" height="509" alt="image" src="https://github.com/user-attachments/assets/1494e630-34f4-49a0-a378-bb4c73cdbeb7" />
</p>

El nodo turtle_teleop_key que se encuentra ubicado en el paquete turtlesim. Este nodo, permite el movimiento y desplazamiento del robot en el entorno virtual. 

### Acceso al rqt_graph
Se accede a la herramienta rqt con la siguiente instrucción:

```bash
rqt
```
Tenemos el entorno de rqt_graph:

<p align="center">
<img width="473" height="381" alt="image" src="https://github.com/user-attachments/assets/59c3d880-e622-4204-8e6f-00a3e7a3e84c" />
</p>

### Servicio spawn en rqt

<p align="center">
<img width="474" height="380" alt="image" src="https://github.com/user-attachments/assets/8c726fa9-400e-490f-845a-8dade954c48b" />
</p>

Es posible evidenciar parámetros. Estos permiten crear un nuevo robot tortuga llamado turtle2. Es posible cambiar las coordenadas X, Y y Theta. 

<p align="center">
<img width="474" height="377" alt="image" src="https://github.com/user-attachments/assets/c5b28303-f511-491e-8542-6e0bde12c38d" />
</p>
