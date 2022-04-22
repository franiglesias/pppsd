# Sobre la persistencia en DDD

Hay un temilla relacionado con DDD sobre el que me han preguntado varias veces, aunque no es exclusivo de DDD, sino de cualquier tipo de arquitectura limpia, incluyendo la Hexagonal… LA PERSISTENCIA.

🧻👇🏿

O incluso diría que más que la persistencia, el tema es: cómo tratar la relación entre Entidades de dominio y bases de datos. Si sí, si no o si todo lo contrario.

Porque cómo va a ser que una aplicación no tenga base de datos, dónde va a parar. Que una aplicación sin base de datos no es nada, es una mindundi de las aplicaciones, el nivel más bajo del escalafón.

Pues todo se resume en una frase sencilla: la base de datos es un detalle de implementación.

Y ya.

Veamos. La cuestión clave es que DDD define la capa de dominio como agnóstica del mecanismo de persistencia. En otro 🧻 mencioné que un repositorio no es más que un espacio en memoria en donde _guardamos_ las entidades/agregados para cuando necesitemos usarlas.

Y, de hecho, un repositorio no tiene más métodos que los necesarios para guardar o recuperar entidades individuales o grupos de entidades que cubran un criterio.

Desde el punto de vista del dominio eso es lo único que sabemos. El cómo se las arregla el repositorio para hacerlo es SU problema y si guarda las cosas en la RAM, en un disco o en configuraciones cuánticas entrelazadas es SU problema, no problema del dominio.

En esencia, lo que se pretende decir es que el dominio se debe modelar sin pensar en que la información se persistirá con una tecnología concreta. De hecho, entidades y agregados exponen comportamientos que podemos invocar enviándoles mensajes. No sabemos nada de sus propiedades.

Las propiedades de entidades/agregados/de cualquier objetos son SU problema. Orientación a objetos: information hiding, de los information hiding de toda la vida.

El problema viene porque, por lo general, los mecanismos de almacenamiento requieren acceder a la estructura interna de las entidades/agregados, acceder a sus propiedades de alguna manera. Incluso bbdd orientadas a objetos tienen que serializarlos en forma de documentos o algo.

En fins. Veámoslo ahora desde otro prisma. Con frecuencia usamos alguna librería o framework que nos ofrece un patrón para lidiar con una tecnología de base de datos. Lo típico sería una base de datos relacional con SQL. Así que se han inventado patrones como Active Record, etc.

O librerías de ORM, que gestionan por nosotras las transformaciones entre objetos del lenguaje y su representación en un sistema de base de datos. Y aquí es donde empieza el lío porque estas librerías nos van a ofrecer extender sus modelos para crear los nuestros (active récord).

O bien nos van a dar ciertos requisitos para crear nuestras entidades de modo que sean _persistibles_, o que se puedan mapear de alguna manera (verbigracia, con annotations o así).

Esto presenta algunos problemas bastante gordos. Con Active Record tenemos una violación del SRP: toda entidad tendrá dos responsabilidades/razones para cambiar: la suya propia y las derivadas de saber persistirse….

… esto es porque en Active Record un objeto es como un _proxy_ a una fila de una tabla de una bd y a sus relacionadas. Si hay que cambiar algo para la persistencia la entidad tendrá que cambiar. Aparte seguramente no podrás testear estas entidades aisladamente y necesitarás…

… ¡tachán! una bbdd activa para poder hacer un tests. Esto pinta bastante mal.

Y con otros patrones la cosa mejora más o menos, porque tus entidades de dominio pueden verse _contaminadas_ por necesidades del ORM, como tener que exponer getters/setters o propiedades públicas. Y no queremos eso en nuestras entidades de dominio, right?

[— Insertar aquí meme Anakin-Padmé —]

Esto es un follón de narices porque finalmente tenemos que aceptar algún tipo de compromiso. @matthiasnoback propone algunas soluciones aquí

Preview

Creo que la raíz de las dificultades está en que normalmente consideramos la base de datos como algo _nuestro_ e inherente a la aplicación y nos cuesta mucho entender que lo que guardamos en la base de datos no es otra cosa que una representación de nuestros objetos de dominio.

Por otro lado, esta representación no tiene que ser isomórfica a las entidades, pero sí contener información suficiente como para reconstruirlas. Es decir: no tienes que tener los mismos campos, no todas las entidades en el dominio tienen que tener su propia tabla en la bd…

Toda la clave está en cómo una implementación del repositorio se las arregla para extraer la representación adecuada para guardarla en una bd. Si esa representación usa el patrón Active Record u otro es indiferente porque solo afecta al ámbito del repositorio y no al dominio.

Existen patrones que pueden usarse para hacerlo. Por ejemplo, esta sería una idea.

https://franiglesias.github.io/representation-pattern/

Aunque el ejemplo está orientado a presentación, también aplicaría para persistencia. Se trata de una forma de obtener una representación de una entidad sin dependencia.

Preview

Por otro lado, nos queda el temilla de _acceder a información que está en base de datos sin tener que traerme agregados enteros_.

Esto tiene que ver con los ViewModel. ¿Qué pasa si tengo una vista que solo necesita unos pocos campos de una entidad? ¿Añado métodos al repositorio para esto?

No.

Necesitas crear otro tipo de servicios que puedan implementar acceso a la base de datos de forma que exponen métodos que nos permiten obtener ViewModels. Los ViewModel son poco más que DTO que usamos únicamente para poder poblar esas vistas con información.

Básicamente se necesita un ViewModel por vista. La implementación del _ViewModelRepository_ si lo quieres llamar así es muy sencilla: es básicamente una query SQL. Además, es muy fácil añadir soporte para filtros o criterios de ordenación, que son _concerns_ de las vistas.

El caso es que con esto estamos aplicando un patrón MVC (o MVVC) el cual no tiene que pasar para nada por el dominio. Los ViewModelRepository puedes _invertirlos_, definiendo interfaces en la capa de aplicación, que se implementan en la infrastructura.

Oye, que en mi caso no es una vista, que necesito alguna información para que el dominio haga algo, pero está en base de datos, o en un yaml o algo así ¿Qué hago? ¿Tiro de repositorio?

No.

Creas abstracciones en el dominio de esos servicios con los que obtener tal información, implementando en infraestructura con la tecnología de persistencia de que se trate.

En resumen: todo lo que sea acceder a algo que está fuera de la aplicación (como una base de datos) y que en último término no es otra cosa que un estado global se debe abstraer.

Lo dicho, que la base de datos no es más que un detalle de implementación.