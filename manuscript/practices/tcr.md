# Test and commit or revert 

Hoy me ha dado por practicar un poco el flujo _test && commit || revert_ y me lo estoy pasando muy bien.

{float: right}
![Test and Commit or Revert](images/test-commit-revert.png)

Por supuesto, es un flujo propuesto por Kent Beck. TCR (Test && Commit || Revert) consiste en que tras cada cambio en el código de producción se lanzan los tests. Si los test pasan, se ejecuta un commit con los cambios.

Pero si los tests NO pasasen, se borran los cambios aplicando un reset _duro_ para eliminarlos. Es decir, si tu cambio rompe los test, se descarta por completo.

Para automatizarlo se crea un pequeño script que realiza todo el proceso. La versión más básica simplemente hace lo que se indica: ejecutar los tests y hacer _commit_ si han pasado o _revert_ si no.

Esta versión simple tiene algunos problemas, porque también borraría los tests nuevos si no pasan. O si haces _TDD_ sería bastante engorroso, ya que, por defecto, se borrarían los tests nuevos al intentar ejecutarlos.

Por esa razón, se han creado algunas versiones _tuneadas_ que, por ejemplo, aseguran que el código compila y que solo se revierten los cambios en el código de producción y no se revierten los tests.

Con eso, se puede hacer _TDD_ con TCR. Y resulta hasta mágico.

Haces un test, ejecutas el script TCR y lo ves fallar. Añades código de producción para hacerlo pasar y TCR de nuevo. Y así hasta terminar. Si metes la pata y un test que pasaba, falla, el código de producción que lo provoca se elimina. Vuelta a empezar.

Con este flujo puedes aprender a refactorizar en pequeños pasos, ya que favorece la parte de _make the change easy_, manteniendo los tests en verde.

Además, como no querrás perder mucho código de una vez, te fuerza a añadir muy poquito código de producción. Si lo pierdes que sea poco.

Este flujo complementa a _TDD_ en la parte de refactor, puesto que se parte de que los tests están en verde y se trata de mantenerlos en verde. Y puede ser una buena base para hacer refactor en código legacy una vez que hayas introducido tests (por ejemplo, mediante Approval tests)