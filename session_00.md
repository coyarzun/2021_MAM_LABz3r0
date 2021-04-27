Sesión 01
---------
Algunas reglas de sintaxis básicas
----------------------------------

Todo lenguaje de programación tiene sus propias reglas de escritura que denominamos sintaxis.
Para ejecutarse, un programa no puede tener errores de sintaxis.

Todo texto que se encuentre entre un `/*`y un `*/` se considerará un comentario, es decir, no se ejecutará.
`/* hola
nada de esto
se ejecutará
*/`

Muchas veces encontraremos esta sintaxis, que llamaríamos comentarios de desarrollador:
`/**  
Suelen contener información relevante 
respecto de autorías, referencias, propósitos, avances y pendientes, 
para nosotrxs mismxs, con otrxs desarrolladorxs o para quienes accedan a este código. 
*/`

Todo texto en una línea despues de un `//` también se transforma en comentario.

`//a continuación sumaremos los índices
var k=i+j;
k*=2//y duplicamos nuestro valor`

Utilizamos comentarios para comunicarnos y como manera de documentar nuestro código, así como para inhabilitar líneas de código por ejemplo cuando debuggeamos o queremos saber qué hace un programa.

Debemos poner un punto y coma `;` al final de cada instrucción para que ésta sea evaluada como tal.

`instruccion1();
instruccion2();`

La única excepción es a continuación de las llaves `{}`. Entre estas se pueden anidar múltiples instrucciones que serán entendidas como un bloque.

`function prueba(){
  hacealgo();//punto y coma después de la primera instrucción
  haceOtraCosa();//punto y coma después de la segunda
}//no hay punto y coma a continuación de las llaves`

Los espacios en blanco o whiteSpaces no son relevantes en el funcionamiento o interpretación del programa, es decir,

`var a = 2*b;`

es equivalente a

`var
  a
= 2*
b
;`

El sentido de los espacios blancos, indentados y tabulaciones es darle una organización visual personalizada al código, facilitando su lectura y acceso. Su uso por tanto es bastante subjetivo y en general responde tanto a convenciones como a decisiones basadas en el gusto del autor.

p5.js es un lenguaje case sensitive, es decir sensible a la caja, lo que quiere decir que mayúsculas y minúsculas son diferentes:



Para facilitar la lectura de nombres compuestos, se utiliza la estrategia de camelCase o cajaDeCamello, es así como encontramos palabras como:

rectMode(center);
strokeWeight(1.0)

Finalmente, sólo podemos utilizar instrucciones y palabras reservadas.

Un primer vistazo a p5.js
-----------------

Lo primero que tenemos cuando nos enfrentamos a la interfaz de p5.js es un código base con el siguiente código:

Aparecen las definiciones de las funciones `setup()` y `draw()`

Las funciones son estructuras de código que se etiquetan bajo un nombre, pudiendo o no recibir argumentos entre los paréntesis.
Entre las llaves `{}` se encuentran las instrucciones que se ejecutarán cuando se invoque o llame a la función.
Algunas funciones realizan operaciones y retornan uno o más valores.
Otras se encargan de realizar tareas sin devolver valor a cambio.

setup() y draw() son funciones "especiales" que denominaremos eventos.
Otros eventos serian mouseUp, mouseDown, onKey?, etc
son funciones reservadas de p5 que están disponibles para ser editadas.

Asimismo definen el flujo de nuestro programa, setup() será invocada una única vez al correr nuestro programa.
draw() en cambio se ejecutará en adelante a un frameRate teórico de 60 fps.
Podemos modificar la velocidad de reproducción usando la función frameRate():

`void setup(){`
`  createCanvas(100,100);`
`  frameRate(10);//correré a 10 fps`
`}`

y podemos leer cuanistos frames hemos ejecutado usando frameCount, una variable de sistema.

`void draw(){
  println(frameCount);//println nos permite imprimir el valor del argumento entre paréntesis, en este caso, de frameCount
}`

Volvamos al código que nos aparece por defecto en el editor.

`createCanvas(400,400);`

Esta línea ejecuta la función createCanvas, creando un lienzo de 400x400 píxeles en base a los argumentos ingresados y que corresponden al ancho y el alto de éste.
En adelante, width y height se encargarán de contener esta información.
El listado de funciones y palabras clave de p5.js se encuentra aquí y es lo que se conoce como API, Application Programming Interface.

Si volvemos a la plantilla de p5.js, tenemos la siguiente instrucción que se ejecuta en draw():

`background(220);`

background es una función que nos permite colorear el fondo de nuestro canvas del color indicado en su argumento.
En el ejemplo, 220 equivale a un gris.
Cuando background recibe UN sólo argumento, este valor es interpretado como una escala de grises de 8 bits, es decir, con valores entre 0 y 255.

