# No lo vas a necesitar

"Your ain't gonna need it" es una expresión acuñada por Ron Jeffries para indicar que no deberías estar desarrollando prestaciones en el software si nadie te las ha pedido o por si en el futuro resultasen ser valiosas.

La dificultad con YAGNI es que muchas personas se vienen arriba creando código _por si acaso_. A veces resulta _tan_ evidente la necesidad de introducir alguna característica, aunque nadie la vaya a usar a corto plazo, que resulta irresistible añadirla. Incluso sin tests, ya puestos.

Esto puede generar varios problemas. Al introducir código que no se está usando ni se usará, añadimos ruido a nuestro software. Cuando alguien pase por ahí tendrá que preguntarse: ¿Qué es esto? ¿Afecta a lo que estoy haciendo? ¿Podría verse afectado por lo que estoy haciendo? ¿Está cubierto por algún test? ¿Por qué está aquí si no parece que se use en ninguna parte?

De hecho, es muy posible que no esté cubierto por tests, lo que hará bajar el índice de cobertura. Esta métrica en medida absoluta no es muy significativa. Sin embargo, sus variaciones son muy importantes para valorar la salud del proyecto. Si un conjunto de cambios hace bajar la cobertura de tests tenemos un problema.

Por otro lado, desde el punto de vista de desarrollo _lean_, introducir prestaciones que no se necesitan provocará dificultades en las siguientes iteraciones. Es posible que el feedback recibido nos indique que esa prestación que habías añadido se confirme irrelevante, o que haya que implementarla de una manera diferente. Tendrás que deshacer el trabajo y verificar que eso no provoca efectos inesperados.

Posiblemente la mejor forma de practicar para evitar caer en YAGNI sea Test Driven Development. TDD nos requiere añadir únicamente el código de producción necesario para pasar cada test, ni más, ni menos. El riesgo aquí es introducir código que no sea usado por los tests ya creados. La única forma de detectar ese código es ejecutar los tests con coverage. De este modo puedes identificar las líneas que no reciben ninguna llamada y borrarlas.

Si no tienes una buena cobertura de tests es más complicado identificar el código que te sobra. Las herramientas de análisis estático pueden ayudarte en esto. Un buen IDE te alertará de código al que no se llama nunca, pero únicamente una suite de tests que verifique todo el comportamiento de tu aplicación te dará seguridad para hacerlo.

En resumidas cuentas, es preferible que nunca añadas más código del que necesitas.

Otra cosa distinta es que dediques tiempo a realizar refactors preparatorios. Una vez que has terminado una historia tiene sentido dedicar un tiempo a refactorizar el código y dejarlo en mejor estado para el futuro. Pero esto no es añadir funcionalidad, que es de lo que nos previene YAGNI.
