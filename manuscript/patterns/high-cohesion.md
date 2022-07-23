# Alta cohesión

El reverso de _low coupling_ es _high cohesion_, otro patrón GRASP y otro concepto acuñado por Larry Constantine.

Cohesión nos da una idea de cuan fuertemente relacionados están los elementos de un módulo de software.

Nota previa: módulo de software es una medida un tanto flexible. Para el caso de nuestro _estudio_ de la cohesión lo que digamos se puede aplicar a una clase o a un conjunto de ellas que forman un módulo.

Como tantas otras cosas en el diseño de software una buena forma de analizar la cohesión es ver cómo cambian las cosas. En este caso si cambian juntas o no. Aunque hay algunos matices, porque también depende de lo cercanas que estén las cosas que cambian o si nos perjudica.

Así, las cosas que cambian juntas deberían estar juntas. Es la primera heurística de la cohesión. Esto es: si cuando cambiamos una clase tenemos que cambiar otra, posiblemente ambas pertenecen al mismo módulo. Incluso podría ser que debieran fusionarse.

Por supuesto, siempre respetando otros principios como Single Responsibility, etc. Dicho de otro modo, tienes alta cohesión cuando al realizar cambios en el software estos afectan al menor número de elementos. Idealmente solo a uno.

Cuando dos cosas alejadas entre sí cambian juntas puede ocurrir que estén acopladas, pero no quiere decir necesariamente que tengan que estar juntas (no son cohesivas). Esto es: tenemos que preguntarnos si el cambio es por acoplamiento (malo) o porque están separadas cosas que van juntas.

Obviamente, si un objeto tiene que cambiar porque otro lo hace y pensamos que no debería ser así, es un caso de acoplamiento. Como hemos visto, tendríamos que introducir patrones que reduzcan el acoplamiento directo.

En el segundo caso, tenemos que refactorizar para incrementar la cohesión.

¿Y si metemos todo el código en un sólo objeto?

Pues no.

Hay dos maneras de lograr alta cohesión:

* Poniendo juntas las cosas que deberían estar juntas (porque cambian juntas)
* Separando las cosas que no cambian junto con las otras.

En cierto modo, la cohesión es también el arte de saber decir no. Si tenemos una clase en la que unos métodos cambian juntos, pero otros no, es muy posible que tengamos varias responsabilidades y que debamos separarlas.

Es como decir que la alta cohesión y la responsabilidad única van de la mano. 

Si tenemos una clase que expone muchos métodos, va contra Segragación de Interfaces (también SRP) y, por tanto, necesitamos “partirla”. Otro principio que va de la mano de la alta cohesión.

Y lo mismo con otros muchos principios: seguirlos nos conduce a tener alta cohesión. Buscar la alta cohesión nos ayuda a respetar los principios de diseño.

Lo mismo cuando buscamos reducir al máximo el acoplamiento. Es un círculo virtuoso.