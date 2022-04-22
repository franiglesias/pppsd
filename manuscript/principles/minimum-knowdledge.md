“No hables con extraños”. Seguro que más de una vez te dijeron esto las primeras veces que salías de casa sin compañía adulta, aunque solo bajases a la tienda del portal de al lado a buscar el pan. También es una de las formulaciones de un principio de diseño de software. 🧻👇🏿
Que no es que aclare mucho, aunque sí algo más que su nombre más popular: La ley de Demeter, que más formalmente se conoce como “Principio del mínimo conocimiento”.
Todo el clickbait de esta introducción es para hablar de uno de los principios que ayuda a reducir el acoplamiento en OOP. Fue introducido por Ian Holland como “regla” en un proyecto llamado “Demeter”, de ahí su nombre.
El principio de mínimo conocimiento viene a decir que los objetos deben tener el mínimo conocimiento posible sobre otros objetos. Exactamente el que exponen a través de sus API públicas.
Para entendernos, digamos que por conocimiento aquí entenderemos a la capacidad de interactuar y usar al otro objeto. El problema viene si hacemos trampa.
Imagina que tienes un objeto Service y otro Consumer. Consumer usa Service a través de su interfaz pública que expone un método “doServiceThing”. Hasta aquí todo bien.
Resulta que Consumer necesita escribir en un log. Consumer no tiene logger, pero  Service sí. Como tú sabes eso, haces que Service pueda entregar su Logger y lo usas. Todo bien, ¿no? Pues no.
Para empezar Consumer no tendría que saber que Service tiene un Logger, ni tú tendrías que exponerlo para que otros objetos puedan usarlo ya que no es la responsabilidad de Service. Service hace “doServiceThing” y eso es todo lo que debería preocuparle a Consumer.
Al usar el Logger, Consumer está hablando con un extraño. Sabe algo de Service que no debería saber, por lo que su acoplamiento con Service aumenta. Me explico:
Si Consumer solo usa la interfaz pública de Service, podríamos abstraer esta interface (doServiceThing) de modo que otros ServicesDoingThings pudiesen implementarla y, por tanto, Consumer podría usar otro más conveniente.
Pero… puesto que Consumer utiliza algo de Service que solo tiene Service y que Consumer “sabe” que tiene, resulta que Consumer está fuertemente acoplado con Service y no puede usar otro implementación.
Este drama es una de las cosas que intenta evitar el Principio de Mínimo Conocimiento. Que, en este ejemplo, estaría estrechamente relacionado con el Principio de Sustitución de Liskov (del que ya caerá otro 🧻 )
En la práctica, el Principio se utiliza así: en un método de un objeto solo se puede hablar con objetos conocidos y no puede hablar con extraños. ¿Qué objetos puede conocer un método? A saber:
El objeto que contiene el método. OK
Objetos que recibe como parámetros en ese método. OK
Objetos que se instancian en el método. OK.
Objetos que son miembros del objeto que tiene el método. OK.
Y ¿quienes son desconocidos?
Todos los demás.
Incluyendo objetos que puedan ser entregados por otros objetos.
Esto último suena rarísimo, porque básicamente obliga a que:
a) El consumer pase el objeto recibido como parámetro a otro objeto o método y actúa como intermediario. Esto puede llevar a cadenas de indirección largas como días sin pan.
b) Si el Consumer solo necesita una respuesta o acción del objeto recibido, Service tendría que entregar esa respuesta o ejecutar la acción sin exponer su estructura interna. Esto puede generar interfaces con muchos métodos.
Por tanto, hay que combinar el principio con otros. Ya hemos mencionado el de sustitución, pero también tendríamos que fijarnos en el de Segregación de Interfaces (otro 🧻 para el futuro).
¡Compromisos!¡Compromisos!
Sin embargo, este principio ayuda mucho a reducir el acoplamiento. Una regla muy práctica para ver si tenemos problemas relacionados con él es la de “un solo punto” (en PHP sería una sola flecha), referida a la manera de invocar métodos en objetos con la notación objeto.método.
Si hay más de un punto,(objeto.metodo.metodo2) es que posiblemente estamos rompiendo el principio de mínimo conocimiento.
Así que, en resumen, el principio de mínimo conocimiento nos dice que los objetos solo deberían interactuar con otros objetos del que tengan conocimiento directo y no basarse en el conocimiento de su estructura interna.
En OOP los objetos son cajas negras que exponen una manera de interactuar con ellos y no tenemos que saber nada de su estructura interna (y mucho menos usarla fuera del objeto).