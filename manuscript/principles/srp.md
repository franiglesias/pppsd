# Única responsabilidad

_Single Responsibility Principle (SRP)_ es uno de los principios de diseño orientado a objetos que más discusiones provoca. Todo gira en torno a la idea de _Responsibility_: ¿qué significa? El principio dice que:

> Las unidades de software solo deberían tener una responsabilidad.

A veces esto se interpreta como _las clases solo deberían hacer una cosa_. Pero este camino es una vía muerta porque:

* no define cuál es el alcance de esa _cosa_.
* puede llevar a diseños excesivamente complicados.

El _SRP_ está modulado por otros principios. En realidad todos los principios de diseño OO se modulan mutuamente.

El _SRP_ _extiende_ del más general _separation of concerns_: partes distintas del software se ocupan de asuntos distintos. Pero la magnitud de la separación depende del principio de cohesión: lo que cambia junto permanece junto y se separa lo que no cambia.

Una de las claves del _SRP_ está en mantener ese equilibrio, pero la otra clave es cómo se define la responsabilidad de una clase.

La propuesta de Robert C. Martin es que responsabilidad es una única razón para cambiar. Por tanto: las clases solo deberían tener una única razón para cambiar. Obviamente, esto no zanja el problema: ¿Qué es tener una única razón para cambiar?

En realidad, habría que pensar más en _agentes de cambio_. Un ejemplo sería una clase que pueda esperar cambios por parte de varios equipos en una empresa, como podrían ser Finanzas y Clientes, o Adquisición y Ventas.

Los cambios originados en uno de los equipos podrían ser indeseables para el otro. Cuando estamos en esta situación lo apropiado sería repartir las responsabilidades o razones de cambio en diferentes clases, incluso aunque representen el mismo concepto.

Pero esto, a su vez, tiene múltiples formas de manifestarse. El ejemplo anterior, desde una perspectiva de _DDD_, nos estaría diciendo que un mismo concepto puede ser visto de manera diferente según el contexto: _Bounded Contexts_.

Claro que lo anterior puede ocurrir en el caso del diseño de la capa de dominio en una aplicación de negocio. Es un nivel muy alto de abstracción. ¿Aplica el _SRP_ en niveles más bajos? Yo diría que sí.

Por ejemplo, es buena idea separar la obtención del contenido de un archivo y su procesamiento. De hecho el primer paso es muy genérico, mientras que el segundo es específico de nuestra aplicación y cambia por razones diferentes: unas técnicas y otras de dominio.

A su vez, la obtención del archivo puede tener varias razones para cambiar. Por ejemplo, será distinto si usa el sistema de archivos local, S3, FTP... Con _SRP_ en lugar de una clase que _lea_ cualquier tipo de sistema, tendríamos clases diferentes, seleccionables por su consumidor.

Esto es: separo obtención y procesamiento, pero también separo distintas estrategias de obtención. La cuestión es que el principio actúa a la vez sobre distintos niveles de abstracción:

El servicio que se ocupa de obtener el resultado final tiene la responsabilidad de procesar un archivo. Y para ellos usa como colaboradores un módulo que obtiene archivos y otro que los analiza.

El módulo de obtención tiene la responsabilidad de obtener una representación procesable del archivo físico, para lo que usa distintos adaptadores y posiblemente una factoría para escoger el adecuado.

A su vez, cada adaptador es responsable de entenderse con el sistema _físico_ que almacena los archivos. La factoría sabe como montar cada adaptador.

El módulo de procesamiento tiene la responsabilidad de convertir la representación recibida en lo que sea que es importante para el dominio de la aplicación.

Parece como que el servicio tiene muchas razones para cambiar al englobar todos los componentes. Sin embargo, el servicio ignora los detalles de esos componentes, su única responsabilidad es coordinarlos y cambiará si esa coordinación cambia.

La responsabilidad del módulo de obtención es cargar el contenido del archivo y delega el entenderse con el sistema físico al adaptador que toque. Su responsabilidad es entregar el contenido, para lo cual coordina varias cosas: elegir el adaptador y entregar su salida.

La responsabilidad de un adaptador sería entregar el contenido del archivo indicado en la forma que se le pide. Hace varias cosas, como comunicarse con el sistema físico y transformar los datos para el módulo superior los pueda manejar.

En resumen: cada nivel de abstracción nos proporciona un contexto en el cual interpretar y aplicar el _SRP_.

Otra forma de verlo es que al aplicar el _SRP_ podemos usar varias estrategias. A veces tendremos que separar en un mismo nivel de abstracción y otras veces tendremos que separar y delegar cada parte.

El _SRP_, bien aplicado, ayuda a que el software sea más mantenible al delimitar las fuentes de cambio de una clase. Pero hacer que las clases sean _SRP_ puede hacer que los diseños ganen cierta complejidad.

Obviamente, es un compromiso, pero diseñar es básicamente decidir qué compromisos estamos dispuestas a aceptar.