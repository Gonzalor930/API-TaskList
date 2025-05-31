# API-TaskList
Esta es una API RESTful simple desarrollada con Java y Spring Boot que permite gestionar una lista de tareas (To-Do List). Es un proyecto diseñado para entender los fundamentos del desarrollo backend, incluyendo la creación de endpoints HTTP, el manejo de datos en memoria y la interacción con una API usando herramientas como Postman.  

Estructura del Objeto Task
El objeto Task (tarea) se define con las siguientes propiedades:
{
  "id": 1,          // Long: Identificador único de la tarea (generado por el backend para POST)
  "title": "Aprender Spring Boot", // String: Descripción de la tarea
  "completed": false // Boolean: Estado de la tarea (true si está completada, false si no)
}

🛠️ Tecnologías Utilizadas
Java 17+
Spring Boot
Maven
Postman


⚙️ Cómo Ejecutar el Proyecto (Paso a Paso)

1. Pre-requisitos
Asegurarse de tener instalado lo siguiente:

Java Development Kit (JDK) 17 o superior:
Puede verificar su versión abriendo una terminal y ejecutando: java -version
Apache Maven 3.x o superior:
Puede verificar tu versión abriendo una terminal y ejecutando: mvn -version
Un IDE (Entorno de Desarrollo Integrado):
IntelliJ IDEA Community Edition (recomendado para Spring Boot)
Eclipse IDE
VS Code con las extensiones de Java.
Postman (o Insomnia, cURL): Para interactuar con la API.

2. Clonar el Repositorio (o Descargar el Proyecto)

3. Importar el Proyecto en su IDE 
Abre IntelliJ IDEA.
Ve a File -> Open....
Navega hasta la carpeta raíz donde se encuentra el proyecto API-Tasklist (la carpeta que contiene el archivo pom.xml).
Selecciona la carpeta y haz clic en OK o Open. IntelliJ detectará automáticamente que es un proyecto Maven y descargará las dependencias necesarias. Esto puede tardar unos minutos la primera vez.
4. Configurar el JDK en IntelliJ (Si tienes problemas)
Si al intentar ejecutar la aplicación recibes un error como Cannot run program "..." CreateProcess error=2, El sistema no puede encontrar el archivo especificado, es probable que IntelliJ no esté apuntando a tu JDK correctamente.

En IntelliJ, ve a File -> Project Structure... (o Ctrl+Alt+Shift+S).
En el panel izquierdo, selecciona SDKs (bajo Platform Settings).
Verifica que tu JDK (Java 17 o superior) esté listado y que la ruta sea correcta. Si no lo está o es incorrecta, elimínala (-) y agrégala de nuevo (+ -> Add JDK...) navegando a la carpeta raíz de tu instalación de JDK (ej. C:\Program Files\Java\jdk-17).
Luego, ve a la sección Project (bajo Project Settings).
En Project SDK, selecciona el JDK que acabas de configurar. Asegúrate de que Project language level también coincida (ej. 17).
Haz clic en Apply y OK.
En la barra de herramientas de Maven (panel derecho), haz clic en el icono de "Reload All Maven Projects" (dos flechas circulares).
5. Verificar la Estructura de Paquetes y Clases
Asegúrate de que tus archivos estén en las ubicaciones correctas y que la declaración de package sea la adecuada.

Tu estructura de código Java debe ser similar a esta:

src/main/java/
└── com/
    └── gonzalo/
        └── API_Tasklist/          <-- Tu paquete base
            ├── ApiTasklistApplication.java
            ├── model/             <-- Paquete para el modelo
            │   └── Task.java
            ├── service/           <-- Paquete para la lógica de negocio
            │   └── TaskService.java
            └── controllers/       <-- Paquete para los controladores REST
                └── TaskController.java

Haz clic en el icono "Play" y selecciona Run 'ApiTasklistApplication.main()'.

🧪 Cómo Probar la API con Postman

Abre Postman.
Crea una nueva solicitud (pestaña +).
Configura las solicitudes según los endpoints definidos:
a) Obtener Todas las Tareas (GET)
Método: GET
URL: http://localhost:8080/api/tasks
Send: Haz clic en Send.
Respuesta esperada: Un arreglo JSON con las tareas precargadas:
JSON

[
  {
    "id": 1,
    "title": "Aprender Spring Boot",
    "completed": false
  },
  {
    "id": 2,
    "title": "Crear la API de Tareas",
    "completed": false
  },
  {
    "id": 3,
    "title": "Conquistar el mundo backend",
    "completed": false
  }
]
b) Obtener una Tarea por ID (GET)
Método: GET
URL: http://localhost:8080/api/tasks/1 (cambia 1 por el ID que quieras)
Send: Haz clic en Send.
Respuesta esperada:
Si existe el ID: El objeto Task correspondiente (código de estado 200 OK).
Si no existe: Un código de estado 404 Not Found.
c) Crear una Nueva Tarea (POST)
Método: POST
URL: http://localhost:8080/api/tasks
Headers:
Content-Type: application/json
Body: Selecciona raw y luego JSON. Pega el siguiente JSON:
JSON

{
    "title": "Comprar pan",
    "completed": false
}
Send: Haz clic en Send.
Respuesta esperada: La tarea recién creada con un id asignado por el servidor (código de estado 201 Created).
JSON

{
  "id": 4,
  "title": "Comprar pan",
  "completed": false
}
d) Actualizar una Tarea Existente (PUT)
Método: PUT
URL: http://localhost:8080/api/tasks/4 (cambia 4 por el ID de la tarea a actualizar, ej. la que acabas de crear)
Headers:
Content-Type: application/json
Body: Selecciona raw y luego JSON. Pega el JSON con los datos actualizados:
JSON

{
    "id": 4,
    "title": "Comprar pan (Listo!)",
    "completed": true
}
Send: Haz clic en Send.
Respuesta esperada:
La tarea actualizada (código de estado 200 OK).
Si el ID no existe: Un código de estado 404 Not Found.
e) Eliminar una Tarea (DELETE)
Método: DELETE
URL: http://localhost:8080/api/tasks/4 (cambia 4 por el ID de la tarea a eliminar)
Send: Haz clic en Send.
Respuesta esperada:
Si la tarea se eliminó: Un código de estado 204 No Content.
Si el ID no existe: Un código de estado 404 Not Found.


⏭️ Próximos Pasos (para Futuras Mejoras)
Algunas mejoras futuras podrían incluir:

Persistencia de Datos: Conectar la API a una base de datos (ej. PostgreSQL) utilizando Spring Data JPA para que las tareas no se pierdan al reiniciar la aplicación.

Validación de Datos: Añadir validaciones a los objetos Task entrantes para asegurar que los datos cumplen con los requisitos (ej. el title no sea vacío).

Manejo de Errores Global: Implementar un mecanismo centralizado para manejar excepciones y devolver respuestas de error consistentes.

DTOs (Data Transfer Objects): Introducir DTOs para separar la estructura de los datos que se envían y reciben de la API del modelo de dominio interno.

Autenticación y Autorización: Proteger los endpoints para que solo usuarios autorizados puedan acceder o modificar tareas.

