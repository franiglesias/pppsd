# Refactor (sin piedad)

Hablemos de _Refactor Mercilessly_ o *Merciless Refactoring*. Una de las prácticas de Extreme Programming.

Para empezar, creo que muchos equipos confunden refactor con reescritura. Vale, que sí, que son bastante sinónimos... Yo defino refactor como pequeños cambios inocuos, sin riesgo. Reescritura la entiendo como cambios muy grandes, con frecuencia en nivel de arquitectura.

_Refactor mercilessly_, refactorizar despiadadamente, consiste en hacerlo frecuentemente, continuamente y sin pedir permiso.

* _Frecuentemente_ quiere decir varias veces al día.
* _Continuamente_ quiere decir todos los días.
* Sin pedir permiso quiere decir que no es una tarea planificada, ni importa quién escribió la línea a refactorizar.

– Pero Fran, ¿qué salvajada es esa?

Todo esto se relaciona con la _regla del campamento_ y el _WTF factor_. Vayamos por partes:

La _regla del campamento_ reza: _deja el código por el que pases mejor de lo que estaba_.

Pasamos la mayor parte del tiempo leyendo código. Para implementar cualquier cosa nueva o para solucionar un problema tenemos que leer código. Incluso después de escribir código tenemos que releerlo.

Si encontramos algo que no se entiende dedicamos un rato a pensar en ello. Ese rato puede ser muy largo. Puede que no haya nadie a quien preguntarle. O sí, pero ya se ha olvidado. Puede que ese código lo escribiésemos nosotras mismas.

Ese es el _WTF factor_: ese trocito de código que nos parece raro, incomprensible, contradictorio... Al llegar el momento _ajá!_ y entender aquello tenemos dos opciones:

1. Seguir adelante, dejarlo como está y quedarnos con ese conocimiento en la memoria.
2. Hacer un pequeño arreglo seguro, ya sea por tests o por refactor automático, commit y push.

La opción 2 es la buena.

Habremos ahorrado al developer del futuro un tiempo importante para otras cosas. Habremos mejorado la velocidad del equipo en el futuro. Habremos reducido un poco la deuda técnica.

El tiempo de hacer este refactor puede ser de minutos: cambiar el nombre de algo, extraer un método, ordenar unas líneas... Es una pequeña inversión con alto retorno.

Para hacer esto, son necesarias algunas condiciones. Estos refactorings tienen que ser seguros por lo que:

* Debería haber un test cubriendo esa área de código.
* Si no lo hay, el refactor debería ser automatizado con el IDE
* El _scope_ es limitado, como ser interno a una función

Si lo que cambia son interfaces públicas el riesgo aumenta un poco, pero teniendo tests que cubran ese cambio, no deberías encontrarte con problemas, aunque es posible que el volumen de cambios sea grande. En ese caso, hay estrategias para ir progresivamente, de modo que reduces el riesgo. Por ejemplo, añade un nuevo método con la nueva signatura y úsalo solo en el lugar que provocó el cambio, haciendo que el viejo lo llame _por debajo_. Luego podrás cambiar los usos del viejo por el nuevo progresivamente.

Aparte, necesitas un compromiso por parte del equipo: ¿cómo es vuestro _workflow_? ¿Puedes garantizar que el cambio estará en _main_ lo antes posible? ¿O habrá un _pull request_ de dos líneas languideciendo durante días o semanas?

Otro punto es la propiedad del código. En un equipo, el código es del equipo o no es de nadie. Si hay que pedir permiso para hacer un cambio así al autor de la línea tienes un _smell_ en el equipo.

Estos pequeños cambios acumulados nos llevan progresivamente a un código en mejor estado. En un momento dado, nos pueden facilitar un cambio de mayor calado que será más evidente y más fácil de hacer.

Este refactor cotidiano, o refactor oportunista, debería ocurrir constantemente. Contribuye a mantener la _deuda técnica_ bajo control al mejorar la representación del negocio en código, pero también contribuye a un mejor conocimiento del código por parte del equipo.

Pero es muy importante entender que este tipo de refactor, como señalaba al principio, se hace en unidades muy pequeñas, pero muy frecuentes: varias veces al día, todos los días.

_Piri is qui isí ni si siqui nidi i pridicciín..._ Nope. Todo esto se aplica mientras trabajas para sacar las historias de usuario a producción.

Buenos recursos para iniciar a los equipos en Refactor Mercilessly:

Aparte de leerse Extreme Programming Explained:

![](images/extreme-programming-explained.png)

Esta charla de Martin Fowler:

![](images/workflows-of-refactoring.png)

Su libro clásico:

![](images/refactoring-second-edition.png)

Y algo propio:

![](images/keeping-code-healthy.png)