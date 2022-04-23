# Entidades

Toda aplicación, por pequeña que sea, tiene que contener un modelo del mundo. Al menos de la parte del mundo que es su dominio. En DDD esto se hace de forma intencionada y explícita, pero con frecuencia, usamos metodologías menos rigurosas y el modelo queda difuso.

Incluso el típico primer programa para sumar dos números contiene un modelo de ese dominio en el que representamos conceptos como sumandos, operación y resultado. Solo que solemos mezclarlo con la presentación y otros.

Por ejemplo: print (a + b) a y b son los sumandos, + representa la suma y (a+b) el resultado. He aquí un modelo de un dominio muy pequeñito y limitado. Pero es un modelo de ese trocito del mundo.

Claro que nosotras solemos trabajar modelando dominios bastante más complicados que ese, que implican diversos conceptos e interacciones entre ellos. Incluso aunque no hagas DDD, ser consciente de esto y expresarlo en código de forma separada es una gran inversión.

Como ya hemos comentado, en DDD la capa de dominio es una representación en código del modelo que no tiene más dependencias que el propio lenguaje de programación. Es decir, el dominio se expresa mediante objetos puros del lenguaje en que se desarrolla.

Nota sobre DDD y programación funcional: Eric Evans deja claro que DDD nace en el paradigma de Orientación a Objetos.

En este punto se introducen los llamados _building blocks_: entidades, value objects, servicios y eventos de dominio. (¿Cabría considerar aquí los agregados?… bueno, ya veremos)

Estos _building blocks_ también se podrían utilizar aunque no hagas realmente DDD, es decir, si quieres tener una capa de dominio con un modelo rico.

Antes de continuar, una nota superimportante: la capa de dominio es agnóstica acerca de la tecnología de persistencia. Es decir, la capa de dominio no sabe nada acerca de bases de datos o whatever sistema de persistencia… pero me estoy adelantando.

En este capítulo quería hablar de las Entidades

Las entidades son la representación de conceptos del dominio que tienen:

* identidad: cada instancia es diferente aunque tenga las mismas propiedades.
* ciclo de vida: el estado cambia a lo largo de ese ciclo.
* comportamiento

Estas entidades nos interesan por su identidad.

Identidad es eso tan difícil de definir en la vida real, pero que sin embargo percibimos en nosotras mismas, en las demás personas, en los animales, en los objetos. Esa identidad persiste a pesar de los cambios que suceden en el tiempo.

Siempre es el mismo río, pero con distinta agua.

Esa identidad la podemos representar con cierta facilidad mediante una propiedad específica, un identificador que es único en el contexto de la aplicación (aunque puede ser único en un contexto más amplio usando identificadores universales UUID)

(Nota, no es obligatorio usar UUID, pero actúa como si lo fuese por el bien de tu salud mental y la de tu aplicación)

La identidad de las entidades representa la identidad de los objetos del mundo real. Nos permite trabajar con un ejemplo concreto, por eso la necesitamos.

La identidad persiste en el tiempo… he usado la palabra persiste con intención. En un mundo ideal, las entidades estarían en la memoria del sistema durante todo su ciclo de vida. Pero en el mundo real los ordenadores se paran, se reinician.

Necesitamos una forma de persistir la identidad en el tiempo. DDD introduce el concepto de repositorio para lograr esto y, ojo a la definición: un repositorio proporciona la ilusión de una colección en memoria en la que se pueden guardar o recuperar entidades.

Una ilusión de colección en memoria.

No un acceso a una base de datos. Esto es superimportante entenderlo bien. Los repositorios no son la puerta de acceso a la base de datos. Puedes implementarlos con una tecnología concreta de base de datos, pero no es el acceso a ella.

Si el dominio necesita crear una entidad, lo hace y mientras no la usa, la pone en el repositorio y la recupera por su identidad cuando sea necesario. El cómo se las arregla el repositorio para hacer eso no le interesa al dominio para nada.

Si la entidad contiene dentro colecciones del otras entidades hijas (por ejemplo Pedido/Items) es problema de la implementación del repositorio lidiar con los detalles de cómo guardarlas o recuperarlas del almacenamiento físico. Pero el dominio solo ve que pone allí Pedidos y puede recuperar Pedidos por su id. Y quien dice Entidades, dice Agregados, pero esa es otra historia.

Las entidades tienen ciclo de vida, esto es: se crean, hacen cosas y les pasan cosas y pueden llegar a _morir_ de algún modo. Por ejemplo, un pedido se inicia, se le añaden productos, se prepara, se envía, se factura y, una vez entregado y todo en orden, acaba su proceso.

También tienen comportamiento. Todos esos pasos del proceso cambian el estado de la entidad, pero es cosa de la entidad mantener su estructura interna, cumplir la reglas de negocio y las invariables. Por ejemplo, el pedido puede añadir productos como items del pedido.

O puede ser facturado, enviado, etc, etc. Todo esto se refleja en sus comportamientos: `Order.start`, `Order.addProduct`, `Order.invoice`, `Order.cancel`… En cada uno de estos comportamientos, `Order` tiene que asegurar que se cumplen las reglas de negocio.

Por ejemplo: solo se pueden añadir 3 productos del mismo tipo. Pues de eso se encarga `Order` en `addProduct`. Que solo se puede facturar un pedido si tiene productos, que no se puede cancelar un pedido facturado, etc. De todo eso, al ser reglas de negocio se encarga `Order`. Para eso es el Information Expert.

Podríamos decir que `Order` es aquí un agregado, pero me gustaría dedicar un capítulo a eso específicamente. Pero sí, sería un agregado.

Así que ahí tenemos a las entidades, representando conceptos de nuestro dominio con identidad. Como veremos las entidades pueden incluir Value Objects. Además, las entidades generan Eventos de Dominio. Ya tendrán su capítulo también.

¿Qué como persistimos entidades en un repositorio o cómo las buscamos? Lo hablamos en otro capítulo, porque hacerlo realmente bien, sin acoplarse a la tecnología de persistencia completa da cierto trabajo, pero diría que merece la pena.