# Principio de abstracción

El principio de abstracción lo introduce Benjamin C. Pierce en el libro _Types and Programming Languages_, y viene a decir que cada pieza significativa de funcionalidad en un programa debería estar implementada en un solo lugar del código. Y cuando hay funciones similares es beneficioso combinarlas en una sola, abstrayendo las partes que varían.

Seguramente este ha removido algo en tu interior y estés pensando: Pero eso, ¿no es el principio de _Don't repeat yourself?_ Y no te falta razón. Ambos principios remiten a la misma idea de que es conveniente tener una única fuente de verdad para todo conocimiento que resida dentro del código.

Hay dos puntos principales por los que tener en cuenta este principio.

Uno tiene que ver con el principio de separación de intereses de Dijsktra y la modularización. Al hacer que distintas partes del código se ocupen de asuntos diferentes, comenzaremos a ver un encaje a la idea de que algunas de ellas puedan reutilizarse. Por ejemplo, si una función realiza determinado cálculo, no tenemos más que invocarla desde cualquier lugar del código en el que necesitemos ese cálculo. Esa función es la fuente de verdad sobre cómo actúa ese comportamiento específico.

El otro aspecto es que al evitar la duplicación, prevenimos comportamientos incongruentes entre diversas partes del código. Si tenemos un mismo conocimiento expresado en varios lugares distintos del código, es posible que en caso de realizar alguna modificación pasemos por alto alguna de las versiones. Esto generará comportamientos del sistema diferentes según la forma en que se use, los cuales pueden ser difíciles de localizar incluso contando con tests.

Este principio nos llama a buscar la abstracción que pueda hacer única la fuente de verdad sobre piezas de funcionalidad de un programa y gestionar sus variantes parametrizándola. Como veremos al hablar de DRY es un proceso que entraña algunos riesgos, ya que es importante definir hasta qué punto la duplicidad de código representa realmente una duplicidad de comportamiento.

¿Y qué es una abstracción? Pues es una pregunta filosófica. Abstraer es un proceso por el que buscamos separar los elementos esenciales de una idea, de las variaciones accidentales que observamos en sus ejemplos. Esa idea abstracta nos permite, entre otras cosas, comprender lo que nos rodea. Si ves un gato sabes que es un gato porque identificas ciertos elementos esenciales, pese a las muchas variantes en forma de tamaño, color, forma, longitud del pelo y un largo etcétera.

Abstraer, en programación, es básicamente identificar fragmentos de código que representan una misma idea aunque lo hagan de forma un poco diferente. A veces las detectamos al observar código duplicado casi literalmente. Sin embargo, en otros casos podría revelarse de una manera más sutil. 
