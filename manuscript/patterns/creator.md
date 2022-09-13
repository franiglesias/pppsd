# Creator

Tomemos por ejemplo, el patrón Creator…

El patrón creador nos ayuda a decidir quién crea ciertos objetos. La responsabilidad será de quien cumpla una de estas condiciones:

1. Contiene o agrega instancias de la clase a crear: un ejemplo típico es Pedido/Item. El pedido agrega items, por tanto, debería instanciarlos.
2. Registra instancias de la clase a crear. Por ejemplo: Cliente/Pedidos.
3. Usa instancias de la clase a crear. Por ejemplo: Cliente/Dirección de entrega. 
4. Contiene la información necesaria para instanciar objetos de la clase a crear: en general, si un objeto tiene información para crear otros objetos puede ser su creador. Esto nos lleva a las distintas implementaciones de patrones creacionales.

{float: right}
![New no, lo siguiente.](images/new-no-lo-siguiente.png)

Se podría decir entonces que un objeto que tenga mucho interés en otro, y que sepa mucho sobre él, puede ser creador de este segundo tipo de objetos.

Aparte, los objetos agregadores (en DDD serían los agregados) deberían crear esos objetos internamente. Es decir, no se les pasan los objetos agregados ya instanciados, sino los datos que puedan necesitar para construirlos.

Normalmente, esto es porque tales objetos agregados no tienen _vida_ fuera de la agregación. La idea de una línea de factura _independiente_ de una factura no tiene sentido. Por tanto, no creas líneas y luego se las pasas a la factura. Le pasas los datos de la línea.

Por otro lado, es muy conveniente que haya un solo lugar para la creación de cada tipo de objetos. Más allá de su función constructora, si la creación de un objeto implica algún tipo de lógica que no se puede encapsular en ella, introduce un builder o un factory que lo haga.

En resumen: la responsabilidad de creación de objetos pertenece a sus contenedores o agregadores o aquellos que tengan el conocimiento necesario.
