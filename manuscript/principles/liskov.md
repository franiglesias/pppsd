# Sustitución de Liskov

El principio de sustitución de Liskov es la L de SOLID y se refiere a cómo se definen las jerarquías de herencia. Fue enunciado por Barbara Liskov y Jeannette Wing.

¿Y qué dice el principio? La formulación informal más común es: en una jerarquía de clases, las clases _hijas_ o subclases deben poder ser sustitutas de las clases _madre_ o superclases. Y también al revés.

¿Cómo te quedas?

Una forma de ver esto es que todas las clases de una familia deberían ser intercambiables. Veamos un ejemplo: supongamos una clase User que tiene dos clases _hijas_: Customer y Administrator.

Pues bien, desde el punto de vista de sus consumidores esas clases deberían ser intercambiables. En otras palabras: tendrías que poder usar tanto Customer, como User, como Administrator, sin tener que cambiar el código consumidor.

Si puedes intercambiar Customer con User y Administrator con User, entonces podrías intercambiar Customer con Administrador. En conclusión: las clases de una jerarquía deberían ser intercambiables.

Pero… ¿Hasta qué punto? El principio de sustitución se formuló a partir de un artículo titulado: _A Behavioral Notion of Subtyping_. En resumen, lo que dice es que el subtipado no es una cuestión puramente sintáctica, sino también semántica.

https://www.cs.cmu.edu/~wing/publications/LiskovWing94.pdf

Las clases de la jerarquía tienen que tener un comportamiento equivalente desde el punto de vista de su consumidor.

Nuestro ejemplo de User, Customer y Administrator, puede ser válido porque su comportamiento en un sistema sería equivalente. Eso no quiere decir que sea el mismo, pues tienen distintas capacidades de acción en el programa.

Ahora otro ejemplo: tenemos una clase Logger que escribe logs. También queremos hacer una clase Service que necesita escribir logs, así que hacemos que Service extienda de Logger.

¡Wrong! ¡Todo mal!

Sintácticamente hablando, puedes hacer eso, pero semánticamente no.

La responsabilidad de Service no sería escribir logs aunque necesite poder hacerlo. Semánticamente, nuestro Service no es un Logger. Si cambiamos Service por Logger no tendremos el comportamiento que el consumidor espera.

Dicho de otra forma: No debes extender una clase para reutilizar funcionalidad a partir de otra no relacionada. En su lugar, utiliza la composición. No hay nada que impida a Service usar a Logger, pero Service no puede ser _hija_ de Logger.

La herencia no es un mecanismo para _compartir_ comportamiento, sino para _especializar_ comportamiento. La clase base contiene el comportamiento común y las derivadas las versiones especializadas.

Por ejemplo, una empresa proveedora de energía podría tener `Contract` como clase _base_ y `ElectricityContract` y `GasContract` como clases derivadas. Ambas son `Contract`, pero especializadas en un tipo de suministro.

Con todo, el principio tiene discusión. ¿Qué pasa si las clases base son abstractas? ¿Aplica esto a familias de clases que implementan una interfaz?

En su formulación original el principio no contempla esto, pero creo que se puede aplicar si lo reformulas de esta manera: los subtipos no deben romper los contratos establecidos por los tipos de los que descienden.

Preview

Una recomendación relacionada es que las jerarquías de clases tampoco deberían ser muy profundas: mejor un nivel que dos. Por otro lado, si sientes que querrías tener herencia múltiple es posible que necesites composición en vez de herencia.

Recuerda siempre que la herencia es el mayor acoplamiento posible entre clases.

Una limitación que se puede extraer del principio de sustitución es que una clase derivada no puede establecer nuevos contratos. Es decir: no puedes tener métodos en una subclase que no estén en su clase base.

De ser así, el consumidor quedaría acoplado a la subclase porque no habría forma de reemplazar esta con su ancestro u otras de la familia.

Claro que esto nos podría llevar a situaciones en las que una clase _arrastra_ métodos que están en el contrato de su ancestro y que no necesita realmente. Y ahí entra el principio de Segregación de Interfaces del que hablamos en otro capítulo.

En pocas palabras: los contratos, o interfaces, también deberían ser pequeños y muy centrados en las necesidades de los consumidores.

Así que, según el principio de sustitución las clases que derivan de otras tienen que ser intercambiables. Eso hace posible aprovechar el polimorfismo de modo que un consumidor pueda usar distintas versiones o especializaciones de un concepto sin tener que saber de cuál de ellas se trata.