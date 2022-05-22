# Abierto para extensión, cerrado para modificación

_Open-Closed_ es la O de SOLID. Se refiere a situaciones en las que un cambio de funcionalidad podría suponer un cambio en un código en producción, como por ejemplo, en una clase, por simplificar. Obviamente no aplica cuando estamos desarrollando o diseñando. Por tanto, insisto en que nos estamos refiriendo a código en producción. Dice así:

> Las clases deberían estar abiertas para extensión y cerradas para modificación.

Tenemos un problema si para modificar la funcionalidad:

* Tienes que volver compilar todos los módulos que usan esa clase. Ahora igual no es tan importante, hace unos años podía ser un marrón.
* El cambio de funcionalidad no se aplica a todos los usos de esa clase, lo cual es problemático, porque podría introducir efectos indeseados en lugares que no esperamos.

En lenguajes interpretados tampoco supone mucho problema pues no tienen tiempo de compilación, pero la posibilidad de introducir errores o cambio indeseado de comportamiento afecta igualmente.

Para prevenir eso se aplica el principio de que las clases sean abiertas a extensión y cerradas a modificación. De este modo, aprovechas la clase extendiéndola sin perjudicar los usos de la clase que no están afectados por el cambio.

Como no se puede predecir el futuro y lo más posible es que _YAGNI_ (no lo necesitarás), tampoco habría que agobiarse en diseñar cada clase para que sea _open-close certified_.

Si, llegado el caso, la clase no está abierta a extensión, lo adecuado es hacer un refactor preparatorio que la _abra_, manteniendo su comportamiento actual, pero permitiendo alguna forma de extensión.

By the way, esto es más fácil si las clases tienen responsabilidades bien definidas y no tienen múltiples razones de cambio.

Pero, por otro lado, tampoco tiene sentido hacer _open-closed_ cualquier clase. Una asunción del principio es que te interesa conservar la funcionalidad de la clase actual. Otra es que duplicarla, creando una clase nueva para la nueva feature, por ejemplo, es demasiado caro por compilación, mantenimiento, etc..

Y es que, en muchos casos, añadir una clase nueva duplicando una existente es una buena solución para el mismo problema. Pero hay que valorar el coste de duplicación frente a los beneficios.

Por otro lado, ¿de qué cambio estamos hablando? En algunos casos puede ser parametrización de un comportamiento, en otros casos de un cambio en el algoritmo, en otros modificar sobre el output.

Para ello tenemos diversos patrones aplicables, como puede ser _Strategy_, en el que el consumidor puede decidir el algoritmo, o _Decorator_, que transforma el _output_ según el consumidor.    

En general, si una clase tiene responsabilidad única es fácil hacerla extensible. Si no, será complicado.

Pero tampoco hay que agobiarse intentando hacer que todo sea _open-closed_ por si acaso. Por encima de cualquier decisión suele estar _YAGNI_, no adivines el futuro, y siempre podemos hacer refactor para abrir las clases cuando toque.