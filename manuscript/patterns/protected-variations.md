# Variaciones protegidas

Protected variations es un patrón GRASP y es una consecuencia de la aplicación de otros patrones y principios. En muchos sentidos se encuentra en la base de lo que es la orientación a objetos. Consiste en proteger a unos elementos de los cambios en otros.

🧻👇🏽

Si hay algo que podemos dar por seguro es que las cosas cambiarán. El diseño de software tiene que tener en cuenta esto. Pero el objetivo no es prever cualquier cambio posible y tener una respuesta para cada uno de ellos. El objetivo es gestionar el cambio.

Pero, ¿quién debería hacerlo?

Veámoslo con un ejemplo. Supongamos un objeto Consumer que utiliza un objeto Service. ¿quién debería proteger del cambio?

Analicemos el caso de Consumer. ¿Debería estar preparado para los posibles cambios de Service?

No, dado que Consumer no tiene forma de predecir o anticipar los cambios de Service. No puede tomar medidas imaginando que esos cambios pueden producirse en un sentido u otro. ¿entonces?

Entonces es Service quien tiene que proteger al resto del sistema de sus posibles cambios. ¿Cómo? Escondiéndolos en una interfaz estable, de modo que Consumer no tiene que saber si Service ha tenido que cambiar o de qué modo.

Polymorphism es un ejemplo muy claro. Existe una ServiceInterface que puede ser implementada por diversas variantes de Service, de modo que Consumer no tiene que saber cuál está usando exactamente.

La posible fuente de cambio que oculta para Consumer, de tal modo que podemos añadir variantes sin tener que tocar Consumer para nada.

Para ello el acoplamiento es el mínimo posible (inversión de dependencias, dependemos de la abstracción), Service es cerrado a modificación (Open Close), las variaciones de Service son intercambiables (Liskov), Consumer solo habla con Service a través de su interfaz (Demeter…)

Hay una explicación muy completa aquí:

https://www.rose-hulman.edu/class/cs/csse374-201020-02/SlidePDFs/session23.pdf

El riego de protected variaciones está en la posibilidad de _sobre diseñar_ para prevenir cualquier cambio posible o si se identifica incorrectamente las posibles razones.

Pero básicamente se trata de que los objetos establezcan un contrato estable acerca de lo que hacen: qué mensajes les puedes enviar y que respuesta te pueden dar a ellos.