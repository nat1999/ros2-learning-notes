# 🤖 Instalación de Gazebo en ROS 2

Para instalar la integración de Gazebo con Ros2 Humble:

```bash
sudo apt install ros-humble-gazebo-ros-pkgs
```

Para verificar si la instalación fue correcta, ejecutar el siguiente comando. 

```bash
gazebo --version
```
Salida esperada: 

```bash
Gazebo multi-robot simulator, version 11.10.2
Copyright (C) 2012 Open Source Robotics Foundation.
Released under the Apache 2 License.
http://gazebosim.org
```
# 💻  Abrir el aplicativo de Gazebo

Abrir una terminal y poner el siguiente comando:

```bash
ros2 launch gazebo_ros gzserver.launch.py
```
Este comando inicia la parte interna de Gazebo, donde se cargan el robot, el entorno virtual, la física del simulador y las configuraciones necesarias para el funcionamiento de la simulación

Abrir una segunda terminal y colocar el comando:
```bash
gzclient
```
Este comando abre la interfaz gráfica de Gazebo, permitiendo visualizar e interactuar con la simulación.

# 🧑‍💻 Entorno de Gazebo 
<img width="1129" height="583" alt="image" src="https://github.com/user-attachments/assets/8a09e3ba-eecf-48d3-be1f-c8258083c420" />

