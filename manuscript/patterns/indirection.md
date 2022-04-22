Indirection es uno de los patrones GRASP que más nos puede ayudar en hacer software “a prueba de futuro”. ¿Cómo? Ayudándonos a evitar el acoplamiento directo entre objetos de modo que ambos puedan evolucionar separadamente. Vayamos poco a poco.
🧻👇🏽
Es más fácil ver el valor de este patrón cuando necesitamos implementar algo usando algún vendor específico. Imagina que tienes que acceder a una API externa. Lo típico es usar alguna librería que te ofrezca un cliente HTTP. Así podrías tener un APIClient y un VendorHTTPCLient.
La forma de usar VendorHTTPClient con APIClient, podría ser:
1. Herencia: Haces que APIClient extienda VendorHTTPClient. Mal asunto: la herencia es el máximo acoplamiento. Si VendorHTTPClient cambia, APIClient tiene que cambiar. Si APIClient tiene que cambiar, VendorHttpClient …
   … podría no servirte ya. Un Horror.
2. Composición: APIClient usa VendorHTTPClient como colaborador. Si éste cambia, APIClient es relativamente fácil de cambiar. Si APIClient cambia, VendorHTTPClient puede ser sustituido, pero… si el OtroVendorHTTPClient tiene distinta…
   … interfaz, sigue siendo un percal. Composición es mejor que herencia, pero si la interfaz está definida por el vendor, APIClient sigue estando acoplado. Menos que en la herencia, pero lo bastante como para que sea un trabajo extra de mantenimiento.
   La solución es la indirección (quedaría bien en una camiseta)
   En este ejemplo, la indirección consiste en introducir un objeto intermediario entre APIClient y VendorHTTPClient, llamémosle MyHTTPClient. APIClient usará MyHTTPClient (pref. por composición) y MyHTTPClient se implementará usando VendorHTTPClient (pref. por composición).
   (Si esto te suena a patrón Adapter, es que lo es)
   ¿Y qué hace MyHTTPClient? Pues:
* Proporciona una interfaz estable para que APIClient  esté protegido de los cambios en VendorHTTPClient. Los cambios serán para MyHTTPClient, por supuesto.
* Nos permite reemplazar VendorHTTPClient por OtroVendorHTTPClient simplemente cambiando…
  …MyHTTPClient. Aún mejor si definimos una interfaz HTTPClientInterface y hacemos que nuestros HTTPClient la implementen usando diferentes vendos.
  O para tests podemos crear HTTPClients dummies, stubs o lo que nos haga falta.

Lo importante es que no tenemos que tocar APIClient para nada en caso de que tengamos que cambiar o actualizar el Vendor. Podrías decir “es que tienes que cambiar el mediador igualmente”.  Claro…
… pero la función del mediador es justamente regular la relación entre los otros objetos, de modo que protege a cada objeto de los cambios del otro. Ambos pueden evolucionar a su aire.
Además del adapter, hay otros patrones que aplican indirection como facade, mediator, o bridge. Por ejemplo, facade es un objeto que simplifica la interfaz de otro objeto o módulo que sea complicado de utilizar. Mediator maneja u orquesta la interacción entre distintos objetos…
El punto clave es evitar el acoplamiento directo, haciendo que el objeto intermediario sea el que tiene el conocimiento para hace interactuar los otros objetos de modo que la dependencia sea responsabilidad del intermediario que, por otro lado, es controlado por nosotros.
Indirection es una herramienta para lograr Inversión de dependencias. Muchas bases de código problemáticas lo son por tener acoplamiento alto con vendos, por lo que introducir indirección nos ayuda a producir la inversión de control que nos lleva a la inversión de dependencias…
… lo que mejora significativamente la mantenibilidad del código. La indirección también nos permite personalizar vendors sin quedar ancladas en versiones concretas que luego nos impiden actualizar o mejorar otras partes del código.
De hecho, una buena estrategia es introducir el mediador antes incluso de saber qué vendor vas a utilizar. Esto es: cuando sabes que vas a necesitar alguna librería externa, en vez de hacer una dependencia directa, introduce un objeto intermediario que la abstraiga, de modo que…
… cuando lo tengas que implementar no necesites hacer cambios en el consumidor, solo en el mediador.
Así que la próxima vez que vayas a extender un vendor o usarlo en composición, piénsalo dos veces e introduce un objeto “indirector”. Tu yo del futuro te estará eternamente agradecida.