# Polimorfismo

Otro de los patrones GRASP es el Polimorfismo. Es la propiedad de la programación orientada a objetos que nos permite enviar mensajes sintácticamente iguales a objetos de tipos distintos. Esto nos permite gestionar variantes de comportamiento basadas en tipos.

¿Y todo eso qué significa? Vayamos por partes. Primero: ¿Cuál es el caso de aplicación del patrón? Imaginemos que ofreces un `Service` con tres niveles (_tiers_): _free_, _premium_, _professional_. Una forma típica de modelar esto que `Service` tiene la propiedad `tier` (o `type`, o `category`…)

Eso implica que en ciertas situaciones necesitarás preguntar a `Service` por su _tier_ para saber qué precio cobrar, o qué límites de acceso tiene, etc., etc. Eso son muchos `if` o `switch` en muchos lugares del código. Incluso respetando _tell, don’t ask_. Por ejemplo, `Service.price` incluiría `if/else` o `switch` para decidir el precio del servicio, y así cualquier otro comportamiento asociado al _tier_.

En lugar de eso: polimorfismo.

Con polimorfismo crearíamos subclases de `Service` basadas en su _tier_: `FreeService`, `PremiumService`, `ProfessionalService`. Todas ellos responderían al mensaje `price`, cada una a su manera. La única decisión basada en el _tier_ sería en el momento de la instanciación, posiblemente en una factoría. Gracias al polimorfismo, los consumidores no tienen que preocuparse de qué servicio concreto se trata. Los objetos derivados son más simples y fáciles de testear. Si en tu negocio se introduce un nuevo _tier_, no hay más que añadir una clase nueva y actualizar la factoría.

Por supuesto, el principio de sustitución de Liskov aplica aquí: _subtipado semántico_. También KISS, ya que los componentes serán más simples, manteniendo la complejidad bajo control y eliminando la necesidad de preguntar por el tipo.

Las clases base manejarán los mensajes comunes, y las variantes serán manejadas por los subtipos. Esto también podemos hacerlo con interfaces explícitas o implícitas.

La clave del polimorfismo está en identificar las variantes de comportamiento y expresarlas como especializaciones, cediendo el control a los propios objetos.

{float: right}
![Programar sin ifs](images/programar-sin-ifs.png)