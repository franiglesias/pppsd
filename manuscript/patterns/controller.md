# Controller

La verdad es que explicar los patrones GRASP en tuits es bastante complicado, porque en algunos casos se tarda menos con un ejemplo de código. Esta vez le toca el turno a Controller, que se puede explicar de forma bastante sencilla sin necesidad de ejemplos de código. 🧻👇🏼

Controller responde a la pregunta: ¿por dónde se entra al sistema? Y básicamente la responde introduciendo un objeto (el controller) que actúa de intermediario entre la capa de interfaz de usuario y la aplicación, vinculando eventos que suceden en UI con casos de uso…

… en la aplicación. Por supuesto, esto remite al patrón MVC que nació en las GUI y se usa habitualmente en aplicaciones web. En principio Controller se refiere a un objeto que es capaz de gestionar un determinado evento de la UI y lanzar el caso de uso correspondiente…

… aunque también cabe la posibilidad de que un solo controller agrupe varios métodos que responden a distintos eventos de la UI… como los verbos de una API REST para un cierto tipo de recursos.

Esto es, por ejemplo: si el usuario envía un formulario, hay un controlador que _captura_ ese evento (en HTTP una request a una URI específica) , extrae los datos, instancia un caso de uso y lo ejecuta, provocando un efecto o recuperando info, y devolviendo la respuesta adecuada.

La tarea del controller es gestionar ese proceso, pero no debe contener lógica de negocio. Tan solo es un traductor entre la intención de la usuaria de la aplicación y el caso de uso que representa esa intención. Si hay lógica de negocio en el controller tienes un problema.

Controller es un elemento de infraestructura y _adapta_ una tecnología concreta. Existen muchos frameworks que nos ofrecen todo lo necesario para montar controladores y, como tales, deberían estar en la capa de infraestructura de la aplicación. Sí… ya sé que Rails, Laravel…

… y un largo etcétera se postulan como la base de las aplicaciones con sus MVC y sus Active Record y acaban mezclándolo todo, siendo habitual encontrar aplicaciones basadas en ellos con lógica de negocio en controladores _gordos_, pero esa es otra discusión.

Lo importante es quedarse con la idea de que Controller es un patrón para resolver el problema de cómo entrar a una aplicación y cómo ejecutar las intenciones de las usuarias. También, que la única lógica que debería contener es la necesaria para identificar cuál es esa intención

y, por tanto, lanzar el caso de uso que le da respuesta. LO mejor es hacerlos muy pequeños y aunque puedas agrupar varias acciones en ellos, es importante que estén muy cohesionadas. Es mejor tener muchos objetos controller con pocas responsabilidades, que pocos que hacen de tó.

Por cierto, en este artículo están explicados los patrones GRASP y con ejemplos en varios casos:

Preview
