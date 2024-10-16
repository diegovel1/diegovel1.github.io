+++
title = 'Funcionamiento de un Arraylist en Zig'
date = 2024-10-14T14:41:27-05:00
draft = true
categories = ['zig']
[params]
    author = 'Diego Velásquez'
+++
En la biblioteca estándar de Zig, un `ArrayList` es la implementación
oficial de un vector dinámico.

Un vector dinámico es una estructura de datos que permite almacenar una
lista de elementos y se puede redimensionar sin hacer la gestión de
memoria correspondiente manualmente.

El caso de uso principal para un vector dinámico es la necesidad de
almacenar una cantidad indeterminada de elementos. Si la cantidad de
elementos a almacenar se conoce previamente, un vector estático es más
apropiado.

Veamos el funcionamiento:

1. La implementación viene de la biblioteca estándar de Zig, por lo cual
es necesario importarla:
``` Zig
const std = @import("std");
```
2. Habiendo importado la biblioteca estandar, podemos por ejemplo asignar
la función de `ArrayList` a una variable:
``` Zig
pub fn main() {
    const ArrayList = std.ArrayList;
```
3. El `ArrayList` acepta un Tipo `(T)`, `i32` en nuestro ejemplo, como
argumento y la gestión de memoria ocurre de forma automática durante el
ciclo de vida del mismo. Sin embargo, la inicialización y destrucción del
vector debe hacerse explicitamente:
``` Zig
    const allocator = std.heap.page_allocator;
    var list = ArrayList(i32).init(allocator);
    defer list.deinit();
```
La variable `allocator` guarda el asignador de memoria `page_allocator`
que provee la biblioteca estándar de Zig. La variable `list` inicializa el
`Arraylist`. Por último, hacemos la destrucción de `list` usando el método
`deinit()` acompañado de la palabra `defer`.

En una posible futura entrada estudiaremos el funcionamiento de `defer`.

4. Para demostrar el funcionamiento del `ArrayList`, agreguemos el número
100, usando el método `append()`:
``` Zig
    try list.append(100)
```
Es necesario usar `try` ya que el método `append()` puede retornar un error.

5. Por último, podemos imprimir en pantalla el elemento que añadimos
accediendo a él usando el método `items()` y la notación `[ n]` donde *n*
es el índice en el que se encuentra el elemento, en este caso es el índice
`0`:
``` Zig
    std.debug.print(
        "El Elemento en el indice 0 es: {}",
        .{list.items[0]},
    );
```
El `Arraylist` resultante es:
{{< gist diegovel1 04dd4a58f0ab17ceb06ead559a0006da >}}
