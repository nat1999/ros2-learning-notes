# 🤖 Condiciones para los la creación de nodos en Ros2 con tópicos

## Pasos para crear un nodo en Ros2

En ROS2, un nodo es un proceso encargado de ejecutar una tarea específica. Para que un nodo pueda intercambiar información con otros nodos, utiliza tópicos y tipos de mensajes. A continuación, se describe el procedimiento para crear y ejecutar un nodo publicador en C++.

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

## 1. Configuración de dependencias: 
El archivo package.xml contiene la información del paquete y las dependencias necesarias para su compilación y ejecución. En este ejemplo, el paquete denominado robot_study utiliza las bibliotecas:

- `rclcpp:` Proporciona las funciones necesarias para desarrollar nodos en C++.
- `std_msgs:` Contiene tipos de mensajes básicos.
- `geometry_msgs:` Incluye mensajes para representar información geométrica.

Por tanto, estas dependencias deben declararse dentro del archivo package.xml.

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

## 2. Configuración del archivo CMakeLists.txt

El archivo CMakeLists.txt define el proceso de compilación del paquete.

En primer lugar, se buscan las dependencias requeridas mediante las instrucciones:

- find_package(ament_cmake REQUIRED)
- find_package(rclcpp REQUIRED)
- find_package(std_msgs REQUIRED)
- find_package(geometry_msgs REQUIRED)

Posteriormente, se crea un ejecutable denominado **test_node**, asociado al archivo fuente **test_node.cpp**:


```bash
add_executable(test_node src/test_node.cpp)
```

Luego, se establecen las dependencias necesarias para la compilación del nodo:

```bash
ament_target_dependencies(test_node rclcpp std_msgs)**
```

Finalmente, se indica la ubicación donde será instalado el ejecutable:

```bash
install(TARGETS
   test_node
   DESTINATION lib/${PROJECT_NAME}
)
```

Ver archivo CMakeLists.txt: 

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

## 3. Compilación del paquete 
Una vez configurados los archivos del paquete, se debe acceder al espacio de trabajo y ejecutar:

```bash
colcon build --symlink-install 
```
Este comando compila todos los paquetes presentes en el workspace y genera los archivos ejecutables correspondientes.

## 4. Ejecución del nodo

Después de la compilación, el nodo se ejecuta mediante:

**ros2 run robot_study test_node**

donde:

- robot_study corresponde al nombre del paquete.
- test_node es el nombre del ejecutable generado.

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

# 🤖 Ejemplo de nodo publicador y nodo suscriptor 

## Nodo publicador

```bash
//! NODO PUBLICADOR

// Librerías para trabajar con medidas de tiempo
#include <chrono>
// Librería para desarrollar nodos en Ros2
#include "rclcpp/rclcpp.hpp"
// Librería donde se encuentra asociado el tipo de mensaje String
#include "std_msgs/msg/string.hpp"

//! Espacio de nombres: Es un mecanismos que agrupa variables, funciones y clases.

//  Es un espacio de nombres(std) dentro de la librería chrono_literals.
//  Si se tiene una funcion() dentro de un espacio de nombres,
//  se puede acceder a la funcion() escribiendo namespace::funcion()

using namespace std::chrono_literals;

//  Se define una clase llamada MinimalPublisher que heredara los atributos y métodos de la
//  clase rclcpp::Node
//  rclcpp es el espacio de nombres, Node es la clase dentro de ese espacio de nombres.

class MinimalPublisher : public rclcpp::Node
{
public:
  // Las funciones son accesibles fuera de la clase
  MinimalPublisher()
      // Se inicializa la clase con el nombre "minimal_publisher" y la variable count en cero(0)
      : Node("minimal_publisher"), count_(0)
  {
    // Crea el nodo publicador con el método //*create_publisher
    // Se tiene en cuenta el tipo de mensaje asociado String
    publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
    // Crea un temporizador con el método // *create_wall_timer
    timer_ = this->create_wall_timer(
        // Se llama la función timer_callback cada 500ms
        // sts::bind, se utiliza para enlazar la clase MinimalPublisher con la función timer_callback
        500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }

private:
  // Establece los datos del mensaje y los mensajes que se publican
  void timer_callback()
  {
    // Se crea un objeto del tipo String, es decir, que se reserva memoria para guardar datos
    auto message = std_msgs::msg::String();
    // Se construye la cadena de caracteres
    message.data = "Hello, world! " + std::to_string(count_++);
    // Se imprime en pantalla
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
    // Se publica el mensaje
    publisher_->publish(message);
  }
  // Declarar variables temporizador, publicador y contador
  rclcpp::TimerBase::SharedPtr timer_;
  rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
  size_t count_;
};

//Función principal
int main(int argc, char *argv[])
{
  // Incializa el entorno de Ros2
  rclcpp::init(argc, argv);
  // Gestiona la ejecución de suscriptores, publicadores y temporizadores en el nodo
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  // Finaliza la ejecución del programa
  rclcpp::shutdown();
  return 0;
}
```

