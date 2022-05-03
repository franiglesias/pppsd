# Bajo acoplamiento

Low Coupling, otro de los patrones GRASP. Y es que este tema del acoplamiento es más que importante, es fundamental.

Así que primero hablaremos de qué es el acoplamiento, por qué debería preocuparnos y cómo conseguir bajo acoplamiento.

El término se lo debemos a Larry Constantine, junto con el de cohesión, del que hablamos en otro capítulo. Coupling o acoplamiento es el grado de interdependencia entre dos unidades de software. Por ejemplo, entre dos objetos.

El acoplamiento es algo inevitable si queremos que dos objetos colaboren. Esto es, si seguimos principios como Single Responsibility, Polimorfismo, etc., tendremos objetos pequeños que colaboran. Para que puedan colaborar, tendrán dependencias unos de otros. No existe el acoplamiento cero. Por esa razón hablamos de alto o bajo acoplamiento (o tight/loose — fuerte/débil). En otras palabras: el problema no está en la existencia de acoplamiento, sino en el grado de acoplamiento y en tenerlo controlado.

Si tenemos una clase `Consumer` y otra ``Service``, siendo así que `Consumer` usa `Service` para hacer algo, decimos que `Consumer` tiene una dependencia de `Service` y está, de hecho, acoplada a `Service`. Una forma de medir esto es preguntarse: ¿Cuánto necesita saber `Consumer` para poder utilizar `Service`? Cuantas más cosas, más acoplamiento. Cuantas menos cosas, menos acoplamiento. Así, por ejemplo, lo menos que debería saber `Consumer` son los mensajes que tiene que enviar a `Service` y parámetros. Supongamos que el mensaje en cuestión es `Service`::doSomething.

Menos que eso es no poder usar `Service`. Pero más que eso es incrementar el acoplamiento. ¿De qué conocimiento extra estamos hablando? Pues por ejemplo:

* Conocer el tipo concreto de `Service`
* Saber instanciar un `Service`
* Saber encontrar un `Service`
* Conocer propiedades de `Service`

S. Martín de Fowler llama a esto “inappropriate intimacy”, cuando un objeto sabe demasiado de otro objeto.

Conocer un tipo concreto de `Service` significa usar una implementación concreta. Para evitar eso aplicamos la Inversión de dependencias, haciendo que `Consumer` dependa de una Interfaz.

Saber instanciar un `Service` ocurre cuando hacemos new de un `Service` dentro de `Consumer`. Este tipo de dependencia puede hacer no testeable a `Consumer`. Para evitarlo, usamos el patrón de Inyección de dependencias, vía constructor o vía setter.

Saber encontrar un `Service` suele implicar que tenemos un smell _Service Locator_. Esto pasa por acoplarnos al contenedor de inversión de dependencias para pedírselas desde cualquier sitio que nos venga en gana. De nuevo, aplicar la inyección de dependencias correctamente es la solución.

La herencia genera el mayor acoplamiento posible, ya que no puedes usar una clase sin sus ancestros, por eso hay que tener mucho cuidado cuando decidimos usar el mecanismo de herencia. Debería limitarse a especializaciones, y no para "compartir" comportamiento.

En resumen, para mantener el acoplamiento bajo entre dos objetos hay que:

* Inyectar las dependencias: no instanciarlas dentro de otros objetos. Ojo a la distinción entre objetos newables e injectables ![](images/to-new-or-not-to-new.png)
* Aplicar el principio de Inversión de Dependencias y depender de las interfaces, no de las implementaciones.
* Mantener aisladas las dependencias dentro del objeto que las usa. Utiliza métodos privados cuando tengas que delegar en la dependencia, de modo que no aparezcan menciones a ella en ninguna otra parte del código.
* Nunca, pero nunca, inyectes el contenedor de inyección de dependencias. Nunca, _never_, ni se te ocurra.

¿En qué nos beneficia el bajo acoplamiento? El código con bajo acoplamiento es fácil de testear, ya que todos los colaboradores de una clase son fácilmente reemplazables por dobles en tests unitarios o fakes en tests de integración.

Es fácil de extender por las mismas razones. Hay pocos puntos en los que tocar en caso de necesitar introducir nuevos comportamientos. Es más posible que solo tengas que añadir código, en lugar de tener que borrar o modificar. El bajo acoplamiento facilita cumplir open/close.

Es incluso más fácil detectar los errores y dónde se producen porque si se produce un fallo seguramente podrás identificar la pieza de software que falla o aquella que controla esa fallo. En una situación de acoplamiento, el error se produce en `Consumer` aunque sea de `Service`.

El acoplamiento es especialmente peligroso cuando la dependencia es con módulos de software que no controlamos, particularmente _vendors_. Para usarlos deberías aplicar siempre inversión de dependencia, introduciendo patrones de indirección, como _Adapter_.

Si te acoplas a _vendors_, en caso de que estos cambien, tu aplicación se verá afectada. Es posible que para evitar esos efectos decidas quedarte en una versión concreta de ese veedor, lo cual introduce riesgos de seguridad, de finalización de mantenimiento, de _performance_… es MAL.

Pero el MAL, ¿eh? Sufrimiento, llanto y rechinar de dientes.

Así que, ya sabes: procura que tus objetos sepan lo mínimo de los objetos de los que dependen. Depende las interfaces, inyecta las dependencias, mantenlas aisladas, usa patrones de indirección.

Mantener a raya el acoplamiento es salud. La de tu aplicación y la tuya.