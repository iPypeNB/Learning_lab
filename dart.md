# Lenguaje de programación Dart

## ¿Que es Dart?

Es un lenguaje de progamación optimizado al cliente creado en 2011 por Google con la inteción de crear aplicaciones de forma rapida para cualquier plataforma. Dart es un lenguaje estructurado, fuertemente tipado e "interpretado" que hace uso de una vm para su interpretación (dartVM). Aunque dependiendo del modo de ejecución dartVM va a interpretar (JIT) o compilar (AOT) el código dart.

## Caractarísticas de Dart

- Es un lenguaje multiparadigma (permite programar de forma imperativa y declarativa (flutter)).
- "Todo en dart es un objeto" (orientado a objetos).
- Especializado a tener uso en multiplataformas y crear apps de forma rapida.
- Inspirado en lenguajes como C, C#, Java.
- Fue pensado para hacer aplicaciones web.
- Tiene un transpilador web llamado dart2js.
- flutter usa dart utilizando el traspilador dart2native.

## ¿Como funciona?

Como mencioné anteriormente dart es un lenguaje que según su forma de ejecución es interpretado o compilado por dartVM, estos dos modos de ejecución son:
- just in time (JIT): permite programar a mayor velocidad, ya que al interpretar el código con dartVM está implementa ciertas herramientas que permite el desarrollo simultaneo con el debug (esto es conocido como hot reload).
- Ahead of time (AOT): Este tipo de ejecución crea un archivo compilado de forma optimizada ya que al generar las aplicaciones remueve recursos inecesarios y hace que la aplicación funcione de forma nativa a partir de un archivo binario, este modo de ejecución tiene una optimización con el "garbage collector" (recolector de basura) lo que le permite tener como resultado apps mas rápidas y optimizadas con el uso de memoria.</br>
[¿Como funciona DartVM?](https://medium.com/comunidad-flutter/introducci%C3%B3n-a-dart-vm-889aedcd9c00)

## Palabras reservadas

Las palabras reservadas de los lenguajes con aquellas palabras que utiliza el interpretador o compilador para realizar una accion predeterminada (una accion definida por los creadores del lenguaje), por lo tanto en nuestros códigos es importante tener en cuenta que estar palabras no se debe usar como nombres en las variables. a continuación voy a mostrar las palabras reservadas mas comúnes de Dart:
- enum: permite crear una enumeracion de variables constantes con sus propios nombres, esto normalmente es utilizado para crear una maquina de estados en la aplicación.
- abstract: permite crear una función abstracta.
- assert: permite validar una afirmación sobre una expresion, esta palabra normalmente se usa para validar y generar los posibles casos de error en nuestra aplicación.
- as: se utiliza como operador de fundicion de tipo, normalmente se utiliza para asignar un nuevo "nombre" a las librerias importadas.
- async: se utiliza para definir una funcion como una funcion asincronica.
- show: se utiliza para exponer elementos especificos de las importaciones realizadas en un archivo dart.
- catch: "Captura" el error generado dentro de una función try.
- continue: permite saltar las declaraciones subsiguientes a la iteración actual en un ciclo.
- break: rompe la ejecucion iterativa de un ciclo o funcion, finalizando esa ejecución (parte del código).
- export: permite exportar los algoritmos de otros archivos dart.
- import: permite importar el algoritmo de otro archivo dart.
- static: se utiliza para la gestión de memoria de los miembros de datos globales, en un objeto cuando los metodos se declaran estaticos estos pertenecen a la clase en lugar de a la instancia.
- late: inidica al compilador que una variable al momento de ser utilizada tendrá un valor pero al momento de definirla no.
- required: define un parametro obligatorio para las funciones.

## Comentarios en dart:

Los comentarios son pequeñas descripciones sobre el códgio escrito, que el interptretador o compilador no toma en cuenta al momento de ejecutar el algoritmo. Los comentarios son una parte fundamental para el desarrollo de software ya que esto nos permite trabajar de una forma mas verbal y compresible con nuestro código, conservando la intención (objetivo) de un algoritmo y experandola de forma comprensible, aumentando la capacidad del trabajo en equipo, la forma de hacer comentarios en Dart es:

- //*texto*: permite hacer comentarios en una sola linea.
- /* *texto* */: permite hacer comentarios en varias lineas. (comentarios en bloque).

### Comentarios para la documentación

_Nota*: los comentarios con documentación son aquellos comentarios que toma el interpretador, editor de codigo o IDE para mostrar en los intelisense optimizando la escritura de código._

- ///*texto*: esto permite documentar en una linea.
- /** *texto* */: esto permite documentar en bloque.

## Operadores

1. **Aritmeticas:**
    - suma (+)
    - resta (-)
    - multipicacion (*)
    - division (/)
    - division entera (~/)
    - modulo (%)
1. **Asignacion aritmetica:**
    - += : suma y asigna.
    - -= : resta y asigna.
    - /= : divide y asigna.
    - *= : multiplica y asigna.
    - ~/= : division entera luego asigna.
    - =% : modulo y luego asigna.
1. **Relacionales:**
    - == :  valida si dos variables son "iguales".
    - =! : valida si dos variables son "diferentes".
    - \> : mayor que.
    - \< : menor que.
1. **Bit a bit:**
    - & :  and bit a bit
    - | :  or bit a bit
1. **Logicas:**
    - || : or.
    - && : and.
    - ! : not.
1. __Incremento y decremento (tipos de datos numericos):__ 
    - i++ : primero asigna luego suma
    - ++i : primero suma luego asigna
    - i-- : primero asigna luego resta
    - --i : primero resta luego asigna
1. **Operador de tipo**
    - is : valida si el tipo coincide
    - is! : valida si el tipo no coincide
2. **Operadores condicionales**
    - ? : operador ternario. (valida una condicion verdadera)
    - ??: operador nulo. (valida si el elemento es nulo)

## Tipo de datos y variables

### Variables

1. ¿Qué es una variable?<br>
Es un espacio reservado en la memoria donde se va a almacenar un tipo de dato. (a dart le gusta utilizar camelCase) (snake_case)

1. Operaciones de las variables (manipulacion de los tipos de variables)<br>
    _Nota*: la declaracion de las variables es muy similar al de C++._
    - __Declaración__: es cuando se define el tipo de la variable. (por primera ves definimos su nombre y su tipo).
    - __Inicialización__: cuando le definimos por primera vez su valor.
    - __Asignación__: cuando una varible ya teniendo un valor le cambiamos el valor.

1. Tipos de variable
- __const__: es una variable que no puede cambiar su valor una vez inicializado (es una "variable" que debe ser inicializada con un valor constante) (es constante en tiempo de compilacion).
- __final__: esta es una variable que define como "constante" la direccion o el valor definidos en la inicializacion (es constante en tiempo de ejecucion).
- __late__: permite declarar variable, dando como "garantia" de que estas van a ser inicializadas en tiempo de ejecucion.

    > **final vs const:**
    >    - las variables *final* pueden ser instanciados en tiempo de ejecucion las variables *const* no.
    >    
    >    ```dart
    >    main() {
    >        const a = 10;
    >        final b;
    >        b = 10;
    >    }
    >    ```
    >    - *final* no defina a los objetos como inmutables al 100%, es decir en el caso de las colecciones. (con *final* se pueden agregar parametros a una coleccions pero sus valores no pueden ser modificados, esto no es posible con *const*)
    >    ```dart
    >    main () {
    >        final a = [1,2,3]
    >        a.add(4)
    >    }
    >    ```

### Datos

1. ¿Que es un dato?<br>
Los datos en los lenguajes de programación definen el el tipo del contenido de las variables, es decir, definen que va a contener la direccion reservada en la memoria por la variable.
1. Tipos de datos.
    - **Booleano:** true or false (se usa bool) define o verdadero o falso (1 o 0)
    - **int:** numeros en enteros sin decimales (8 bytes).
    - **double:** numero enteros y con decimales (utiliza 16 bytes segun donde se transpile). utiliza mas espacio en memoria, ya que debe almacenar las decimas para los numeros con decimales.
    - **String:** nos permite almacenar cadena de caracteres
    - **colecciones:** nos permite almacenar muchos valores de un mismo tipo de dato a la vez en una sola variable.
        - list (palabra reservada List): se coloca el tipo enter <> y los valores entre []
    - **var:** infiere el tipo de dato, aunque es buena politica de programacion saber que tipo de dato vamos a declarar. Cuando se declara una variable var y se le asigna un tipo de dato, este tipo de dato no puede ser cambiado despues. (var name = "Felipe", name=10) esto va a arrojar error.
    - **dynamic:** permite inferir el tipo de valor que vamos a almacenar y tambien permite despues cambiar su tipo de valor.

## Operaciones especiales

### Manipulacion de strings

- **concatenacion e interpolacion:** se utiliza el simbolo de +
- **interpolacion:** se utiliza el simbolo $ permite la asignacio o incrustacion de un string dentro de otro.
- **\\:** no permite la implementacion de caracteres especiales dentro de los strings.
- **toUpperCase:** todo mayuscula
- **toLowerCase:** todo minuscula

### Conversion entre tipos de variables

1. numerico & string:
    - **string to num:** int.parse(), double.parse()
    - **num to string:** toString()
1. int y double:
    - **suma:** el resultado de la suma entre un entero y un double es un double.

## Controles de flujo

### condicionales
anidados
consecutivos inclusivos
consecutivos exclusivos
if () {
    verdadero
}
else {
    falso
}

switch(expresion){
    case:
        break;
}

### ciclos
while(condicion){
    verdadero
}

do{
    verdadero
}while(condicion);

for (inicio; final; paso){
    codigo
}

# colecciones
es una estructura que representa un grupo de valores mediante una unica variable, por lo general solo contiene un tipo de dato.

# tipos de colecciones

- List: 
    - definicion: List <int> nombre_variable;
    - first, isempty, length, last, reversed.
    - add, insert, removeAt, clear. print(${name[i]})
    - con ... podemos concatenar listas. ["as","asd",...lista]
- Set:
    - no se pueden repetir los elementos en un set.
    - Set <int> nombre_variable;
    - se usan corchetes en vez de parentesis.
    - elementAt: busca el indice indicado.
- Map:
    - es un diccionario en python.
    - keys: devuelve las llaves.
    - remove: se remueve un valor segun su llave.
    - Map <String,dynamic> nombre_variable;

se pueden poner condiciones y ciclos for adento de las colecciones.


## Bibliografia
https://medium.com/comunidad-flutter/por-qu%C3%A9-flutter-usa-dart-8e7703650def


https://dart.dev/tools/dart-compile

https://dart.dev/tools/dart-run


https://medium.com/@Loopa/paradigmas-de-programaci%C3%B3n-programaci%C3%B3n-imperativa-y-programaci%C3%B3n-declarativa-4c4a4182fd87

www.dart.dev
www.pub.dev (sistema de paquetes)
www.dartpad.dev