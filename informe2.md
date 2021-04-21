# Informe #2 Dise�o de la Aplicaci�n  


### integrantes 

- Daniel de la Cruz Prieto C-311
- Camilo Rodriguez Vel�zquez C-312
- Frank Adrian Perez Moralez C-311   



El tipo de arquitectura que vamos a utilizar para recompilar la informaci�n acerca del comportamiento del **Clash Royale** va a ser la arquitectura Cliente-Servidor N-Capas (tres capas) donde existir�n tres tipos de capas:

- **Capa de Presentaci�n:** Esta capa esta destinada al usuario, por lo cual tambi�n se le denomina **"Capa de Usuario"**. En esta, el usuario intercambiar� con una interfaz gr�fica , donde se le presentar� el sistema de una manera f�cil y entendible de usar, para que este pueda comunicarle a la base de datos toda la informaci�n que desea solicitar. Estar� representada en el esquema que aparece a continuaci�n  por los **Clientes**.

- **Capa de Negocio:** En esta se reciben las peticiones del usuario, a trav�s de la comunicaci�n con la **Capa de Usuario**, se eval�a esta informaci�n y se procesa para solicitar al gestor de base de datos el almacenamiento o la recuperaci�n de datos. Luego se comunica nuevamente con la **Capa de Presentaci�n**  para presentar los resultados adquiridos. En esta capa se consideran los programas de la aplicaci�n. **Servidores de Aplicaci�n**.

- **Servidores de la base de datos:**  Es la capa encargada del almacenamiento de los datos y tambi�n del acceso a los mismos. En esta se almacenan, recuperan o se reciben a trav�s de la **Capa de Negocio** los datos . **Servidores de Datos**.

Como la aplicaci�n que se desarrollar� es una p�gina web, estas capas tendr�n caracter�sticas espec�ficas como en la **Capa de Presentaci�n** que  incluir� al servidor web, que es el responsable de presentar los datos en un formato adecuado, en la **Capa de Negocios**, como es la capa l�gica del sistema estar� un programa o script el cual ser� el encargado de hacer todas las funcionalidades expuestas anteriormente. Por �ltimo la **Capa de datos**, se conforma por uno o varios gestores de bases de datos los cuales realizar�n las acciones determinadas. 

Una aplicaci�n web recoger� los datos del usuario (Primera Capa), los enviar� al servidor que ejecutar� el programa (Segunda y Tercera Capa) y cuyo resultado ser� presentado al usuario en la interfaz Gr�fica (Primera Capa nuevamente).

![](img/1bd.png)

#### Ventajas:

Utilizaremos esta arquitectura para nuestro programa debido a que aporta diversas ventajas a los desarrolladores como:

- Al ser una arquitectura de varias capas, hace mas f�cil reemplazar o modificar una capa sin afectar a las otras y sin que los usuarios se vean afectados completamente. Es m�s sencillo crear diferentes interfaces sobre un mismo sistema sin requerirse cambio alguno en la capa l�gica o de datos.

- El acceso a los servicios  es a trav�s de una "interfaz de usuario", por lo que no se necesita que se hagan sesiones de comando remotas directamente en el servicio.

- Se reduce el Acoplamiento Inform�tico y permite la distribuci�n del trabajo por niveles, donde cada grupo de trabajo estar� abstra�do del resto de los niveles.

- Como cada capa tiene distintos roles, se les conf�a una misi�n simple, lo que permite que puedan ampliarse con mayor facilidad en caso de que aumenten las necesidades. 
 
La **desventaja fundamental**  de la arquitectura de Tres Capas es que los servidores pueden sobrecargarse debido al exceso de peticiones hechas por el cliente.

#### Aspectos Generales en el procesamiento de la Formaci�n

 La aplicaci�n deber� no solo recompilar datos acerca del **Clash Royale**, tambi�n posibilitar� al usuario realizar varios tipos de consultas sobre el juego y obtener los resultados de estas. Este tipo de consultas est�n relacionadas con las estad�sticas de los jugadores, cartas, batalla, desaf�os, etc... u otros tipos de informaciones las cuales explicaremos en el Manual de Usuario.

  Estas consultas se realizar�n en la p�gina web a trav�s de un "formulario", el cual el usuario completar�.
 
#### Ejemplo:

El usuario desea saber, dado un jugador espec�fico, a que clanes se puede unir; primero 
debe rellenar cada uno de los objetos de inter�s que desee consultar (en este caso ser�a 
el jugador y los clanes) a trav�s de la interfaz visual de la p�gina web que le ayudar� 
a rellenar cada uno de estos de una manera mas f�cil.  Algunos de estos campos a rellenar 
no tendr�n car�cter obligatorio para poder completar el formulario, sin embargo en el 
ejemplo en cuesti�n es necesario rellenar el campo de jugador para saber a partir de este, 
a cu�les clanes puede unirse. 
 
 

