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

Después de compilar, se crean automáticamente varias carpetas:

```bash
ls
```

Salida esperada:

```bash
build  install  log  src
```

En conclusión, así serían los pasos a seguir:

```bash
mkdir -p ~/ros2_ws/src
~/ros2_ws/src$ cd ..
~/ros2_ws$ colcon build 
~/ros2_ws$ ls
> build install log src
```



