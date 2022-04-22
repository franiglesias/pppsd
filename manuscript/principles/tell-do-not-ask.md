# Dime, no preguntes

"Tell, Don't Ask" más que un principio es un consejo de los pragmáticos Hunt y Thomas, que es muy útil para ayudarnos a mantener el principio de encapsulación y ocultamiento de información. Pura orientación a objetos.

Incluso diría que es más bien un consejo de refactor. Más o menos dice que: no deberías tomar decisiones basándote en el estado de un objeto si van a resultar en que cambies el estado del objeto. Es una forma un poco liosa de expresarlo.

La cuestión es que en OOP el estado (propiedades) de un objeto deberían estar ocultas (ocultación de información) y cambiarían como resultado de enviar mensajes a ese objeto (invocando sus métodos). El objeto es responsable de gestionar su estado (encapsulación).

Salvando el caso de los que solo son portadores de datos (DTO), no deberíamos tener acceso directo a las propiedades de los objetos. Las propiedades son privadas (en algunos lenguajes lo son por defecto), ni exponemos getters ni setters, para no exponer la estructura.

Entonces, ¿cómo se cambia el estado de los objetos? Mediante el envío de mensajes (invocación de métodos para entendernos) que cambien las propiedades como corresponda y que tengan valor semántico en el dominio de esa pieza de software.

Los mensajes que un objeto entiende conforman su interfaz pública. Una interfaz pública bien definida o contrato (no hace falta que sea explícita) hace que tengamos total libertad para cambiar la implementación del objeto. Siempre que mantengamos la interfaz.

Este es uno de los cambios de mentalidad más complicados cuando venimos del estilo procedural. En OOP, los objetos nos ocultan información, a cambio de ofrecernos comportamiento y colaboración.

Un problema es que solemos intentar explicar OOP a partir de las propiedades de los objetos, es decir, de cómo convertimos la expresión de ciertos conceptos mediante tipos primitivos en objetos. Y tendemos a verlos como contenedores de datos.

Sin embargo, el enfoque sería tratarlos como "information experts", es decir: cada objeto sabe de los suyo y es a quién tenemos que pedirle cosas. Este entronca con los llamados "patrones GRASP", de los que ya hablaremos. Pero puedes empezar pensando en que un objeto...

debería ser el máximo experto del sistema en lo suyo y, por tanto, reunir todos los comportamientos que le correspondan (semánticamente hablando). Esto contribuye al SRP y DRY.

Otro aspecto es que los objetos deberían crearse consistentes (con toda lo que necesiten para funcionar y cumpliendo las reglas de negocio) de modo que no tengas que "preguntar" al objeto si está completo o bien formado: si está en el sistema es que puede trabajar.

Por tanto, si tienes que preguntarle al objeto "cómo estás" para decirle "cómo deberías estar", significa que esa operación concreta debería formar parte de las habilidades de ese objeto (encapsulación).