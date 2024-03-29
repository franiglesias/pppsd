# Las vistas en DDD

Tienes un caso de uso: mostrar todos los pedidos que han caducado. Así que en el dominio de pedidos, defines `OrderRepositoryInterface`, y agregas `getExpiredOrders`, pero...

Para explicar una solución _rigurosa_ a este problema tendría que haber hablado de eventos antes, por lo que haré un inciso con unos pocos párrafos al respecto y luego me meto en harina.

En una aplicación pueden circular tres tipos de mensajes. Dos de ellos los conocemos ya: imperativos (comandos) e interrogativos (queries).

El tercer tipo son los _mensajes enunciativos_: los eventos. Los eventos comunican cosas _interesantes_ que han ocurrido en el dominio.

Comandos y Queries tienen un solo destinatario. Los eventos pueden ser escuchados por cualquier número de interesados, que son sus Listeners o Subscribers. Estos se _apuntan_ a responder a ciertos eventos y actúan cuando estos son lanzados por un _despachador de eventos_.

Los eventos los generan las entidades y/o agregados. La forma más habitual de gestionar esto es que en lugar de lanzar los eventos exactamente cuando se producen, se acumulan y se recolectan para lanzar una vez que los casos de uso hayan terminado con éxito.

Y hasta aquí esta breve introducción. Quédate con que si se produce algo _interesante_ en el dominio podemos suscribirnos a ese evento para saber que ha ocurrido y hacer algo al respecto.

Volvamos al problema de la vista…

Una vista es un asunto de infraestructura, pues se trata de un interés de la interfaz de usuario. Así que empecemos por ahí. Una vista de lista típica consiste en una colección de representaciones de una entidad que contiene un subconjunto de sus datos. Aparte de eso, suelen necesitar filtros, ordenación y paginación. 

Para las vistas existe un patrón clásico: _Model-View-Controller_ o _MVC_. La parte que nos importa ahora es la M. La M puede entenderse también como _ViewModel_ y en los frameworks MVC es típico que estén vinculados a la base de datos usando un patrón _Active Record_.

¿Y qué papel juega el _ViewModel_ en nuestro ejemplo? Un _ViewModel_ es básicamente un DTO que representa una entidad en esa vista específica. Para obtener ese _ViewModel_, o colección de ellos, podríamos pedirlo a una tabla específica en una base de datos si es el caso.

¿Pero no tenemos ya las entidades persistidas? ¿Para qué otra tabla? ¿No basta con añadir un método al repositorio y obtener las entidades y tal y cuál? Hay varios problemas con esto último. El principal es introducir asuntos de persistencia en el dominio. El rol del repositorio es proporcionar persistencia a las entidades, pero no resolver los problemas de las vistas. Tenemos el patrón _Specification_ para obtener subconjuntos de las entidades, pero ese patrón no contempla paginación, ordenación o filtrado en el sentido de las vistas.

La solución es tener una tabla que esté asociada a una vista concreta, un _ViewModel_ (o _ReadModel_, si lo prefieres más genérico), pero tenemos el problema de poblarla. También hay otra solución _low-cost_ de la que hablaré más adelante.

Y aquí es donde entran en juego los eventos. Cada vez que se lanza un evento que pueda afectar a esa vista, como que se ha creado un nuevo pedido, o se ha actualizado, un suscriptor se encarga de actualizar el _ViewModel_ si es necesario. Esto se puede considerar como una _Proyección_.

Así que si se ha creado un pedido, se añade una fila a la tabla del _ViewModel_ que corresponda, o se hace lo que haga falta para mantenerlo en sincronía. De hecho, si guardas los eventos de modo que se puedan rebobinar y reproducir podrías reconstruir los _ViewModels_ desde el principio de los tiempos. Y eso te sonará a _Event Sourcing_ aunque la actualización de proyecciones solo es una parte de ese patrón.

Las grandes ventajas de este sistema son: simplicidad y rendimiento. Es bastante obvio que son tablas fáciles de mantener, y las queries son rapidísimas porque no traen datos de más, no tienen asociaciones ni otras cargas relacionadas. 

Además, es fácil introducir ideas como filtros, ordenación, paginación, etc., precisamente porque trabajas con tablas básicas y tipos de datos simples.

El problema, porque nada es gratis, es mantener la consistencia.

Solución _low-cost_: para sistemas más sencillos, simplemente accede a la persistencia a través de otro servicio que lance queries simples contra las tablas que guardan tu entidad o agregado y te devuelva los _ViewModel_. No necesitas sincronización porque accedes a los mismos datos.

En este caso, nunca escribimos nada que no sea a través del repositorio en dominio.

En resumen: una vista es como una _micro-aplicación MVC_ dentro de tu gran aplicación. Puedes introducir un caso de uso para gestionarla. A veces nos interesa que diferentes vistas usen el mismo caso de uso, como una vista web y un archivo CSV para exportar. El _ViewModel_ simplifica el acceso a los datos y las operaciones que le interesan a la vista en la UI como filtros, ordenación o paginación, sin contaminar el dominio.