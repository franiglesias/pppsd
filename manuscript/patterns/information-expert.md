Otro de los patrones GRASP es el Information Expert. Sirve para responder a la pregunta de “¿quién debería ocuparse de esto?”. Y la respuesta es: pues el que sabe de ello: el experto.

Otra forma de verlo: ¿qué objeto debería ser el que responde a este mensaje?

🧻👇🏼
Pienso que es un patrón que podemos vincular a “Tell, don’t ask”: si tienes que preguntarle a un objeto por su estado para tomar alguna decisión que afecte al objeto, ese comportamiento pertenece al objeto que no deja de ser el experto en ese tema.
¿En qué es “experto” un objeto? Pues depende del concepto que representa y de las propiedades que componen su estado. Aparte, un objeto debería ser experto en su propia consistencia interna, y ser capaz de inicializarse válido y proteger sus invariables.
Es muy fácil verlo con el clásico ejemplo de Pedido/Items. ¿A quién le preguntamos sobre el importe total? Pues al Pedido, porque al contener los Items puede sumar los importes de cada ítem. Y cada ítem, por su parte, podrá calcular su importe porque sabe de su precio unitario…
… y de su cantidad. Además, un pedido “sabe” que necesitará un cliente y dirección de entrega y facturación. Además, puede que haya un tope en el número de items que se pueden pedir. O tal vez, los gastos de envío son gratis si se supera un cierto importe…
… lo cual es algo que Pedido puede decidir. Para algo es el experto… en pedidos. Si no tiene toda la información necesaria sabrá que está incompleto o que no es un pedido válido. Saber eso es su trabajo.
Su antipatrón suele estar relacionado con los modelos anémicos: el objeto tiene la información, pero no hace nada con ella porque no tiene comportamientos y son otros objetos los que saben qué hacer con ello. Si separas “Información” y “experto” entonces no estás haciendo OOP.
¿Te parece un patrón obvio? Pues no veas la cantidad de bases de código que no lo usan o no lo usan suficientemente. Es bastante típico si provienes de un estilo procedural ya que tiendes a ver los objetos como “tipos” que contienen datos, que son manipulados por funciones.
Pero la potencia de la programación orientada o objetos reside en que los objetos sean expertos en lo suyo, que solo tengas que pedirles que hagan cosas e interactúen sin tener que supervisarlos (en el sentido de verificar a cada paso que las cosas son correctas).
Ojo. Dar este salto puede ser difícil. En programación procedural importa el conocimiento global del sistema y su control. En programación orientada a objetos el conocimiento está distribuído en objetos que interactúan y colaboran para realizar el trabajo y tienen sus propias…
…parcelas de control. Son dos formas de ver la programación. No son incompatibles, pero parten de puntos de vista diferentes.
Así que, en lo tocante a asignar responsabilidades a los objetos, tienes que dárselas al que sabe y confiar en que lo hará bien.
Por cierto, los information experts suelen ser fáciles de testear unitariamente, así que es muy sencillo y eficaz garantizar que están capacitados para realizar su trabajo.