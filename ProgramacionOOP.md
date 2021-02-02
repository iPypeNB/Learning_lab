# Programación orientada a objetos

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
Es aquel elemento conceptual en la programacion orientada a objetos que se compone por unas propiedades (atributos) y unos comportamientos (metodos).

### Clases
Es un modelo por el cual los objetos se van a construir, es decir, las clases son las plantillas que le permiten a los objetos cobrar vida, cuando un objeto se declara a partir de una clase a esto se le llama instancia de la clase.

#### Abstracción
Es cuando se abstraen los datos (propiedades y comportamientos) de un "objeto real" y se contruye un molde (clase) a partir de la abstraccion.

### Modularidad
Es cuando se subdivide un sistema en elementos mas pequeños, estas divisiones se le llaman modulos.

### Herencia
La clase padre en POO se suele conocer como la super clase (hay algunos lenguajes que utilizan esa palabra clave para identificar a la clase padre) y las clases que heredan las caracteristicas de la clase padre son las subclases. 

## Codigo
la clases se pueden contruir de diferente manera segun el lenguaje de programación que se utiliza.

### Ejemplos:

#### Java
```java
class Person{
    String name = "felipe";
    
    void walk(){
        process
    }
}
```
#### Python
```python
class Person:
    name = 'felipe'

    def walk():
        pass
```
#### Javacript
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

#### PHP
```php
class Person {
    $name = "Felipe";
    
    function walk(){
        process
    }
}
```


