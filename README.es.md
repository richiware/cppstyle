<!-- TOC GitLab -->

- [Formato](#formato)
    - [Codificación de carácteres](#codificación-de-carácteres)
    - [Longitud de línea](#longitud-de-línea)
    - [Espaciado](#espaciado)
    - [Llaves](#llaves)
    - [Funciones](#funciones)
    - [Condicionales](#condicionales)
    - [Namespaces](#namespaces)
- [Nombrado](#nombrado)
    - [Reglas generales](#reglas-generales)
    - [Tipos](#tipos)
        -[Class vs Struct](#class-vs-struct)
    - [Variables](#variables)
        - [Miembros de una clase](#miembros-de-una-clase)
        - [Miembros de una estructura](#miembros-de-una-estructura)
    - [Variables globales](#variables-globales)
    - [Funciones](#funciones-1)
    - [Ficheros](#ficheros)
        - [Cabeceras](#cabeceras)
- [Código](#código)
    - [Punteros y referencias](#punteros-y-referencias)
        - [Referencias rvalue](#referencias-rvalue)
    - [Puntero nulo](#puntero-nulo)

<!-- /TOC -->

# Formato

## Codificación de carácteres

Es obligatorio usar la codificación de carácteres UTF-8.

## Longitud de línea

Cada línea de texto en el código debe tener como mucho 120 caracteres de largo.

Si una determinada instrucción no puede ocupar menos longitud, se truncará con el carácter '\' en un
separador lo más legible posible, y e indexada respecto al inicio de la intrucción.

```c++
very_long_object_name->very_long_method_name(very_long_variable_name, other_very_long_variable_name)\
    .very_long_method_again();
```

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

El paréntesis de apertura de la lista de cláusulas debe encontrarse espaciado de la palabra reservada `if`.

```c++
// Correcto
if (!error)
{
    return success;
}

// Incorrecto
if(!error)
{
    return success;
}
```

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

## Namespaces

Evitar el uso de "using namespace", en general. Excepto quizás, en ámbitos de método donde pueda clarificar mucho la
lectura del mismo.
Estrictamente prohibido usarlo en ficheros cabecera 
para evitar dificultar la detección de errores por colisiones de nombres.

El código periférico de un bloque ``namespace`` (y cualquiera anidado) no debe estar indentado.
Ademas la llame de apertura debe estar en la misma línea que la declaración del ``namespace``.

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

# Nombrado

## Reglas generales

Los nombres tienen que ser descriptivos, intentando evitar las abreviaciones.
El nombre debe comunicar de la manera más explicita qué es la variable y la información pertinente para que un
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

Deberá usarse el tipo *struct* únicamente para tipos que no realizan operaciones sobre sus miembros,
es decir, tipos que únicamente almacenan datos, y quizás, provean métodos de acceso a sus miembros.
Aunque se recomienda que las *struct* no tengan método alguno y sus miembros sean públicos, como
ya son por defecto.
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
Siguen las reglas de nombrado pero añadiendoles `m_` al comienzo.
Con esto se consigue saber facilmente al leer codigo cuando se cambia el estado de la clase.

Los miembros que se quieran exponer de forma `public` o `protected` tendrá getters y setters.
El nombre de estas funciones será el mismo que la variable pero sin el prefijo `m_`.

```c++
class Table
{
    public:

    void row_count(long count) { m_row_count = count; }

    long row_count() const { return m_row_count; }

    long& row_count() { return m_row_count; }

    void row_content(std::string& content) { m_row_content = content; }

    void row_content(std::string&& content) { m_row_content = content; }

    const std::string& row_content() const { return m_row_content; }

    std::string& row_content() { return m_row_content; }

    private:

        long m_row_count;

        string m_row_content;
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

El nombre de las funciones tienen que estar en minúsculas, con subrayado entre las palabras.

```c++
void set_row_content(std::string content);

bool increase_one_row_above();
```

## Ficheros

Las extensiones usadas para código C++ serán `.h`, `.hpp` y `.cpp`.
Las extensiones usadas para código C serán `.h` y `.c`.

El nombre de ficheros que contengan clases se nombrarán con el nombre de la clase, es decir, usando *CamelCase*.
En otro caso seguirán la nomenglatura de minúsculas separada las palabras por `_`.

### Cabeceras

Los ficheros de cabecera deben nombrarse siempre con extensión `.h` o `.hpp` y ser autocontenidos, es decir, 
que incluyan por sí mismos todos los ficheros cabecera de los que dependan.

Debe evitarse el uso de *forward declaration* en la medida de lo posible y 
en su lugar incluir la cabecera que lo declara.

# Código

## Punteros y referencias

Al declarar punteros y referecias, el simbolo ``*`` y ``&`` debe estar pegado al nombre para evitar confusiones.

```c++

// Correct
int *pointer;
int &reference;
void func(void *data, int &count);
int *x, *y, z; // No confusion here

 // Incorrect
int* pointer;
int& reference;
int* pointer, not_pointer; // Separate it for non confusion.
```

### Referencias rvalue

Siempre que una clase adquiera cierta complejidad o se le de un gran uso interno, implementar
constructor y asignación *move*.

Cualquier implementación de *move* debe invalidar la referencia rvalue. Si no es el mecanismo deseado,
implementar en su lugar *swap* o crear un método explícitamente para dicho mecanismo.

Si una clase tiene recursos que no pueden ser copiados, su constructor y asignación *copy* 
deben marcarse como *delete*, e implementar el constructor y asignación *move* si se desea.
 
```c++
class A
{
    protected:
        Socket m_socket;
        Buffer *m_buffer;
    
    A(A&& other)
    {
        m_socket = std::move(other.m_socket);
        m_buffer = other.m_buffer;
        other.m_buffer = nullptr;
    }
    
    A& operator=(A&& other)
    {
        m_socket = std::move(other.m_socket);
        m_buffer = other.m_buffer;
        other.m_buffer = nullptr;
    }
    
    A(const A&) = delete;
    A& operator=(const A&) = delete;
}
```

## Puntero nulo

El valor nulo se debe declarar en C++ como ``nullptr``.