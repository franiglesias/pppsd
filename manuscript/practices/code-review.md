# Code review

Voy a hacer capítulo sobre por qué las _code reviews_ al hacer _pull request_ no sirven para aprender a desarrollar bien. De hecho, las considero contraproducentes en ese aspecto. Y no solo para juniors, sino también para seniors que sean nuevos a un proyecto.

Una asunción es que la persona que hace la petición de _code review_ ha trabajado sola en ese _pull request_ específico. El primer problema que se puede ver aquí es que la revisora, o revisoras, no tiene el contexto ni del problema ni de como se ha llegado a la solución.

De hecho, el que una persona trabaje sola en un equipo es una mala práctica. Pero eso lo trataré en otro momento.

Puesto que los problemas raramente tienen una solución única y en programación hay cientos de formas de hacer algo, la review en estas condiciones puede ser algo tremendamente subjetivo e injusto. Como desarrolladoras nos hemos encontrado muchas veces en la necesidad de aceptar compromisos. Por ejemplo, hacer un código no muy limpio para no eternizarnos refactorizando cosas que no tienen que ver con la historia que tenemos en la mano en ese momento. Diréis: pues documéntalo con un comentario. Y yo digo: la revisora no va a leer el comentario.

Pero bueno, el punto es que hay algunas decisiones que parecerán erróneas a la revisora porque le falta el contexto. Incluso cuando esas decisiones las ha tomado alguien de sobrada seniority. Hablando de lo cual…

El caso de persona junior que pide la review y se le tira casi todo para atrás porque ha hecho varias cosas _mal_ según las revisoras. Pues esto es una mala práctica atroz. En primer lugar, porque convierte la _code review_ en un examen de programación que, además, es injusto.

Es injusto porque a la _junior_ le falta información. Ojo, no digo formación, digo información. De hecho, si una _junior_ llega a una _review_ en estas condiciones no es que le falte información, es que no se le ha dado. Se le está ocultando.

Me explico. Típica revisión: _es que no has considerado que nosotros no lo hacemos así porque…_. En primer lugar, si hay condicionantes, compromisos o requisitos para hacer las cosas: ¿por qué no se ha ayudado a la persona _junior_ a conocer esa información antes?

Por otro lado, está el cambio de contexto al hacer la _review_. Tú estás en otra cosa y tienes que cambiar tu contexto de un problema a otro, y tratar de entender que está pasando en ese otro contexto. _Pero es que en la daily ya coordinamos y sabemos en qué está cada quién_… Ya.

Por no hablar de lo que ocurre mientras la _review_ no se lleva a cabo. La solicitante: ¿tiene que pararlo todo y esperar a recibirla? Porque entonces también sufrirá el cambio de contexto, más el marrón de integrar los cambios que haya habido en paralelo.

Y eso contando con que no se hayan introducido conflictos, que también puede pasar.

¿Solución a esto? Pues programación colectiva, pairing o mobbing. ¿Por qué? En primer lugar, porque compartimos el contexto, aunque vengamos con ideas diferentes. De este modo todas podemos proponer soluciones distintas que se discuten en el momento, en un contexto compartido.

Sirven para mentorizar a personas con menos experiencia, pueden hacer sus propuestas y se discuten en el momento, incluso probándola. Sirven para descubrir y aprender aquellas cosas que no están documentadas, o que lo están en algún lugar que no se actualiza desde hace años.

¿Pero cómo puedes tener dos personas (o más) trabajando en lo mismo? Qué pérdida de tiempo. Pues en realidad es un ahorro de tiempo. Esto del tiempo me hace gracia porque nunca (o casi nunca) se cuenta el tiempo que se pierde en la revisión y en el ir y volver con los cambios.

Es ahorro de tiempo porque en un poco más, y a veces menos, del tiempo en que se completa una historia, se hace con menos problemas y menos frustraciones. Además, todas las personas que participan aprenden más, lo que las hará más productivas en el futuro inmediato.

Una posible ventaja de las _code review_ es cuando un cambio puede afectar a un entorno mayor que el equipo. Con todo, en ese caso puede que sea más productivo e interesante invitar a otros implicados a una sesión de mob programming de modo que los problemas se puedan prevenir y evitar de una manera más eficaz y precoz, en lugar de tener que parchear o volver atrás a la causa raíz con el pull request hecho.

Por otro lado, en las sesiones de mob programming puede, y debería, participar gente de producto, clientes, etc. Igual no en todas o todo el tiempo, pero sí cuando se tratan reglas de negocio, UI, UX, etc. o no se comprende bien el problema en el que se está trabajando.

