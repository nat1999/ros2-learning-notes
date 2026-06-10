# 🤖 Condiciones para los la creación de nodos en Ros2 con tópicos

## Pasos para crear un nodo en Ros2
Se tiene el siguiente nodo en c++. El nombre del proyecto se llama test_node.cpp. 


```bash
#include <chrono>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

/* We do not recommend this style anymore, because composition of multiple
 * nodes in the same executable is not possible. Please see one of the subclass
 * examples for the "new" recommended styles. This example is only included
 * for completeness because it is similar to "classic" standalone ROS nodes. */

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  auto node = rclcpp::Node::make_shared("minimal_publisher");
  auto publisher = node->create_publisher<std_msgs::msg::String>("topic", 10);
  std_msgs::msg::String message;
  auto publish_count = 0;
  rclcpp::WallRate loop_rate(500ms);

  while (rclcpp::ok()) {
    message.data = "Hello, world! " + std::to_string(publish_count++);
    RCLCPP_INFO(node->get_logger(), "Publishing: '%s'", message.data.c_str());
    try {
      publisher->publish(message);
      rclcpp::spin_some(node);
    } catch (const rclcpp::exceptions::RCLError & e) {
      RCLCPP_ERROR(
        node->get_logger(),
        "unexpectedly failed with %s",
        e.what());
    }
    loop_rate.sleep();
  }
  rclcpp::shutdown();
  return 0;
}
```

Se verifica en el archivo package.xml, que las dependencias a utilizar sean las correctas. 


```bash
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>robot_study</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="automate@todo.todo">automate</maintainer>
  <license>TODO: License declaration</license>

  <buildtool_depend>ament_cmake</buildtool_depend>

  <depend>std_msgs</depend>
  <depend>rclcpp</depend>
  <depend>geometry_msgs</depend>

  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_lint_common</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

En el archivo anterior, es posible evidenciar que el proyecto depende de los tipos de mensajes std_msgs y geometry_msgs. 
Con el archivo CMakeLists.txt,  se utiliza para crear un ejecutable y establecer las dependencias para compilar el ejecutable. 


```bash
cmake_minimum_required(VERSION 3.8)
project(example_robot)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(rclcpp REQUIRED)
find_package(geometry_msgs REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

#ESTE ES EL CÓDIGO QUE SE AGREGA

#Agrega un ejecutable llamado node_publisher_cpp
add_executable(test_node src/test_node.cpp)
#Se establece las dependencias (rclcpp std_msgs)
ament_target_dependencies(test_node rclcpp std_msgs)

install(TARGETS
   #Indica la ruta en donde se construye el ejecutable
   #en este caso se guarda en la carpeta lib
   test_node
   DESTINATION lib/${PROJECT_NAME}
)

ament_package()
```

Luego, nos dirigimos al espacio de trabajo y realizamos la respectiva compilación de paquetes. 

```bash
colcon build --symlink-install 
```

Finalmente, se ejecuta el nodo. 

```bash
ros2 run robot_study test_node

>  [INFO] [1687459302.461055015] [minimal_publisher]: Publishing: 'Hello, world! 0'
[INFO] [1687459302.961166842] [minimal_publisher]: Publishing: 'Hello, world! 1'
[INFO] [1687459303.461144976] [minimal_publisher]: Publishing: 'Hello, world! 2'
[INFO] [1687459303.961146222] [minimal_publisher]: Publishing: 'Hello, world! 3'
[INFO] [1687459304.461168516] [minimal_publisher]: Publishing: 'Hello, world! 4'
[INFO] [1687459304.961161509] [minimal_publisher]: Publishing: 'Hello, world! 5'
[INFO] [1687459305.461181778] [minimal_publisher]: Publishing: 'Hello, world! 6'
[INFO] [1687459305.961165848] [minimal_publisher]: Publishing: 'Hello, world! 7'
[INFO] [1687459306.461144249] [minimal_publisher]: Publishing: 'Hello, world! 8'
```