## Nodo suscriptor

```bash
//! NODO SUSCRIPTOR

#include <memory>

// Librería para trabajar con medidas de tiempo
#include <chrono>
// Librería para trabajar con Ros2, permite desarrollar nodos en C++
#include "rclcpp/rclcpp.hpp"
// Librería que tiene asociado el tipo de mensaje String
#include "std_msgs/msg/string.hpp"

// Espacio de nombres dentro de la librería chrono_literals
using namespace std::chrono_literals;
// using std::placeholders::_1;

// Se define una clase Subscriber
// La clase Subscriber esta heredando los atributos y métodos de la clase Node
class Subscriber : public rclcpp::Node
{

public:
    // Las funciones son accesibles fuera de la clase
    // Se inicializa la clase con el nombre "subscriber_node"
    Subscriber(): Node("subscriber_node")
    { // Se crea el nodo suscriptor con el mensaje asociado que se publicará en el tópico
        // No hay temporizador, porque cada vez que se ejecuta el nodo suscriptor,
        // Este accede a la función topic_callback, en donde se encuentran los mensajes a publicar
        subscription = this->create_subscription<std_msgs::msg::String>(
            "topic", 10, std::bind(&Subscriber::topic_callback, this,  std::placeholders::_1));
    }

private:
    void topic_callback(const std_msgs::msg::String & msg)const
    {
        // Se crea un objeto del tipo String, es decir, que se reserva memoria para guardar datos
        auto message = msg;
        // Se imprime en pantalla
        RCLCPP_INFO(this->get_logger(), "I heard: '%s'", message.data.c_str());
    }
    // Declaración de la suscripción
    rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription;
};

//Función principal
int main(int argc, char *argv[])
{
    // Inicializa el entorno de ROs2
    rclcpp::init(argc, argv);

    // Gestiona la ejecución de suscriptores, publicadores y temporizadores en el nodo
    rclcpp::spin(std::make_shared<Subscriber>());
    // Finaliza la ejecución del programa
    rclcpp::shutdown();
}
```

## Ejecutar nodo publicador y nodo suscriptor.

## 1. Nodo publicador

```bash
ros2 run robot_study publisher 

> [INFO] [1688496185.989231499] [minimal_publisher]: Publishing: 'Hello, world! 0'
[INFO] [1688496186.489182372] [minimal_publisher]: Publishing: 'Hello, world! 1'
[INFO] [1688496186.989209774] [minimal_publisher]: Publishing: 'Hello, world! 2'
[INFO] [1688496187.489151294] [minimal_publisher]: Publishing: 'Hello, world! 3'
[INFO] [1688496187.989131579] [minimal_publisher]: Publishing: 'Hello, world! 4'
[INFO] [1688496188.489122373] [minimal_publisher]: Publishing: 'Hello, world! 5'
[INFO] [1688496188.989081592] [minimal_publisher]: Publishing: 'Hello, world! 6'
[INFO] [1688496189.489082208] [minimal_publisher]: Publishing: 'Hello, world! 7'
[INFO] [1688496189.989023864] [minimal_publisher]: Publishing: 'Hello, world! 8'
[INFO] [1688496190.489040028] [minimal_publisher]: Publishing: 'Hello, world! 9'
[INFO] [1688496190.989007960] [minimal_publisher]: Publishing: 'Hello, world! 10'
[INFO] [1688496191.488960461] [minimal_publisher]: Publishing: 'Hello, world! 11'
[INFO] [1688496191.988964365] [minimal_publisher]
```


## 2. Nodo suscriptor 

```bash
ros2 run robot_study subscriber 

>[INFO] [1688496190.489571526] [minimal_subscriber]: I heard: 'Hello, world! 9'
[INFO] [1688496190.989241433] [minimal_subscriber]: I heard: 'Hello, world! 10'
[INFO] [1688496191.489382910] [minimal_subscriber]: I heard: 'Hello, world! 11'
[INFO] [1688496191.989334586] [minimal_subscriber]: I heard: 'Hello, world! 12'
[INFO] [1688496192.489372118] [minimal_subscriber]: I heard: 'Hello, world! 13'
```
