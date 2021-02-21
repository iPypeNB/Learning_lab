# Que es Pyhton
Python es un lenguaje de programacion 

# Programacion orientada a objetos.
es una forma de hacer code

# Caracteristicas de python en POO.
Python es un lenguaje que nos (lema de python - tienes que saber lo que envias o algo asi -> obj)

- En Python todo es un objeto y todo tiene un tipo, esto siginifica que todo lo que nosotros manejamos en el codigo tienen una representacion en memoria y el que todo este catalogado con un tipo nos permite encapsular los datos y el comportamiento adentro de un objeto.
- cuando python pierde todas las referencias a los objetos (el programa lo deja de utilizar) el Garbage collector destruye el objeto en la memoria.
- en python no existe el encapsulamiento de las variables privadas con la palabra reservada `private` en vez de eso python utiliza una convencion que especifica que la variables privadas comienzan con `_`, las variables privadas en python se verian asi `_name_variable`. 

# Clases

```python
class nombre_clase(super_clase):
    
    def __init__(self,params):
        expression

    def nombre_metodo(self,params):
        expression
```
## decoradores
los decoradores en python son la forma sencilla de llamar `funciones de orden mayor`, es decir,funciones que toman a otra funcion como parametro y retornan otra funcion como resultado, de esta manera un decorador le añade capacidade a una funcion sin modificar la misma.

los decoradores se puede utilizar con el simbolo @ 

```python
@funcion_decoradora
def zumbido():
	print("Buzzzzzz")
```

### funciones como obejto de primera-clase
funciones que reciben a otras funciones y resotrnan el resultado de la convinacion.

### Funciones anidadas
funciones dentro de otras funciones

# Metaprogramacion
no ides
## getters and setter
A diferencia de otros lenguajes de programación, en Python los getters y setters tienen el objetivo de asegurar el encapsulamiento de datos. Cómo habrás visto, si declaramos una variable privada en Python al colocar un guión bajo al inicio de esta (_) y normalmente son utilizados para: añadir lógica de validación al momento de obtener y definir un valor y, para evitar el acceso directo al campo de una clase.

La realidad es que en Python no existen variables netamente privadas, pues aunque se declaren con un guión bajo podemos seguir accediendo a estas. En Programación Orientada a Objetos esto es peligroso, pues podemos alterar el método de alguna clase y tener efectos colaterales que afecten la lógica de nuestra aplicación.

```python
class CasillaDeVotacion:
    
    def __init__(self, identificador, pais):
        self._identificador = identificador
        self._pais = pais
        self._region = None

    @property
    def region(self):
        return self._region

    @region.setter
    def region(self, region):
        if region in self._pais:
            self._region = region
        else:
            raise ValueError(f'La region {region} no esta en la lista')
```

# funcion property
Esta función está incluida en Python, en particular crea y retorna la propiedad de un objeto. La propiedad de un objeto posee los métodos getter(), setter() y del().

En tanto la función tiene cuatro atributos: property(fget, fset, fsel, fdoc) :

- fget : trae el valor de un atributo.
- fset : define el valor de un atributo.
- fdel : elimina el valor de un atributo.
- fdoc : crea un docstring por atributo.

```python
class Millas:
	def __init__(self):
		self._distancia = 0

	# Función para obtener el valor de _distancia
	def obtener_distancia(self):
		print("Llamada al método getter")
		return self._distancia

	# Función para definir el valor de _distancia
	def definir_distancia(self, recorrido):
		print("Llamada al método setter")
		self._distancia = recorrido

	# Función para eliminar el atributo _distancia
	def eliminar_distancia(self):
		del self._distancia

	distancia = property(obtener_distancia, definir_distancia, eliminar_distancia)
```
## Decorador property
```python
class Millas:
	def __init__(self):
		self._distancia = 0

	# Función para obtener el valor de _distancia
	# Usando el decorador property
	@property
	def obtener_distancia(self):
		print("Llamada al método getter")
		return self._distancia

	# Función para definir el valor de _distancia
	@obtener_distancia.setter
	def definir_distancia(self, valor)
		if valor < 0:
			raise ValueError("No es posible convertir distancias menores a 0.")
		print("Llamada al método setter")
		self._distancia = valor
```
## Herencia

```python
class Rectangulo:

    def __init__(self, base, altura):
        self.base = base
        self.altura = altura

    def area(self):
        return self.base * self.altura

class Cuadrado(Rectangulo):

    def __init__(self, lado):
        super().__init__(lado, lado)
```
## Polimorfismo
```python
class Persona:

    def __init__(self, nombre):
        self.nombre = nombre

    def avanza(self):
        print('Ando caminando')


class Ciclista(Persona):

    def __init__(self, nombre):
        super().__init__(nombre)

    def avanza(self):
        print('Ando moviendome en mi bicicleta')
```