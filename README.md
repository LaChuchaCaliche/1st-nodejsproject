# 1st-nodejsproject
Objetivos
Configurar un entorno de desarrollo Node.js.
Crear un servidor web utilizando Node.js y Express.
Implementar rutas y middlewares en Express.
Leer y escribir datos en el sistema de archivos utilizando el módulo fs.
Manejar errores y asegurar la API con middlewares.
Descripción del Proyecto
Crearás una API RESTful para gestionar una lista de tareas (To-Do List). Las tareas se almacenarán en un archivo JSON en el sistema de archivos.

Historias de Usuario
1. Como usuario, quiero poder crear una nueva tarea para agregarla a mi lista de tareas.
Ruta: POST /tasks
Cuerpo de la solicitud:
{
  "title": "Nombre de la tarea",
  "description": "Descripción de la tarea"
}
Respuesta:
{
  "message": "Tarea creada exitosamente",
  "task": {
    "id": 1,
    "title": "Nombre de la tarea",
    "description": "Descripción de la tarea"
  }
}
2. Como usuario, quiero poder ver todas mis tareas para revisarlas.
Ruta: GET /tasks
Respuesta:
[
  {
    "id": 1,
    "title": "Nombre de la tarea",
    "description": "Descripción de la tarea"
  },
  ...
]
3. Como usuario, quiero poder ver una tarea específica por su ID para conocer sus detalles.
Ruta: GET /tasks/:id
Respuesta:
{
  "id": 1,
  "title": "Nombre de la tarea",
  "description": "Descripción de la tarea"
}
4. Como usuario, quiero poder actualizar una tarea existente para modificar su información.
Ruta: PUT /tasks/:id
Cuerpo de la solicitud:
{
  "title": "Nuevo nombre de la tarea",
  "description": "Nueva descripción de la tarea"
}
Respuesta:
{
  "message": "Tarea actualizada exitosamente",
  "task": {
    "id": 1,
    "title": "Nuevo nombre de la tarea",
    "description": "Nueva descripción de la tarea"
  }
}
5. Como usuario, quiero poder eliminar una tarea para mantener mi lista organizada.
Ruta: DELETE /tasks/:id
Respuesta:
{
  "message": "Tarea eliminada exitosamente"
}
Requisitos del Proyecto
1. Configuración del Entorno
Descarga e instala Node.js desde nodejs.org. Recomendamos la versión LTS.
Verifica la instalación con los siguientes comandos:
node -v
npm -v
2. Inicialización del Proyecto
Inicia un nuevo proyecto Node.js:
mkdir nodejs-first-project
cd nodejs-first-project
npm init -y
3. Instalación de Dependencias
Instala Express:
npm install express
4. Creación de la API RESTful
Estructura del Proyecto
nodejs-first-project/
├── data/
│   └── tasks.json
├── src/
│   ├── routes/
│   │   └── tasks.js
│   ├── middlewares/
│   │   └── errorHandler.js
│   └── app.js
├── package.json
└── index.js
1. Crear el archivo tasks.json
Crea la carpeta data y el archivo tasks.json:
mkdir data
echo "[]" > data/tasks.json
2. Crear el Servidor con Express
Crea la carpeta src y el archivo app.js:
const express = require("express"); // Importamos Express
const tasksRoutes = require("./routes/tasks"); // Importamos las rutas de la API
const errorHandler = require("./middlewares/errorHandler"); // Importamos el middleware para manejo de errores

const app = express(); // Instanciamos Express
const PORT = 3000; // Puerto del servidor en donde se ejecutará la API

