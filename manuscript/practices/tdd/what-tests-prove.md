# Lo que prueban los tests

Voy a secuestrar este tweet. La frase de Dijkstra tiene un problema gordo: ¿cuál es el criterio que define lo que son los errores? Si afirmamos que los tests no pueden probar la ausencia de errores es que existe otro criterio que, obviamente, no son los test.

Julio César Pérez

・9h

Siento lo mismo. Es una sensación rara, verdad?

Pienso en la frase de Djikstra: los tests pueden probar la presencia de errores, no su ausencia. Aún así intento tener mejores tests.

También pienso que los tests son herramientas para desarrollar mejor

Por ejemplo, si construimos una pieza de software con TDD siguiendo estrictamente las reglas de cambios mínimos suficientes, los tests prueban la total ausencia de errores en el dominio de conocimiento definido por esos mismos tests.

Si ese código sale a producción y aparece un error, ¿qué significa? Pues básicamente que el conocimiento necesario no estaba reflejado en los tests y, por consiguiente, no podía estar reflejado en el código.

Este espacio de no conocimiento es donde viven los bugs. Pero ¿dónde reside ese conocimiento completo que nos permite afirmar que un código contiene errores?

El caso es que ese conocimiento (más) completo puede existir o no. A veces tal conocimiento es algo así como "vox populi" y nadie se preocupa de hacerlo explícito hasta que pasa algo (el bug) y se nos enciende la bombilla.

A veces es conocimiento que alguien tiene pero no comunica. Y otras veces es conocimiento que es completamente nuevo y que solo ha surgido como consecuencia de desplegar un código y encontrarse con ese caso que hace aflorar la laguna.

El problema de escribir software es el problema de representar un conocimiento, incompleto y cambiante, de una forma lo más aproximada posible. Los tests proporcionan una segunda representación que podemos usar para verificar el software, pero si es una representación incompleta

o incorrecta, pues estamos en las mismas. Habrá un desfase entre el conocimiento necesario y el representado en el código y los tests. Idealmente, los tests y el código deberían representar exactamente el mismo conocimiento.

Por esto mismo es tan importante trabajar en iteraciones pequeñas y baby steps en todas las fases del proceso de desarrollo. Cuanto menos código introduces en una iteración, menos riesgo de que el desfase de conocimiento sea grande. Y más fácil de resolver si ocurre.

Cada iteración nos sirve para evaluar el desfase de conocimiento y si el nuevo código introduce o revela nuevos desfases. Si desplegamos montañas de código en cada iteración, los desfases serán abismales y difíciles de resolver.