# Value Objects

¿Qué pasa cuando los conceptos del dominio no nos interesan por su identidad, sino por su valor? Pues que tenemos un nuevo building block del DDD: los Value Objects.

¿Qué significa que un concepto nos interesa por su valor? Pues básicamente que ese concepto tiene una o más propiedades y los diferenciamos porque sus valores son diferentes, o los consideramos el mismo si sus valores son iguales. Pensemos por ejemplo en una longitud.

Una longitud de 5 metros es igual a otra longitud de 5 metros. Parece obvio, pero eso quiere decir que podríamos usar la misma instancia de un objeto longitud para representar esa propiedad incluso en diferentes entidades. Pero bueno, eso es una sutileza que igual no nos ayuda.

Por comparar, dos entidades que tengan exactamente las mismas propiedades excepto la identidad serían distintas y se representarían con instancias distintas.

Aunque digamos que los Value Objects nos interesan por su valor no son simples contenedores de datos. Eso serían los DTO, por ejemplo y cierta Java old school llamaba value objects a lo que no eran otra cosa que DTO. Los Value Objects en DDD tienen comportamiento también.

Y es un elemento superimportante. Mathias Verraes decía en un post en su blog que los VO atraen comportamiento.

Pero, ¿cómo nace un VO? Imagina que tienes que modelar el concepto Precio. El Precio puede representarse con un _float_. Dos consideraciones:

* No todos los _float_ pueden ser precios, pues los precios siempre son positivos.
* La representación no es completa sin la unidad monetaria. Así que un precio necesitaría dos variables.

O sea que en realidad tenemos un _float_ limitado y un _string_. Así que los juntamos en un objeto que tendrá dos propiedades, Por ejemplo: `amount` y `currency`, y unas reglas de construcción, `amount` es mayor o igual a 0 y puede tener decimales, `currency` es un string representando una moneda según la norma ISO 4217; y con eso tendremos un VO `Price`.

De hecho, `Currency` también es candidato a VO porque aunque es un _string_, no todas las infinitas _string_ posibles representan un valor adecuado para `currency`. Así que `Currency` puede ser un VO que tiene un valor `string` el cual solo puede ser uno de EUR, USD, YEN, GBP, etc…

En cierto modo, los VO nos sirven para extender el sistema de tipos con aquellos propios de nuestro dominio. Veamos ahora algunas propiedades interesantes que deben tener los VO.

_Igualdad por valor_: como hemos dicho, dos VO son iguales si tienen los mismos valores. Normalmente, tendremos que introducir un método `equals` (que recibe otro VO del mismo tipo) que nos permite chequear esa igual conforme a las reglas relevantes en cada caso. A veces no podemos comparar todas las propiedades del VO o tenemos que tener en cuenta más cosas en la comparación. Por ejemplo, no puedes decir que 10 USD = 10 EUR, tienes que convertirlos primero.

_Inmutabilidad_: Los VO representan un valor, simple o compuesto. Si ese valor cambia, se debe cambiar la instancia por otra con el nuevo valor. Si cambia la propiedad precio de un producto, no mutamos el objeto `Price`, sino que reemplazamos la propiedad con una instancia distinta de `Price`.

De este modo, si el objeto `Price` tiene métodos _mutator_, por ejemplo: para subir o bajar el precio un porcentaje, en realidad serán métodos factoría que nos devuelven una nueva instancia con el valor resultado de la operación.

Esta inmutabilidad es la que nos permite usar la misma instancia en diferentes lugares.

Antes mencioné que el VO `Price` tenía unas propiedades y unas reglas. Los VO se han de crear válidos y consistentes conforme a las reglas que los definen. Por ejemplo, unas coordenadas tienen que estar en un rango de valores (latitud 0 a ± 90, longitud 0 a ± 180), y tienen que ser dos valores. De este modo, si tenemos un VO instanciado ya sabemos que es válido y consistente y lo podemos usar sin más.

Podemos modelar como VO cualquier concepto de dominio que no tenga identidad y nos interese su valor. Habitualmente serán conceptos relacionados con la cuantificación o la medida, pero diría que cualquier concepto que requiera algún tipo de regla de dominio o negocio es modelable como VO. Como reglas prácticas:

* Un concepto que se puede modelar con un tipo básico, pero que requiere alguna regla de validación.
* Un concepto que requiere más de una variable para su representación.

Decimos que los VO atraen comportamiento. Entre otras razones, es porque también son responsables de mantener sus propias invariantes y, aplicando _Tell, don’t ask_, las entidades no deben preguntar al VO por su estado para hacer algo, sino que más bien delegan en el VO todo lo que tenga que ver con el VO. Puedes ver un ejemplo en este artículo (al hablar de TaskStatus)

Preview
![](images/the-way-to-ddd.png)

Por cierto, que refactorizar a VO es un muy buen primer paso para mejorar un código existente. Y dentro de los VO me gustaría señalar también las virtudes de los Enumerables, que serían un tipo de VO también.

En fin, podría hablar de VO y ejemplos de modelado con VO de aquí a final de año, así que lo dejo por ahora. En este artículo tienes un buen resumen:

![](images/value-objects.png)

