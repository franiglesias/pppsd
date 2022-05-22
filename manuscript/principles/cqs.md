# Command-query separation

Hablemos de _CQS_. No, de _CQ-R-S_ no, sino de _C-Q-S_: el principio _Command Query Separation_. Enunciado por Bertrand Meyer, reza más o menos así:

> Cada método debería ser o bien un comando que ejecuta una acción o bien una pregunta que devuelve información.

Esta distinción es fundamental y puede ayudar muchísimo a tu paz de espíritu y a la predictibilidad y testeabilidad de tu código. Es el _no mezclar churras con merinas_ de la orientación a objetos. Por supuesto, es una aplicación del principio de separación de intereses. Y en realidad es muy fácil de respetar.

Empecemos por los comandos:

Un comando (_command_) produce un efecto o cambio en el estado del sistema. Por ejemplo: crea un nuevo registro en una base de datos, o genera un archivo en algún sitio. Lo que haga falta. Pero no devuelve ninguna respuesta: _void_. Si no ha fallado es que ha ido bien. Si algo ha ido mal lo mejor es que lance una excepción.

– Oye, y eso ¿cómo se testea?

– Pues se me ocurren dos formas:

* Si es posible comprobamos que se ha producido el cambio deseado en el sistema.
* En el nivel unitario, usamos mock para verificar que se ha enviado el mensaje que produce el efecto.

– ¿Y si devuelve OK o true o ACK para indicar que ha ido todo bien?

– ¿Qué tiene de malo tirar una excepción? De otro modo tienes que esperar una respuesta y comprobarlo. Eso te lo da `try/catch` y es bastante más bonito.

Y no te confundes con las _queries_.

Las preguntas, o _queries_, por su parte devuelven una respuesta informando sobre el estado del sistema: ¿me das el producto con Id 1234? ¿Cuánto suman 2 y 3,45? ¿Cuál es el sentido del universo y todo lo demás?

El problema que tienen las queries es que, _ya que estamos_ podríamos hacer algo, además de preguntar. Pues oye: NO. Porque ese _hacer algo_ es producir un cambio en el sistema y si al hacer una pregunta cambias el estado: ¿cómo te puedes fiar de la respuesta?

Imagina un sistema de coche autónomo que al preguntar las rpm del motor también las cambia. Por ejemplo, las aumenta un 5%. ¿Qué te indica la respuesta de las rpm? ¿Las mide antes o después de del cambio? ¿Qué consecuencias tiene eso? Básicamente que no puedes confiar en la respuesta.

Por eso deben separarse las acciones que cambian el sistema (_command_) de las acciones que obtienen información sobre el sistema (_query_). Por cierto, testear las _queries_ es bastante sencillo, ya que solo tenemos que verificar la respuesta que devuelven.

Si una _query_ produce algún efecto en el sistema hablamos de _side effects_ y es algo que debemos evitar. Por el buen funcionamiento del sistema y porque de este modo podemos testear con confianza.

Una clase puede tener tanto commands como queries siempre que respetemos el SRP, claro. El principio CQS se refiere únicamente a que un comando no devuelva respuestas: se ejecuta y confiamos en que irá bien; y a que una query no produzca _side effects_ poniendo el sistema en estado indeterminado. Y nadie quiere eso.

Llevando eso a objetos-método, como pueden ser los Casos de Uso, tenemos que separar aquellos que son comandos de los que son queries. Y aplica lo mismo y por las mismas razones.

¿Y _CQRS_? _CQRS_ son las siglas de _Command Query Responsibility Segregation_ y es algo así como llevar _CQS_ hasta las últimas consecuencias, separando los _commands_, que implican escrituras, y las _queries_, que implican lecturas, incluso al nivel de la infraestructura. Por ejemplo, tendrías una base de datos para escritura, pero leerías los datos de una o más réplicas. Pero CQRS es más un patrón que un principio.

En cualquier caso, la separación _command-query_ es fundamental para construir sistemas confiables y fáciles de mantener. No hay nada peor que un _side effect_ ocurriendo vaya usted a saber dónde.
