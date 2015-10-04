---
title: 'Matplotlib: Tutorial de Pyplot &#8211; Parte I'
author: Alejandro Alvarez
layout: page
permalink: /?p=126
categories:
  - Computación
  - Matemática
tags:
  - Documentación Oficial
  - Español
  - gráficas
  - Matplotlib
  - Ploteo
  - PyPlot
  - Python
---
<!-- 		@page { margin: 2cm } 		P { margin-bottom: 0.21cm } -->

<p style="margin-bottom:0;" align="justify">
  <span style="color:#888888;">Lo siguiente es una traducción del capítulo 3 de la documentación oficial de Matplotlib [1]:</span>
</p>

<p style="margin-bottom:0;" align="justify">
  <p style="margin-bottom:0;" align="justify">
    <strong>Tutorial de Pyplot</strong>
  </p>
  
  <p style="margin-bottom:0;" align="justify">
    matplotlib.pyplot es una colección de funciones estilo comando que hacen que matplotlib trabaje como matlab. Cada función de pyplot hace algún cambio a una figura, por ejemplo, crea una figura, crea un área de ploteo en una figura, plotea algunas lineas en un área de ploteo, decora el ploteo con etiquetas, etc &#8230;, matplotlib.pyplot es de estado, en la medida en que realiza un seguimiento de la figura actual, y el ploteo de funciones dirigida a los ejes actuales.
  </p>
  
  <p style="margin-bottom:0;" align="justify">
    <p style="margin-bottom:0;" align="justify">
      <strong>Ejemplo 1:</strong>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <span style="color:#0000ff;"># -*- coding: utf-8 -*-</span>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <span style="color:#0000ff;"> import matplotlib.pyplot as plt </span>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <span style="color:#0000ff;"> plt.plot([1,2,3]) </span>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <span style="color:#0000ff;"> plt.ylabel(&#8216;Algunos Números&#8217;) </span>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <span style="color:#0000ff;"> plt.show() </span>
    </p>
    
    <p style="margin-bottom:0;" align="justify">
      <p style="margin-bottom:0;" align="justify">
        <img class="aligncenter" title="Ejemplo1" src="http://img37.imageshack.us/img37/6808/ej1d.png" alt="" width="416" height="312" />
      </p>
      
      <p style="margin-bottom:0;" align="justify">
        <p style="margin-bottom:0;" align="justify">
          Usted tal vez se este preguntando ¿por qué el eje &#8220;x&#8221; va de 0-2 y el eje “y” de 1-3?. Si proporcionamos una única lista o matriz a el comando plot(), matplotlib supone que es una sucesión de valores de “y”, y genera automáticamente los valores de x para usted. Como los rangos (ranges) en python comienzan desde el 0, por defecto el vector x tiene la misma longitud. Por lo tanto, los datos para x son [0,1,2]. plot() es un comando versatil, puede tomar un número arbitrario de argumentos. Por ejemplo, para la plotear “y” versus “x”, podemos emitir la orden:
        </p>
        
        <p style="margin-bottom:0;" align="justify">
          <p style="margin-bottom:0;" align="center">
            <span style="color:#0000ff;">plt.plot ([1,2,3,4], [1,4,9,16]) </span>
          </p>
          
          <p style="margin-bottom:0;" align="justify">
            <p style="margin-bottom:0;" align="justify">
              Para cada par de argumentos x, y, existe un tercer argumento opcional que es una cadena de formato que indica el color y el tipo de línea del ploteo. Las letras y los símbolos de la cadena de formato son de matlab, y podemos concatenar una cadena de color con una cadena de estilo de línea. La cadena de formato por defecto es &#8216;b- &#8216;, que es una línea sólida azul. Por ejemplo, para la ploteo de arriba con círculos rojos, colocamos:
            </p>
            
            <p style="margin-bottom:0;" align="justify">
              <p style="margin-bottom:0;" align="justify">
                <strong>Ejemplo 2:</strong>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <span style="color:#0000ff;"> # -*- coding: utf-8 -*-</span>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <span style="color:#0000ff;"> import matplotlib.pyplot as plt </span>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <span style="color:#0000ff;"> plt.plot([1,2,3,4], [1,4,9,16], &#8216;ro&#8217;) </span>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <span style="color:#0000ff;"> plt.axis([0, 6, 0, 20]) </span>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <span style="color:#0000ff;"> plt.show() </span>
              </p>
              
              <p style="margin-bottom:0;" align="justify">
                <p style="margin-bottom:0;text-align:center;" align="justify">
                  <img class="aligncenter" title="Ejemplo 2" src="http://img10.imageshack.us/img10/8720/ej2.png" alt="" width="458" height="343" />
                </p>
                
                <p style="margin-bottom:0;" align="justify">
                  Ver la documentación de plot() para obtener una lista completa de los estilos de línea y de cadenas de formato. El comando axis() en el ejemplo de arriba tiene una lista de [Xmin, Xmax, Ymin, Ymax] y especifica la vista de los ejes. Si matplotlib se limitara a trabajar con listas, sería bastante inútil para el procesamiento numérico. Normalmente, se utilizan arreglos (o matrices) de numpy. De hecho, todas las sucesiones se convierten a arreglos de numpy internamente. El siguiente ejemplo ilustra un ploteo varias líneas con distintos estilos de formato en un comando usando arreglos.
                </p>
                
                <p style="margin-bottom:0;" align="justify">
                  <p style="margin-bottom:0;" align="justify">
                    <strong>Ejemplo 3:</strong>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> # -*- coding: utf-8 -*-</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> import numpy as np</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> import matplotlib.pyplot as plt</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> # Partición uniforme del intervalo de tiempo [0,5] </span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"># segundos en sub-intervalos uniformemente distribuidos de 200 ms </span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> t = np.arange(0., 5., 0.2)</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> # guiones rojos, cuadrados azules y triángulos verdes</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <span style="color:#0000ff;"> plt.plot(t, t, &#8216;r&#8211;&#8216;, t, t**2, &#8216;bs&#8217;, t, t**3, &#8216;g^&#8217;)</span>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <img class="aligncenter" title="Ejemplo3" src="http://img208.imageshack.us/img208/5307/ej3.png" alt="" width="454" height="341" />
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    <strong>Referencias</strong>
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
                    [1] http://matplotlib.sf.net/Matplotlib.pdf
                  </p>
                  
                  <p style="margin-bottom:0;" align="justify">
