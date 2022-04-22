# Inversión de dependencias

Ya tengo ganas de terminar con SOLID, así que hablaremos del principio de inversión de dependencias. Contribuye a que el código sea sostenible y flexible. Y no hay que confundirlo con el patrón Inyección de Dependencias.

Dice así:

* Los módulos de alto nivel no deberían depender de los módulos de bajo nivel. Ambos deberían depender de abstracciones
* Las abstracciones no deberían depender de los detalles. Los detalles deben depender de abstracciones.

Alto nivel, abstracciones, detalles... Otra forma de enunciarlo es que las dependencias deberían apuntar en el sentido de mayor estabilidad. Las abstracciones serían más estables que las implementaciones.

¿Qué es un detalle? Detalle es una implementación concreta. Por ejemplo: un detalle sería una tecnología de persistencia, como una base de datos relacional. ¿Y una abstracción? Pues por ejemplo, un repositorio. El repositorio se puede implementar usando diferentes tecnologías de persistencia, pero la idea de repositorio es abstracta y se representa mediante una interfaz (explícita o no) que expone comportamientos como guardar, recuperar y seleccionar. La interfaz es lo que nuestra aplicación "ve", podemos cambiar la implementación sin afectarla siempre que cumplamos el principio de inversión de dependencias, de tal modo que:

* La interfaz (abstracción) del repositorio no dependa de una implementación concreta (detalle)
* Cada implementación concreta depende de la interfaz.

En la práctica, esto significa que la aplicación no sabe si está usando una base de datos relacional, noSQL, o un JSON o una API, o un doble de test. Hay gente que dice "es que (casi) nunca vas a cambiar la base de datos, no importa"... Pues no: si haces tests, cambias de base de datos porque los dobles, stubs, mocks o fakes, son implementaciones alternativas de la abstracción "repositorio". Y quien dice repositorio, dice cualquier otro concepto que pueda tener múltiples implementaciones.

El principio también actúa como una propiedad de toda arquitectura multicapa sostenible. Las dependencias apuntan hacia las capas más abstractas. En la clásica "Dominio/Aplicación/Infrastructura", Infraestructura depende de Dominio, Aplicación usa los elementos de Dominio y Dominio no tiene dependencias, porque es la "abstracción" de negocio. Dominio define las abstracciones que luego se concretan en las otras capas (principio de segregación interfaces). Y dominio no tiene ninguna dependencia. De este modo, se pueden posponer decisiones de implementación, mientras desarrollamos el core de la lógica de negocio. Podríamos trabajar con componentes fake (como repositorios en memoria, stubs de ciertos servicios y otros) hasta decidir qué tecnología nos conviene más. O cambiarla si necesitamos escalar en algún momento, simplemente escribiendo un nuevo adaptador.

La violación de este principio suele tener consecuencias bastante problemáticas. Caso típico de los frameworks "database-first" en lo que la aplicación acaba estando acoplada a un detalle. Cuando necesitas crecer descubres que todo el código está acoplado a la base de datos vía Active Record en los lugares más insospechados. Con otros ORM también es fácil que ocurra esto.

A la hora de asegurarnos que nuestro código es Dependencia Inversión Compliant, es importante definir interfaces estables (explícitas o no) y favorecer la composición frente a la herencia también ayuda.