Luego de que el usuario complete el formulario, este pasar� por un controlador que es el 
encargado de entender que es  lo que se solicita. Tomando el ejemplo en cuesti�n, el 
controlador detectar� que los objetos a los que tiene que acceder en la base de datos 
son  los que pertenecen a la informaci�n relacionada con los jugadores y a los clanes. 
Por lo tanto el controlador verificar� esta informaci�n para que esta pueda ser procesada por 
las demas capas y tomar las desiciones que correspondan en la aplicaci�n . Estos resultados nuevamente ser� procesada por el controlador para poder enviar 
una respuesta la cual el usuario podr� entender, en el ejemplo en cuesti�n debe devolver 
todos los clanes que tengan la cantidad de trofeos de entrada menor o igual que la cantidad 
de trofeos obtenidos por el jugador en cuesti�n. El proceso se describe de la siguiente 
manera:

 
![](img/2bd.png)

### 3. Esquema de Seguridad 

La aplicaci�n va a tener dos roles principales 

- Usuario (interacci�n b�sica con la App)
- Administrador (mayores privilegios )

El siguiente diagrama muestra como funcionar�a el flujo de datos de nuestra API 

![](img/diagramadeflujo.jpg)


###### Ejemplo 

El usuario hace un request a la API. Esta valida que el usuario tenga los privilegios necesarios para
poder acceder a la informaci�n que esta pidiendo en el momento que hace el request. Entonces si la aplicaci�n
determina  que el usuario tiene los privilegios requeridos para acceder a este tipo de informaci�n entonces se le devuelven los 
resultado de las base de datos. Si el usuario no tiene los privilegios necesarios entonces el server devuelve un "Bad Request". 

Si un usuario quisiera tener informaci�n acerca de los 10 mejores usuarios (con mayor cantidad de puntos , ordenados de mayor a menor ) el diagrama muestra como a groso modo se realizar�a el flujo de datos para nuestra app 

![](img/flujodedatos.jpg)


##### Aspectos Generales y procesamiento de la informaci�n 

La aplicaci�n la vamos a desarrollar en C# con NetCore. Como ORM vamos a usar EntityFramework. para el manejo de la 
base de datos para (Crear, Actualizar, Consultar y Borrar registros de la base de datos). 

Para crear la base de datos vamos a usar ***Microsoft SQL Server Management Studio***, por la facilidad que nos brinda 
de forma gr�fica al crear la base de datos. (es decir que no vamos a usar la filosof�a de *"Code First"* 
para la creaci�n de la misma). 

