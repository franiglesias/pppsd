# Eventos

Tenía pendiente hablar de eventos. No de saraos, claro, sino de mensajes. 🧻👇🏿

Hace tiempo comenté que había tres tipos de mensajes:

* imperativos (commands): producen un cambio en el sistema

* interrogativos (queries): recuperan info del sistema

* enunciativos (eventos): informan de algo que ha pasado en el sistema

Los tres mensajes se pueden modelar con un patrón message/handler.  Message es un objeto inmutable que contiene la información interesante y Handler es un objeto que recibe Message como parámetro y hace lo que tenga que hacer.

Tanto los command como las queries tienen un único handler o destinatario (1:1). Sin embargo, los events pueden tener un número indefinido de destinatarios (1:n).

Los handlers de comandos y eventos no devuelven nada (son comandos).

Los eventos son clave en las arquitecturas limpias dado que nos permiten algunas cosas importantes, entre ellas:

* Que los casos de uso sean _single responsibility compliant_

* Que partes de la aplicación separadas puedan comunicarse sin acoplarse

¿Cómo funciona esto de los eventos? Básicamente se hace a través de un patrón de suscripción. Un mediador (EventDispatcher) puede recibir eventos y despacharlos a todos los handlers que se han apuntado como suscriptores.

Así, cuando ocurre algo interesante, se instancia el evento correspondiente y se pasa al EventDispatcher. Este identifica los posibles handlers y les pasa el evento, ejecutando el handler.

Este proceso así explicado es síncrono. Cuando despachamos el evento la ejecución pasa al primer handler suscriptor, luego al siguiente, y así hasta acabar la lista, y luego vuelve al punto donde estábamos.

En asíncrono la ejecución de los diferentes handlers se hace en paralelo. Conceptualmente es la misma idea: al lanzar el evento se ejecutan ciertas acciones en respuesta.

By the way, creo que es buena idea considerar los eventos como si fuesen asíncronos (aunque no lo sean) y todo lo que eso conlleva.

Algunas consideraciones: En aplicaciones estilo DDD, la capa de dominio es en la que se producen los eventos. ¿Quienes generan eventos? Pues normalmente, entidades y agregados. Les pasan cosas interesantes y lo dicen.

Ahora bien, hay que tener cuidado con temas como los límites transaccionales. Por ejemplo, para emitir el evento de que un agregado ha sido creado, tenemos que asegurarnos de que está persistido (no bastaría con haberlo instanciado y tal).

Por eso, aunque _en teoría_ el evento se emite cuando se produce, lo normal es que entidades y agregados instancien y guarden los eventos y que éstos se despachen en el caso de uso, una vez que sabemos que todo se ha hecho bien.

Consejo: no uses herencia para tener gestión de eventos en agregados, sino traits o equivalente.

¿Dónde viven los handlers de los eventos? Pues mi preferencia personal es ponerlos en la capa de aplicación como si fuesen casos de uso. Los eventos en sí en la capa de dominio.

Decía que los eventos nos proporcionan SRP para los casos de uso. Así es: tendremos un caso de uso que realiza la acción principal, emitiendo uno o más eventos, y los suscriptores nos permiten añadir acciones (notificación, proyecciones, lo que sea) sin contaminar el caso de uso.

Igualmente nos ayuda con Open/Close, ya que no tenemos que tocar el caso de uso si tenemos que añadir funcionalidades o acciones. Escribimos un nuevo suscriptor y ya.

Por otro lado, es igualmente fácil quitar suscriptores o reemplazar por uno nuevo.

No he entrado aquí en un tema más complejo como es el event sourcing. Es algo que se escapa del scope del 🧻, pero básicamente consiste en no mantener estado en los agregados, sino los eventos que conducen a ese estado.

Y hasta aquí el 🧻 de hoy.