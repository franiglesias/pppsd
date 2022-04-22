Llevo un tiempo dándole vueltas al concepto de "bug". Lo que viene a continuación es muy subjetivo y discutible, as usual... 👇🧻
En principio, existe un cierto acuerdo en definir un "bug" como un defecto al implementar un programa que proporciona resultados inesperados o mensajes de error y operaciones que no pueden terminar.
Claro que también depende del punto de vista. Todas hemos visto reportes de bugs que relatan la odisea de una usuaria usando mal la aplicación cuando el sistema funciona perfectamente... bueno, podría ser un bug de UX si vamos a eso.
Pero yendo al código, un bug... ¿qué es?
Podríamos definirlo como un defecto del software que provoca resultados erróneos.
Pero, ¿cómo es posible escribir software con defectos?
La pregunta va totalmente en serio. No estoy preguntando: "¿Es posible hacer software sin defectos?":
Ya, bueno... (oigo decir) todo el mundo puede tener un mal día y olvidarse de chequear que un divisor pueda ser cero y provocar un error de división por cero.
ajá...
Dejando aparte los despistes... una cobertura de tests correcta debería detectar esos defectos antes de que lleguen a producción... ¿Cómo es posible no detectar eso? (Obvio: porque no está testeado)
pero ¿qué es y cómo se consigue que una batería de tests cubra todos los casos?
Pues a veces no se consigue, lo que viene siendo demostrado por nuestros abultados backlogs de bugs, incluso eliminando aquellos en los que la "culpa" es del cha-cha-chá.
Una cobertura suficiente de tests se consigue teniendo una especificación completa de las prestaciones del sistema y que ésta sea "traducida" a tests.
Esto tiene el problema de que no hay forma de hacer esto sin caer en el waterfall o cosas peores.
solo se me ocurre una manera de hacer esto: usar metodología BDD y TDD y desarrollar el producto de forma iterativa.
Pero si haces esto ocurre una cosa curiosa... dejas de tener bugs.
Bueno, no exactamente. 🤣🤣🤣🤣🤣
Pero los defectos se pueden reconceptualizar como comportamiento no definido. Para resolverlos se escribe un nuevo test que defina el comportamiento que falta, exponiendo el defecto. El código que hace pasar el test, "resuelve el defecto"
Yo diría que no es solo una cuestión semántica, sino que también es una cuestión psicológica. Los bugs tienen un componente de "culpa": alguien ha metido la pata.
Sin embargo, desde este otro punto de vista, el defecto puede tener dos causas principales:
* era una situación desconocida (la descubrimos al llevarla a la práctica)
* era un conocimiento implícito (lo dábamos por sabido) que habría que hacer explícito
  Y en ambos casos, me parece algo positivo ya que es descubrir conocimiento (el que no sabíamos y el que estaba "encubierto")
  Para lograr esto hay que trabajar en iteraciones e incrementos muy pequeños, mezclando y desplegando frecuentemente. Y acompañando de nuevos tests en cada conjunto de cambios.
  Los defectos se esconden en las partes de código que no están cubiertas por algún test. E incluso teniendo 100% de cobertura de buenos tests puedes tener comportamientos no especificados que se manifiesten en producción.
  La diferencia está en si la ausencia de esos comportamientos ha sido una decisión (el 20% de funcionalidad que no vas a desarrollar en esta iteración) o ha sido algo inesperado.