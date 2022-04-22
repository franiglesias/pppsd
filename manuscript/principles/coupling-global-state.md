Pues llevo todo el día peleándome con una variable estática (que no una propiedad) en una clase PHP usada para evitar un acceso a disco. Un ejemplo de optimización prematura violando principios OOP… TODO MAL. Lo que unido al 🧻 sobre acoplamiento me da excusa para hacer otro 🧻
Esta vez sobre el acoplamiento al estado global.
El 🧻 es de papel Elefante.

🧻👇🏿

¿A qué me refiero con estado global? Pues no a la ONU precisamente, sino a aquello que es visible o accesible desde cualquier lugar del código de la aplicación. Y esto en OOP es un NO.
Es un NO porque es lo opuesto a la OOP un paradigma en el que básicamente se trata de ocultar el estado en los objetos. Por otro lado, si hay acceso al estado global el comportamiento puede ser impredecible, dado que cualquier objeto podría cambiarlo sin que se enteren los demás.
Aún más, el estado global puede estar definido y ser cambiado por la propia máquina que alberga el programa. No necesariamente por el programa. ¿Nos vamos haciendo una idea de los problemas que esto puede generar?
Estado global es por ejemplo el reloj del sistema. Cada vez que instancias un objeto de hora o fecha estás usando una dependencia global. Lo mismo si usas el generador de números (pseudo)aleatorios, o algo que esté en el sistema de archivos. Aparte de posibles variables o …
…parámetros globales de tu programa, y cualquier cosa “compartida”, como una base de datos para tests “compartida” (😱)…

En general, esto hace que el comportamiento de la aplicación sea impredecible o, cuando menos, que no puedas confiar 100% en ella.
También se consideran globales las llamadas estáticas. El patrón Singleton debe su mala fama a sus implementaciones estáticas más conocidas (porque se pueden tener singleton no estáticos).
Por ejemplo, los tests. ¿Has hecho tests con cosas que usan fechas o números aleatorios? Ha dolido, ¿no? Trucos como poner una fecha muy lejos en el futuro para que ciertos tests pasen (y luego resulta que el futuro llega y hay que cambiar el test)
O los tests sobre el sistema de archivos, que si fallan dejan “sucio” el entorno de CI, falseando otros tests o bloqueando la build. O tests que pasan si se ejecutan solos y no pasan si se ejecuta la suite.
Del mismo modo que los tests tienen estos comportamientos “impredecibles”, la aplicación también los puede tener. El acceso al estado global puede crear dependencias muy difíciles de detectar o errores puntuales muy difíciles de encontrar.
Imagina un objeto que crea un archivo para almacenar una información temporalmente y poder recurrir a ella más tarde, pero hay otro objeto que elimina o escribe ese mismo archivo. Problemas garantizados.
¿Cómo se soluciona esto? Pues en primer lugar evitando acceder al estado global en cualquier momento y lugar. Si necesitas un parámetro de configuración, pásalo a los objetos en construcción o a través de algún sistema controlado si lo necesitas en otro momento.
Si tienes que acceder a estados globales usa patrones de indirección, de modo que un estado global sea representado por un objeto del sistema. Por ejemplo: un TimeService o ClockService que abstraiga el reloj del sistema.
Y cuando necesites un objeto de Tiempo pídeselo solo a ese servicio. De este modo, en testing puedes usar un doble y nunca más tener tests que dependan del día o la hora de su ejecución. Lo mismo para un generador de números aleatorios.
No hay problema que “dentro” uses la implementación nativa del lenguaje, pero tampoco hay problema en que uses otras implementaciones: patrón Adapter y a tirar. Esto no te evita posibles problemas de tu máquina, pero evita el acoplamiento directo entre objetos dispares.
Así que, en general, es recomendable que cualquier estado global tenga una representación en un objeto de tu aplicación en lugar de acceder directamente a él. De hecho, extendiendo la idea podría decirse que cualquier cosa que no sea tu aplicación y te proporcione información es
… estado global (hum… ¿son las usuarias estado global?)
En cualquier caso, representándolo en objetos y usándolos de forma rigurosa tu aplicación será más confiable y más fácil de poner bajo test. De hecho, será más fácil llegar a cambiar en algún momento su implementación por mejores soluciones.
Puede que te preguntes… pero si esos objetos están acoplados al estado global, entonces, ¿en qué quedamos?
Por supuesto. Recuerda que no puede haber acoplamiento cero. Pero en OOP si le damos a un objeto la responsabilidad de proporcionarnos una información específica de ese estado global estamos estableciendo un punto único y controlado de acceso al mismo.
El resto de objetos no se acopla al estado global sino indirectamente (indirection). Puedes reemplazar ese objeto con otro que cumpla el mismo contrato y la aplicación no se verá afectada. Ejemplo: un doble de test, pero podría ser otra cosa.
En la introducción de este paper  Beck y Cunningham hablan sobre lo difícil que es cambiar de la mentalidad procedural (pendiente del estado global) a la OOP (no estado global).

https://c2.com/doc/oopsla89/paper.html
Controlar el acoplamiento es uno de los puntos clave de la buena orientación a objetos.