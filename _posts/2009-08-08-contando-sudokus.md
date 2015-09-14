---
title: Contando Sudokus
author: castarco
layout: post
permalink: /?p=110
categories:
  - Matemática
tags:
  - Matemática
  - Pasatiempos
---
<p style="text-align: justify;">
  ESCRITO ORIGINALMENTE EN <a href="http://blog.viricmind.org">BLOG.VIRICMIND.ORG</a>
</p>

<p style="text-align: justify;">
  El otro día me estaba aburriendo (como casi siempre) y se me ocurrió una pregunta que a la mayoría de los mortales les parecerá carente de importancia&#8230; la verdad es que yo todavía no he conseguido encontrar ningún motivo para considerarla importante, pero la curiosidad (y sobretodo la dificultad de hallar la respuesta) puede más conmigo que la &#8220;importancia&#8221; de la cuestión.
</p>

> <p style="text-align: justify;">
>   La pregunta es:<br /> &#8220;<em>¿Como se puede calcular la cantidad de n-sudokus que existen?</em>&#8220;
> </p>

<p style="text-align: justify;">
  Para intentar responder a ésto lo primero que deberíamos hacer es definir el término <em>n-sudoku</em>. Daré una definición informal que nos servirá para nuestros propósitos.
</p>

> <p style="text-align: justify;">
>   <strong>Definición:</strong><br /> Un <em>n-sudoku</em> es una matriz de números naturales cuadrada con n² filas y columnas que cumple las siguientes restricciones:
> </p>
> 
>   1. Los únicos números válidos van del *1* al *n*².
>   2. En una fila no se puede repetir ningún número
>   3. En una columna no se puede repetir ningún número
>   4. Si dividimos la matriz en n² submatrices cuadradas disjuntas (sólo hay una forma de hacerlo), en ninguna de ellas se puede repetir ningún número.
> 
> Es claro que el 3-sudoku es el [sudoku][1] que todo el mundo conoce.

<p style="text-align: justify;">
  Antes de continuar tengo que aclarar una cosa: No he conseguido ninguna respuesta satisfactoria, parece que para cada número natural <em>n</em> mayor o igual que 2 tenemos que aplicar cálculos especializados en ese caso concreto. Yo por mi parte he hecho el cálculo para el caso más sencillo, el <em>2-sudoku</em>, que en breve os presento <img src="http://proyectociencia.org/blog/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" /> .
</p>

<p style="text-align: justify;">
  Lo que haré para calcular la cantidad de 2-sudokus que existen es ir rellenando cada casilla de un 2-sudoku con la cantidad de números que podría poner si ya hubiera puesto los anteriores números, la primera secuencia os resultará familiar, que es la cantidad de formas en que podemos ordenas 4 números sin repetición en 4 posiciones distintas (Aviso, iré rellenando una matriz, pero no lo confundamos con el hecho de ir resolviendo un sudoku, porque no lo estoy haciendo).
</p>

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <span style="color: #ff6600;">4</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">?</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">?</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">?</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
</table>

Para rellenar la siguiente fila tendremos que hacer algunas observaciones pero sigue siendo muy sencillo:

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <strong><span style="color: #ff6600;">4</span></strong>
    </td>
    
    <td>
      <strong><span style="color: #ff6600;">3</span></strong>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">2</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">1</span>
    </td>
    
    <td>
      <strong><span style="color: #99cc00;">2</span></strong>
    </td>
    
    <td>
      <strong><span style="color: #99cc00;">1</span></strong>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  El primer <em>2</em> viene dado porque ya se han eliminado dos posibilidades en la primera submatriz, el siguiente 1 viene dado porque sólo se puede rellenar de una sola forma la última casilla de la primera submatriz. En los siguientes números también tenemos 2 y 1 pero tenemos que analizarlo con un poco más de cuidado. Podríamos pensar que ese 2 en realidad es un 1 porque tenemos más restricciones que antes (la fila superior, la submatriz y los elementos de la misma fila que hay en la izquierda). El caso es que tenemos suerte, y los elementos que podemos poner en las casillas <em>(2,3)</em> y <em>(2,4)</em> son los mismos que hay en las casillas <em>(1, 1)</em> y <em>(1, 2)</em> aunque podrían tener otro orden, por lo que sólo tenemos <em>2</em> y <em>1</em> opciones respectivamente.
