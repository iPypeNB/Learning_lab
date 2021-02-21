# Programación orientada a objetos

## Abstraccion
abtraer elementos que no se pueden referenciar tangecialmente.
enfocarnos a la informacion relevante.
## Decomposicion
partir un problema grande en prblemas mas pequeños.
## Diagramas de modelado
Los diagramas de modelado son una herramienta grafica que sirve como abstracción de la solución a la problematica encontrada, funcionan como un intermediario entre la problematica de la vida real y la formulación del codigo. estas herramientas graficas nos permiten visualizar de forma sencilla como es que nosotros abtraemos la información necesaria de las problematicas planteadas.

### Diagramas OMT
(Objecto modeling techniques) como su nombre lo describe son una tecnicas que le permiten al desarrollador hacer un análisis orientado a objetos.

### Diagramas UML
(Unified modeling language) tomó las bases tecnicas del OMT y generó un "lenguaje" que le permitia a los desarrolladores representar mas interacciones y abstraciones de los objetos, a continuación unas representaciones del lenguaje UML:

#### Atributos
- para poder representar los atributos de una clase se debe hacer de la siguiente manera:
    - (-) para los atributos privados.
    - (+) para los atributos publicos.
    - (#) para los atributos protegidos.
    - (~) para la configuración por defecto de los atributos.

#### Asociación
- asociacion siginifica que un elemento contiene a otro en su definicion, es decir, cuando las clases se conectan conceptual con otra, esta relacion entre las dos clases se llama asociacion.

#### Herencia
- La herencia es cuando una clase adquiere las caracteristicas de otra clase, es decir, la herencia permite que se puedan definir nuevas clases basadas en unas ya existentes. en uml la direccion de la flecha ira desde el hijo hasta el padre.

#### Agregación
- Este concenpto es muy parecido al de asociacion en cuanto a que un elemento depende de otro, la diferencia esta en que lo que sucede en agregacion es que un elemento depende de muchos otros.

#### Composición
- esta es una relacion mas estricta que la asociacion, esto se debe a que conceptualmente una clase no podria existir si la otra no existe.

## Características y elementos de la POO.

### Objetos
Es aquel elemento conceptual en la programacion orientada a objetos que se compone por unas propiedades (atributos) y unos comportamientos (metodos). Un objeto es una instancia de una clase.

### Clases
Es un modelo por el cual los objetos se van a construir, es decir, las clases son las plantillas que le permiten a los objetos cobrar vida, cuando un objeto se declara a partir de una clase a esto se le llama instancia de la clase.

#### Abstracción
Es cuando se abstraen los datos (propiedades y comportamientos) de un "objeto real" y se contruye un molde (clase) a partir de la abstraccion.

### Modularidad
Es cuando se subdivide un sistema en elementos mas pequeños, estas divisiones se le llaman modulos.

### Herencia
La clase padre en POO se suele conocer como la super clase (hay algunos lenguajes que utilizan esa palabra clave para identificar a la clase padre) y las clases que heredan las caracteristicas de la clase padre son las subclases. 

## Codigo

### crear una clase
la clases se pueden contruir de diferente manera segun el lenguaje de programación que se utiliza.

#### Ejemplos:

##### Java
```java
class Person{
    String name = "felipe";
    
    void walk(){
        process
    }
}
```
##### Python
```python
class Person:
    name = 'felipe'

    def walk():
        pass
```
##### Javacript
```javascript
class Person {
    constructor(){
        this.name = 'felipe'
    }
    
    function walk(){
        pass 
    }
}
```

##### PHP
```php
class Person {
    $name = "Felipe";
    
    function walk(){
        process
    }
}
```
### crear un objeto
Como se menciono anteriormente un objeto es una instacia de una clase, es decir si tenemos una clase vehiculo un objeto seria ese hermoso dodge challenger que tanto quieres 😎.

#### Ejemplos

##### Java
```java
Person person = new Person();
```

##### Python
```python
person = Person()
```

##### JavaScript
```javascript
var person = new Person();
```

##### PHP
```php
$person = new Person();
```

### Metodo constructor
El metodo constructor es el metodo que se llama cuando se instancia una clase y es el encargado de dar un estado inicial a el objeto, tiene el mismo nombre de la clase y solicita los parametros minimos necesarios para poder instanciar la clase, por norma de buenas practicas los metodos constructores no deben retornar ningun valor.

#### Ejemplos

##### Java
```java
public Person(String name){
    this.name = name;
}
```
##### Python
```python
def __init__(self,name):
    self.name = name
```
##### JavaScript
```javascript
function Person(name){
    this.name = name
}
```
##### PHP
```php
public function _construct($name){
    $this->name = name;
}
```
### Declaracion de clases Caso Especial JavaScript

#### Antes de EcmaScript6

```javascript
function Car(license, driver){
    this.id;
    this.license = license;
    this.driver = driver;
}

Car.prototype.printData = function(){
    console.log(this.license)
    console.log(this.driver)
}
```
#### Despues de EcmaScript6
```javascript
class Car {
    constructor (license, driver){
        this.id;
        this.license = license;
        this.driver = driver;
    }
    
    printData(){
        console.log(this.driver);
        console.log(this.license);
    }
}
```

### Herencia
la forma de declarar la herencia en los distintos lenguajes es:
#### java
```java
class Student extends Person{
    public Student(){
        super();
    }
}
```
#### PHP
```php
class Student extends Person{
    public function __construct(){
        parent::__construct();
    }
}
```
#### Python
```python
class Student(Person):
    def __init__():
        super.__init__()
```

#### JavaScript

##### antes de EcmaScript 6
```javascript
student.prototype = new Person();
```

##### despues de EcmaScript 6
```javascript
class Student extends Person {
    constructor(){
        super()
    }
}
```
Como se puede ver es importante al momento de usar la herencia en el constructor de la clase hijo hacer referencia al constructor de la clase padre ya que es importante "inicializar" la clase padre a traves de la clase hijo con todos los parametro obligatorios.

### Encapsulamiento
haces que un dato sea inmmutable cuando se le asigne un modificador de acceso, esto es cambiar los modificadores de acceso:
- public:
- protected: 
- default:
- private:

getter and setter: son unos metodos que permiten acceder a esos atributos que se encuentran encapsulados solo reescribir los atributos si cumplen con el proceso en especifico (ejemplo: solo si la variable es <= 3 almacenela)

### Polimorfismo
Es cuando cada una de las clases hijo tiene la capacidad de modificar los metodos heredados de la misma clase padre. Es cuando se contruyen metodos con el mismo nombre pero de comportamiento diferente.