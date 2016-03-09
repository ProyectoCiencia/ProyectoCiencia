---
title: Un ejemplo sencillo de Gnuplot con Python
author: Alejandro Alvarez
layout: post
categories:
  - General
tags:
  - código
  - Gnuplot
  - gráficas
  - GUPy
  - Proyecto Ciencia
  - Python
---
<a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://www.python.org/images/python-logo.gif"><img style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; width: 211px; height: 71px;" src="http://www.python.org/images/python-logo.gif" alt="" border="0" /></a>  
Buscando la manera de hacer una gráfica sencilla en Python, logré escribir un programa pequeño que usa el módulo Gnuplot que gráfica una parábola. La partición del dominio en el que gráfico [-4,4] no es muy buena, pero la precisión es ajustable, solo hace falta crear un pedazo de código que genere data suficientemente fina para que la gráfica sea mas precisa, sin embargo la idea de este articulo es dar un ejemplo básico, así que aquí se los dejo:

> import Gnuplot  
> gp=Gnuplot.Gnuplot(persist=1)  
> gp(&#8216;set data style lines&#8217;)  
> data=[[-4,16],[-3,9],[-2,4],[-1,1],[0,0],[1,1],[2,4],[3,9],[4,16]]  
> gp.plot(data)

El resultado al ejecutar este programa es:

<div style="text-align: center;">
  <a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://2.bp.blogspot.com/_q-FSc51jNQg/SjcWRFLcKOI/AAAAAAAAADs/PR59hHcvvZ4/s1600-h/grafica.png"><img style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; width: 320px; height: 240px;" src="http://2.bp.blogspot.com/_q-FSc51jNQg/SjcWRFLcKOI/AAAAAAAAADs/PR59hHcvvZ4/s320/grafica.png" alt="" id="BLOGGER_PHOTO_ID_5347767565229500642" border="0" /></a>(click en la imagen para ver los detalles)
</div>

Cualquier duda, pregunta o comentario, les invito a inscribirse en la [lista de correo][1] del Grupo de Usuarios de Python del Proyecto Ciencia:

<http://www.proyectociencia.org/cgi-bin/mailman/listinfo/gupy>

 [1]: http://www.proyectociencia.org/cgi-bin/mailman/listinfo/gupy