Es decir para el backend vamos a trabajar con dotnet (C#). Para el desarrollo de la 
aplicaci�n gr�fica vamos a usar React.(Es decir para el frontend).

De forma general lo que queremos es  crear una Web API y ponerla en un servidor. para poder acceder desde un navegador 
cualquiera a la aplicaci�n.  

#### Funcionalidades de los usuarios y esquema de Navegaci�n 


La aplicaci�n va a tener fundamentalmente dos Roles donde cada uno va a tener privilegios espec�ficos.

Un rol fundamental es el de Administrador de la Base de Datos (DBA): Este va a ser un usuario que tiene un alto nivel de accesibilidad. Tiene la capacidad de administrar las Base de Datos y los datos de los usuarios. 
Este se encarga de otorgar privilegios y accesos especiales a los usuarios comunes de la aplicaci�n. Por lo tanto va a poder crear nuevas tablas y registros en la base de datos. Adem�s de tener el poder de eliminar a cualquier usuario o modificar sus datos. 


**Privilegios que tiene el (DBA):**

- Crear Usuarios (comunes y con privilegios de administrador)
- Eliminar usuarios 
- Consultar tablas 
- Modificar (borrar , actualizar y a�adir  registros )

**Usuarios**

Interact�an con las UI y esta procesa todos los datos para hacer consultas a la aplicaci�n 

**Privilegios de los Usuarios**

- Listar los jugadores que hay en la base de datos. 
- Listar los clanes que hay en la base de datos.
- Poder ver los mejores jugadores y clanes ordenados por cantidad de trofeos obtenidos.
- Poder buscar Jugadores , guerras y clanes por si identificador (o puede ser su nombre).  

Los usuarios comunes de la aplicaci�n van a poder acceder a informaci�n �til para el uso de esta 
como es Conocer los mejores jugadores que participan en una guerra, conocer las cartas mas populares dentro de cada clan existente. 

Por ejemplo un usuario com�n podr�a conocer si un jugador se podr�a unir a un clan determinado , sabiendo las restricciones del clan 
para unirse a este. Un usuario com�n tambi�n podr�a saber cual es la carta mas donada en una regi�n dada. 
Los usuarios con roles de administrador podr�an modificar registros de una tabla, as� como hacer
consultas que har�a cualquier usuario com�n de la aplicaci�n.

Los usuarios con roles de administradores podr�an borrar de la base de datos un usuario 
con todos sus datos almacenados , pero nunca va a poder modificar las base de  datos, 
es decir cambiar el tipo de datos de un campo en un tabla dada, este tipo de acciones 
solo es posible hacerlas desde la actualizaci�n de la aplicaci�n que es tarea de los 
programadores y el equipo de trabajo que desarrolla y mantiene la aplicaci�n. 



### Esquema de Navegaci�n

Nuestra aplicaci�n tendr� un men� principal para el cual ser� el punto de partida 
para navegar por nuestra aplicaci�n. Este Men� principal tendr�a una serie de aspectos los cuales se describen abajo: 

 - Login 
 - Top Player
 - Top Clanes 
 - Cartas 
 - Desaf�os 
 - Guerra de Clanes 
 - Log Out 

Cada uno de estos aspectos ser�n puentes a otras pantallas que responden a cada uno de los apartados que se describen 
entonces.

En la parte derecha del men� principal aparecer�n una serie de barras de b�squedas donde teniendo el Identificador (**id**) de cada uno de los elementos que se describen vamos a poder acceder a datos 
propios de cada apartado, por ejemplo si queremos conocer los datos de un jugador y sabemos el id del mismo podemos poner su id en el campo de b�squeda y autom�ticamente se nos mostrara otra pantalla donde se van a poder ver todos los 
atributos de un jugador en espec�fico. Los elementos de b�squeda que se van a mostrar en este men� principal, son los siguientes: 

 - Buscar Jugador 
 - Buscar Clan 
 - Buscar Desaf�o 
 - Buscar Guerra 
 - Buscar Carta 

Este apartado del men� principal se ver�a de la siguiente manera: 

![](img/esquemadenavegacion1.jpg)


Entonces una vez estando estando en el men� principal si queremos ver cuales son los mejores jugadores nos desplazamos al apartado de  *Top Player* y damos un click, esto nos va a mostrar otra 
pantalla donde veremos un listado de los 10 mejores jugadores ordenado descendente-mente. Cada uno de los record nos dar�a la siguiente informaci�n: 

   - Nombre del Jugador 
   - Nivel 
   - Cantidad de Trofeos  

Este apartado de Top Jugadores se ver�a de la siguiente manera: 

 
 ![](img/esquemadenavegacion2.jpg)

Una vez que estemos en este apartado, se puede saber todos los datos de un jugador en espec�fico si damos click encima de la barra que muestra los datos de este jugador, 
Por ejemplo si damos click encima de la barra que nos muestra los datos de ***Player 1*** la aplicaci�n nos llevar�a hasta otro apartado donde se mostrar�an todo los datos relacionados con este jugador en espec�fico. 
este apartado que describimos se ver�a de la siguiente manera: 

 ![](img/esquemadenavegacion3.jpg)

Desde cada uno de los apartados se podr�a regresar hacia al apartado anterior. y as� sucesivamente hasta el men� principal. 

Lo que se describi� anteriormente para poder navegar y ver los ***Top Players***
se puede hacer para cada uno de los elementos que aparecen a la izquierda en el men� principal. 
Es decir para los *'Top Clanes'* , *Cartas* , *Desaf�os* y  *Guerra de Clanes*. 


Igual para las b�squedas que aparecen a la derecha en el men� principal. se rellena el campo con los 
datos que requiere la b�squeda y se muestra el apartado correspondiente con los resultados obtenidos mediante la 
consulta a la base de datos.


Conjugando las distintas formas de desplazarse y ver informacion de la base de datos desde la aplicaciones podemos ver los resultados de 
cada una de las consultas que se nos propone. 

Por ejemplo si quesieramos conocer el clan con mejor desempe�o durante las guerras por regi�n del mundo, es decir,
por cada regi�n obtener el clan con mayor cantidad de trofeos.
Nos iriamos al apartado de Top Clanes y una ves ahi tendraimos listado los mejores clanes 
ordenados de forma descendente por la cantidad de trofeos obtenidos. 
Ahora si quisieramos saber los mejores clanes de una region en espec�fico (supongamos la regi�n *A*), podriamos escoger que se nos listaran solamente los 
clanes de la region a la cual deseamos conocer en este caso la region *A*. Este ejemplo se ver�a en nuestra aplicaci�n de la siguiente manera: 

 ![](img/esquemadenavegacion4.jpg)

Y as� podr�amos hacer con las dem�s consultas que se nos proponen en la orden del proyecto.
como son conocer los mejores jugadores que participan en una guerra, etc. 










