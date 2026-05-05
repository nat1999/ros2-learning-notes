# 🤖 Creación de paquetes en Ros2

### 1. Compilación de paquetes 
Para la compilación de paquetes se utiliza la instrucción **colcon build** y **colcon build --symlink-install**. La instrucción colcon admite dos opciones de construcción de paquetes: ament_cmake y ament_python. 
- ament_cmake: Se utiliza para construir paquetes escritos en c++.
- ament_python: Se utiliza para construir paquetes escritos en Python.

### 2. Diferencia entre colcon build y colcon build --symlink instal
Ambas instrucciones se encargan de compilar paquetes. 
- colcon build: Comparte los archivos compilados a la carpeta install y esto ocasiona que se ocupe espacio adicional en el disco. 
- colcon build --symlink-install: Utiliza enlaces símbolicos(contiene la ruta y ubicación del archivo) para compartir los archivos compilados en las carpetas install y build, lo que ahorra espacio en el disco.
