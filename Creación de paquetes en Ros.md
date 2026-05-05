# 🤖 Creación de paquetes en Ros2

### 1. Compilación de paquetes 
Para la compilación de paquetes se utiliza la instrucción **colcon build** y **colcon build --symlink-install**. La instrucción colcon admite dos opciones de construcción de paquetes: **ament_cmake** y **ament_python**. 
- `<ament_cmake>:` Se utiliza para construir paquetes escritos en c++.
- `<ament_python:>:` Se utiliza para construir paquetes escritos en Python.

### 2. Diferencia entre colcon build y colcon build --symlink instal
Ambas instrucciones se encargan de compilar paquetes. 
- `<colcon build>:` Comparte los archivos compilados a la carpeta install y esto ocasiona que se ocupe espacio adicional en el disco.
- `<colcon build --symlink-install>:` Utiliza enlaces símbolicos(contiene la ruta y ubicación del archivo) para compartir los archivos compilados en las carpetas install y build, lo que ahorra espacio en el disco.

### 3. Construcción de paquetes 

```bash
ros2 pkg create  <package_name> --build-type <build_type> <dependencies>
```

-  `<package_name>:` Es el nombre que se le asigna al paquete.
-  `<build_type>:`Es el tipo de construcción que se desea utilizar y se puede elegir dos opciones: ament_cmake y ament_python.
-  `<dependencies>:` Son las dependencias de un paquete. Las dependencias son mensajes, librerías y funciones. 

### 4. Ejemplo:

```bash
cd ~/ros2_ws/src$
~/ros2_ws/src$  ros2 pkg create robot_study --build-type ament_cmake --dependencies std_msgs rclcpp geometry_msgs
```

### 5. Visualización del paquete 

Para visualizar la creación del paquete, se realiza lo que se muestra a continuación:

```bash
~/robot_study$ ls
> CMakeLists.txt include package_xml src
```

Se compila el paquete creado con la siguiente instrucción:
```bash
~/ros2_ws$  colcon build
```

Finalmente, para que los nodos puedan correr sin ningún inconveniente desde la terminal de linux, es importante poner la siguiente instrucción:
```bash
source install/local_setup.bash
```
Este comando permite obtener el código fuente del área de trabajo. 

# 📖 Cómo se compone un paquete 

- `<CMakeLists.txt>:` El archivo se utiliza para configurar y compilar el paquete.

- `<package.xml>:`Es un archivo que contiene información sobre el paquete como el nombre del paquete, dependencias, versiones, descripciones y licencias. 

- `<src>:` Es el directorio que contiene el código fuente.
  
- `<include/<package_name>:` Es una carpeta utilizada cuando el paquete contiene librerías y módulos, que deben ser usados por otros paquetes.

- La estructura de la carpeta include:  Nombre del paquete **<package_name>** y los archivos encabezados del paquete **<header1.h**, **header2.h>**. Los encabezados hacen referencias a archivos como clases, funciones, variables y estructuras.

```bash
|-- include/
    |-- <package_name>/
            |-- header1.h
            |-- header2.h
            |-- .
```
