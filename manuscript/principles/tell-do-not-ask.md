# Dime, no preguntes

Más que un principio este es un consejo de los pragmáticos Hunt y Thomas, que es muy útil para ayudarnos a mantener los principios de encapsulación y ocultamiento de información. Pura orientación a objetos.

Incluso diría que es más bien un consejo de refactor. Viene a decir que: no deberías tomar decisiones basándote en el estado de un objeto si van a resultar en que cambies el estado del propio objeto. Es una forma un poco liosa de expresarlo.

La cuestión es que en OOP el estado (propiedades) de un objeto deberían estar ocultas (ocultación de información) y cambiarían como resultado de enviar mensajes a ese objeto (invocando sus métodos). El objeto es responsable de gestionar su estado (encapsulación).

Salvando el caso de los que solo son portadores de datos, no deberíamos tener acceso directo a las propiedades de los objetos. Las propiedades son privadas, de hecho en algunos lenguajes lo son por defecto, ni exponemos _getters_ ni _setters_, para no exponer la estructura.

Dicho de otro modo, lo que contengan los objetos no nos importa para nada. Solo debemos preocuparnos de lo que pueden hacer.

Y ahora mismo me pregunto si los DTO deberían ser considerados objetos o más bien tipos (_structs_) inmutables. Ahí lo dejo.

Entonces, ¿cómo se cambia el estado de los objetos? Mediante el envío de mensajes, o invocación de métodos para entendernos, que produzcan el cambio de propiedades y que tengan valor semántico en el dominio de esa pieza de software.

Los mensajes que un objeto entiende conforman su interfaz pública. Una interfaz pública bien definida o contrato, aunque no hace falta que sea definida explícitamente, hace que tengamos total libertad para cambiar la implementación del objeto. Siempre que mantengamos esa interfaz.

Este es uno de los cambios de mentalidad más complicados cuando venimos del estilo procedural. En orientación a objetos, estos nos ocultan información, a cambio de ofrecernos comportamiento y colaboración.

Un problema es que solemos intentar explicar orientación a objetos a partir de sus propiedades, es decir, de cómo convertimos la expresión de ciertos conceptos mediante tipos primitivos en objetos. Y tendemos a verlos como contenedores de datos.

Sin embargo, el enfoque sería tratarlos como _information experts_, es decir: cada objeto sabe de los suyo y es a quién tenemos que pedirle cosas. Este entronca con los llamados _patrones GRASP_, de los que ya hablaremos. Pero puedes empezar pensando en que un objeto debería ser el máximo experto del sistema en lo suyo y, por tanto, reunir todos los comportamientos que le correspondan semánticamente hablando. Esto contribuye al SRP y DRY.

Otro aspecto es que los objetos deberían crearse consistentes, con toda lo que necesiten para funcionar y cumpliendo las reglas de negocio, de modo que no tengas que _preguntar_ al objeto si está completo o bien formado: si está en el sistema es que puede trabajar.

Por tanto, si tienes que preguntarle al objeto _cómo estás_ para decirle _cómo deberías estar_, significa que esa operación concreta debería formar parte de las habilidades de ese objeto.