# _TDD_ no son tests, son ejemplos

Estoy buscando formas nuevas de explicar lo que es _TDD_, _Test Driven Development_. El mayor problema es, por supuesto, que el nombre no ayuda. Cierto que _TDD_ consiste en escribir primero un test que defina el comportamiento que queremos desarrollar usando un ejemplo del mismo.

Por esa razón, algunas personas proponen usar la expresión _Specification by example_ (Especificación mediante ejemplos) que captura mejor lo que hacemos en el proceso _TDD_: poner ejemplos del comportamiento deseado especificando el contexto, los datos de entrada y lo que esperamos que suceda como consecuencia del comportamiento, ya sea una respuesta o un side effect.

El hecho de usar _Test_ en el nombre también tiene el efecto negativo de que mucha gente piensa en lo difícil que resulta a veces testear su código. Precisamente, es difícil porque ese código no está diseñado para ser testeado, probablemente requiere mucha preparación, un _smell_ a la hora de hablar de tests, y puede que hasta sea imposible ponerlo bajo test tal como está.

Eso se previene haciendo _TDD_.

En fin. Como se ha dicho muchas veces _TDD_ no es testing, sino desarrollo y diseño, aunque la herramienta que utilizamos sea la misma: los tests automáticos. Y lo que debe hacer un test de _TDD_ es mostrar un ejemplo del comportamiento.

En este punto se plantea el problema de cómo tienen que ser esos ejemplos. Y aquí viene la típica historia de _empezar por el caso más sencillo_. En realidad, lo correcto sería decir algo así como _el ejemplo más sencillo_. _Caso_ es terminología de testing.

Tampoco tengo claro que decir _el más sencillo_ sea un buen consejo. A decir verdad, cualquier ejemplo nos valdría para el primer test porque nuestro primer código de producción va a ser devolver una constante. Los siguientes ejemplos son los que moverán el desarrollo.

Sin embargo, si prevemos que ciertos ejemplos van a ser más fáciles de desarrollar puede ser buena idea empezar con ellos. Pero en realidad, lo que nos interesa es desarrollar el siguiente comportamiento que nos interese más, por razones de negocio/dominio.

Una cosa que se suele pasar por alto es cual es la función de cada fase del ciclo de _TDD_.

La primera es el test que falla. Esta fase define el comportamiento que queremos alcanzar para un ejemplo concreto. Este ejemplo representa un comportamiento que no existe aún y que nos interese implementar a continuación, posiblemente por razones de negocio.

El test adecuado debería construirse de una forma trivial: instanciar el componente bajo test, utilizarlo con los datos de ejemplo y verificar que la respuesta es la que se espera.

La siguiente fase es añadir el código de producción necesario para que el test que fallaba, pase. Esta fase busca establecer la _línea base_ de comportamiento hasta ese momento. No implica implementar el algoritmo completo. Solo lo suficiente para tener el nuevo comportamiento a la vez que se mantiene el que ya existía. Es decir, se trata de poner el test en verde cuando antes y establecer la red de seguridad para la fase de refactor. En este punto nos bastaría devolver la respuesta esperada tal cual o abrir una condicional para un ejemplo.

La tercera fase es la de refactor. En _TDD_ clásica esta fase busca introducir o mejorar el diseño de la solución mediante la identificación de oportunidades de generalizar un algoritmo para los ejemplos de que disponemos en el test, sin preocuparse de los que puedan venir después.

Esto se puede hacer aplicando las técnicas de refactoring comunes, buscando los smells generados por las implementaciones simples que hacemos en la segunda fase. Es fundamental mantener todos los tests existentes pasando, lo que garantizará que mantenemos el comportamiento.

Así que en resumen, _TDD_ o especificación mediante ejemplos es:

* Ilustrar mediante un ejemplo el comportamiento que deseamos implementar a continuación, para lo que usamos un test.
* Implementar la solución más obvia posible.
* Eliminar los _code smells_ refactorizando.

Decimos muchas veces que _TDD_ no es testing. Es que no lo es, pues forma parte del proceso de diseño.

Sin embargo, tiene un side-effect interesante al proporcionarnos una batería de tests base. Esta batería necesita cierta limpieza, ya que tras el proceso de _TDD_ pueden quedar muchos ejemplos por caso, un caso se puede representar con uno o más ejemplos, que hacen los tests redundantes y se pueden eliminar.

También se eliminarán algunos tests que han servido para mover el desarrollo, pero no que no aportan nada al proceso de verificación.

Dependiendo de tu enfoque al hacer _TDD_ puedes tener distintos niveles de testing. Por ejemplo, si haces BDD posiblemente con ello tengas un test de aceptación que ejercita el sistema desde fuera. Además de varios tests unitarios.