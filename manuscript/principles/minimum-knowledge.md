# El mínimo conocimiento

_No hables con extraños_. Seguro que más de una vez te dijeron esto las primeras veces que salías de casa sin compañía adulta, aunque solo bajases a la tienda del portal de al lado a buscar el pan. También es una de las formulaciones de un principio de diseño de software.

Que no es que aclare mucho, aunque sí algo más que su nombre más popular: **La ley de Demeter**, que formalmente se conoce como _Principio del mínimo conocimiento_.

Todo el _clickbait_ de esta introducción es para hablar de uno de los principios que ayuda a reducir el acoplamiento en programación orientada a objetos. Fue introducido por Ian Holland como _regla_ en un proyecto llamado _Demeter_, de donde recibe su nombre.

El principio de mínimo conocimiento viene a decir que:

> los objetos deben tener el mínimo conocimiento posible sobre otros objetos.

Exactamente, el que exponen a través de sus API públicas. Para entendernos, digamos que por conocimiento aquí entenderemos a la capacidad de interactuar y usar al otro objeto. El problema viene si hacemos trampa.

Imagina que tienes un objeto `Service` y otro `Consumer`. `Consumer` usa `Service` a través de su interfaz pública que expone un método `doServiceThing`. Hasta aquí todo bien.

Resulta que `Consumer` necesita escribir en un _log_. `Consumer` no tiene _logger_, pero `Service` sí. Como tú sabes eso, haces que `Service` pueda entregar su `Logger` y lo usas. Todo bien, ¿no? Pues no.

Para empezar `Consumer` no tendría que saber que `Service` tiene un `Logger`, ni tú tendrías que exponerlo para que otros objetos puedan usarlo, ya que no es la responsabilidad de `Service`. `Service` hace `doServiceThing` y eso es todo lo que debería preocuparle a `Consumer`.

Al usar `Logger`, `Consumer` está hablando con un extraño. Sabe algo de `Service` que no debería saber, por lo que su acoplamiento con `Service` aumenta. Me explico:

Si `Consumer` solo usa la interfaz pública de `Service`, podríamos abstraer esta interfaz (`doServiceThing`) de modo que otros `ServicesDoingThings` pudiesen implementarla y, por tanto, `Consumer` podría usar otro más conveniente.

Pero puesto que `Consumer` utiliza algo de `Service` que solo tiene `Service` y que `Consumer` _sabe_ que tiene, resulta que `Consumer` está fuertemente acoplado con `Service` y no puede usar otra implementación.

Este drama es una de las cosas que intenta evitar el Principio de Mínimo Conocimiento. Que, en este ejemplo, estaría estrechamente relacionado con el Principio de Sustitución de Liskov, del que ya hablamos en otro capítulo.

En la práctica, el Principio se utiliza así: en un método de un objeto solo se puede hablar con objetos conocidos y no puede hablar con extraños. ¿Qué objetos puede conocer un método? A saber:

* El objeto que contiene el método. √ 
* Objetos que recibe como parámetros en ese método. √ 
* Objetos que se instancian en el método. √ 
* Objetos que son miembros del objeto que tiene el método. √.

Pero, ¿quiénes son desconocidos?

Todos los demás, incluyendo objetos que puedan ser entregados por otros objetos. Esto último suena rarísimo, porque básicamente obliga a que:

1. `Consumer` pase el objeto recibido como parámetro a otro objeto o método y actúa como intermediario. Esto puede llevar a cadenas de indirección largas como días sin pan.
2. Si `Consumer` solo necesita una respuesta o acción del objeto recibido, `Service` tendría que entregar esa respuesta o ejecutar la acción sin exponer su estructura interna. Esto puede generar interfaces con muchos métodos.

Por tanto, hay que combinar el principio con otros. Ya hemos mencionado el de sustitución, pero también tendríamos que fijarnos en el de Segregación de Interfaces.

¡Compromisos!¡Compromisos!

Sin embargo, este principio ayuda mucho a reducir el acoplamiento. Una regla muy práctica para ver si tenemos problemas relacionados con él es la de _un solo punto_ (en PHP sería una sola flecha), referida a la manera de invocar métodos en objetos con la notación `object.method`.

Si hay más de un punto,(`object.method1.method2`) es que posiblemente estamos rompiendo el principio de mínimo conocimiento. No confundir esto con las interfaces fluidas, que devuelven la misma instancia del objeto.

Así que, en resumen, el principio de mínimo conocimiento nos dice que los objetos solo deberían interactuar con otros objetos de los que tengan conocimiento directo a través de su interfaz pública y no basarse en lo que sepan de su estructura interna, que debería ser exactamente nada.

En Programación Orientada a Objetos, los objetos son cajas negras que exponen una manera de interactuar con ellos y no tenemos que saber nada de su estructura interna, y mucho menos usarla fuera del objeto.
