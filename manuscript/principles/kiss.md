# Hazlo estúpidamente simple

_KISS_ no es la banda de _glam rock_, ni un beso. Es un principio formulado por Kelly Johnson, ingeniero de la Lockheed. Allí participó en el diseño de una buena lista de aviones militares, muchos de los cuales son hitos de esa industria. Su enunciado:

> Keep it simple stupid (sin coma).

Efectivamente, la forma original no lleva coma y pierde ese matiz borde de “que sea simple, estúpido”. La estupidez se refería al diseño y no al diseñador. O puede que fuese:

> Keep it simply stupid.

¿En qué sentido debería ser estúpido un diseño?

Primero, un poco de contexto sobre el principio. Un avión militar no es una cosa sencilla, sino bastante compleja. El propósito de Johnson era diseñar aviones cuyos elementos fuesen fáciles de reparar en condiciones adversas, como no disponer de personal cualificado, situaciones de combate, escasez de repuestos, etc.

Así que la idea era mantener los componentes simples y fáciles de reparar, sin grandes sofisticaciones que requiriesen personal o herramientas muy especializadas.

Aplicado al desarrollo de software, podríamos interpretarlo como desarrollar componentes que sean _estúpidos_ y _simples_: poco inteligentes, fáciles de comprender en un vistazo, en los que sea muy sencillo entender lo que ocurre y cómo funcionan.

Una forma de lograr esto, a posteriori, es descomponiendo partes de código muy enrevesadas y complejas en funciones o métodos pequeños con nombres descriptivos, de forma que cada una de ellas sea fácil de entender aisladamente.

Otra manera de lograrlo es escogiendo soluciones sencillas en primer lugar. Por ejemplo: un test _KISS_ solo probaría una cosa, con un único ejemplo. Una función _KISS_ usaría código simple, tomando pocas decisiones. Para tomar decisiones complejas combinaríamos varias funciones _KISS_.

Es difícil explicar esto último sin un ejemplo, pero toda la idea de _programar sin `if`_ de la orientación a objetos es muy _KISS_. Parece complicada, pero en realidad apuesta por tener pequeños elementos que son muy fáciles de entender aisladamente. La clave es tomar primero la decisión de qué objeto simple deberá realizar un trabajo, en lugar de tener objetos complejos que toman decisiones. 

La composición de objetos también es muy _KISS_, porque permite construir comportamientos complejos a base de combinar objetos simples.

Es decir: _KISS_ va de tener elementos que tomados por separados resultan estúpidamente simples, pero combinados desarrollan comportamientos que pueden ser tremendamente complejos.

Al tener componentes muy simples es fácil cambiarlos por otros, es fácil detectar y corregir errores, es fácil entenderlos y razonar sobre ellos, podemos tener todo su código en la cabeza, por así decir, y es muy fácil probarlos unitariamente.

La sencillez es la sofisticación definitiva. Pero hacer cosas sencillas conlleva mucho trabajo.