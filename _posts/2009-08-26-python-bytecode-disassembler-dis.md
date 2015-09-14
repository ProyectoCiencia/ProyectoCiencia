---
title: Python Bytecode Disassembler ( dis )
author: castarco
layout: post
permalink: /?p=129
categories:
  - Computación
tags:
  - Programación
  - Python
---
<p style="text-align: justify;">
  ESCRITO ORIGINALMENTE EN <a href="http://blog.viricmind.org">BLOG.VIRICMIND.ORG</a>
</p>

<p style="text-align: justify;">
  El artículo que sigue es una traducción de un artículo escrito en la página web <a href="http://www.doughellmann.com/PyMOTW/">Python Module of the Week</a>, que es una especie de recopilatorio de artículos sobre módulos de Python escritos por Doug Hellman. Sus textos se publican bajo la licencia <a href="http://creativecommons.org/">Creative Commons</a> <a href="http://creativecommons.org/licenses/by-nc-sa/3.0/es/">By-Nc-Sa</a> ( como los míos, por si alguien no lo había notado todavía con el logo de la página ).
</p>

<h3 style="text-align: justify;">
  Python Bytecode Disassembler ( dis )
</h3>

<p style="text-align: justify;">
  El módulo que trataremos se llama <em>dis</em> y su principal utilidad es convertir código objeto a una representación de bytecode que sea entendible para los seres humanos (o almenos para aquellos que hayan perdido un poco de su tiempo en intentar entender éstas cosas). Éste texto está indicado para versiones de Python iguales o superiores a la versión 1.4, por lo que no tendréis ningún problema (ahora todo el casi mundo usa versiones iguales o superiores a la 2.4).
</p>

<p style="text-align: justify;">
  El módulo <em>dis</em> incluye funciones para <a href="http://es.wikipedia.org/wiki/Desensamblador">desensamblar</a> <a href="http://es.wikipedia.org/wiki/Bytecode">bytecode</a> de Python (que se genera durante la interpretación del código para acelerar el funcionamiento de los scripts).Observar el código bytecode ejecutado por el <a href="http://es.wikipedia.org/wiki/Intérprete_(informática)">intérprete</a> es una buena forma de optimizar a mano bucles y otras secuencias de código. También es útil para encontrar condiciones de carrera en aplicaciones <a href="http://es.wikipedia.org/wiki/Hilo_de_ejecución">multihilo</a> ya que mirando el bytecode se puede ver en qué &#8220;momento&#8221; es más probable que haya un cambio de hilo.
</p>

<h2 style="text-align: justify;">
  Desensamblado básico
</h2>

La función `dis.dis()` muestra por pantalla la representación del desensamblado de código fuente Python (módulo, clase, método, función, o código objeto). Podemos desensamblar código como el siguiente:

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

my_dict = { 'a':1 }</pre>

ejecutando dis desde la línea de comandos. La salida está organizada en columnas con el número de línea original del código fuente, la “dirección” dentro del código objeto, el nombre de [opcode][1] y los argumentos pasados al opcode.

<pre>$ python -m dis codigo.py
  4           0 BUILD_MAP                1
              3 LOAD_CONST               0 (1)
              6 LOAD_CONST               1 ('a')
              9 STORE_MAP
             10 STORE_NAME               0 (my_dict)
             13 LOAD_CONST               2 (None)
             16 RETURN_VALUE</pre>

<p style="text-align: justify;">
  En este caso el código se traduce a 5 operaciones para inicializar el diccionario (crearlo y llenarlo), luego guarda los resultados en una variable global. Como el intérprete de Python está basado en un esquema de pila, los primeros pasos consisten en poner las constantes en la pila siguiendo el orden correcto con la operación <code>LOAD_CONST</code>, y luego usar <code>STORE_MAP</code> para sacar la clave y el valor que se añadirán al diccionario (no nos olvidemos de que antes se ha hecho la operación <code>BUILD_MAP</code>, los valores añadidos entre la ejecución de <code>BUILD_MAP</code> y <code>STORE_MAP</code> serán las claves y los valores del diccionario que estamos creando). El objeto resultante se enlaza con el nombre &#8220;my_dict&#8221; con la operación <code>STORE_NAME</code>.
