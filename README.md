# Alexandria Lib
## Descripción
Alexandria Lib es una base de conocimiento para la comunidad de estudiantes de carreras relacionadas con tecnología, donde la misma comunidad puede compartir lo que sabe y aportar por medio de artículos al crecimiento académico  de los usuarios.
La aplicación cuenta con tres tipos o roles de usuario, cada uno tiene permisos distintos y funcionalidades a las que puede acceder. Para entrar a la aplicación con un rol en específico es necesario que el usuario se registre o autentique en la plataforma, esto se hace por medio del botón ubicado en la parte superior derecha de la pantalla.
  ![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/1.png "Login/Register Button")
Si el usuario escoge la opción de registro "Sign Up", es dirigido a otra pantalla donde debe llenar un formulario con alguna información básica para tener una cuenta dentro de la plataforma. La siguiente imágen muestra la pantalla de registro. Las opciones de registrarse con Github y Google no están en funcionamiento pero se visualizan para futura implementación.
![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/2.png "Register View")

Si el usuario escoge la opción de iniciar sesión "Sign In", es dirigido a otra pantalla donde debe ingresar sus credenciales para poder continuar usando la aplicación y las funcionalidades que tiene permitidas según su rol de usuario. Al igual que en la pantalla de registro, las funcionalidades de inicio de sesión con Github y Google están expuestos para futura implementación, pero aún no está en funcionamiento.

![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/3.png "Login View")

 # TODO: poner pantallazos de toda la aplicacion, con la descripcion nde cada pantallazo, y en el code editor poner un GIF con cada 

