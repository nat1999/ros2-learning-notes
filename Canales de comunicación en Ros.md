# 🦾Canales de comunicación entre nodos en ROS 2

Nodos

Definición:
Los nodos son programas que se ejecutan como procesos independientes dentro de un sistema robótico. Cada nodo se encarga de una tarea específica y se comunica con otros nodos para cumplir el comportamiento global del sistema.

Comunicación entre nodos
Tópicos (Topics)

Son canales de comunicación basados en el modelo publicador/suscriptor.
Un nodo puede publicar mensajes en un tópico, mientras otros nodos pueden suscribirse a ese mismo tópico para recibir la información.
Este método es ideal para intercambio continuo de datos.

Servicios (Services)

Son un mecanismo de comunicación basado en el modelo solicitud/respuesta.
Un nodo cliente envía una petición a otro nodo que ofrece el servicio, y este responde con un resultado.
Se utiliza cuando se requiere una respuesta puntual y síncrona.

Acciones (Actions)

Son similares a los servicios, pero están diseñadas para tareas de larga duración.
Permiten enviar una solicitud y recibir actualizaciones del progreso mientras la tarea se ejecuta.
A diferencia de los servicios, los nodos pueden continuar realizando otras tareas mientras esperan la finalización de la acción.
