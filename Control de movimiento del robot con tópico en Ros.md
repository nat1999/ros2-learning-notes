# 🤖Movimiento del robot con tópicos

Para mover el robot es necesario poner cierta velocidad. En el eje x, la velocidad es lineal y en el eje z es angular. 

### 1. El robot se mueve con velocidad lineal sin ninguna restricción de parada.

```bash
//!NODO COMANDOS DE VELOCIDAD LINEAL ROBOT

//Librería estándar de c++
#include <iostream>
//Librerías para trabajar con medidas de tiempo
#include <chrono>
//Librería para desarrollar nodos en C++
#include "rclcpp/rclcpp.hpp"
//Librería que contiene el mensaje asociado
#include "geometry_msgs/msg/twist.hpp"

using namespace std::chrono_literals;
using namespace std;

//Se crea una clase con el nombre Velocity
//La clase Velocity hereda los atributos y métodos de la clase Node
class Velocity : public rclcpp::Node
{

public:
    
    Velocity()
    //Se inicializa la clase con el nombre "node_velocity"
    : Node("node_velocity")
    {
      //Se crea un nodo publicador 
      publisher = this->create_publisher<geometry_msgs::msg::Twist>("/turtle1/cmd_vel",10);
      //Se crea un temporizador con el método create_wall_timer
      timer = this->create_wall_timer(50ms,
      std::bind(&Velocity::velocitycommand, this));
    }

private:

//Función para establecer los mensajes que se van a publicar 
  void velocitycommand()
  {
    //Se crea un objeto tipo Twits
    auto vel = geometry_msgs::msg::Twist();

    //Velocidad lineal
    vel.linear.x = 0.3;
    //Velocidad angular
    vel.angular.z = 0.0;
    //Publica el mensaje 
    publisher->publish(vel);
  }

    //Declaración del temporizador y publicador
    rclcpp::TimerBase::SharedPtr timer;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher;
};

//Función principal
//Estos argumentos permiten el procesamiento de la línea de comandos 
int main(int argc, char *argv[])
{
    //Incializa el entorno de Ros2, configuración parámetros o comunicaciones e inicializar nodos
    rclcpp::init(argc, argv);
    //Gestionar la ejecución de los publicadores y los nodos 
    rclcpp::spin(std::make_shared<Velocity>());
    //Finaliza la ejecución del programa
    rclcpp::shutdown();
    return 0;
}

```

<p align="center">
<img width="490" height="528" alt="image" src="https://github.com/user-attachments/assets/accd808b-be88-45c6-8f73-507e9c0dad9e" />
</p>

### 2. El robot se mueve con velocidad lineal y se detiene al pasar 5 segundos.

```bash
//!ROBOT REALIZA MOVIMIENTO Y DESPUÉS DE 5 SEGUNDOS SE DETIENE 

//Se importan las librerías 
#include <chrono>
#include "rclcpp/rclcpp.hpp"
#include "geometry_msgs/msg/twist.hpp"

//Se crea una clase
class TurtleMovement : public rclcpp::Node
{
public:
//Constructor 
    TurtleMovement() : Node("turtle_movement"), timer_count_(0)
    {   //Nodo publicador
        publisher_ = this->create_publisher<geometry_msgs::msg::Twist>("/turtle1/cmd_vel", 10);
        //Temporizador
        timer_ = this->create_wall_timer(std::chrono::seconds(1), std::bind(&TurtleMovement::moveTurtle, this));
    }

private:
    void moveTurtle()
    {   
        //Contador 
        timer_count_++;
        
        //Publicar mensaje 
        auto vel = geometry_msgs::msg::Twist();
        vel.linear.x = 0.3;
        vel.angular.z = 0.0;
        publisher_->publish(vel);
        
        //Mostrar en pantalla
        RCLCPP_INFO(this->get_logger(), "Moving the turtle...");
         
        //Condición
        if (timer_count_ >= 5)
        {
            stopRobot();
        }
    }

    void stopRobot()
    {   
        //Publicación de mensaje 
        auto vel = geometry_msgs::msg::Twist();
        vel.linear.x = 0.0;
        vel.angular.z = 0.0;
        publisher_->publish(vel);
        
        //Para detener el temporizador 
        timer_->cancel();
        
        //Mostrar en pantalla
        RCLCPP_INFO(this->get_logger(), "Robot stopped.");
        
    }
 
    //Declaración de variables 
    rclcpp::TimerBase::SharedPtr timer_;
    rclcpp::TimerBase::SharedPtr timer_stop;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher_;
    int timer_count_;
};

//Función principal 
int main(int argc, char *argv[])
{  
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<TurtleMovement>());
    rclcpp::shutdown();
    return 0;
}
```

<p align="center">
<img width="491" height="519" alt="image" src="https://github.com/user-attachments/assets/81f675f6-23ab-4cc5-93c9-b88eb3521d89" />
</p>

