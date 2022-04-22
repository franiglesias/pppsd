Los agregados en DDD… quizá sería mejor hablar de Aggregate Roots (o raíces del agregado)… pero bueno, ¿qué es esto y por qué tengo que saber sobre ellos?

Es fácil ver que los conceptos tienen muchas maneras de relacionarse. Unos conceptos pueden contener otros, referenciarlos o “poseerlos”. Así, por ejemplo, una factura “se refiere” a una cliente, contiene un importe, una forma de pago y tiene “líneas” en las que se detallan los conceptos y precios, entre otras cosas.

Todos ellos “viven” en la factura, aunque de distinta forma. La cliente lo hace de manera independiente, así que la factura solo necesita tener una referencia que las asocie.

Sin embargo, las “líneas” no son independientes. Viven literalmente “dentro” de la factura. No existe la idea de “línea de factura” fuera de ahí. Solo podemos llegar a ellas a través de la factura.

Este conjunto de conceptos relacionados que van juntos y son tratados como una unidad sería un agregado, aunque habitualmente nos referimos a él por su punto de entrada o “raíz del agregado” (aggregate root). 

Pero hay más. DDD tiene mucho que ver con los límites. Cada unidad en DDD (y en OOP si vamos a eso) se encarga de definir unos límites. Por ejemplo, una clase (entidad o value object) define límites de consistencia para los objetos: se crean de forma que sean consistentes, válidos, con todo lo necesario.

Los agregados definen límites de consistencia para el conjunto de entidades que agrupan. Protegen activamente sus invariantes que, en este contexto, son las reglas que rigen sus relaciones internas. Y es la raíz del agregado la que se encarga de ello.
Aplicando el patrón Creator de GRASP, el agregado es responsable de crear o instanciar sus entidades “hijas”, de modo que para añadir líneas a una factura no instancias líneas y las pasas al agregado. En su lugar, pasas los datos necesarios al agregado para que las instancie.

De ese modo, las “líneas” nunca están fuera del agregado. El resto de la aplicación no sabe nada de ellas.


Esto también define límites de transaccionalidad al llevar esto a la persistencia. El agregado se persiste como una unidad y es el repositorio del agregado el responsable de guardar la información como sea más conveniente. En consecuencia, los repositorios reciben y entregan agregados. Un reverso de esto es que solo se persiste un agregado por transacción.

Algunas cuestiones:

Los agregados son conceptos bastante fluidos y lo que es raíz del agregado en un contexto puede no serlo en otro. Ejemplo: una cliente puede ser raíz del agregado y “contener” todas sus facturas. Pero en otro contexto, la raíz del agregado es la factura.

Esencialmente, los agregados son equivalentes a las entidades. Tienen identidad, tienen ciclo de vida. La diferencia es que sus invariantes (reglas de negocio) regulan la relación entre varios objetos, mientras que las entidades son objetos discretos, que se encargan de proteger sus invariantes internas.

¿Un bounded context debe tener solo un agregado? Nope. Un agregado representa un concepto complejo del negocio que está compuesto por varios conceptos relacionados. En un contexto puede haber un único agregado, en otros más de uno. La función de los agregados es representar esos conceptos complejos ofreciendo un único “punto de acceso” y garantizando su consistencia coordinando esos objetos agregados.

Es decir: cada objeto es responsable de su propia consistencia, y la raíz de un agregado es responsable de la consistencia del conjunto agregado.

Aquí una serie de artículos bastante completa acerca de los agregados:

https://www.jamesmichaelhickey.com/domain-driven-design-aggregates/

IMHO diseñaría los agregados “de arriba hacia abajo”. Es decir, considerando primero los conceptos más generales (que podrían acabar siendo raíces de agregado) y bajando luego a los detalles, guiándome por lo que dicen las reglas de negocio que apliquen.

Acerca de la persistencia… me he quedado rumiando en unos temillas sobre persistencia. En este artículo de Matthias Noback se dice que a la hora de diseñar agregados “te olvides” de la persistencia.

https://matthiasnoback.nl/2018/06/doctrine-orm-and-ddd-aggregates/

Lo dice en el sentido de no dejar que las cuestiones de persistencia, que son de infraestructura, condicionen tu diseño del agregado, que es del dominio. De hecho, un poco más abajo propone otra regla: “actúa como si fuesen a guardarse de una base de datos orientada a documentos”. Un noSQL, cosa que encaja realmente bien con la misma idea de agregado. Para entender mejor esto hay que repetir la idea de que “un repositorio no es la puerta de acceso a la base de datos” y añadir que la estructura de tablas en una base de datos relacional no tiene que reflejar la estructura del agregado.

Me dan ganas de repetir esto: si el sistema de persistencia es una base de datos SQL, la estructura de tablas en la bd relacional no tiene que reflejar la estructura del agregado.

Esto quiere decir que a la hora de persistir lo que guardamos es una representación del agregado, no el agregado como tal. Para eso nada mejor que una bd orientada a documentos. Por ejemplo, en un caso de agregado con más de media docena de entidades podrías necesitar tan solo un par de tablas para persistirlo.

Eso puede suponer algo de desnormalización, lo que seguramente hará más sencillo todo con la bd y hasta me atrevería a decir que podría ser bueno en lo que toca a performance.

De hecho, el objetivo sería que el agregado y su persistencia pudiesen evolucionar independientemente. Dentro de lo que cabe, por supuesto. Seguramente los Database Administrator del mundo me quieran dar collejas, pero DDD es “code driven” y es la base de datos la que tiene que adaptarse.

Según E. Evans, desde el punto de vista del dominio, un repositorio es una colección en memoria de agregados, que nosotros tenemos que implementar con algún mecanismo de persistencia no volátil.

Eso sí, tener esos datos en una base de datos nos permite crear servicios que puedan acceder a ellos para otras necesidades de la aplicación, como obtener listados para vistas, sin necesidad de pasar por los repositorios.