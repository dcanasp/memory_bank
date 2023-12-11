Para problemas que ya todos han sufrido pero que ya muchos han resueltos
para ver mas: [refactorin.guru](https://refactoring.guru/design-patterns)
# creational
mecanismos para crear objetos, aumentando flexibilidad y reuso de codigo

### singleton

la clase solo tiene una instancia. si la instancia existe se le da la que existe. Esto proporciona un unico punto de acceso.

Se usa el metodo getInstance 

Es lazy, no carga por default

no es muy bueno el singleton, porque viola la single responsibility.
Si hay multithread es un problema entero


### Factory method

Tiene un metodo responsable de crear la instancia. Para no usar el constructor

Es mejor retornar una interfaz, programar abstracciones no 


### builder

Cuando un constructor es muy grande (mas de 5 propiedades), se le llama constructor telescopido (porque es muy cargadao)

java tiene implementado este patron, algunos como `string.builder` 

aislar la logica de construccion.

Puedes mirar los fluent builder 

se puede hacer lo mismo con interfaces/clases fluidas, se retorna en this

en vez de en el builder poner todo. se retorna el this y se hace algo asi:
clase.builder.add('').template().update().Build();

y se van añadiendo las clases

### prototype

es mas facil copiar que crear desde 0
Se puede obtener un objeto a su totalidad clonado asi tenga propiedades privadas
es una alternativa a herencia

en c# se puede hacer, sin saber nada, serializando el objeto y luego copiandolo

### abstract factory
una factory de factorys, se tiene una interfaz con cada uno de los metodos, unas fabricas internas y asi se crean los productos finales para crear lo final

ejemplo son los botones de windows, tu no lo creas, lo anañdes a un abstract factory
# structural

como guardar objetos en clases y estructuras mas grandes, manteniendolas eficientes pero flexibles


### adapter 
permite que 2 objetos incompatibles puedan hablar normal (convertir un formato a otro o cosas asi)

hay 2 tipos, adaptador de clase y de objeto

### decorator

permite añadir a objetos ya existentes, sin modificar las actuales

por ejemplo si se tiene una clase grande, se le añade un pedazito unicamente envez de herencia

los decoradores se añaden de una forma secuencial

Se termina creando como una pila de decoradores (cuando hay muchos)

### facada

proporcionar una interfaz simplificada

### proxy
es igual a un decorador
pero envez de añadir da permisos, o hace cosas especiales. El proxy es mas de seguridad pero hay muchisimos tipos

### composite 
crear una estructura jerarquica que no diferencia entre objetos simples y objetos compuestos, tambien es un decorador 
segun rene es el mas bacano y mas flexible


# comportamiento
como se realiza la comunicacion y entre objetos

### chain or responsabilities

Multiples controladores que se llaman uno despues de otro, tienen un metodo next para ir al siguiente

igual que los middleware de express


### command 

Convertir todo un request en un objeto completo que se puede pasar con metodos 

### Iterator
iterar una coleccion sin que importe que estructura este abajo

### Mediator

es el que evita el caos entre multiples componentes, todos los componentes hablan con este, y este se encarga de lo dificil

lo malo es que puede volverse en un "objeto dios" que si falla todo falla

### Memento

Guardar estados pasados de un objeto sin tener que guardar la implementacion de este, 

### Observer

lo mismo que una subscripcion, se deja un observador con una lista, cada vez que hay nuevo evento a cada subscriptor se le envia el evento

### state

alterar el estado de un objeto dependiendo de en que estado este (como una maquina de estados finitos)

### strategy

permite definir una familia de algoritmos, y usar cada uno de estos de forma intercambiable

estos patrones se pueden ejecutar con funciones lambda

### template method
definir un esqueleto de un algoritmo. pero esto de una forma abstracta. Cada clase que implemente este template sigue esos pasos pero el decide como hacerlo

esto es muy restrictivo pero bueno si se tiene un caso de uso que siempre necesita el mismo procedimiento


### visitor 
permite separar algoritmos de los objetos en el que opera