</p>

<h2 style="text-align: justify;">
  Desensamblando funciones
</h2>

<p style="text-align: justify;">
  Desafortunadamente desensamblar el módulo entero no lo hace con las funciones que hay en él automáticamente. Por ejemplo, si desensamblamos éste módulo:
</p>

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

def f(*args):
    nargs = len(args)
    print nargs, args

if __name__ == '__main__':
    import dis
    dis.dis(f)</pre>

<p style="text-align: justify;">
  los resultados muestran como se carga el código objeto en la pila y luego se salta dentro de la función (LOAD_CONST, MAKE_FUNCTION), pero el cuerpo de la función <em>no</em> está.
</p>

<pre>$ python -m dis dis_function.py
  4           0 LOAD_CONST               0 (<code>)
              3 MAKE_FUNCTION            0
              6 STORE_NAME               0 (f)

  8           9 LOAD_NAME                1 (__name__)
             12 LOAD_CONST               1 ('__main__')
             15 COMPARE_OP               2 (==)
             18 JUMP_IF_FALSE           29 (to 50)
             21 POP_TOP

  9          22 LOAD_CONST               2 (-1)
             25 LOAD_CONST               3 (None)
             28 IMPORT_NAME              2 (dis)
             31 STORE_NAME               2 (dis)

 10          34 LOAD_NAME                2 (dis)
             37 LOAD_ATTR                2 (dis)
             40 LOAD_NAME                0 (f)
             43 CALL_FUNCTION            1
             46 POP_TOP
             47 JUMP_FORWARD             1 (to 51)
        &gt;&gt;   50 POP_TOP
        &gt;&gt;   51 LOAD_CONST               3 (None)
             54 RETURN_VALUE
</code></pre>

<p style="text-align: justify;">
  Para ver dentro de la función tenemos que pasarla como argumento a <code>dis.dis()</code>.
</p>

<pre>$ python dis_function.py
  5           0 LOAD_GLOBAL              0 (len)
              3 LOAD_FAST                0 (args)
              6 CALL_FUNCTION            1
              9 STORE_FAST               1 (nargs)

  6          12 LOAD_FAST                1 (nargs)
             15 PRINT_ITEM
             16 LOAD_FAST                0 (args)
             19 PRINT_ITEM
             20 PRINT_NEWLINE
             21 LOAD_CONST               0 (None)
             24 RETURN_VALUE</pre>

<h2 style="text-align: justify;">
  Clases
</h2>

<p style="text-align: justify;">
  Se pueden pasar también clases a la función <code>dis</code>, en este caso todos sus métodos son desensamblados a la vez.
</p>

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

import dis

class MyObject(object):
    """Example for dis."""

    CLASS_ATTRIBUTE = 'some value'

    def __init__(self, name):
        self.name = name

    def __str__(self):
        return 'MyObject(%s)' % self.name

dis.dis(MyObject)</pre>

<pre style="text-align: left;">$ python dis_class.py
Disassembly of __init__:
 12           0 LOAD_FAST                1 (name)
              3 LOAD_FAST                0 (self)
              6 STORE_ATTR               0 (name)
              9 LOAD_CONST               0 (None)
             12 RETURN_VALUE

Disassembly of __str__:
 15           0 LOAD_CONST               1 ('MyObject(%s)')
              3 LOAD_FAST                0 (self)
              6 LOAD_ATTR                0 (name)
              9 BINARY_MODULO
             10 RETURN_VALUE</pre>

<h2 style="text-align: left;">
  Desensamblando para debuggear
</h2>

<p style="text-align: justify;">
  A veces puede ser útil ver qué bytecode causó el problema cuando se está debuggeando una excepción. Hay un par de formas de desensamblar el código que encierra el error.
</p>

<p style="text-align: justify;">
  La primera forma consiste en usar <code>dis.dis()</code> dentro del intérprete interactivo para que analize la última excepción ocurrida. Si no se le pasa ningún argumento a <code>dis</code>, ésta busca la última excepción ocurrida y muestra el desensamblado de la parte &#8220;más alta&#8221; de la pila que la causó.
</p>