`background(0);//negro  
background(128);//gris medio  
background(255);//blanco`  

Sin embargo, background también puede recibir TRES argumentos, y en este caso los interpretará como RGB, es decir como un sistema de color aditivo de tres canales de 8 bits cada uno, correspondientes al Rojo, Verde y Azul respectivamente.

`background(255,0,0);//soy rojo
background(0,255,255);//soy cyan
background(255,128,0);//quién soy?`

Usando la función colorMode, podemos modificar el modo de color e interpretar los colores en el sistema HSB, H de tinte, S de saturación y B de brillo.
Entre las ventajas de utilizar este modo de color, está su plasticidad, ya que es más sencillo e intuitivo poder generar relaciones y variaciones de color en base a estos componentes.
El tinte corresponde a la posición el el espectro cromático y se mide generalmente en grados decimales, es decir, su valor está entre 0° y 360°.
La saturación se suele medir en porcentajes y corresponde a la cantidad de color, a menor saturación nos acercamos a la escala de grises.
El brillo es un valor que se suele medir en porcentajes, a menor brillo nos acercamos al negro.

`colorMode(HSB, 360, 100, 100);//configura el modo de color a HSB con los rangos para cada uno de los componentes según standar
background(180, 50, 100);`

`colorMode(HSB);//configura el modo de color a HSB con los rangos de cada uno de los componentes entre 0 y 255
background(128,128,255);//me he resultado más práctico este manera`

Correlaciones
-------------
Veamos el sgte ejemplo:

`background(frameCount);//un valor entre 1 e infinito`

el color de fondo vá de negro a blanco y luego se queda pegado.
lo que sucede es que frameCount sobrepasó el valor de 255, límite válido para nuestro sistema de color,
usando el operador módulo % podemos convertir este valor en una sierra, que vá de 0 a 255 y luego vuelve a 0.

`background(frameCount%256);//un valor entre cero y 255` 

`a%b`nos retorna el resto de `a` y `b`, un valor entero entre cero y `(b-1)`.
Si `a%b` nos retorna cero, quiere decir que `b` es múltiplo de `2`.
Esto suele ser de utilidad para saber si un número es par o no ( múltiplo de `2` ) caso en que `n%2` sería `0`.

Si aplicamos esto a un `background` definido en `HSB`:

`colorMode(HSB, 255);
background(frameCount%256,255,255);//obtenemos que el color cicla una y otra vez`

Tambien podemos asociar argumentos a valores aleatorios:

`background(random(255));//nos presenta grises aleatorios`

`colorMode(HSB, 255);
background(random(255),255,255);//obtenemos un color aleatorio full saturacion y brillo`

`random(n)` nos entrega un número aleatorio entre `0` y `n`, sin incluir `n`.
`random(n, m)` nos entrega un número aleatorio entre `n` y `m`, sin incluir` m`.

`colorMode(HSB, 255)
background(random(20,50), 255, 255);//un color anaranjado, full saturación y brillo`

`colorMode(HSB, 255)
background(random(20,50), 255, random(255));//un color anaranjado, full saturación y con un brillo que parpadea`

Y, así como podemos vincular nuestros valores a comportamientos deterministas y lineales como el `frameRate`, y aleatorios como el `random`,
también podemos correlacionarlos con eventos indeterminados, como la posición de nuestro mouse, por ejemplo, usando sus coordenadas `mouseX` y `mouseY`:

`function setup(){
  size(256,256);
  colorMode(HSB, 25);
}
function draw(){
  background(mouseX, mouseY, 255);//el tinte queda determinado por la posición horizontal, la saturación por la posición vertical
}`

Bonus track!!
-------------

En el ejemplo anterior, hemos asegurado el funcionamiento de nuestro script dimensionando el canvas a un tamaño seguro de 256x256px,
pero, que sucedería si deseáramos un canvas de distinto tamaño y/o proporciones? Para ello está la función map, que hace las veces de regla de tres, mapeando o escalando nuestro valor de entrada `i` ( con sus respectivos límites, `minI`, `maxI` ), y sus equivalentes de salida ( entre `minO` y `maxO` )

`map(i, minI, maxI, minO, maxO);`

lo cual, aplicado a nuestro ejemplo:

`function setup(){
  createCanvas(600,200);//ancho y alto diferentes a 256
  colorMode(HSB, 25);
}
function draw(){
  background( //acá ocupamos la flexibilidad de los whiteSpaces
                map(mouseX,0,width,0,255),//width nos permite parametrizar nuestro cálculo independiente de las dimensiones dadas en setup
                map(mouseY,0,height,0,255),//y lo mismo height 
                255);//el tinte queda determinado por la posición horizontal, la saturación por la posición vertical
}`


