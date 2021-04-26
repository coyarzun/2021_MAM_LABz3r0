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

Utilizamos comentarios para comunicarnos y como manera de documentar nuestro código.
Todo texto en una línea despues de un `//` también se transforma en comentario.

`//a continuación sumaremos los índices
var k=i+j;
k*=2//y duplicamos nuestro valor`

punto y coma

white spaces

usar sólo palabras reservadas.


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

`void setup(){  
  createCanvas(100,100);
  frameRate(10);//correré a 10 fps
}`

y podemos leer cuantos frames hemos ejecutado usando frameCount, una variable de sistema.

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

background(frameCount);

el color de fondo vá de negro a blanco y luego se queda pegado.
lo que sucede es que frameCount sobrepasó el valor de 255, límite válido para nuestro sistema de color,
usando el operador módulo % podemos 