### 3.El robot se mueve con velocidad lineal y se detiene al recorrer cierta distancia.

```bash
//!ROBOT REALIZA MOVIMIENTO Y DESPUÉS DE 5M SE DETIENE

//Importan librerías
#include <chrono>
#include "rclcpp/rclcpp.hpp"
#include "geometry_msgs/msg/twist.hpp"

//Se crea una clase
class Distance : public rclcpp::Node
{
    public:
                                                                     //Obtiene el tiempo actual del sistema                     
         Distance() : Node("node_distance"), distance_traveled(0.0),start_time(this->now())
         {
            //Nodo publicador
            publisher = this->create_publisher<geometry_msgs::msg::Twist>("/turtle1/cmd_vel",10);
            //Temporizador 
            timer = this->create_wall_timer(std::chrono::milliseconds(100),std::bind(&Distance::moveTurtle,this));
         }

    private:

         void moveTurtle()
         {
         
            //Publicación de mensaje 
            auto vel = geometry_msgs::msg::Twist();
            vel.linear.x = 0.3;
            vel.angular.z = 0.0;
            publisher->publish(vel);

            //Mostrar en pantalla
            RCLCPP_INFO(this->get_logger(), "Moving robot.. ");
         
            //Calcular el tiempo recorrido
            auto time_init = this->now();
            auto time_finality = time_init-start_time;
            //El tiempo transcurrido en segundos
            double time_seconds = time_finality.seconds();

            //La distancia
            distance_traveled = vel.linear.x*time_seconds;
            
            if (distance_traveled >= 5.0)
            {
                stoprobot();
            }
            
         }
            
        void stoprobot()
         {
            //Publicación de mensaje
            auto vel = geometry_msgs::msg::Twist();
            vel.linear.x = 0.0;
            vel.angular.z = 0.0;
            publisher->publish(vel);

            //Detener el temporizador 
            timer->cancel();

            //Mostrar en pantalla
            RCLCPP_INFO(this->get_logger(), "Robot stopped...");

         } 

    //Definir variables 
    rclcpp::TimerBase::SharedPtr timer;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher;
    double distance_traveled;
    rclcpp::Time start_time;

};

//Función principal
int main(int argc,char *argv[])
   {
    
    rclcpp::init(argc,argv);
    rclcpp::spin(std::make_shared<Distance>());
    rclcpp::shutdown();
    return 0;

   }
```

<p align="center">
<img width="487" height="499" alt="image" src="https://github.com/user-attachments/assets/3d388bb4-4f41-4753-a91b-0ca66957da48" />
</p>

### 4.El robot se mueve con velocidad angular sin ninguna restricción de parada.


```bash
//!NODO COMANDOS DE VELOCIDAD ANGULAR ROBOT

//Librería estándar de c++
#include <iostream>
//Librerías para trabajar con medidas de tiempo
#include <chrono>
//Librería para desarrollar nodos en C++
#include "rclcpp/rclcpp.hpp"
//Librería que contiene el mensaje asociado
#include "geometry_msgs/msg/twist.hpp"

using namespace std::chrono_literals;

//Se crea una clase con el nombre Velocity
//La clase Velocity hereda los atributos y métodos de la clase Node
class Velocity : public rclcpp::Node
{
public:
    //Se inicializa la clase con el nombre "node_velocity"
    Velocity() : Node("node_velocity")
    {
      //Se crea un nodo publicador 
      publisher = this->create_publisher<geometry_msgs::msg::Twist>("/turtle1/cmd_vel",10);
      //Se crea un temporizador con el método create_wall_timer
      timer = this->create_wall_timer(50ms,std::bind(&Velocity::velocitycommand, this));     
    }

private:

//Función para establecer los mensajes que se van a publicar 
  void velocitycommand()
  {
    //Se crea un objeto tipo Twits
    auto vel = geometry_msgs::msg::Twist();

    //Velocidad lineal
    vel.linear.x = 0.0;
    //Velocidad angular
    vel.angular.z = 0.2;
    //Publica el mensaje 
    publisher->publish(vel);
  }

    //Declaración del temporizador y publicador
    rclcpp::TimerBase::SharedPtr timer;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher;
};

//Función principal
//Estos argumentos permiten el procesamiento de la línea de comandos 
int main(int argc, char *argv[])
{
    //Incializa el entorno de Ros2, configuración parámetros o comunicaciones e inicializar nodos
    rclcpp::init(argc, argv);
    //Gestionar la ejecución de los publicadores y los nodos 
    rclcpp::spin(std::make_shared<Velocity>());
    //Finaliza la ejecución del programa
    rclcpp::shutdown();
    return 0;
}
```

<p align="center">
<img width="492" height="528" alt="image" src="https://github.com/user-attachments/assets/a65c2b88-da46-4df4-b17f-dc40a3744f6c" />
</p>
