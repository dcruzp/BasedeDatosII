# Informe #2 Dise�o de la Aplicaci�n  


### integrantes 

- Daniel de la Cruz Prieto 
- Camilo Rodriguez Vel�zquez C-312
- Frank Adrian Perez Moralez C-311   



El tipo de arquitectura que vamos a utilizar para re-compilar la informaci�n acerca del comportamiento del **Clash Royale** va a ser la arquitectura Cliente-Servidor multicapas (tres capas) donde existir�n tres tipos de nodos: 


- **Clientes:** Son los que interact�an con los usuarios finales.
- **Servidores de aplicaci�n:** Procesan los datos para los usuarios.
- **Servidores de la base de datos:** Almacenan los datos para los servidores de la aplicaci�n.

![](img/3cbd.png)

#### Ventajas:

Utilizaremos esta arquitectura para nuestro programa debido a que aporta diversas ventajas a los desarrolladores como:

- Al ser una arquitectura de varias capas podemos aumentar las cantidades de los nodos anteriormente expuestos. Nuestro programa puede tener diversos clientes en la arquitectura, as\'i como se le pudieran agregar o eliminar alguno de estos, y gracias a esta arquitectura se podr� hacer sin que ninguno de los otros nodos, se afecten.

- Como los desarrolladores vamos a utilizar los datos de una aplicaci�n altamente consumida a nivel mundial existe el riesgo de que intenten hackear la informaci�n, aspecto el cual algunas tecnolog�as, dise�adas bas�ndose en esta arquitectura nos  ayudaran para mantener la seguridad de la informaci�n.

- Debido a la estabilidad de esta, es posible reparar, actualizar o reemplazar cualquier servidor sin que los usuarios se vean afectados completamente. 

 
La **desventaja fundamental**  de la arquitectura **Cliente- Servidor de aplicaci�n - Servidor de Base de Datos**, es que el flujo de informaci�n solo es a trav�s de la que proporciona el servidor en cuesti�n. A los clientes no se les permite compartir informaci�n entre ellos.

#### Aspectos Generales en el procesamiento de la Formaci�n

  La aplicaci�n deber� no solo re-compilar datos acerca del **Clash Royale**, tambi�n posibilitar\'a al usuario realizar varios tipos de consultas sobre el juego y obtener los resultados de estas. Este tipo de consultas est\'an relacionadas con las estad�sticas de los jugadores, cartas , batalla, desaf�os etc... u otros tipos de informaciones las cuales explicaremos en el Manual de Usuario. 

 Estas consultas se realizaran en la pagina web a trav�s de un "formulario", el cual el usuario completara de  la siguiente manera: 
 
#### Ejemplo:
 El usuario desea saber, dado un jugador especifico a que clanes se puede unir, primero debe rellenar cada uno de los objetos de inter\'es que desee consultar (en este caso seria el jugador y los clanes) a trav�s de la interfaz visual de la pagina web que le ayudara a rellenar cada uno de estos de una manera mas f�cil.  Estos campos a rellenar no tendr�n car�cter obligatorio para poder completar el formulario, pero al menos uno debe rellenarse. 
 
  Luego de que el usuario complete el formulario, este pasara por un controlador que es el encargado de entender que es  lo que solicita. Tomando el ejemplo en cuesti�n, el controlador detectar\'a que los objetos a los que tiene que acceder en la base de datos son  los que pertenecen a la informaci�n relacionada con los jugadores y a los clanes. Por lo tanto el controlador convertir\'a esta informaci�n en un lenguaje  el cual  podr� acceder directamente a la base de datos y obtener los resultados requeridos. 
 
 Pero el resultado que la base de datos entregara  no podr� ser la respuesta deseada por el usuario debido a que este, debe ser procesado por el controlador nuevamente para poder conformar una respuesta la cual el usuario podr� entender, en este caso debe devolver todos los clanes que tengan la cantidad de trofeos de entrada menor o igual que la cantidad de trofeos obtenidos por el jugador en cuesti�n. El proceso se describe de la siguiente manera: 
 

### 3. Esquema de Seguridad 

Como la aplicaci�n va a tener fundamentalmente dos Roles donde cada uno va a tener privilegios especificos de cada uno 

Un Rol fundamental es el de Administrador de la Base de Datos (DBA): Este es va a ser un usuario que tiene un alto nivel. Tiene la capacidad de administrar las Base de Datos y los objetos a los usuarios. 
Este se encarga de otorgar privilegios y accesos especiales a los usuarios comunes de la aplicacion 

**Privilegios que tiene el (DBA):**

- Crear Usuarios (comunes y con privilegios de administrador)
- Eliminar usuarios 
- Crear Tablas 
- Borrar Tablas
- Consultar tablas 
- Modificar (borrar , actualizar y a�adir  registros )

**Usuarios**

Interact�an con las UI y esta procesa todos los datos para hacer consultas a la aplicaci�n 

**Privilegios de los Usuarios**

- Conectarse a la Base de datos 
- Crear tablas a su esquema de usuarios 
- Crear vistas en su esquema de usuarios 
- Crear secuencias y procedimientos en su esquema de usuarios 

 El siguiente diagrama muestra como funcionaria el flujo de datos de nuestra API 

![](img/diagramadeflujo.jpg)


###### Ejemplo 

El usuario hace un Request a la API. Esta valida que el usuario tanga los privilegios necesarios para
poder acceder a la informaci�n que esta pidiendo en el momento que hace el request. Entonces si la aplicaci�n
determina  que el usuario tiene los privilegios requeridos para acceder a este tipo de informaci�n entonces se le devuelven los 
resultado de las base de datos. Si el usuario no tiene los privilegios necesarios entonces el server devuelve un "Bad Request". 


![](img/flujodedatos.jpg)

Vamos a usar Entity Framework para el trabajo con la base de datos y para el mapeo de los datos vamos a utilizar Automapper que es un framework que nos va a facilitar el trabajo en la API

