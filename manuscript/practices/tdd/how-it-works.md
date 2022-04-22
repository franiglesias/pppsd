# Cómo funciona TDD

Voy a intentar explicar por qué funciona Test Driven Development. No cómo se hace, sino más bien los mecanismos que hacen que partiendo de un test, se pueda desarrollar código de producción. 

Como sabemos TDD consiste en escribir primero un test que describa un comportamiento que deseamos implementar en software. Un test, en realidad, no es otra cosa que un programa que invoca una unidad de software y verifica que se ha generado un resultado específico.

Entendamos unidad de software algo que se puede ejecutar, independientemente de su tamaño o su forma. El resultado puede ser tanto una respuesta de esa unidad como un efecto en alguna parte. Para simplificar, imaginemos que la unidad es una función o un método de un objeto.

Según la 1ª ley de TDD no se escribe nada de código de producción sin un test previo que falle. Así que sea cual sea el primer test siempre fallará porque no hay código que se pueda compilar o interpretar.

Obviamente el primer requisito para que un código se ejecute y tenga un comportamiento observable es que exista. Y el requisito para que un test se ejecute es que la unidad bajo test se pueda importar, instanciar y ejecutar.

Por ese motivo, el primer test no debería ir más allá de requerir la existencia del código de producción y no más que lo que exige el lenguaje para que el test pueda correr. Para conseguir esto tienes que añadir código hasta que el test deje de fallar.

Los tests pueden fallar por dos tipos de motivos:

* errores relacionados con la compilación: el código tiene que poder compilarse/interpretarse y ejecutarse.

* errores relacionados con el comportamiento: el código puede ejecutarse pero no realizar el comportamiento deseado.

Los errores relacionados con la compilación tienen que ver con todo lo que es la sintaxis del lenguaje, pero también podrían tener que ver con detalles de uso de frameworks, configuraciones, etc (esto si estamos haciendo outside-in tdd, por ej., testeando contra un endpoint, etc)

Tenemos que corregir esos errores hasta hacer que el test falle por la razón correcta: que el código de producción no implementa el comportamiento.

Este es el punto clave de todo. En TDD un test debe fallar solo porque aún no existe un código en producción que lo haga pasar.

La 2ª ley de TDD nos dice que este test debería ser lo más pequeño posible. Una forma de asegurarse es que el test solo pueda fallar por una única razón. Esto puede ser difícil de entender al principio.

Si no hay código, la razón por la que fallará el test es porque no existe la unidad bajo test. Por eso, en ese primer test, no deberíamos hacer aserciones sobre comportamiento. solo cuando tenemos la seguridad de que la unidad es ejecutable las introducimos.

El test, entonces, sería una especificación formal de comportamiento de la unidad bajo test, por lo que la tarea de desarrollo consiste en introducir el código que haga pasar ese test (sin hacer fallar cualquier otro test existente sobre la misma unidad).

Además de formal, el test es una especificación operativa: nos dice cómo tiene que comportarse la unidad a través de su ejecución en un cierto contexto (que incluye los parámetros que recibe la unidad, etc).

Hay muchos códigos posibles que podrían hacer pasar el test. Por ejemplo, si testeo la función sum(a, b) para sum(2, 3) == 5, me bastaría devolver 5 (sin realizar ningún cálculo) o hacer bucles _for_ contando y acumulando. Da igual mientras el test pase.

Entonces tenemos la 3ª ley, que nos dice que solo añadimos el código de producción suficiente para hacer pasar el test. No más. Así que entre las infinitas posibilidades escogemos la más sencilla, que muchas veces es devolver la respuesta tal y como se espera en el test.

Esto provoca que el test pase, estableciendo la _línea base_ de comportamiento de la clase en ese escenario. Una vez que tenemos esto, es cuando podemos introducir refactoring porque el comportamiento está definido (aunque muy limitado)

En el ejemplo anterior, nuestro código es correcto para todas las sumas de dos número que den 5 como resultado. Fallará en todas las demás… porque no hay código que se encargue de ellas.

Sin embargo, para que el algoritmo pueda cambiar (incluso aunque sepamos de antemano cómo es ese algoritmo) tenemos que introducir nuevos ejemplos en forma de tests que provoquen la necesidad de introducir los cambios requeridos en el algoritmo.

En nuestro ejemplo de la suma, tendríamos que introducir un nuevo test con datos de ejemplo que sumados NO den 5, ya que es la manera de hacer que el test falle. Si introdujésemos un test para una suma de resultado 5 pasaría, lo que NO nos aporta información para añadir código

de producción, ya que el test verifica el mismo comportamiento que la unidad de software ya implementa.

Si introduces un ejemplo como sum(2,4) = 6 estás _cuestionando_ la implementación existente, lo que obliga a introducir algún cambio. Se podría decir que al añadir un test estás haciendo la hipótesis de que la unidad de software implementa un comportamiento.

Como el test falla, la hipótesis no se verifica y tienes que cambiar el código de producción para conseguirlo. De nuevo, da igual el código que escribas si:

* el test nuevo pasa

* todos los tests anteriores siguen pasando

Cuando el nuevo test pasa (junto los anteriores) se ha establecido una nueva línea base de comportamiento. La unidad bajo test es capaz de cubrir más casos. Esto te permite refactorizar ya que el comportamiento (hasta ahora) está definido y eres libre de cambiar el código siempre

que se mantengan los test funcionando. Los test que pasan garantizan el comportamiento, si dejan de pasar, es que has _eliminado_ parte de ese comportamiento. (los test de TDD se convierten en tests de regresión una vez los haces pasar).

El ciclo se repite hasta que no puedes imaginar un nuevo test que pueda cuestionar la implementación existente.

Esto es posible también porque los tests son especificaciones replicables: puedes ejecutarlos una y otra vez obteniendo los mismos resultados.

Así que, en resumen, se podría decir que TDD consiste en someter a prueba una unidad de software para ver en qué falla, de modo que el test nos diga exactamente qué es lo que necesitamos hacer.

Incluso aunque no exista código.