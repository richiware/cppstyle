# Guía de estilo para el lenguaje C++

## Contenido

* [Formato](#formato)
    * [Longitud de línea](#longitud-de-línea)
    * [Espaciado](#espaciado)
    * [Llaves](#llaves)
    * [Condicionales](#condicionales)
    * [Namespaces](#namespaces)
* [Nombrado](#nombrado)
    * [Reglas generales](#reglas-generales)
    * [Ficheros](#ficheros)
    * [Tipos](#tipos)
    * [Variables](#variables)
    * [Funciones](#funciones)
* [Código](#código)
    * [Punteros y referencias](#punteros-y-referencias)
    * [Puntero nulo](#puntero-nulo)

## Formato

### Longitud de línea

Cada línea de texto en el código debe tener como mucho 120 caracteres de largo.

### Espaciado

* Se tiene que indentar usando 4 espacios, nunca indentando con tabuladores. Casi todos los editores actuales soportan
configurarlo.
* No se debe utilizar tabuladores a lo largo de la línea ni espacios en blanco al final de la línea.
* La lista de parámetros de un método o la lista de clausulas de una condición que estén en otra línea, distinta a la
del método o condición, debe tener dos indentaciones (8 espacios) con respecto al método o condición.

    ```c++
    void func(int param1,
            int param2,
            int param3)
    {
        if(param1 == 0 &&
                param2 == 0 &&
                param3 == 0)
        {
        }
    }
    ```

* Debe de haber exactamente una línea en blanco entre métodos para mejorar la claridad y organización visual.
* Los espacios en blanco dentro de los métodos deben de separar funcionalidad (aunque en algunas ocasiones esto
significa que el método puede ser dividido en métodos más pequeños). También es aconsejable un comentario por cada
bloque que defina una funcionalidad, explicando lo que hace.

### Llaves

Los métodos o cualquier otro bloque de código que utilice llaves (`if`/`else`/`switch`/`while` etc.) deben de abrirse
y cerrarse siempre en una nueva línea.

```c++
if(vector.empty())
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
void func(int param1,
        int param2,
        int param3) {
    int varible1;
    int variable2;

    if(param1 == 0 &&
            param2 == 0 &&
            param3 == 0) {
        variable1 = 0;
        variable2 = 0;
    }
}

// Llave en la distinta línea.
void func(int param1,
        int param2,
        int param3)
{
    int varible1;
    int variable2;

    if(param1 == 0 &&
            param2 == 0 &&
            param3 == 0)
    {
        variable1 = 0;
        variable2 = 0;
    }
}
```

### Condicionales


Los condicionales deben de tener siempre llaves, incluso cuando no sean necesarias se deben de utilizar (por ejemplo,
cuando sólo hay una línea de código). Con ello se intenta prevenir errores. Estos errores pueden ser,
agregar una segunda línea de código dentro del `if` esperando que sea parte del mismo bloque. Otro error más peligroso
sería comentar la única línea de código del `if`, lo que convertiría la siguiente línea parte del primer bloque.

```c++
// Correcto
if(!error)
{
    return success;
}

// Incorrecto
if(!error)
    return success;

// Incorrecto
if(!error) return success;
```

Es aconsejable romper condiciones muy ragas tras conexiones lógicas && y ||.

### Namespaces

El código periférico de un bloque ``namespace`` (y cualquiera anidado) no debe estar indentado. Ademas la llame de
apertura puede estar en la misma línea que la declaración del ``namespace``.

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

## Nombrado

### Reglas generales

Los nombres tienen que ser descriptivos, intentando evitar las abreviaciones. El nombre debe comunicar de la manera más
explicita que es la variable y la información pertinente para que un desarrollador pueda usarla apropiadamente.

```c++
// Correcto
int stock_size;
int num_errors;

// Incorrecto
int n;
int nerr;
int s_size;
```

### Ficheros

### Tipos

### Variables

El nombre de las variables (incluyendo los argumentos de una función) y los miembros de tipos tienen que estar en
minúsculas, con subrayado entre las palabras.

```c++
string tablename ;
long row_count;
```

#### Miembros de una clase

Los miembros de una clase siguen las reglas de nombrado de variables. A los miembros privados se les añade un subrayado
al final.

```c++
class Table
{
    public:

        long row_count;

    private:

        string row_content_;
};
```

#### Miembros de una estructura

Los miembros de una estructura siguen las reglas de nombrado de variables.

```c++
struct TableRow
{
    long cell_count;
    string cell_content;
};
```

### Funciones

El nombre de las funciones tienen que estar en minúsculas, con subrayado entre las palabras.

```c++
void set_row_content(std::string content);

bool increase_one_row_above();
```

# Código

## Punteros y referencias

Al declarar punteros y referecias, el simbolo ``*`` y ``&`` debe estar pegado al tipo.

```c++

// Correct
int* pointer;
int& reference;
void func(void* data, int& count);

// Incorrect
int *pointer;
int &reference;
int* pointer, not_pointer; // Separate it for non confusion.
```

## Puntero nulo

El valor nulo se debe declarar en C++ como ``nullptr``.
