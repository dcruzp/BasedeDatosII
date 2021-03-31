# Informe #2 Diseño de la Aplicación  


### integrantes 

- Daniel de la Cruz Prieto 
- Camilo Rodriguez Velázquez C-312
- Frank Adrian Perez Moralez C-311   



El tipo de arquitectura que vamos a utilizar para re-compilar la información acerca del comportamiento del **Clash Royale** va a ser la arquitectura Cliente-Servidor multicapas (tres capas) donde existirán tres tipos de nodos: 


- **Clientes:** Son los que interactúan con los usuarios finales.
- **Servidores de aplicación:** Procesan los datos para los usuarios.
- **Servidores de la base de datos:** Almacenan los datos para los servidores de la aplicación.

![](img/3cbd.png)

#### Ventajas:

Utilizaremos esta arquitectura para nuestro programa debido a que aporta diversas ventajas a los desarrolladores como:

- Al ser una arquitectura de varias capas podemos aumentar las cantidades de los nodos anteriormente expuestos. Nuestro programa puede tener diversos clientes en la arquitectura, as\'i como se le pudieran agregar o eliminar alguno de estos, y gracias a esta arquitectura se podrá hacer sin que ninguno de los otros nodos, se afecten.

- Como los desarrolladores vamos a utilizar los datos de una aplicación altamente consumida a nivel mundial existe el riesgo de que intenten hackear la información, aspecto el cual algunas tecnologías, diseñadas basándose en esta arquitectura nos  ayudaran para mantener la seguridad de la información.

- Debido a la estabilidad de esta, es posible reparar, actualizar o reemplazar cualquier servidor sin que los usuarios se vean afectados completamente. 

 
La **desventaja fundamental**  de la arquitectura **Cliente- Servidor de aplicación - Servidor de Base de Datos**, es que el flujo de información solo es a través de la que proporciona el servidor en cuestión. A los clientes no se les permite compartir información entre ellos.

#### Aspectos Generales en el procesamiento de la Formación

  La aplicación deberá no solo re-compilar datos acerca del **Clash Royale**, también posibilitar\'a al usuario realizar varios tipos de consultas sobre el juego y obtener los resultados de estas. Este tipo de consultas est\'an relacionadas con las estadísticas de los jugadores, cartas , batalla, desafíos etc... u otros tipos de informaciones las cuales explicaremos en el Manual de Usuario. 

 Estas consultas se realizaran en la pagina web a través de un "formulario", el cual el usuario completara de  la siguiente manera: 
 
#### Ejemplo:
 El usuario desea saber, dado un jugador especifico a que clanes se puede unir, primero debe rellenar cada uno de los objetos de inter\'es que desee consultar (en este caso seria el jugador y los clanes) a través de la interfaz visual de la pagina web que le ayudara a rellenar cada uno de estos de una manera mas fácil.  Estos campos a rellenar no tendrán carácter obligatorio para poder completar el formulario, pero al menos uno debe rellenarse. 
 
  Luego de que el usuario complete el formulario, este pasara por un controlador que es el encargado de entender que es  lo que solicita. Tomando el ejemplo en cuestión, el controlador detectar\'a que los objetos a los que tiene que acceder en la base de datos son  los que pertenecen a la información relacionada con los jugadores y a los clanes. Por lo tanto el controlador convertir\'a esta información en un lenguaje  el cual  podrá acceder directamente a la base de datos y obtener los resultados requeridos. 
 
 Pero el resultado que la base de datos entregara  no podrá ser la respuesta deseada por el usuario debido a que este, debe ser procesado por el controlador nuevamente para poder conformar una respuesta la cual el usuario podrá entender, en este caso debe devolver todos los clanes que tengan la cantidad de trofeos de entrada menor o igual que la cantidad de trofeos obtenidos por el jugador en cuestión. El proceso se describe de la siguiente manera: 
 

### 3. Esquema de Seguridad 

Como la aplicación va a tener fundamentalmente dos Roles donde cada uno va a tener privilegios especificos de cada uno 

Un Rol fundamental es el de Administrador de la Base de Datos (DBA): Este es va a ser un usuario que tiene un alto nivel. Tiene la capacidad de administrar las Base de Datos y los objetos a los usuarios. 
Este se encarga de otorgar privilegios y accesos especiales a los usuarios comunes de la aplicacion 

**Privilegios que tiene el (DBA):**

- Crear Usuarios (comunes y con privilegios de administrador)
- Eliminar usuarios 
- Crear Tablas 
- Borrar Tablas
- Consultar tablas 
- Modificar (borrar , actualizar y añadir  registros )

**Usuarios**

Interactúan con las UI y esta procesa todos los datos para hacer consultas a la aplicación 

**Privilegios de los Usuarios**

- Conectarse a la Base de datos 
- Crear tablas a su esquema de usuarios 
- Crear vistas en su esquema de usuarios 
- Crear secuencias y procedimientos en su esquema de usuarios 

 El siguiente diagrama muestra como funcionaria el flujo de datos de nuestra API 

![](img/diagramadeflujo.jpg)


###### Ejemplo 

El usuario hace un Request a la API. Esta valida que el usuario tanga los privilegios necesarios para
poder acceder a la información que esta pidiendo en el momento que hace el request. Entonces si la aplicación
determina  que el usuario tiene los privilegios requeridos para acceder a este tipo de información entonces se le devuelven los 
resultado de las base de datos. Si el usuario no tiene los privilegios necesarios entonces el server devuelve un "Bad Request". 


![](img/flujodedatos.jpg)

Vamos a usar Entity Framework para el trabajo con la base de datos y para el mapeo de los datos vamos a utilizar Automapper que es un framework que nos va a facilitar el trabajo en la API

