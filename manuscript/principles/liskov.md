El principio de sustitución de Liskov es la L de SOLID y se refiere a cómo se definen las jerarquías de herencia. Fue enunciado por Barbara Liskov y Jeannette Wing. 🧻👇🏽
¿Y qué dice el principio? La formulación informal más común es: en una jerarquía de clases, las clases “hijas” o subclases deben poder ser sustituidas por las clases “madre” o superclases.
¿Cómo te quedas?
Una forma de ver esto es que todas las clases de una familia deberían ser intercambiables. Veamos un ejemplo: supongamos una clase User que tiene dos clases “hijas”: Customer y Administrator.
Pues bien, desde el punto de vista de sus consumidores esas clases deberían ser intercambiables. En otras palabras: tendrías que poder usar tanto Customer como User sin tener que cambiar el código consumidor.
Si puedes intercambiar Customer con User y Administrator con User, entonces podrías intercambiar Customer con Administrador. En conclusión: las clases de una jerarquía deberían ser intercambiables.
Pero… ¿hasta qué punto? El principio de Liskov se formuló en un artículo titulado: A Behavioral Notion of Subtyping. Para que el principio aplique, el subtipado no es simplemente sintáctico (una clase extiende de otra), sino semántico.
Las clases de la jerarquía tienen que tener un comportamiento equivalente desde el punto de vista de su consumidor.
Nuestro ejemplo de User, Customer y Administrator, puede ser válido porque  su comportamiento en un sistema sería equivalente. Eso no quiere decir que sea el mismo (tienen distintas capacidades de acción en el programa).
Ahora otro ejemplo: tenemos una clase Logger que escribe logs. También queremos hacer una clase Service que necesita escribir logs, así que hacemos que Service extienda de Logger.
¡Wrong! ¡Todo mal!
Sintácticamente puedes hacer eso, pero semánticamente no.
La responsabilidad de Service no sería escribir logs aunque necesite poder hacerlo. Semánticamente nuestro Service NO es un Logger. Si cambiamos Service por Logger no tendremos el comportamiento que el consumidor espera.
Dicho de otra forma: No debes extender una clase para proporcionar funcionalidad a otra no relacionada. En su lugar, utiliza la composición. No hay nada que impida a Service usar a Logger, pero Service no puede ser “hija” de Logger.
La herencia es un mecanismo no tanto para compartir comportamiento sino para especializar comportamiento. La clase madre contiene el comportamiento común y las hijas las versiones especializadas.
Por ejemplo, una empresa proveedora de energía podría tener Contract como clase "madre" y ElectricityContract y GasContract como clases "hijas". Ambas son "Contract", pero especializadas en un tipo de suministro.
Con todo, el principio tiene discusión. ¿Qué pasa si las clases madre son abstractas? ¿Aplica esto a familias de clases que implementan una interfaz?
En su formulación original el principio no contempla esto, pero creo que se puede aplicar si lo reformulas de esta manera: los subtipos no deben romper los contratos establecidos por los tipos de los que descienden.
Preview
Una recomendación relacionada es que las jerarquías de clases tampoco deberían ser muy profundas: mejor un nivel que dos. Por otro lado, si "sientes" que querrías tener herencia múltiple es posible que necesites composición en vez de herencia.
Recuerda siempre que la herencia es el mayor acoplamiento posible entre clases.
Una limitación que se puede extraer del principio de sustitución es que una clase derivada no puede establecer nuevos contratos. Es decir: no puedes tener métodos en una subclase que no estén en su clase madre.
De ser así, el consumidor quedaría acoplado a la subclase porque no habría forma de reemplazar esta con su ancestro u otras de la familia.
Claro que esto nos podría llevar a situaciones en las que una clase “arrastra” métodos que están en el contrato de su ancestro y que no necesita realmente. Y ahí entra el principio de Segregación de Interfaces del que ya tocará otro 🧻 algún día.
En pocas palabras: los contratos (Interfaces) también deberían ser pequeños y muy centrados en las necesidades de los consumidores.
Así que, según Liskov las clases que derivan de otras tienen que se intercambiables. Eso hace posible aprovechar el polimorfismo para que un consumidor pueda usar distintas versiones o especializaciones de un concepto sin tener que saber cuál de cual de ellas se trata.