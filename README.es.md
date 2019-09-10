<!-- TOC GitLab -->

- [Formato](#formato)
    - [Codificación de carácteres](#codificación-de-carácteres)
    - [Longitud de línea](#longitud-de-línea)
    - [Espaciado](#espaciado)
    - [Llaves](#llaves)
    - [Funciones](#funciones)
    - [Templates](#templates)
    - [Condicionales](#condicionales)
    - [Constructores](#constructores)
    - [Namespaces](#namespaces)
- [Nombrado](#nombrado)
    - [Reglas generales](#reglas-generales)
    - [Tipos](#tipos)
        - [Class vs Struct](#class-vs-struct)
    - [Variables](#variables)
        - [Miembros de una clase](#miembros-de-una-clase)
        - [Miembros de una estructura](#miembros-de-una-estructura)
    - [Variables globales](#variables-globales)
    - [Funciones](#funciones-1)
    - [Ficheros](#ficheros)
- [Código](#código)
    - [Punteros y referencias](#punteros-y-referencias)
    - [Puntero nulo](#puntero-nulo)
- [TODO](#todo)

<!-- /TOC -->

# Formato

## Codificación de carácteres

Es obligatorio usar la codificación de carácteres UTF-8.

## Longitud de línea

Cada línea de texto en el código debe tener como mucho 120 carácteres de largo.

## Espaciado

* Se tiene que indentar usando 4 espacios, nunca indentando con tabuladores.
Casi todos los editores actuales soportan configurarlo.
* No se debe utilizar tabuladores a lo largo de la línea ni espacios en blanco al final de la línea.
* Debe de haber exactamente una línea en blanco entre métodos para mejorar la claridad y organización visual.
* Las líneas en blanco dentro de los métodos deben de separar funcionalidad (aunque en algunas ocasiones esto
significa que el método puede ser dividido en métodos más pequeños).
También es aconsejable un comentario por cada bloque que defina una funcionalidad, explicando lo que hace.

## Llaves

Los métodos o cualquier otro bloque de código que utilice llaves (`if`/`else`/`switch`/`while` etc.) deben de abrirse
y cerrarse siempre en una nueva línea.

```c++
if (vector.empty() &&
    array.empty())
{
}
else if (!vector.empty() &&
        array.empty())
{
}
else
{
}
```

Con ello se intenta que sea más legible, sobre todo cuando el método tiene muchos parámetros o la condición tiene
muchas clausulas y estan en varias líneas.

```c++
// Llave en la misma línea.
void func(
        int param1,
        int param2,
        int param3) {
    int varible1;
    int variable2;

    if (param1 == 0 &&
        param2 == 0 &&
        param3 == 0) {
        variable1 = 0;
        variable2 = 0;
    }
}

// Llave en la distinta línea.
void func(
        int param1,
        int param2,
        int param3)
{
    int varible1;
    int variable2;

    if (param1 == 0 &&
        param2 == 0 &&
        param3 == 0)
    {
        variable1 = 0;
        variable2 = 0;
    }
}
```

Además las llaves son obligatorias incluso cuando solo hay una sola sentencia en el bloque.

## Funciones

A excepción de las funciones con un único parámetro, los parámetros de un método no deben estar en la misma línea que
define al método y además cada parámetro debe estar en su propia línea.
Además deben tener dos indentaciones (8 espacios) con respecto al método.
Con ello se busca la facilidad de indentación en editores exclusivamente texto y la lectura de los parámetros.

El paréntesis de cierre estará a la altura del último parámetro. Así se evita mejor que se intercambie el último
parámetro por otro sin detectar el cambio de coma.

Esto aplica tanto a la declaración como a la definiciones de la función.

Las definiciones de los métodos tienen que empezar al principio de la línea.


```c++
// Correcto
void function(int param1)
{
}

// Correcto
void function(
        int param1,
        int param2,
        int param3)
{
}

// Incorrecto
void function_with_the_name_so_large(int param1,
        int param2,
        int param3)
{
}

// Correcto
void function_with_the_name_so_large(
        int param1,
        int param2,
        int param3)
{
}

// Correcto
void function_with_the_name_so_large(int param1)
{
}
```

## Templates

Los parámetros del template seguirán la normal de los parámetros de funciones, cada uno en una línea cuando sean más de
uno.
La declaración del template deberá ir en una línea diferente a la entidad que modifica.

```c++
template<class T>
class Test
{
};

template<
    class T,
    int Size>
void function()
{
}
```

## Condicionales

Los condicionales deben de tener siempre llaves, incluso cuando no sean necesarias se deben de utilizar (por ejemplo,
cuando sólo hay una línea de código).
Con ello se intenta prevenir errores.
Estos errores pueden ser, agregar una segunda línea de código dentro del `if` esperando que sea parte del mismo bloque.
Otro error más peligroso sería comentar la única línea de código del `if`, lo que convertiría la siguiente línea parte
del primer bloque.

```c++
// Correcto
if (!error)
{
    return success;
}

// Incorrecto
if (!error)
    return success;

// Incorrecto
if (!error) return success;
```

Entre la palabra clave (`if`, `while`, `for`, etc..) y el parèntesis deberá haber un espacio.

Es aconsejable romper condiciones muy largas tras conexiones lógicas && y || o con el objeto de agruparlas lógicamente.

La lista de clausulas de una condición `if` que estén en otra línea distinta a la de la condición, debe tener una
indentación (4 espacios) con respecto a la condición.
La lista de clausulas de una condición `else if` que estén en otra línea distinta a la de la condición, debe tener dos
indentaciones (8 espacios) con respecto a la condición.

```c++
if (param1 == 0 && param1 > 3 &&
    param2 == 0 && param3 == 0)
{
}
else if (param1 != 0 || param2 == 0 &&
        param3 > 0)
{
}
else
{
}
```

Si por límite de línea una cláusula debe ser partida en varias líneas, se indentará una vez más (+4 espacios).
Si una o más cláusulas resultan poco legibles tras aplicar esta división, 
dichas cláusulas se simplificarán como variables locales.

Si el bloque condicional es demasiado largo o complejo, deberá crearse una función para realizar su funcionalidad.

```c++
// Incorrect
if (very_long_parameter_name_->extremely_long_method_name(long_argument, long_argument2, very_long_cargument) && second_clausule->method_name(arg1, arg2))

// Correct
if (very_long_parameter_name_->extremely_long_method_name(
        long_argument, long_argument2, very_long_cargument) 
    && second_parameter_name->method_name(arg1, arg2))
    
// Correct
bool first_clausule = very_long_parameter_name_->extremely_long_method_name(
        long_argument, long_argument2, very_long_cargument);
bool second_clausule = second_parameter_name->method_name(arg1, arg2);

if (first_clausule && second_clausule)
```

## Constructores

Los parámetros de inicialización irán en líneas separadas, y a excepción del primer parámetros que llevará delantes `:`,
el resto llevará la coma delante.
La indentación será de una identación (4 espacios).

```c++
Constructor(
        int size,
        std::string& msg)
    : size_(size)
    , msg_(msg)
{
}
```

## Namespaces

El código periférico de un bloque ``namespace`` (y cualquiera anidado) no debe estar indentado.
Además la llave de apertura debe estar en la misma línea que la declaración del ``namespace``.

```c++
namespace network {
namespace ip {

class IPv4
{
    public:

        long socket;
};

}
}
```

Usar `using namespace` está prohibido en los ficheros cabecera para evitar dificultar la detección de errores por
colisiones de nombres.

# Nombrado

## Reglas generales

Los nombres tienen que ser descriptivos, intentando evitar las abreviaciones.
El nombre debe comunicar de la manera más explicita que es la variable y la información pertinente para que un
desarrollador pueda usarla apropiadamente.

```c++
// Correcto
int stock_size;
int num_errors;

// Incorrecto
int n;
int nerr;
int s_size;
```

## Tipos

Los tipos seguiran la regla *CamelCase*, es decir, la primera letra es en mayúscula y las letras de inicio de palabra
también mayúscula.

```c++
void clean_space(
        Space space_indoor,
        Time timeout)
{
    Route route();
}
```

### Class vs Struct

Deberá usarse el tipo *struct* únicamente para tipos que no realizan operaciones sobre sus miembros, es decir, tipos que
únicamente almacenan datos, y quizás, provean métodos de acceso a sus miembros.
Aunque se recomienda que las *struct* no tengan método alguno y sus miembros sean públicos, como ya son por defecto.
Si hay más funcionalidad involucrada, deberá definirse como *class*.

## Variables

El nombre de las variables (incluyendo los argumentos de una función) y los miembros de tipos tienen que estar en
minúsculas, con subrayado entre las palabras.

```c++
string table_name;
long row_count;
```

### Miembros de una clase

Todos los miembros de una clase deben ser privados.
Siguen las reglas de nombrado pero añadiendoles un subrayado al final.
Con esto se consigue saber facilmente al leer codigo cuando se cambia el estado de la clase.

Los miembros que se quieran exponer de forma `public` o `protected` tendrá getters y setters.
El nombre de estas funciones será el mismo que la variable pero sin el subrayado.

```c++
class Table
{
    public:

    void row_count(long count) { row_count_ = count; }

    long row_count() const { return row_count_; }

    long& row_count() { return row_count_; }

    void row_content(std::string& content) { row_content_ = content; }

    void row_content(std::string&& content) { row_content_ = content; }

    const std::string& row_content() const { return row_content_; }

    std::string& row_content() { return row_content_; }

    private:

        long row_count_;

        string row_content_;
};
```

### Miembros de una estructura

Los miembros de una estructura siguen las reglas de nombrado de variables.

```c++
struct TableRow
{
    long cell_count;
    string cell_content;
};
```

## Variables globales

Las variables globales siguen las reglas de nombrado de variables pero añadiendoles un prefijo `g_`.


```c++
int g_active_threads = 0;
```

## Funciones

El nombre de las funciones tiene que estar en minúsculas, con subrayado entre las palabras.

```c++
void set_row_content(std::string content);

bool increase_one_row_above();
```

## Ficheros

Las extensiones usadas para código C++ serán `.hpp` y `.cpp`.
Las extensiones usadas para código C serán `.h` y `.c`.

El nombre de ficheros que contengan clases se nombrarán con el nombre de la clase, es decir, usando *CamelCase*.
En otro caso seguirán la nomenglatura de minúsculas separada las palabras por `_`.

# Código

## Punteros y referencias

Al declarar punteros y referecias, el simbolo ``*`` y ``&`` debe estar pegado al tipo.
La excepción será cuando se definan dos variables juntas.

```c++

// Correct
int* pointer;
int& reference;
void func(void* data, int& count);
int *x, *y;

// Incorrect
int *pointer;
int &reference;
int* pointer, not_pointer; // Separate it for non confusion.
```

## Puntero nulo

El valor nulo se debe declarar en C++ como ``nullptr``.


# TODO

Lambdas
Operadores
Uso de c++11
Prácticas recomendadas.
