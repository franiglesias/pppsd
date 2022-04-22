El patrón GRASP que me quedaba por repasar es Pure Fabrication. Es como el patrón de último recurso, o el comodín de la llamada.
🧻👇🏼
El problema que resuelve es el de no poder atribuir una responsabilidad a un clase concreta, fundamentalmente porque no tiene mucho sentido (o ninguno) desde un punto de vista semántico.
O bien porque la idea que se quiere expresar es, de alguna manera, artificial… pero necesaria.
Por lo general, pretendemos que un diseño orientado a objetos exprese un modelo del mundo, o al menos de la parte del mundo en la que se desarrolla nuestro negocio. Por eso, sus conceptos, reglas y procedimientos, se representan con objetos.
Sin embargo, a veces necesitamos incluir alguna idea que no forma parte del negocio como tal, pero que nos ayuda a conseguir algo. Creo que un buen ejemplo es el patrón Repositorio.
Un repositorio no existe en el mundo real (Bueno, puede existir, pero no es un concepto de negocio). Necesitamos un repositorio para guardar entidades de dominio (pienso en el repositorio DDD) y reproducir su persistencia en el tiempo y su ciclo vital.
En DDD un repositorio busca proporcionar “una ilusión de colección en memoria” de las entidades, de modo que cuando necesitemos manejar alguna tengamos algún lugar de dónde obtenerla. En cierto modo, representa la persistencia de las entidades del mundo real.
Este concepto de repositorio, pues, es “pure fabricación”. Lo introducimos porque no podemos introducir la idea de persistencia en las entidades sin violar unos cuantos principios de diseño (active record, te estamos mirando a ti).
Algunos objetos que siguen el patrón Mediator entrarían también en esta idea de pure fabrication. Nos ayudan a evitar acoplamientos directos, introduciendo cierta artificialidad en el modelo. En DDD esto viene siendo un Servicio de Dominio.
Otro ejemplo que se me ocurre es un “identity provider” y cosas así. De nuevo, no forman parte del dominio modelado, pero nos ayudan a mantener un buen diseño.
Esto no debe ser excusa para introducir pure fabrication para resolver cualquier problema. Como decíamos al principio del 🧻 es más bien un recurso cuando hemos agotado otras posibilidades. Voy a intentar poner un ejemplo.
En una aplicación bancaria supongamos que vamos a implementar un servicio de transferencia entre cuentas. Imagina que introducimos un TransferManager al que le pasamos las dos cuentas para ejecutar la transferencia.
Sin embargo, no tenemos necesidad ya que podríamos tener métodos Account.makeTransfer(DestAccount) y Account.receiveTransfer(OriginAccount). No hace falta un “Manager” entre ambas.
De hecho, es posible que si tiene que nombrar a un servicio como Manager o similar, tengas un problema de diseño por “exceso de fabrication”. Así que conviene revisarlo.
En realidad, el exceso de “Managers” o “Services” puede ser un problema de no tener buenos fundamentos de OOP. Es un tema para otro 🧻y es el “lamento de Alan Kay” desde hace décadas.
En este canal de Youtube hay alguna explicación (capítulos 10 y 11) https://youtube.com/playlist?list=PLGLfVvz_LVvS5P7khyR4xDp7T9lCk9PgE
Así que con este 🧻 se acaban los patrones GRASP.