</p>

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <span style="color: #ff6600;">4</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">2</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">1</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  La casilla <em>(3, 1)</em> la rellenamos con un 2 porque solo tiene las restricciones de la columna a la que pertenece (a la que de momento sólo hemos asignado <em>2</em> números), automáticamente vemos que a la casilla <em>(4, 1)</em> sólo le queda <em>1</em> opción. La casilla <em>(3,2)</em> también tiene dos opciones disponibles, otra vez podría parecer que tiene más restricciones que las de la columna a la que pertenece, pero si observamos bien, veremos que los elemenos que pertenecen a su misma submatriz son los mismos que la estan restringiendo en su columna, por lo que de <em>4</em> opciones seguirá pudiendo escoger <em>2</em>. Obviamente a la casilla <em>(4,2)</em> sólo le queda una opción (o por las restricciones de la columna, o por las de la submatriz).
</p>

<p style="text-align: justify;">
  Ahora es cuando nos encontramos con el problema que por lo visto aparece más veces en el caso de los <em>3-sudokus</em>. En el caso de la casilla (3,3) no tenemos una cantidad fija de números que podamos poner habiendo fijado los anteriores&#8230; a priori parece que esa cantidad depende de la configuración de los números que hayamos escrito anteriormente (mientras construíamos el sudoku, no lo confundamos con los números que hemos anotado nosotros para contar). Pondré dos ejemplos de 2-sudokus para mostrar lo que estoy diciendo.
</p>

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <span style="color: #ff6600;">1</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">4</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">3</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">4</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">4</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">4</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">3</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
</table>

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <span style="color: #ff6600;">2<br /> </span>
    </td>
    
    <td>
      <span style="color: #ff6600;">4</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">1</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">4</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">3</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">4</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">?</span>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  En el caso del primer 2-sudoku resuelto vemos que en la casilla <em>(3, 3)</em> solo podemos poner un número, el 4. En el segundo caso tenemos dos posibilidades para la posición (3, 3), podríamos poner o bien un 1 o bien un 4, pero ojo, lo que a priori parecía un sudoku resoluble ahora se muestra como algo sin solución. Como bien podemos ver, si en la casilla <em>(3, 3)</em> ponemos un 1 o un <em>4</em>, el que no hayamos puesto se tendrá que poner en una de las 3 casillas vacías que nos quedan&#8230; ¡pero en ninguna se puede poner porque las restricciones no lo permiten!
</p>

<p style="text-align: justify;">
  No voy a demostrarlo formalmente, pero es facil ver que no se puede dar el caso en que la casilla <em>(3, 3)</em> pueda tener dos opciones, porque siempre nos encotraremos con el mismo problema, que habrá un número imposible de escribir si se quieren seguir las restricciones.
</p>

<p style="text-align: justify;">
  Por lo que la matriz que usabamos para contar nos quedará así (las casillas restantes a parte de las <em>(3, 3)</em> obviamente solo tendran una opción posible dadas las restricciones).
</p>

<table style="height: 80px;" border="1" width="80">
  <tr>
    <td>
      <span style="color: #ff6600;">4</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">3</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #ff6600;">2</span>
    </td>
    
    <td>
      <span style="color: #ff6600;">1</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">2</span>
    </td>
    
    <td>
      <span style="color: #99cc00;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">2</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">1</span>
    </td>
  </tr>
  
  <tr>
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #3366ff;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">1</span>
    </td>
    
    <td>
      <span style="color: #ff0000;">1</span>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Ahora solo tenemos que multiplicar los números que hemos obtenido y obtendremos <del datetime="2009-08-07T10:43:18+00:00">la cantidad de <em>2-sudokus</em> existentes</del> una cota superior de los sudokus existentes (tendríamos que eliminar las configuraciones que no nos permitían encontrar solución, como la que he mostrado para ejemplificar).<br /> 4·3·2·1 · 2·1·2·1 · 2·2·1·1 · 1·1·1·1 = <strong>384</strong>
</p>

