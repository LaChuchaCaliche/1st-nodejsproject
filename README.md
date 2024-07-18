8. Preguntas de Reflexión y trabajo investigativo
¿Qué es el filesystem (fs) en Node.js y para qué se utiliza?
El filesystem es una función que trae por defecto el node.js que sirve para leer e interactuar con archivos del sistema 
¿Qué es un middleware en Express y cuál es su propósito?
Un middleware es una funcion programada en js que sirve como intermediario entre el usuario/cliente y el backend, sirve para revisar los endpoints y capturar los errores que podrian generar y mostrandolos en consola 
¿Qué es un endpoint en una API RESTful y cuál es su función?
La funcion del endpoint es brindarle al front end un punto de acceso a la información en el backend, por lo general el endpoint esta creado para enlazar con una base de datos especifica y le permite hacer las distintas solicitudes GET,PUT,POST,DELETE
¿Qué son los verbos HTTP y cuáles son los más comunes?
GET,PUT,POST,DELETE
son verbos para realizar peticiones atravez del endpoint a la api 
¿Qué es JSON y por qué es utilizado en las API RESTful?
El json es un formato usado para almacenar datos y se usa en las api por ser un formato de facil lectura
En lo que respecta al envio de datos a lo largo de los verbos http responde:
¿Qué es el body de una petición?
el body de la peticion es la forma del  objeto que trae la peticion post
¿Qué es el body de una respuesta?
el body de una respuesta es la forma en la que quiero recibir la peticion get
¿Qué es el query de una petición?
Es una forma de filtrar la información y se configura de acuerdo a la necesidad
¿Qué es el params de una petición?
los params son el conjunto de parametros que se añaden a la URL 

En lo que respecta al verbo POST responde:
¿Qué es un verbo POST y cuál es su propósito?
el verbo POST es un verbo de solicitud HTTP que me permite agregar información a la base de datos por medio de una petición 
¿Cuándo se utiliza un verbo POST?
cuando necesito agregar elementos nuevos
¿En qué se diferencia un verbo POST de los otros verbos HTTP como GET, PUT y DELETE?
los verbos get,put y delete solo se usan con elementos ya presentes en la base de datos
¿Como se envian datos en un verbo POST?
se envian a travez de la URL con parametros
En lo que respecta al verbo GET responde:
¿Qué es un verbo GET y cuál es su propósito?
El verbo get tiene como proposito obtener información de la base de datos 
¿Cuándo se utiliza un verbo GET?
el verbo get se utiliza cuando tengo un endpoint co nel criterio de busqueda que necesito 
¿En qué se diferencia un verbo GET de los otros verbos HTTP como POST, PUT y DELETE?
el verbo get solo me trae información no me permite modificar,publicar o borrar
En lo que respecta al verbo PUT responde:
¿Qué es un verbo PUT y cuál es su propósito?
el verbo put se usa para actualizar datos ya existentes dentro del api o la base de datos
¿Cuándo se utiliza un verbo PUT?
cuando tengo información preexistente que se necesita actualizar
¿En qué se diferencia un verbo PUT de los otros verbos HTTP como POST, GET y DELETE?
el verbo put solo envia información por medio de un identificador y actualiza, no añade o trae informacion
En lo que respecta al verbo DELETE responde:
¿Qué es un verbo DELETE y cuál es su propósito?
El verbo delete sirve para eliminar información por medio de un parametro identificador 
¿Cuándo se utiliza un verbo DELETE?
cuando necesito eliminar información de la base de datos
¿En qué se diferencia un verbo DELETE de los otros verbos HTTP como POST, GET y PUT?
solo sirve para eliminar 
¿Qué es un status code y cuáles son los más comunes?
los status codes son codigos que reportan el estado de las solicitudes del cliente / pagina web con la base de datos, son 5 en total, los 100 informan continuidad ,los 200 exitos, los 300 movimiento de la informacion y los 400 errores 
Códigos de estado comunes para el verbo POST:
200 OK: La solicitud fue exitosa.
201 Created: La solicitud fue exitosa y un nuevo recurso fue creado.
204 No Content: La solicitud fue exitosa, pero no hay contenido que devolver.
400 Bad Request: La solicitud no se puede procesar debido a un error del cliente.
401 Unauthorized: La solicitud requiere autenticación.
403 Forbidden: El servidor entiende la solicitud, pero se niega a autorizarla.
404 Not Found: El recurso solicitado no se encuentra en el servidor.
409 Conflict: Conflicto en el estado actual del recurso (por ejemplo, intento de crear un recurso que ya existe).
500 Internal Server Error: Error interno del servidor.
Códigos de estado comunes para el verbo GET:
200 OK: La solicitud fue exitosa y el recurso solicitado se devuelve en el cuerpo de la respuesta.
204 No Content: La solicitud fue exitosa, pero no hay contenido que devolver.
304 Not Modified: El recurso no ha sido modificado desde la última solicitud.
400 Bad Request: La solicitud no se puede procesar debido a un error del cliente.
401 Unauthorized: La solicitud requiere autenticación.
403 Forbidden: El servidor entiende la solicitud, pero se niega a autorizarla.
404 Not Found: El recurso solicitado no se encuentra en el servidor.
500 Internal Server Error: Error interno del servidor.
Códigos de estado comunes para el verbo PUT:
200 OK: La solicitud fue exitosa y el recurso ha sido actualizado.
201 Created: La solicitud fue exitosa y un nuevo recurso fue creado (si no existía antes).
204 No Content: La solicitud fue exitosa, pero no hay contenido que devolver.
400 Bad Request: La solicitud no se puede procesar debido a un error del cliente.
401 Unauthorized: La solicitud requiere autenticación.
403 Forbidden: El servidor entiende la solicitud, pero se niega a autorizarla.
404 Not Found: El recurso solicitado no se encuentra en el servidor.
409 Conflict: Conflicto en el estado actual del recurso.
500 Internal Server Error: Error interno del servidor.
Códigos de estado comunes para el verbo DELETE:
200 OK: La solicitud fue exitosa y el recurso ha sido eliminado (a veces se usa).
204 No Content: La solicitud fue exitosa y no hay contenido que devolver.
400 Bad Request: La solicitud no se puede procesar debido a un error del cliente.
401 Unauthorized: La solicitud requiere autenticación.
403 Forbidden: El servidor entiende la solicitud, pero se niega a autorizarla.
404 Not Found: El recurso solicitado no se encuentra en el servidor.
409 Conflict: Conflicto en el estado actual del recurso.