app.use(express.json()); // Middleware para parsear el cuerpo de las solicitudes en formato JSON. Tambien conocido como middleware de aplicación.
app.use("/tasks", tasksRoutes); // Middleware para manejar las rutas de la API. Tambien conocido como middleware de montaje o de enrutamiento.
app.use(errorHandler); // Middleware para manejar errores.

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}/`);
});
3. Crear las Rutas de la API
Crea la carpeta routes y el archivo tasks.js:
const express = require("express");
const fs = require("fs");
const path = require("path");

const router = express.Router();
const tasksFilePath = path.join(__dirname, "../../data/tasks.json");

// Leer tareas desde el archivo
const readTasks = () => {
  const tasksData = fs.readFileSync(tasksFilePath); // Leer el archivo. Este poderoso metodo nos permite leer archivos de manera sincrona.
  return JSON.parse(tasksData); // Retornar los datos en formato JSON.
};

// Escribir tareas en el archivo
const writeTasks = (tasks) => {
  fs.writeFileSync(tasksFilePath, JSON.stringify(tasks, null, 2)); // Escribir los datos en el archivo. Este poderoso metodo nos permite escribir archivos de manera sincrona.
};

// Crear una nueva tarea
router.post("/", (req, res) => {
  const tasks = readTasks();
  const newTask = {
    id: tasks.length + 1, // simulamos un id autoincrementable
    title: req.body.title, // obtenemos el titulo de la tarea desde el cuerpo de la solicitud
    description: req.body.description, // obtenemos la descripcion de la tarea desde el cuerpo de la solicitud
  };
  tasks.push(newTask);
  writeTasks(tasks);
  res.status(201).json({ message: "Tarea creada exitosamente", task: newTask });
});

// Obtener todas las tareas
router.get("/", (req, res) => {
  const tasks = readTasks();
  res.json(tasks);
});

// Obtener una tarea por ID
router.get("/:id", (req, res) => {
  const tasks = readTasks();
  const task = tasks.find((t) => t.id === parseInt(req.params.id));
  if (!task) {
    return res.status(404).json({ message: "Tarea no encontrada" });
  }
  res.json(task);
});

// Actualizar una tarea por ID
router.put("/:id", (req, res) => {
  const tasks = readTasks();
  const taskIndex = tasks.findIndex((t) => t.id === parseInt(req.params.id));
  if (taskIndex === -1) {
    return res.status(404).json({ message: "Tarea no encontrada" });
  }
  const updatedTask = {
    ...tasks[taskIndex],
    title: req.body.title,
    description: req.body.description,
  };
  tasks[taskIndex] = updatedTask;
  writeTasks(tasks);
  res.json({ message: "Tarea actualizada exitosamente", task: updatedTask });
});

// Eliminar una tarea por ID
router.delete("/:id", (req, res) => {
  const tasks = readTasks();
  const newTasks = tasks.filter((t) => t.id !== parseInt(req.params.id));
  if (tasks.length === newTasks.length) {
    return res.status(404).json({ message: "Tarea no encontrada" });
  }
  writeTasks(newTasks);
  res.json({ message: "Tarea eliminada exitosamente" });
});

module.exports = router;
4. Crear Middleware para Manejo de Errores
Crea la carpeta middlewares y el archivo errorHandler.js:
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ message: "Ocurrió un error en el servidor" });
};

module.exports = errorHandler;
5. Archivo de Entrada del Proyecto
Crea el archivo index.js en la raíz del proyecto:
require("./src/app");
5. Ejecución del Proyecto
Ejecuta el proyecto con el siguiente comando:

node index.js
Deberás ver un mensaje similar al siguiente:

Server running at http://localhost:3000/
Abre tu navegador y accede a http://localhost:3000/tasks para probar la API.

6. Probando la API (Ejemplo con POST)
Para probar nuestra API, podemos utilizar herramientas como Postman o Insomnia. Descarga e instala una de estas aplicaciones para realizar las siguientes pruebas.

Para este ejemplo, consideraremos que estamos utilizando Postman. Una vez descargado e instalado, sigue los pasos a continuación:

Abre Postman y encontrarás una interfaz similar a la siguiente:
Postman

Le daremos click al boton new para crear una colección de peticiones.

Se nos abrirá una venta donde elegiremos colección. En postman, las colecciones son grupos de peticiones que se pueden ejecutar juntas. Es mas que todo para organizar las peticiones que haremos a nuestra API y poder compartirlas con otros desarrolladores.

Postman

Le damos un nombre a nuestra colección, en este caso Node.js Kick-off Project. A este punto puedes indagar más sobre funcionalidades de postman como variables de entorno, autenticación, etc. Te dejaré un link a la documentación oficial de postman aquí. Y un video de youtube que explica como usar postman mas a profundidad aquí.
Postman

Postman

Ahora crearemos una petición para crear una tarea. Para ello, le daremos click al boton ... que se encuentra al lado de la colección que acabamos de crear y seleccionaremos Add request.
Postman

Se nos abrirá una ventana donde podremos configurar nuestra petición. Le daremos un nombre a nuestra petición, en este caso Create Task. En el campo Request URL colocaremos la dirección de nuestra API, en este caso http://localhost:3000/tasks. En el campo Request type seleccionaremos POST. En el campo Body seleccionaremos raw y en el tipo de dato seleccionaremos JSON y en el campo inferior colocaremos el siguiente JSON:
{
  "title": "Comprar leche",
  "description": "Ir al supermercado y comprar leche"
}
Postman

Postman

Ahora le daremos click al boton Send y veremos la respuesta de nuestra API.
Postman

A este punto, ya debes suponer que el archivo tasks.json creado en la carpeta data contiene la tarea que acabamos de crear.

Postman

Si no ves una respuesta similar a la que se muestra en la imagen, es posible que haya un error en tu código. Revisa el paso a paso y asegúrate de que todo esté configurado correctamente.

7. Probando la API (Resto de Verbos HTTP)
Como trabajo autonomo, prueba el resto de los verbos HTTP que se mencionan en las historias de usuario los cuales son:

GET /tasks
GET /tasks/:id
PUT /tasks/:id
DELETE /tasks/:id
8. Preguntas de Reflexión y trabajo investigativo
¿Qué es el filesystem (fs) en Node.js y para qué se utiliza?
¿Qué es un middleware en Express y cuál es su propósito?
¿Qué es un endpoint en una API RESTful y cuál es su función?
¿Qué son los verbos HTTP y cuáles son los más comunes?
¿Qué es JSON y por qué es utilizado en las API RESTful?
En lo que respecta al envio de datos a lo largo de los verbos http responde:
¿Qué es el body de una petición?
¿Qué es el body de una respuesta?
¿Qué es el query de una petición?
¿Qué es el params de una petición?
En lo que respecta al verbo POST responde:
¿Qué es un verbo POST y cuál es su propósito?
¿Cuándo se utiliza un verbo POST?
¿En qué se diferencia un verbo POST de los otros verbos HTTP como GET, PUT y DELETE?
¿Como se envian datos en un verbo POST?
En lo que respecta al verbo GET responde:
¿Qué es un verbo GET y cuál es su propósito?
¿Cuándo se utiliza un verbo GET?
¿En qué se diferencia un verbo GET de los otros verbos HTTP como POST, PUT y DELETE?
En lo que respecta al verbo PUT responde:
¿Qué es un verbo PUT y cuál es su propósito?
¿Cuándo se utiliza un verbo PUT?
¿En qué se diferencia un verbo PUT de los otros verbos HTTP como POST, GET y DELETE?
En lo que respecta al verbo DELETE responde:
¿Qué es un verbo DELETE y cuál es su propósito?
¿Cuándo se utiliza un verbo DELETE?
¿En qué se diferencia un verbo DELETE de los otros verbos HTTP como POST, GET y PUT?
¿Qué es un status code y cuáles son los más comunes?
¿Cuales son los status code mas comunes para el verbo POST?
¿Cuales son los status code mas comunes para el verbo GET?
¿Cuales son los status code mas comunes para el verbo PUT?
¿Cuales son los status code mas comunes para el verbo DELETE?
