# Domain Driven Design

Ya que hace unos días salió el tema, voy a largar un rato sobre ese ente mítico del desarrollo de software: Domain Driven Design, o DDD para abreviar.

Con el DDD pasa como con otros muchos conceptos y paradigmas. Muchas veces hablamos sobre ellos de tercera o cuarta mano, o buscamos la receta para usarlo de alguna manera. Se dice que DDD es solo para desarrollos muy grandes y complejos. Sin embargo, mi opinión es que ofrece tantas ideas aplicables a cualquier escala que merece la pena el esfuerzo de estudiarlo.

Pero ¿qué es DDD?

Fundamentalmente, DDD es una manera de afrontar el desarrollo de software complejo. 

Y entonces, ¿qué es complejo? Sinceramente, no tengo ni idea. Pero algo que he aprendido en estos años es que a poco que quieras tener impacto con tu negocio tienes que pensar en él como si fuese complejo, porque algún día lo será.

Básicamente, DDD nos propone una metodología que tiene dos grandes áreas: el DDD estratégico y el DDD táctico. El DDD táctico ofrece una serie de patrones que van orientados a la implementación. Ahora me quedo en el estratégico.

DDD estratégico es una metodología para analizar y entender el dominio de nuestro negocio. ¿Y qué es el dominio? Pues aquello de lo que trata nuestra empresa.

Fíjate que no hablo de una aplicación, hablo de la empresa o del negocio. Así que el primer paso es _entender el negocio_ mediante un proceso llamado _knowledge crunching_: obtener y procesar conocimiento de tu dominio.

Y esto, ¿cómo se hace? Pues: hablando.

Hablando con los expertos del dominio, o sea, las personas que trabajan cada día en tu empresa, con el objetivo de construir un modelo que represente ese dominio.

Uno de los objetivos es desarrollar _el lenguaje ubicuo_. Es algo tan simple como utilizar las mismas palabras para designar los mismos conceptos en absolutamente todos los lugares, incluyendo el código, los tests o la documentación. Si a un cliente se le llama cliente, en el código se llamará cliente. Si a un proceso le llamamos Alta de Cliente, en el código se llamará Alta de Cliente.

Este lenguaje ubicuo se crea de manera interactiva. Desarrolladoras y Expertas de dominio hablan y exploran cada concepto o proceso, resolviendo ambigüedades y sobreentendidos, haciendo explícito lo implícito. Las desarrolladoras también pueden introducir términos en el lenguaje ubicuo porque, a veces, las expertas del dominio no son conscientes de algunos conceptos que manejan de forma implícita o que tienen sentido dentro de un contexto, pero no en otro.

Así que DDD tiene una buena parte de lingüística.

Otro de los objetivos del DDD estratégico es identificar los distintos subdominios o partes del dominio y cómo se relacionan.

¿Qué es lo que hace tu empresa? Eso es el dominio, pero para lograrlo tiene que hacer otras muchas cosas. Algunas son muy específicas de tu empresa, otras son comunes a todas las del sector, y otras son comunes a cualquier empresa.

Eso que hace que tu empresa sea única, que las clientes la elijan, que nadie más sabe hacer como ella, es lo que llamamos el _core domain_ o _dominio principal_. Si le quitas eso a la empresa, deja de existir.

El core domain no lo puede hacer nadie por tu empresa, no se puede externalizar, no se debería hacer con aplicaciones de terceras partes. Nadie lo va a hacer como tú. Es donde tienes que poner la potencia de desarrollo.

Para poder realizar el core domain, la empresa necesita hacer otras cosas. Muchas de ellas son comunes a otras empresas del mismo sector, pero es posible que tú las hagas de manera especial para dar _soporte_ a tu core. Por eso se llaman subdominio de soporte.

Muchas veces podrás resolver esto con herramientas de terceros que te permitan suficiente personalización. A veces es algo que tendrás que desarrollar en casa. Posiblemente no quieres externalizar esto.

Cada tipo de negocio tendría distintos subdominios de soporte. Quizá la atención al cliente puede estar ahí.

Después existen toda una serie de subdominios que son comunes a cualquier empresa (nóminas, facturación….). Son los subdominio genéricos, que puedes resolver externalizando o con herramientas de terceras partes.

Este análisis te dice en qué te tienes que focalizar, dónde tienes que poner más esfuerzo y qué cosas debes resolver de la manera más sencilla posible (externalizar, terceras partes)

El análisis de dominio en suma consiste en definir el _espacio del problema_. Los subdominios tienen una representación en el _espacio de la solución_ en forma de _contextos acotados_ o _bounded contexts_.

Dentro de un bounded context viven conceptos y procesos propio, que no están en otras partes. Por otro lado, los conceptos generales del dominio pueden tener distinto significado. Es decir, cada bounded context puede ver un concepto del dominio de forma diferente.

Si vamos moviendo un concepto entre los distintos contextos podremos percibir esos cambios. Una cliente no es lo mismo desde el punto de vista de facturación, de ventas o de marketing. Pero mantiene una identidad a través de todos ellos.

Por otro lado, los contextos mantienen relaciones entre ellos. Algunos son más próximos, otros se superponen en cierta medida, otros tienen una relación de dependencia. Este análisis busca obtener un _Context map_ o mapa de contextos, que nos dice cómo se regula la relación.

Todo esto merece detallados.

También merecen 🧻 los llamados _building blocks_. El dominio se expresa en código usando una serie de elementos: entidades, value object, servicios y agregados.

Así que, resumiendo mucho, DDD es una manera de abordar el desarrollo de software, diría que en entornos empresariales complejos. Incluye un análisis estratégico en el que se busca desarrollar un modelo del dominio que luego se representará en forma de software.

Más sobre esto aquí, por ejemplo:

Preview

PS1: Por cierto, que lo que para una empresa puede ser un dominio genérico o de soporte, para otra puede ser su core.

PS2: La Biblia del DDD es el libro azul:

Preview

PS3: Muy recomendable:

Preview

PS4:

Preview

PS5: Desde aquí os podéis bajar la DDD Reference

Preview

