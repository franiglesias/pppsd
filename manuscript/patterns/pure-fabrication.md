# Pura fabricación

El patrón GRASP que me quedaba por repasar es _Pure Fabrication_. Es como el patrón de último recurso, o el comodín de la llamada.

El problema que resuelve es el de no poder atribuir una responsabilidad a una clase concreta, fundamentalmente porque no tiene mucho sentido, o ninguno, desde un punto de vista semántico. 

Esto puede ocurrir porque la clase necesita colaborar con otra. O bien porque la idea que se quiere expresar es, de alguna manera, artificial pero necesaria.

Por lo general, pretendemos que un diseño orientado a objetos exprese un modelo del mundo, o al menos de la parte del mundo en la que se desarrolla nuestro negocio. Por eso, sus conceptos, reglas y procedimientos, se representan con objetos.

Sin embargo, a veces necesitamos incluir alguna idea que no forma parte del negocio como tal, pero que nos ayuda a conseguir algo. Creo que un buen ejemplo es el patrón Repositorio.

Un repositorio no existe en el mundo real [^repo]. Necesitamos un repositorio para guardar entidades de dominio (pienso en el repositorio DDD) y reproducir su persistencia en el tiempo y su ciclo vital.

[^repo]; Bueno, puede existir, pero no es un concepto de negocio. 

En DDD un repositorio busca proporcionar _una ilusión de colección en memoria_ de las entidades, de modo que cuando necesitemos usar alguna tengamos algún lugar de donde obtenerla. Representaría la persistencia o continuidad de las entidades del mundo real.

Este concepto de repositorio, pues, es _pure fabricación_. Lo introducimos porque no podemos introducir la idea de persistencia en las entidades sin violar unos cuantos principios de diseño (_active record_, te estamos mirando a ti).

Algunos objetos que siguen el patrón _Mediator_ entrarían también en esta idea de _pure fabrication_. Nos ayudan a evitar acoplamientos directos, introduciendo cierta artificialidad en el modelo. En DDD esto viene siendo un Servicio de Dominio.

Otro ejemplo que se me ocurre es un _identity provider_ y cosas así. De nuevo, no forman parte del dominio modelado, pero nos ayudan a mantener un buen diseño.

Esto no debe ser excusa para introducir _pure fabrication_ para resolver cualquier problema. Como decíamos al principio del capítulo es más bien un recurso cuando hemos agotado otras posibilidades. Voy a intentar poner un ejemplo.

En una aplicación bancaria supongamos que vamos a implementar un servicio de transferencia entre cuentas. Imagina que introducimos un `TransferManager` al que le pasamos las dos cuentas para ejecutar la transferencia.

Sin embargo, no tenemos necesidad, ya que podríamos tener métodos `Account.makeTransfer(DestAccount)` y `Account.receiveTransfer(OriginAccount)`. No hace falta un _Manager_ entre ambas.

De hecho, es posible que si tienes que nombrar a un servicio como _Manager_ o similar, tengas un problema de diseño por _exceso de fabrication_. Así que conviene revisarlo.

En realidad, el exceso de _Managers_ o _Services_ puede derivar del hecho de no tener buenos fundamentos de OOP. Es un tema para otro momento y es el _lamento de Alan Kay_ desde hace décadas.

Puedes ver una explicación sobre el asunto en estos vídeos (capítulos 10 y 11):

![](images/object-oriented-design.png)

Así que con este capítulo se acaban los patrones GRASP.