<p style="text-align: justify;">
  Así pues deberíamos calcular cuantas veces puede ocurrir esta situación y restarle ese número a 384. Las submatrices azul y verde determinan los valores de la submatriz<strong> </strong>naranja, por lo que<strong> </strong>sólo hace falta contar cuantas configuraciones pueden tener las matrices azules y verdes manteniendo esa configuración que transformaba el sudoku en irresoluble. Para la casilla (1, 3) (submatriz verde, esquina superior izquierda) podemos poner 4 números, para la casilla (2, 3) (esquina inferior izquierda de la submatriz verde) podemos poner 3 números, para lo que queda de verde sólo nos quedan dos opciones. Para la fila superior de la submatriz azul tenemos dos posibles órdenaciones, podría parecer que lo mismo pasa para la fila inferior, pero resulta que no es así, pues una de las dos posibles ordenaciones sería incompatible también con una ordenación correcta para la submatriz naranja.
</p>

<p style="text-align: justify;">
  Lo que nos da una cantidad de 4·3·2·2 = <strong>48</strong> , con lo que tenemos (ahora sí) que el número de <em>2-sudokus</em> existentes es 384-48 = <strong>336</strong> .
</p>

<p style="text-align: justify;">
  Para acabar, algunos apuntes. El problema que hemos tenido con la casilla (3, 3) ha sido relativamente sencillo de resolver, pero se puede dar el caso en el que realmente no se pueda contar la cantidad de números que se pueden poner en una casilla sabiendo que se han escrito los anteriores, puede que la configuración de los números haga variar dicho número. Y parece que realmente es lo que pasa en los casos en los que n es superior o igual a 3.
</p>

<p style="text-align: justify;">
  Por lo visto la cosa es mas complicada de lo que a primera vista parecía, pues la primera solución encontrada para contar el número de 3-sudokus posibles se halló en <a href="http://es.wikipedia.org/wiki/2005">2005</a> por <a href="http://es.wikipedia.org/wiki/Bertram Felgenhauer">Bertram Felgenhauer</a> y <a href="http://es.wikipedia.org/wiki/Frazer Jarvis">Frazer Jarvis</a>. Para ello contaron con razonamientos lógicos parecidos a los que yo he hecho para este caso más sencillo (obviamente los suyos debieron ser mucho más sofisticados) pero tambien necesitaron que un ordendor estuviera haciendo cálculos por fuerza bruta unas cuantas horas. La cosa no parece fácil. Así pues la pregunta que me hice sigue sin resolver.
</p>

<p style="text-align: justify;">
  Para los que sientan curiosidad por este tipo de juegos, hay que decir que se pueden llegar a complicar mucho, y de muchas formas distintas. Una es aumentar el tamaño del <em>n-sudoku</em>, es decir, aumentar la <em>n</em>. Otra es hacer que las submatrices no sean cuadradas, sino rectangulares.. para eso podríamos definir el concepto <em>(m,n)-sudoku</em>, habría n·m números diferentes, y <em>n·m</em> submatrices no cuadradas de tamaño <em>n·m</em>. Es claro que los n-sudokus son un caso particular de los <em>(m,n)-sudokus</em>, y si ya es complicada la pregunta para el caso particular&#8230; no quiero imaginar como sería en éste.
</p>

<p style="text-align: justify;">
  Pero todavía nos estamos quedando cortos, la cosa se podría complicar más aun si las regiones que hemos usado para las restricciones no fueran submatrices sino conjuntos conexos pero no necesariamente con una distribución tan uniforme y regular como la de los rectángulos o cuadrados. En el artículo de Sudoku de la wikipedia podemos ver un ejemplo, se llaman sudokus nonominos y son no poco complicados.
</p>

<p style="text-align: justify;">
  Si os aburrís ya tenéis algo más en qué pensar, ahora parece que este juego ya no se reduce solo a intentar rellenar huecos :p .
</p>

<p style="text-align: justify;">
  Enlaces adicionales:
</p>

  * [http://en.wikipedia.org/wiki/Mathematics\_of\_Sudoku][2]

 [1]: http://es.wikipedia.org/wiki/Sudoku
 [2]: http://en.wikipedia.org/wiki/Mathematics_of_Sudoku