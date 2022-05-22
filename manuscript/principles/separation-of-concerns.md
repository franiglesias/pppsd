# Cada cosita en su lugar

Edsger W. Dijkstra (1930-2002) es todo un personaje en el campo de las ciencias de la computación, no solo por la cantidad y calidad de sus aportaciones, sino también por su particular carácter y algunas frases lapidarias. También es responsable de introducir el principio de la separación de intereses, en su artículo de 1974 _On the role of scientific thought_.

![](images/on-the-role-of-scientific-thought.png)

Básicamente, el principio nos dice que los programas no deberían escribirse como una única pieza que resuelva el problema. En lugar de eso, debe organizarse en partes más pequeñas que se ocupan de tareas especializadas. O dicho de una forma más sencilla:

> Diferentes partes del problema son tratadas por diferentes partes del programa.

Para ilustrarlo voy a usar un ejemplo exageradamente simplificado.

Consideremos este código en _python_:

```python
#!/usr/bin/env python3

# Separation of concerns principle
# Different parts of the program address different concerns

import sys


if __name__ == '__main__':
    print(sum(map(int, sys.argv[1:])))
```

Este programa simplemente suma los números que se le pasan como argumento:

```
./main.py 20 30 40   # --> 90
```

No parece tener nada incorrecto, ¿verdad? De hecho, este tipo de _one liners_ suele considerarse como especialmente inteligente. Sin embargo, para este artículo, este código pone de manifiesto un problema.

En primer lugar, cualquier programa básico tiene tres partes, y es la primera separación de intereses que vamos a considerar aquí:

* conseguir la información necesaria
* procesarla para obtener un resultado
* mostrar el resultado

En nuestro programa la única línea que tiene el programa se ocupa de los tres intereses. Esto quiere decir que si necesitamos modificar algo en relación con cualquiera de los tres intereses principales, tendremos que alterar **todo** el programa.

Da igual si se trata de mejorar algo en la presentación de resultados, obtener los números a sumar de otra fuente o utilizar un algoritmo diferente que haga el cálculo. Cambiar un aspecto del software implica hacer cambios que afectan a otros.

Podríamos simplemente separar cada uno de los intereses en una línea, algo así:

```python
if __name__ == '__main__':
    numbers_to_sum = map(int, sys.argv[1:])
    sum_result = sum(numbers_to_sum)
    print(sum_result)
```

Ahora hemos separado los tres intereses. Sin embargo, las líneas de código no representan bien las abstracciones que hemos definido. Para eso utilizamos unidades como las funciones:

```python
#!/usr/bin/env python3

# Separation of concerns principle
# Different parts of the program address different concerns

import sys


def obtain_input_data():
    return sys.argv[1:]


def sum_numbers(input):
    return sum(map(int, input))


def show_result(result):
    print(result)


if __name__ == '__main__':
    show_result(
        sum_numbers(
            obtain_input_data()
        )
    )
```

Ahora tenemos módulos diferentes que se ocupan de cosas distintas. El programa principal simplemente las coordina. Podríamos cambiar cualquiera de ellas internamente sin afectar al resto del código.

Puedes decir que no hay mucha diferencia. Sin embargo, ahora cada interés está siendo atendido por un módulo diferente del programa. Partes diferentes del programa se ocupan de intereses diferentes, en un mismo nivel de abstracción del proceso completo.

El principio de separación de intereses está en la base de otros muchos principios de diseño, entre ellos el _Single Responsibility Principle_ y _Tell, don't ask_. De esa relación nos ocuparemos más adelante.

Pero si únicamente pudieses quedarte con una idea de este libro, quédate con este principio.
