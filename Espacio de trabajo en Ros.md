# 🤖 Creación de un espacio de trabajo en ROS 2

### 1. Cargar el entorno de ROS 2

Antes de trabajar, debes cargar el entorno de ROS 2 para que el sistema reconozca sus comandos y paquetes. Ejemplo (si usas Ubuntu y ROS 2 Humble):

```bash
source /opt/ros/humble/setup.bash
```

Si tienes otra distribución de ROS 2 como Iron o Jazzy, cambia humble por la que corresponda.

Para no hacerlo cada vez, puedes agregarlo al archivo ~/.bashrc:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### 2. Crear el espacio de trabajo

Se crea la carpeta del workspace y su estructura básica:

```bash
mkdir -p ~/ros2_ws/src
```

Luego, nos movemos a la carpeta principal del workspace:

```bash
cd ~/ros2_ws
```

### 3. Compilar los paquetes

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

Nota: Los paquetes siempre se compilan desde la raíz del espacio de trabajo (ros2_ws), no desde la carpeta src.


### 4. Cargar el workspace creado

Después de compilar, debes cargar el entorno del workspace:

```bash
source install/setup.bash
```
Este paso es muy importante, porque sin eso ROS 2 no reconoce los paquetes de tu workspace.


### 5. Instalar colcon (si no está disponible)

Si el comando colcon build no funciona, es necesario instalarlo:

```bash
sudo apt update
sudo apt install python3-colcon-common-extensions
```

