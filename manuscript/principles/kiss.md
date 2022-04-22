# Hazlo estúpidamente simple

KISS… no es la banda de rock, ni un beso… es un principio de diseño formulado por Kelly Johnson, ingeniero de la Lockheed. Allí participó en el diseño de una buena lista de aviones militares, muchos de los cuales son hitos. Su enunciado:

Keep it simple stupid (sin coma) 🧻👇🏼
Efectivamente, la forma original no lleva coma y pierde ese “matiz” de bordería “mantenlo simple, estúpido”. La estupidez se refería al diseño. ¿En qué sentido debería ser estúpido un diseño?
Primero, un poco de contexto sobre el principio. Un avión militar no es una cosa sencilla, sino bastante compleja. Pero el propósito de Johnson era diseñar aviones cuyos elementos fuesen fáciles de reparar en condiciones adversas (personal no cualificado, combate, escasez…)
Así que la idea era mantener los componentes simples y fáciles de reparar, sin grandes sofisticaciones que requiriesen personal o herramientas muy especializadas.
Aplicado al desarrollo de software, podríamos interpretarlo como desarrollar componentes que sean “estúpidos” y “simples”: poco inteligentes, fáciles de comprender en un vistazo, en los que sea muy sencillo entender lo que ocurre y cómo funcionan.
Una forma de lograr esto (a posteriori) es descomponiendo partes de código muy enrevesadas y complejas en funciones o métodos con nombres descriptivos, pero que cada una de ellas sea fácil de entender aisladamente.
Otra forma es escogiendo soluciones sencillas en primer lugar. Por ejemplo: un test KISS compliant sólo probaría una cosa, con un ejemplo. Una función KISS compliant usaría código simple, tomando pocas decisiones. Para tomar decisiones complejas combinaríamos varias funcs KISS.
Es difícil explicar esto último sin un ejemplo, pero toda la idea de “programar sin hfs” de la orientación a objetos es muy KISS, parece compleja, pero en realidad apuesta por tener pequeños elementos que son muy fáciles de entender aisladamente.
Lac composición de objetos también es muy KISS, porque permite construir comportamientos complejos a base de combinar objetos simples.
Es decir: KISS va de tener elementos que tomados de uno en uno resultan estúpidamente simples, pero combinados desarrollan comportamientos que pueden ser tremendamente complejos.
Al tener componentes muy simples es fácil cambiarlos por otros, es fácil detectar y corregir errores, es fácil entenderlos y razonar sobre ellos, podemos tener todo su código en la cabeza por así decir, y es muy fácil testearlos unitariamente.
La sencillez es la sofisticación definitiva. Pero hacer cosas sencillas conlleva mucho trabajo.