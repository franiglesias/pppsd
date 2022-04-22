
Otro de los building blocks de DDD son los Servicios. Ya me estoy esperando la pregunta: ¿dónde van los servicios? 🤣. Pero, vayamos por partes, que primero tenemos que entender lo que son los servicios.

🧻👇🏼
Nota pijotera: la palabra servicio, ¿no os parece que está tan abusada que casi no significa nada a estas alturas? Fin de la nota.
En DDD los procesos del negocio se representan preferentemente como comportamientos de entidades (o agregados) de la capa de dominio. Es decir, si es posible atribuir todo el proceso a una entidad (o agregado).
Ejemplo, aplicación “bancaria”: un traspaso entre cuentas puede modelarse en la entidad Account, pasándole la otra cuenta y el importe del traspaso. Lo que sea necesario “saber” está en Account, tanto si actúa de emisora como si es receptora.
Ahora bien, supongamos que el proceso requiere información que no está disponible en la entidad (o agregado), especialmente si el acceso a esa información requiere algún tipo de dependencia externa. Se necesita algún proveedor de esa información (o validador o whatever) .
(Por ejemplo, la transferencia entre cuentas de distintos bancos seguramente requiere algún tipo de servicio)
O bien, no hay una relación entre las Entidades (o agregados) que participan en ese proceso. Dicho de otra forma: necesitamos que sean independientes aunque puedan intercambiar información…
¿Te suena el patrón Mediator o Indirection?
Pues eso es básicamente un servicio: un objeto mediador que provee un comportamiento que no puede ser proporcionado completamente por una entidad (o agregado), que puede requerir colaboración de otras entidades (o agregados) de forma que no se cree una dependencia entre ellas.
Los servicios de dominio representan procesos del negocio que implican o la coordinación de entidades (o agregados) o requieren una dependencia fuera del dominio que se debe invertir. Un ejemplo de servicio de dominio es… ¡tachán!… el repositorio.
Una llamada a una API de terceros para obtener información (imagina un convertidor de moneda) también se modelaría como servicio de dominio usando inversión de dependencias. En pocas palabras…
Si modela un proceso de negocio es un servicio de dominio. Si no tiene dependencias externas al dominio se implementa como un objeto de dominio, si las tiene, se invierten las dependencias as usual.
¿Servicios de aplicación? ¿Es que nadie piensa en los servicios de aplicación? Ya hablaré de estos en otro momento si me da el cerebro, pero hoy no es ese día.
solo decir que la ubicación de un servicio en la capa de dominio o de aplicación depende fundamentalmente de si modela o no un proceso del negocio/dominio.
Un ejemplo típico es de las notificaciones por email… “Eso es de aplicación, que enviar emails no es de dominio...”

A ver…
La RGE (Respuesta Gallega Estándar) aplica aquí.
Depende.
¿Es “notificación” un concepto importante del dominio? La forma de notificación, ¿es relevante de algún modo? Es muy posible que tengas que modelar un servicio de dominio de notificación que pueda atender a las preferencias de la cliente en cuando a la forma de la misma.
De hecho, el mecanismo (email, WhatsApp, slack, whatever) es una cuestión de la capa de infraestructura. Lo que suele ocurrir es que la notificación se gestiona habitualmente en el caso de uso (capa aplicación) bien sea directamente o mediante un suscriptor al evento interesante.
Esto puede llevar a confusión. Pero del mismo modo usamos repositorios en la capa de aplicación porque los casos de uso son coordinadores de objetos de dominio (otro mediador) para dar cumplimiento a una intención de la usuaria.
Por otro lado, es cierto que hay servicios de notificación que podrían vivir únicamente en la capa de aplicación, pero precisamente porque solo están interesados en aspectos “técnicos” del funcionamiento de la aplicación. Ejemplo: logs y similares.
En resumen, si me preguntas, te diría que es muy probable que ese “servicio” que estás buscando ubicar pertenezca al dominio si modela algún proceso del negocio.
Una regla práctica para identificar un servicio de aplicación sería si podemos trasladar el mismo servicio a otro proyecto. Es decir: es de dominio si solo tiene sentido en nuestro dominio, y es de aplicación si se podría usar en cualquier dominio.
Con todo, no hay reglas mágicas. DDD no es un conjunto de recetas para organizar una aplicación, sino un paquete de herramientas para poder entender y modelar un dominio.