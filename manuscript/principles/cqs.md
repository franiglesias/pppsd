# Command-query separation

Aparquemos los GRASP por un rato y hablemos de CQS… No, no de CQRS, sino de CQS: Command Query Separation. Enunciado por Bertrand Meyer, reza más o menos así:

Cada método debería ser o bien un comando que ejecuta una acción o bien una pregunta que devuelve información. 🧻👇🏼

Esta distinción es fundamental y puede ayudar muchísimo a tu paz de espíritu. Es el _no mezclar churras con merinas_ de la orientación a objetos. Y en realidad es muy fácil lograrlo.

Empecemos por los comandos:

Un comando (command) produce un efecto en el estado del sistema. Por ejemplo: crea un nuevo registro en una base de datos, o genera un archivo en algún sitio. Lo que haga falta. Pero… no devuelve ninguna respuesta: void. Si no ha fallado es que ha ido bien. Si algo ha ido mal…

… lo mejor es que lance una excepción.

– Oye, y eso ¿cómo se testea?

– Pues se me ocurren dos formas:

* Si es posible comprobamos que se ha producido el cambio en el sistema.

* En el nivel unitario, usamos mock para verificar que se ha enviado el mensaje que produce el efecto.

  – ¿Y si devuelve OK o true o algo para indicar que ha ido todo bien?

  – ¿Qué tiene de malo tirar una excepción? De otro modo tienes que esperar una respuesta y comprobarlo. Eso te lo da el try/catch y es bastante más bonito.

  Y no te confundes con las queries.

  Las preguntas (queries) por su parte devuelven una respuesta informando sobre el estado del sistema: ¿me das el registro con id 1234? ¿Cuánto suman 2 y 3,45? ¿Cuál es el sentido del universo y todo lo demás?

  El problema que tienen las queries es que "ya que estamos" podríamos hacer algo, además de preguntar. Pues oye, NO. Porque ese hacer algo es producir un cambio en el sistema y si al hacer una pregunta cambias el estado: ¿cómo te puedes fiar de la respuesta?

  Imagina un sistema de coche autónomo que al preguntar las rpm del motor también las cambia. Por ejemplo, las aumenta un 5%… ¿qué te indica la respuesta de las rpm? ¿Antes o después de del cambio? ¿Qué consecuencias tiene eso? Básicamente que no puedes confiar en la respuesta.

  Por eso deben separarse las acciones que cambian el sistema (command) de las acciones que obtienen información sobre el sistema (query).

Por cierto, testear las queries es bastante sencillo ya que solo tenemos que verificar la respuesta que devuelven.

Si una query produce algún efecto en el sistema hablamos de _side-effects_ y es algo que debemos evitar. Por el buen funcionamiento del sistema y por que de este modo podemos testear con confianza.

Una clase puede tener tanto commands como queries (siempre que respetemos el SRP claro). El principio CQS se refiere únicamente a que un comando no devuelva respuestas (se ejecuta y confiamos en que irá bien) y una query no produzca side-effects poniendo el sistema en un…

… estado indeterminado. Y nadie quiere eso.

Llevando eso a objetos-método, como pueden ser los Use Case, tenemos que habría que separar los que son comandos de los que son queries. Y aplica lo mismo y por las mismas razones.

¿Y CQRS? Pues es algo así como llevar CQS hasta las últimas consecuencias, separando los comandos (escrituras), y las queries (lecturas) incluso al nivel de la infraestructura. Pero CQRS es más un patrón, bastante complejo, que un principio.

En cualquier caso, la separación command/query es fundamental para construir sistemas confiables y fáciles de mantener.

No hay nada peor que un side-effect ocurriendo es vaya usted a saber dónde.