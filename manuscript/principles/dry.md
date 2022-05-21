# No te repitas

Ya que hoy no llueve, hablemos del principio DRY.

Personalmente, creo que en programación tenemos un problema con los acrónimos ingeniosos. El caso es que DRY son las siglas de Don't Repeat Yourself (no te repitas). Es como el Principio de Abstracción de Pierce, pero expresado de una manera menos formal.

Este principio, enunciado por Hunt y Thomas en _The Pragmatic Programmer_, dice que _Toda pieza de conocimiento debe tener una representación única, no ambigua y autoritativa dentro de un sistema._

Toda pieza de conocimiento, ¿lo pillas? No _de código_. El principio DRY no habla de duplicación de código. Pero encontrarás cientos de artículos en Internet que dicen algo como _aplicar DRY para eliminar la duplicación de código._ Seguro que yo mismo he incurrido en eso alguna vez.

Y, a su lado, otro trillón de artículos alertando de lo pernicioso que es el principio DRY que te puede llevar a la _abstracción incorrecta_. O del código WET: _Write Everything Twice_.

Pero no. DRY aplica ni más ni menos que a la duplicación de conocimiento, lo que se refiere tanto a código como a datos. Así, por ejemplo, mantener dos fuentes de verdad y tener que sincronizarlas es un problema derivado de no haber pensado en DRY.

En cuanto a código, DRY puede ocurrir tanto con fragmentos de código similares, la consabida y duplicación de código, como fragmentos diferentes. Quiero decir que el problema no es la repetición literal de código _per se_, sino la duplicación de conocimiento.

Como tantas otras cosas en código, suele ser más fácil de diagnosticar cuanto tienes que introducir cambios: si dos fragmentos de código tienen que cambiar a la vez es muy posible que tengamos una violación del principio DRY.

¡Ah! Pero también del principio de cohesión, pues dos cosas que habitualmente cambian juntas deberían estar juntas. Los que nos dice DRY, a mayores, es que incluso podrían ser la misma, representando el mismo conocimiento.

Obviamente, una duplicación de código puede llevarnos a pensar que estamos ante un problema relacionado con DRY. Pero hay que andarse con ojo aquí.

Como heurística, puedes aplicar la _regla de los 3_: espera a tener al menos 3 ejemplos de duplicación antes de pensar que ahí se esconde una abstracción. Y aún haciéndolo así tienes tres posibilidades:

1. que esa duplicación sea inevitable: fragmentos de código muy similares que se ocupan de cosas diferentes.
2. que no haya una abstracción ahí, pero que sí sea posible reducir la duplicación estructural en ese contexto, posiblemente extrayendo un método.
3. que las duplicaciones sean casos de una abstracción.

Respecto a 2 podría argumentarse que esa duplicación representa un conocimiento en ese contexto reducido, pero no generalizable a todo el sistema, _no-sé-si-me-explico_. Aquí podemos aplicar la _regla del tres_, que nos dice que no intentemos resolver la duplicación hasta no tener al menos tres casos.

Por esa razón, se recomienda evitar las abstracciones prematuras: ¿cambian esos códigos repetidos a la vez o lo hacen por separado? Si no cambian a la vez, posiblemente están representando conocimientos diferentes.

DRY es un principio necesario para garantizar que un sistema tiene fuentes únicas de verdad y contribuir de este modo a su consistencia. Pero DRY no es un principio orientado a eliminar la duplicación de código. Esta es solo un indicio, o _smell_, de una posible duplicación de conocimiento.

En resumen, DRY:

* Una sola fuente de verdad para cada conocimiento en el sistema
* Si cosas diferentes cambian juntas: aplica cohesión y DRY
* Duplicación de código no implica necesariamente una abstracción

