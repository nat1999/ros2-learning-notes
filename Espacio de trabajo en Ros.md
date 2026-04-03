# Creación de un espacio de trabajo en ROS 2

## 1. Crear el espacio de trabajo

1. Se crea la carpeta del workspace y su estructura básica:

```bash
mkdir -p ~/ros2_ws/src
```

Luego, nos movemos a la carpeta principal del workspace:

```bash
cd ~/ros2_ws
```

2. Compilar los paquetes

Para compilar los paquetes dentro del workspace, se utiliza el siguiente comando:

```bash
colcon build
```