¿Las mob programming en remoto son complicadas? Un poco, sí. ¿Que a veces hay partes que realmente no haría falta hacer en mob? También, pero gracias a haber hecho mob tenemos mejor definidas y delimitadas esas partes y de todos modos las integraremos durante una sesión de mob.

Como ves, no se trata de eliminar las *code reviews* _because yes_, sino entender que introducir prácticas, propuestas hace décadas, por cierto, de trabajo en equipo permitirán extender el conocimiento de forma más eficaz y sólida a través de un aprendizaje continuo en lugar de hacer _evaluaciones_ en forma de _code review_ en las que realmente no se aprende nada y actúan más de barrera que de feedback constructivo.

Sí, sí, ya sé que tú haces las _code review_ muy bien. Yo, siendo sinceros las hago fatal.

Por no mencionar los proyectos que tienen *code reviews* y están plagados de _bugs_ y problemas igualmente, demostrando que la _code review_ no es garantía de nada.

O por no mencionar el problema de las *code reviews* de muchísimos archivos que es humanamente imposible hacer bien, o las que solo se ocupan del code-style. O las que llevan 3000 approves porque eran dos líneas.

En resumen, para aprender a desarrollar bien lo que hay que hacer es programar juntas.

He debido pinchar en hueso con esto de las *code reviews*[^hilo]. Intentaré contestar algunas de las ideas que han salido y matizar el texto anterior. Prefiero hacerlo así, que es más fácil enlazar un argumento largo. Vamos a ello.

[^hilo]: El capítulo nace de un hilo de twitter que generó una cierta discusión posterior y quedan algunas referencias.

En primer lugar, el punto del argumento es que las _code review_ no sirven para aprender y mucho menos para que alguien junior aprenda. De hecho, ni siquiera son buenas para entender un proyecto grande, necesitas otras estrategias de aprendizaje.

Dicho esto, las _code review_ se supone que sirven para garantizar la calidad del código, evitar errores, particularmente de integración, y aumentar la confianza en el código que se mezcla y se despliega.

No he entrado en ese punto particular, aunque mi opinión es que las pull request con _code review_ no tienen mucho sentido en el contexto de equipos dentro de una empresa, sí en open source y tal. ¿Por qué digo esto?

Porque todas las ventajas que se señalan aumentan su eficacia si se hacen antes, no a posteriori. Las _pull request_ con _code review_ aumentan el trabajo en progreso (WIP). De hecho, son constraints de libro. La _definition of done_ debería ser _feature que el usuario puede usar_.

La asunción básica que estamos haciendo es que las PR se hacen porque trabajamos individualmente. Hablamos de equipos, pero en muchos casos el trabajo concreto se realiza en soledad y es después de _finalizado_ cuando se hace la review. Esto tiene varios problemas.

Un punto sugerido como positivo es que _alguien que no esté tan metido en el problema como tú ayuda a tener menos bias_. Para empezar: ¿Por qué una persona debería estar trabajando en un problema sola? Si sabemos que va a haber sesgo, ¿por qué no estar dos o más trabajando y prevenir ese _bias_ desde el inicio?

También se menciona la capacidad de la Code Review para abrir debate y llegar a acuerdos sobre como escribir software. Pero en la Code Review el código ya está escrito. ¿Por qué no mover ese tipo de debates al principio de los proyectos y durante el desarrollo?

Estoy de acuerdo en que una forma de trabajo no debe ser reemplazada por la otra porque sí y sin tomar medidas adecuadas, pero ese no era el punto del capítulo.

Para mí el feedback en las _code review_ llega tarde y mal. El editor está en modo _acabar la tarea_ y ha invertido tiempo y esfuerzo (coste hundido que le llaman), lo que hace que la _review_ sea más vista como una evaluación que como una contribución.

Por otro lado, ¿por qué alargar el tiempo de feedback cuando puedes hacerlo inmediatamente? Hay un gráfico sobre los ciclos de feedback (de Kent Beck) que es muy ilustrativo sobre esto. _Ensemble-programming_ proporciona feedback instantáneo en el momento requerido. 

Y ya que mencionamos al equipo: _pero es que no es tu código, es el código del equipo_… Entonces, ¿por qué no lo escribe el equipo en conjunto en lugar de hacer que una developer lo haga en solitario para que el equipo juzgue si es aceptable o no?