# TODO: Hacer bien el modelo y actualizarlo al estado actual del código
## Diagrama de clases
![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/ClassDiagram.png "Class Diagram")
## Diagrama de componentes
![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/ComponentDiagram.png "Component Diagram")
## Diagrama de despliegue
![](https://raw.githubusercontent.com/alexandrialib/Alexandria/master/Images/DeploymentDiagram.png "Deployment Diagram")
## Escenarios de calidad
# TODO: Poner requisitos minimos de la maquina y los recomenados, poner el entorno general ej: para todos los esenarios el entorno es el siguiewnte: velocidad de internet de minimo xxx: con un navegador actualizado a la ltima versiuomn, 
### Estructura
Para identificar los escenarios de calidad se seguirá la siguiente estructura:

	1. Fuente del estímulo: quien o que genera el estímulo. 
	2. Estímulo: lo que se quiere llevar a cabo.
	3. Entorno: condiciones dentro de las cuales se presenta el estímulo.
	4. Artefacto: parte del sistema que recibe el estímulo.
	5. Respuesta: actividad que ocurre luego de la llegada del estímulo.
	6. Medida de la Respuesta: criterio para testear el requerimiento.
### Escenario de latencia

El sistema deberá diseñarse de forma que aunque en un inicio el número de usuarios sea bajo, si en un periodo corto de tiempo aumentasen, la disponibilidad y rendimiento de este no se vea afectado.

    1. Fuente: Usuario del sistema, ya sea registrado o anonimo
	2. Estímulo: Navegar en la aplicación
	3. Entorno: Aplicación con un trafico normal de maximo 100 usuarios.
	4. Artefacto: Servidor Backend (API Rest), base de datos y FrontEnd
	5. Respuesta: No hay un retardo excesivo a la hora de responder peticiones.
	6. Medida de la Respuesta: tiempo bajo de respuesta a peticiones por recursos (menos de 3000 ms), número de peticiones denegadas por debajo del 2.5%

	1. Fuente: Usuario del sistema, ya sea registrado o anonimo
	2. Estímulo: Navegar en la aplicación
	3. Entorno: Aplicación con un trafico normal de maximo 100 usuarios tiene un pico de demanda de 150 usuarios navegando a la vez.
	4. Artefacto: Servidor Backend (API Rest), base de datos
	5. Respuesta: No hay un retardo excesivo a la hora de responder peticiones.
	6. Medida de la Respuesta: tiempo bajo de respuesta a peticiones por recursos (menos de 4000 ms), número de peticiones denegadas por debajo del 5%

El sistema debe prestar los servicios de real time de forma optima, respondiendo fluidamente al uso por parte del púbico 

	1. Fuente: Usuarios del sistema registrados
	2. Estímulo: Uso de funcionalidades en tiempo real
	3. Entorno: Trafico normal de maximo 5 usuarios en una sesión de monitoria, trafico normal en la aplicación de maximo 100 usuarios.
	4. Artefacto: Servidor Frontend (Free Dyno en Heroku)
	5. Respuesta: El sistema se comporta de forma natural y fluida. 
	6. Medida de la Respuesta: La información que se transmita en tiempo real debe ser consistente. Se visualizan las acciones de los otros participantes de la sesion en menos de 5000 ms.

### Escenario de Autenticación

Los usuarios registrados podrán validar su identidad y disfrutar de los beneficios de su registro en la plataforma. No se verá vulnerada su identidad ni sus datos, siendo estos protegidos en la medida de lo posible por la plataforma.

	1. Fuente: Ciber atacante
	2. Estímulo: Intento de suplantación
	3. Entorno: Aplicación en entorno productivo (despliegue), trafico normal de la aplicación de maximo 100 usuarios a la vez.
	4. Artefacto: Pagina web (login), servidores Backend/Frontend y base de datos
	5. Respuesta: Acceso denegado por credenciales incorrectas
	6. Medida de la Respuesta: El número de cuentas vulneradas debe ser cero

    1. Fuente: Usuario registrado
	2. Estímulo: Intento de volver a ingresar indicandole al buscador que vuelva atras una pagina, luego de cerrar sesion. 
	3. Entorno: Aplicación en entorno productivo (despliegue), trafico normal de la aplicación de maximo 100 usuarios a la vez.
	4. Artefacto: Pagina web (login).
	5. Respuesta: Acceso denegado por finalizacion de sesion.
	6. Medida de la Respuesta: En ningun intento el usuario tiene acceso nuevamente luego de cerrar sesion (sin ingresar nuevamente sus credenciales).


### Escenario de Autorización
	
Los usuarios no pueden acceder a funcionalidades restringidas para sus roles o perfiles de usuario

    1. Fuente: Usuarios no registrados.
	2. Estímulo: Usuario intenta utilizar cualquier funcion distinta a ver las categorias ya existentes.
	3. Entorno: Simulacion de situacion normal con maximo 100 usuarios a la vez intentando la misma accion.
	4. Artefacto: API Rest y servidor de base de datos.
	5. Respuesta: El sistema negará las operación por permiso denegado.
	6. Medida de la Respuesta: Los usuarios obtienen un error 401 por no permiso denegado, ninguna peticion es aceptada.

	1. Fuente: Usuarios con rol de estudiante.
	2. Estímulo: Estudiante Intenta agregar un articulo.
	3. Entorno: Sistema en entorno de pruebas, simulacion de situacion normal con maximo 100 usuarios a la vez.
	4. Artefacto: API Rest y servidor de base de datos.
	5. Respuesta: El sistema negará dicha operación indicando la falta de permisos.
	6. Medida de la Respuesta: El usuario obtiene un error 401 por no permiso denegado, ninguna peticion de este estilo que realice sera aceptada.


### Escenario de Adaptabilidad

La pagina web deberá ser visible desde cualquier tipo de explorador de Internet curbiertos por el framework **ReactJS** y que soporten **SSE** y dispositivo que hay en el mercado.

	1. Fuente: Equipos de los usuarios
	2. Estímulo: Acceso a la pagina
	3. Entorno: Aplicación en entorno productivo (despliegue)
	4. Artefacto: Frontend (Navegador de articulos, Editor de articulos, Sesion en RealTime)
	5. Respuesta: Debe visualizarse todo el contenido desde distintos exploradores y equipos
	6. Medida de la Respuesta: Debe estar probado en diferentes plataformas

### Escenario de Disponibilidad
El sistema deberá facilitar una alta disponibilidad, el portal será accesible el 90% del tiempo, en alguna de esas ocasiones el servicio será denegado al usuario, pidiéndole que trate de acceder más tarde (fallar con gracia).

	1. Fuente: Interacción de los usuarios con la aplicación
	2. Estímulo: Interacción de los usuarios en la pagina
	3. Entorno: Aplicacion siendo probada con un pico de usuarios accediendo a diversas funcionalidades, maximo 300 usuarios.
	4. Artefacto: Servidor Backend
	5. Respuesta: Recurso solicitado o aviso satisfactorio de error (400)
	6. Medida de la Respuesta: El sistema no muestra errores no planeados o manejados al usuario, solo el 10% de las solicitudes son denegadas.

