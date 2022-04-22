# Domain Driven Design y Arquitectura Hexagonal

Es muy común identificar (erróneamente) DDD con la Arquitectura Hexagonal de Alistair Cockburn. A veces le llamamos a eso directory driven development. Eric Evans cita la arquitectura hexagonal como una implementación de un bounded context compatible con DDD.

¿Y por qué esta identificación? Pues en parte porque hay coincidencias entre Arquitectura Hexagonal y las capas que propone Evans (dominio, aplicación, infraestructura, UI), aunque a decir verdad la Arquitectura hexagonal no postula capas, sino una separación entre la aplicación y los detalles técnicos de implementación. La Arquitectura Hexagonal tiene un objetivo que las implementaciones de DDD también deben cumplir:

Aislar el dominio.

En DDD la capa de dominio es donde reside nuestro modelo. El modelo estará escrito en objetos puros del lenguaje, sin más dependencia técnica que el propio lenguaje de programación. El dominio no debe saber nada de los _detalles de implementación_. Si algo necesita una tecnología concreta lo correcto es definir una abstracción en la capa de dominio (dependency inversion) de modo que el detalle de implementación dependa de la abstracción. El ejemplo típico es el patrón repositorio.

Pues esto mismo es lo que nos dice la arquitectura hexagonal. La aplicación, que coincide más o menos con el dominio en DDD, no debe tener contacto directo con el mundo exterior, sino exponer _Puertos_ (básicamente abstracciones -> interfaces) de forma que las dependencias o cualquier comunicación con el mundo exterior (UI, API, whatever) sea representada en el sistema por un _Adaptador_ que cumple esa interfaz. Puertos/Adaptadores es el segundo nombre de la Arquitectura Hexagonal.

De hecho, el concepto de _Puerto_ es algo más amplio que la mera aplicación de la inyección de dependencias. Los puertos se definen más bien por su rol, administración, interfaz de usuario, sincronización, persistencia, que por una tecnología concreta.

De hecho, los tests interactúan con la aplicación mediante esos puertos. Una aplicación hexagonal es testeable por diseño.

Así que la Arquitectura Hexagonal aísla y protege al dominio del mundo exterior, con lo cual es una buena forma de estructurar una aplicación sin usar DDD, y también para implementar un bounded context en DDD.

Si bien, como hemos dicho hay _tamaños de dominio_ para los que DDD es excesivo, la arquitectura hexagonal puede ser una buena forma de empezar siendo pequeños. Mucho mejor que FDD (Framework Driven Development), donde va a parar.

¿Por qué? Porque FDD te acopla desde el inicio a un detalle de implementación, mientras que Arquitectura Hexagonal te obliga a mantener el framework en su lugar, dejando el dominio aislado. Es un poco más de esfuerzo, pero el día que el negocio se empiece a complicar por temas de nuevas prestaciones, escalado, etc., ¡ay! ¡Cómo lo vas a agradecer ese día! E incluso si algún día se complica lo suficiente como para que DDD tenga sentido, estarás en mejor posición.

Pero también hay que decir lo mismo de las arquitecturas limpias en general. ¿Y qué es una arquitectura limpia?

Para mí una arquitectura limpia cumple tres criterios muy sencillos:

* **Capas**: hay una separación de intereses en capas
* **Regla de dependencia**: las dependencias apuntan en una sola dirección
* **Inversión de control**: los detalles dependen de abstracciones

Una arquitectura contiene tres grandes grupos de elementos:

* Un modelo del mundo: la representación del dominio
* Una representación de las metas o intenciones de las consumidoras de la aplicación: los casos de uso
* Las implementaciones técnicas que la hacen funcionar

Que coinciden con las capas de:

* Dominio (el modelo del mundo)
* Aplicación (los casos de uso)
* Infrastructure (las implementaciones, que no tienen dependencias cruzadas)

La Arquitectura Hexagonal me permite tener todo esto. Algo que funciona bien para una aplicación _pequeña_, como para un bounded context en DDD, porque cada bounded context puede tener su propia _arquitectura_

Así que si bien es completamente incorrecto decir que Arquitectura Hexagonal es DDD, sí que es una opción muy válida para la implementación.

Y Arquitectura Hexagonal no es la única cosa que se identifica erróneamente con DDD. Ojo:

https://franiglesias.github.io/ddd-is-not-what-they-said/
