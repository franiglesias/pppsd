# Falla pronto

_Fail Fast_, o falla pronto, como principio de diseño de software puede parecer contra-intuitivo. Es un principio que he visto atribuido a Jim Gray y que viene a decir:

>Un módulo que falla rápido detecta y comunica errores y deja que el módulo inmediato superior los gestione.

Fallar rápido quiere decir que en cuanto se detecta algo que no está bien no tratamos de arreglarlo en el punto de detección, ni fallar _silenciosamente_. Al contrario, tiramos una excepción o error que _suba_ por la pila de llamadas hasta encontrar quién sabe gestionarlo.

Imagina: un método requiere un parámetro entero en el rango de 5 a 27. Si el valor es menor o mayor... excepción. Quien haya llamado a ese método con el valor incorrecto, será quien tenga que gestionar el error. Nada de intentar _arreglarlo_ u ocultarlo bajo la alfombra.

Esto tiene sentido. El objeto que haya hecho la llamada debería tener más contexto para resolver el problema y decidir si puede usar otro valor. Por ejemplo, si ha pasado uno mayor podría emplear el límite superior en su lugar, o si tiene que fallar igualmente y _hacer subir el error_ un nivel más.

El objeto en el que se detecta el error carece del contexto necesario para tomar decisiones. Por tanto, es mejor fallar y hacerlo sonoramente.

A veces, el lenguaje lo hace por nosotras. Con el tipado estricto de parámetros, el compilador o intérprete fallará si llega un valor de tipo incorrecto. El tipado de retorno hace lo mismo.

Por supuesto, hay condiciones que son del negocio, como el ejemplo de que exista un rango de valores admisible. Estas reglas pueden considerarse _precondiciones_, y cuanto antes las evaluemos, mejor. Para esto, podemos usar cláusulas de guarda o _asserts_.

Que los _asserts_ no son solo para los tests. Se trata de pequeños objetos que encapsulan una regla y lanzan una excepción si les pasamos un objeto que no la cumpla. Los _asserts_ nos permiten verificar que un valor cumple ciertas condiciones, fallando si no es así. Si no tienes _Asserts_, puedes usar cláusulas de guarda: if algo_esta_mal then lanza excepción.

Contra lo que pueda parecer, un sistema que falla rápido es muy robusto. En caso de errores, permite localizarlos más fácilmente y garantiza que si un valor pasa todos esos controles podemos confiar en él siempre.

Una aplicación de este principio es la construcción de objetos con validaciones que no permiten instanciar un objeto si no se cumplen las reglas de negocio. De este modo, si un objeto ha podido ser creado, es que es válido y consistente. No necesitas chequearlo cada vez.

Si tienes un módulo que sientes que debería gestionar el error detectado, es posible que tengas un problema con el diseño y debas separar cosas ahí. Típico caso: bucle que lee datos de un archivo y que valida cada línea para poder incluirla o no. En ese caso conviene aplicar la separación entre el bucle y el proceso del ítem, de modo que el bucle gestione los posibles errores de procesar el ítem.

Así que, ya sabes, en lo tocante a hacer sistemas robustos: falla pronto y falla sonoramente.