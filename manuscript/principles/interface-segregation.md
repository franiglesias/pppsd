# Segregación de interfaces

Principio de Segregación de interfaces, la I de SOLID. No es del todo fácil explicar este principio en un hilo de twitter porque es difícil poner ejemplos. Pero vamos a intentarlo.

Básicamente, el principio pide diseñar interfaces con pocos métodos de modo que sus clientes no necesiten depender de aquellos que no van a usar. Lo mismo las clases que las implementen o extiendan. Veamos un caso típico:

Tienes una clase que implementa una interfaz y ves que necesita un método nuevo para un cierto caso particular. Lo añades, pero... tendrás que añadirlo a la interfaz, o a la clase base, y a todas sus _hermanas_ y posiblemente vacío. Ahí tienes una violación de segregación de interfaces.

Y de Liskov de paso. El nuevo método está pidiendo una interfaz nueva que implementará esa clase específica, así no tienes que contaminar al resto de la familia. La cuestión es: ¿por qué el nuevo método?

Pues porque algún cliente de la clase lo requiere, lo que nos lleva a una de las definiciones del principio: interfaces finamente granulares específicas por cliente. Esto apunta a que las interfaces se deben diseñar a partir de lo que requieren sus usuarias. 

Ejemplos:

Una clase que acumula muchos métodos probablemente está violando SRP y lo mejor sería extraer varias interfaces basándonos en sus consumidores, de modo que cada uno dependa solo de los métodos en que está interesado, haciendo que la clase _gorda_ las implemente.

Esto nos puede facilitar una refactor para repartir esa funcionalidad en clases más pequeñas que implementen cada cual una interfaz. Se gana en capacidad de mantenimiento. Puedes aplicar el patrón adapter usando la clase _gorda_ como colaboradora en una primera aproximación.

Si necesitamos introducir un método nuevo en una clase, plantéate si sería mejor introducir una nueva interfaz antes de nada. Especialmente si esa clase ya implementa una interfaz o es una subclase.

Una clase que tiene que implementar o sobreescribir un método para que no haga nada porque está obligada a tenerlo por herencia o por interfaz, nos está indicando una violación del principio. Y puede que falle _single responsibility_ en la interfaz o la clase base.

Este principio está estrechamente vinculado con SRP y Liskov, incluso con OCP. Quizá sea uno de los mejores chivatos de mal diseño orientado a objetos.

Así que si ves métodos sin implementación porque tienen que cumplir la interfaz, o clases con dependencias de las que solo usan un pequeño porcentaje de métodos, tienes entre manos un caso de violación de Segregación de Interfaces.