<pre>$ python
Python 2.6.2 (r262:71600, Apr 16 2009, 09:17:39)
[GCC 4.0.1 (Apple Computer, Inc. build 5250)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
&gt;&gt;&gt; import dis
&gt;&gt;&gt; j = 4
&gt;&gt;&gt; i = i + 4
Traceback (most recent call last):
  File "", line 1, in
NameError: name 'i' is not defined
&gt;&gt;&gt; dis.distb()
  1 --&gt;       0 LOAD_NAME                0 (i)
              3 LOAD_CONST               0 (4)
              6 BINARY_ADD
              7 STORE_NAME               0 (i)
             10 LOAD_CONST               1 (None)
             13 RETURN_VALUE
&gt;&gt;&gt;</pre>

<p style="text-align: justify;">
  Notad la flecha <code>--&gt;</code> indicando el opcode que causó el error. La variable “i” no está definida, por lo que el valor asociado con el nombre no puede ser cargado en la pila.
</p>

<p style="text-align: justify;">
  Desde tu propio código puedes mostrar por pantalla información sobre el <em>traceback</em> pasándolodirectamente como argumento a dis.distb(). En este ejemplo hay una excepción DivideByZero, pero como la fórmula tiene dos partes, no está claro cual de los elementos es el cero.
</p>

<pre style="text-align: justify;" lang="python">#!/usr/bin/env python
# encoding: utf-8

i = 1
j = 0
k = 3

# ... many lines removed ...

try:
    result = k * (i / j) + (i / k)
except:
    import dis
    import sys
    exc_type, exc_value, exc_tb = sys.exc_info()
    dis.distb(exc_tb)</pre>

<p style="text-align: justify;">
  El valor incorrecto es fácil de detectar cuando está cargado en la pila dentro del desensamblado. La operación incorrecta está remarcada con la flecha <code>--&gt;</code>, y sólo tenemos que mirar unas cuantas líneas hacia arriba para encontrar dónde se ha cargado el valor 0 en la pila.
</p>

<pre>$ python dis_traceback.py
  4           0 LOAD_CONST               0 (1)
              3 STORE_NAME               0 (i)

  5           6 LOAD_CONST               1 (0)
              9 STORE_NAME               1 (j)

  6          12 LOAD_CONST               2 (3)
             15 STORE_NAME               2 (k)

 10          18 SETUP_EXCEPT            26 (to 47)

 11          21 LOAD_NAME                2 (k)
             24 LOAD_NAME                0 (i)
             27 LOAD_NAME                1 (j)
    --&gt;      30 BINARY_DIVIDE
             31 BINARY_MULTIPLY
             32 LOAD_NAME                0 (i)
             35 LOAD_NAME                2 (k)
             38 BINARY_DIVIDE
             39 BINARY_ADD
             40 STORE_NAME               3 (result)
             43 POP_BLOCK
             44 JUMP_FORWARD            65 (to 112)

 12     &gt;&gt;   47 POP_TOP
             48 POP_TOP
             49 POP_TOP

 13          50 LOAD_CONST               3 (-1)
             53 LOAD_CONST               4 (None)
             56 IMPORT_NAME              4 (dis)
             59 STORE_NAME               4 (dis)

 14          62 LOAD_CONST               3 (-1)
             65 LOAD_CONST               4 (None)
             68 IMPORT_NAME              5 (sys)
             71 STORE_NAME               5 (sys)

 15          74 LOAD_NAME                5 (sys)
             77 LOAD_ATTR                6 (exc_info)
             80 CALL_FUNCTION            0
             83 UNPACK_SEQUENCE          3
             86 STORE_NAME               7 (exc_type)
             89 STORE_NAME               8 (exc_value)
             92 STORE_NAME               9 (exc_tb)

 16          95 LOAD_NAME                4 (dis)
             98 LOAD_ATTR               10 (distb)
            101 LOAD_NAME                9 (exc_tb)
            104 CALL_FUNCTION            1
            107 POP_TOP
            108 JUMP_FORWARD             1 (to 112)
            111 END_FINALLY
        &gt;&gt;  112 LOAD_CONST               4 (None)
            115 RETURN_VALUE</pre>

<h2 style="text-align: justify;">
  Análisis de rendimiento en bucles
</h2>

<p style="text-align: justify;">
  Además de para localizar errores, <em>dis</em> también puede ayudar a encontrar problemas de rendimiento en nuestro código. Examinar el código desensamblado es especialmente útil con pequeños bucles en los que el número de líneas de código Python es pequeño pero éstas se ejecutan lentamente ya que se traducen a un conjunto ineficiente de bytecodes. Veremos como el desensamblado nos ayuda a examinar unas pocas implementaciones de una clase, <em>Dictionary</em>, que lee un conjunto de palabras y las agrupa por su primera letra.
</p>

Antes de nada, la aplicación que usaremos para hacer los tests:

<pre lang="python">import dis
import sys
import timeit

module_name = sys.argv[1]
module = __import__(module_name)
Dictionary = module.Dictionary

dis.dis(Dictionary.load_data)
print
t = timeit.Timer(
    'd = Dictionary(words)',
    """from %(module_name)s import Dictionary
words = [l.strip() for l in open('/usr/share/dict/words', 'rt')]
    """ % locals()
    )
iterations = 10
print 'TIME: %0.4f' % (t.timeit(iterations)/iterations)</pre>

<p style="text-align: justify;">
  Podemos usar <em>dis_test_loop.py</em> para ejecutar cada versión de la clase <em>Dictionary</em> que hagamos.
</p>

Una implementación sencilla de la classe Dictionary puede ser algo así:

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

class Dictionary(object):

    def __init__(self, words):
        self.by_letter = {}
        self.load_data(words)

    def load_data(self, words):
        for word in words:
            try:
                self.by_letter[word[0]].append(word)
            except KeyError:
                self.by_letter[word[0]] = [word]</pre>

<p style="text-align: justify;">
  La salida muestra que esta versión ha tomado 0.1074 segundos para cargar las 234936 palabras en mi copia de /usr/share/dict/words en OS X [Recordad que es una traducción y no lo hice directamente yo ésto]. No está demasiado mal, pero como podemos ver en el desensamblado de abajo, el bucle. está haciendo más trabajo del necesario. Tal como entra en el bucle en el opcode 13, se instala el contexto de una excepción (SETUP_EXCEPT). Entonces usa 6 opcodes para encontrar self.by_letter[word[0]] antes de añadir la palabra a la lista. Si se lanza una excepción porque word[0] todavía no está en el diccionario, el manejador de excepciones hace otra vez el mismo trabajo para determinar word[0] (3 opcodes) y inicializa self.by_letter[word[0]] como una nueva lista que contiene la palabra.
</p>

<pre>$ python dis_test_loop.py dis_slow_loop
 11           0 SETUP_LOOP              84 (to 87)
              3 LOAD_FAST                1 (words)
              6 GET_ITER
        &gt;&gt;    7 FOR_ITER                76 (to 86)
             10 STORE_FAST               2 (word)

 12          13 SETUP_EXCEPT            28 (to 44)

 13          16 LOAD_FAST                0 (self)
             19 LOAD_ATTR                0 (by_letter)
             22 LOAD_FAST                2 (word)
             25 LOAD_CONST               1 (0)
             28 BINARY_SUBSCR
             29 BINARY_SUBSCR
             30 LOAD_ATTR                1 (append)
             33 LOAD_FAST                2 (word)
             36 CALL_FUNCTION            1
             39 POP_TOP
             40 POP_BLOCK
             41 JUMP_ABSOLUTE            7

 14     &gt;&gt;   44 DUP_TOP
             45 LOAD_GLOBAL              2 (KeyError)
             48 COMPARE_OP              10 (exception match)
             51 JUMP_IF_FALSE           27 (to 81)
             54 POP_TOP
             55 POP_TOP
             56 POP_TOP
             57 POP_TOP

 15          58 LOAD_FAST                2 (word)
             61 BUILD_LIST               1
             64 LOAD_FAST                0 (self)
             67 LOAD_ATTR                0 (by_letter)
             70 LOAD_FAST                2 (word)
             73 LOAD_CONST               1 (0)
             76 BINARY_SUBSCR
             77 STORE_SUBSCR
             78 JUMP_ABSOLUTE            7
        &gt;&gt;   81 POP_TOP
             82 END_FINALLY
             83 JUMP_ABSOLUTE            7
        &gt;&gt;   86 POP_BLOCK
        &gt;&gt;   87 LOAD_CONST               0 (None)
             90 RETURN_VALUE

TIME: 0.1074</pre>

<p style="text-align: justify;">
  Una técnica para elimnar la excepción es rellenar self.by_letter con una lista para cada letra del alfabeto antes de empezar a llenar el diccionario. Esto significa que siempre podremos hacer la operación append satisfactoriamente sin necesidad de manejar ninguna excepción.
</p>

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

import string

class Dictionary(object):

    def __init__(self, words):
        self.by_letter = dict( (letter, [])
                                for letter in string.letters)
        self.load_data(words)

    def load_data(self, words):
        for word in words:
            self.by_letter[word[0]].append(word)</pre>

<p style="text-align: justify;">
  El cambio reduce el número de opcodes aproximadamente a la mitad, pero solo se reduce el tiempo a 0.0984 segundos. Obviamente el manejo de la excepción añadía un cierto overhead pero tampoco demasiado.
</p>

<pre>$ python dis_test_loop.py dis_faster_loop
 14           0 SETUP_LOOP              38 (to 41)
              3 LOAD_FAST                1 (words)
              6 GET_ITER
        &gt;&gt;    7 FOR_ITER                30 (to 40)
             10 STORE_FAST               2 (word)

 15          13 LOAD_FAST                0 (self)
             16 LOAD_ATTR                0 (by_letter)
             19 LOAD_FAST                2 (word)
             22 LOAD_CONST               1 (0)
             25 BINARY_SUBSCR
             26 BINARY_SUBSCR
             27 LOAD_ATTR                1 (append)
             30 LOAD_FAST                2 (word)
             33 CALL_FUNCTION            1
             36 POP_TOP
             37 JUMP_ABSOLUTE            7
        &gt;&gt;   40 POP_BLOCK
        &gt;&gt;   41 LOAD_CONST               0 (None)
             44 RETURN_VALUE

TIME: 0.0984</pre>

<p style="text-align: justify;">
  Podemos optimizar aún más el rendimiento moviendo el acceso a self.by_letter fuera del bucle (dado que el valor no cambia en ningún momento).
</p>

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

import collections

class Dictionary(object):

    def __init__(self, words):
        self.by_letter = collections.defaultdict(list)
        self.load_data(words)

    def load_data(self, words):
        by_letter = self.by_letter
        for word in words:
            by_letter[word[0]].append(word)</pre>

<p style="text-align: justify;">
  Los opcodes 0-6 ahora encuentran el valor de self.by_letter y lo guardan como la variable local by_letter. Usar variables locales solo requiere un opcode en vez de 2 (en la posición 22 se usa LOAD_FAST para almacenar dictionary en la pila). Después de este cambio el tiempo de ejecución se reduce a 0.0842 segundos.
</p>

<pre>$ python dis_test_loop.py dis_fastest_loop
 13           0 LOAD_FAST                0 (self)
              3 LOAD_ATTR                0 (by_letter)
              6 STORE_FAST               2 (by_letter)

 14           9 SETUP_LOOP              35 (to 47)
             12 LOAD_FAST                1 (words)
             15 GET_ITER
        &gt;&gt;   16 FOR_ITER                27 (to 46)
             19 STORE_FAST               3 (word)

 15          22 LOAD_FAST                2 (by_letter)
             25 LOAD_FAST                3 (word)
             28 LOAD_CONST               1 (0)
             31 BINARY_SUBSCR
             32 BINARY_SUBSCR
             33 LOAD_ATTR                1 (append)
             36 LOAD_FAST                3 (word)
             39 CALL_FUNCTION            1
             42 POP_TOP
             43 JUMP_ABSOLUTE           16
        &gt;&gt;   46 POP_BLOCK
        &gt;&gt;   47 LOAD_CONST               0 (None)
             50 RETURN_VALUE

TIME: 0.0842</pre>

<p style="text-align: justify;">
  Una mayor optimización sugerida por Brandon Rhodes es eliminar la versión Python del bucle por completo. Si usamos <code>groupby()</code> del módulo <em>itertools</em> para agrupar la entrada, la iteración es movida a código <a href="http://es.wikipedia.org/wiki/Lenguaje_de_programación_C">C</a>. Podemos hacer ésto porque sabemos que la entrada está ordenada. En caso de no saber si está ordenada o no, deberíamos ordenarla por si acaso.
</p>

<pre lang="python">#!/usr/bin/env python
# encoding: utf-8

import operator
import itertools

class Dictionary(object):

    def __init__(self, words):
        self.by_letter = {}
        self.load_data(words)

    def load_data(self, words):
        # Arrange by letter
        grouped = itertools.groupby(words, key=operator.itemgetter(0))
        # Save arranged sets of words
        self.by_letter = dict((group[0][0], group) for group in grouped)</pre>

<p style="text-align: justify;">
  La versión con <em>itertools</em> solo tarda 0.0543 segundos en ejecutarse, más o menos la mitad del tiempo original.
</p>

<pre>$ python dis_test_loop.py dis_eliminate_loop
 15           0 LOAD_GLOBAL              0 (itertools)
              3 LOAD_ATTR                1 (groupby)
              6 LOAD_FAST                1 (words)
              9 LOAD_CONST               1 ('key')
             12 LOAD_GLOBAL              2 (operator)
             15 LOAD_ATTR                3 (itemgetter)
             18 LOAD_CONST               2 (0)
             21 CALL_FUNCTION            1
             24 CALL_FUNCTION          257
             27 STORE_FAST               2 (grouped)

 17          30 LOAD_GLOBAL              4 (dict)
             33 LOAD_CONST               3 (<code> at 0x7e7b8, file "/Users/dhellmann/Documents/PyMOTW/dis/PyMOTW/dis/dis_eliminate_loop.py", line 17&gt;)
             36 MAKE_FUNCTION            0
             39 LOAD_FAST                2 (grouped)
             42 GET_ITER
             43 CALL_FUNCTION            1
             46 CALL_FUNCTION            1
             49 LOAD_FAST                0 (self)
             52 STORE_ATTR               5 (by_letter)
             55 LOAD_CONST               0 (None)
             58 RETURN_VALUE

TIME: 0.0543
</code></pre>

<h3 style="text-align: justify;">
  Referencias:
</h3>

  * **Artículo original: **<http://www.doughellmann.com/PyMOTW/dis/>
  * **Módulo dis: **<http://docs.python.org/library/dis.html>
  * **Módulo itertools**: <http://docs.python.org/library/itertools.html>

<div id="_mcePaste" style="overflow: hidden; position: absolute; left: -10000px; top: 8680px; width: 1px; height: 1px;">
  <pre>$ python dis_test_loop.py dis_eliminate_loop
 15           0 LOAD_GLOBAL              0 (itertools)
              3 LOAD_ATTR                1 (groupby)
              6 LOAD_FAST                1 (words)
              9 LOAD_CONST               1 ('key')
             12 LOAD_GLOBAL              2 (operator)
             15 LOAD_ATTR                3 (itemgetter)
             18 LOAD_CONST               2 (0)
             21 CALL_FUNCTION            1
             24 CALL_FUNCTION          257
             27 STORE_FAST               2 (grouped)

 17          30 LOAD_GLOBAL              4 (dict)
             33 LOAD_CONST               3 (&lt;code object &lt;genexpr&gt; at 0x7e7b8, file "/Users/dhellmann/Documents/PyMOTW/dis/PyMOTW/dis/dis_eliminate_loop.py", line 17&gt;)
             36 MAKE_FUNCTION            0
             39 LOAD_FAST                2 (grouped)
             42 GET_ITER
             43 CALL_FUNCTION            1
             46 CALL_FUNCTION            1
             49 LOAD_FAST                0 (self)
             52 STORE_ATTR               5 (by_letter)
             55 LOAD_CONST               0 (None)
             58 RETURN_VALUE

TIME: 0.0543</pre>
</div>

 [1]: http://es.wikipedia.org/wiki/Opcode