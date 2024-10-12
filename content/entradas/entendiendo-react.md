+++
title = 'Entendiendo React'
date = 2024-10-11T23:40:07-05:00
draft = false
categories = ['javascript']
[params]
    author = 'Diego Velásquez'
+++
En esta entrada intentaré entender el funcionamento de la librería React
en Javascript usando el [tutorial oficial](https://react.dev/learn/tutorial-tic-tac-toe) como guía.

El objetivo del tutorial es crear un juego de "triqui" para 2, nombre con
el cual conocemos a este juego en Colombia.

Todo el juego se define en el archivo `app.js`.

Los archivos `index.html`, `styles.css`, `index.js`, y dependencias de NPM
tambien son necesarios para el funcionamento correcto del juego; sin
embargo, en esta entrada únicamente abordaré una parte mínima del archivo
`app.js`.

Luego de completar el tutorial satisfactoriamente, pude identificar partes
que no son demasiado obvias para un principiante, y de ahí la motivación
para escribir esta entrada.

El resultado final se verá similar a:
``` Markdown
Next player: x           1. Go to game start
-------------
|   |   |   |
-------------
|   |   |   |
-------------
|   |   |   |
-------------
```
Empecemos. La sintaxis que usa React se denomina JSX, la cual permite
incluir notación HTML que luego será transpilada a Javascript y
ultimamente renderizada en pantalla.

Para comentar código en React se usa alguna de las siguiente sintaxis. He
descubierto que una de ellas funciona en algunos escenarios donde la otra
no funciona:
``` Javascript
{/* Este es un comentario */}
// Este es otro comentario
```
Cada archivo tiene un único componente principal que se puede identificar
porque en su definición dice `export default function`.

1. Un componente de React es una función. El nombre del componente debe ir
en mayúscula. Para el juego:
``` Javascript
export default function Game() {
    {/* Lógica del juego */}
}
```
`Game` es el componente principal y desde el mismo se controlarán otros
componentes "hijo" necesarios para el funcionamiento del juego.

2. Lo que retorna la función del componente `Game` (`return ()`) es sintaxis
JSX, y esta puede incluir atributos y valores personalizados que han sido
definidos en otros componentes:
``` Javascript
return (
    <div>
        <div>
            {/* Aquí irá un componente de React */}
        </div>
        <div>
            <ol>{/* Aquí irá una variable cuyo retorno es JSX */}</ol>
        </div>
    </div>
)
```
3. `className` en React es equivalente a `class` en HTML:
``` Javascript
return (
    <div className="game">
        <div className="game-board">
            {/* Aquí irá un componente de React */}
        </div>
        <div className="game-info">
            <ol>{/* Aquí irá una variable cuyo retorno es JSX */}</ol>
        </div>
    </div>
)
```
4. Tenemos 2 `<div>`. El primero mostrará el tablero de juego, que es
definido bajo el nombre de `Board`:
``` Javascript
return (
    <div className="game">
        <div className="game-board">
            <Board />
        </div>
        <div className="game-info">
            <ol>
                {/* Aquí irá una variable cuyo retorno es notación JSX */}
            </ol>
        </div>
    </div>
)
```
Para utilizar un componente "hijo" en el JSX retornado por otro
componente "padre", se usa la notación `< />`, añadiendo el nombre en
mayúscula luego del signo `<`.

5. El segundo `div>` contiene una `<ol>`, que muestra el historial de
movimientos de ambos jugadores. En el tutorial usan una variable adentro
de la `<ol>` llamada `moves`. En mi opinión, esto debió ser un componente
para mayor facilidad de lectura y estilo:
``` Javascript
return (
    <div className="game">
        <div className="game-board">
            <Board />
        </div>
        <div className="game-info">
            <ol>{moves}</ol>
        </div>
    </div>
)
```
En JSX, las variables se encapsulan entre `{}`.

Esa es toda la estructura del juego.

En una posible futura entrada estudiaremos la lógica del mismo, pero al
menos ya tenemos una noción extremadamente básica de lo que es React.
