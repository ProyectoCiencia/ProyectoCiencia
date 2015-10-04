---
title: Instalacion de LaTeX y Kile en Ubuntu
author: Alejandro Alvarez
layout: page
categories:
  - Computación
  - Matemática
tags:
  - Aptitude
  - Debian
  - Instalación
  - Kile
  - LaTeX
  - Paqueterias
  - Ubuntu
---
<p style="text-align: left;">
  <a href="http://www.proyectociencia.org/blog/wp-content/uploads/2009/02/latex-logo.png"><img class="aligncenter size-full wp-image-208" title="latex-logo" src="http://www.proyectociencia.org/blog/wp-content/uploads/2009/02/latex-logo.png" alt="" width="200" height="86" /></a><br /> Como es bien sabido, <a href="http://es.wikipedia.org/wiki/LaTeX">LaTeX</a> es un sistema de preparación de documentos técnicos de alta calidad, necesario generalmente para científicos e ingenieros, pero que además posee una extensa paquetería que lo sitúa en cualquier área del conocimiento. El siguiente mini-how to trata sobre las diferentes instalaciones posibles en Ubuntu (también Debian).
</p>

<span style="font-weight: bold;">¿Como instalar LaTeX en Ubuntu?</span>

Podemos instalar [LaTeX][1] de 4 Formas, según nuestros requerimientos o capacidad en el disco duro. Así disponemos de las siguientes:

&#8211; <span style="font-weight: bold;">LaTeX Base:</span> Es la instalación mas compacta de [LaTeX][1]. Destinada a los usuarios que solo quieren hacer documentos sencillos.

Para instalarlo deben abrir la consola y escribir:

<div style="text-align: center; color: #990000;">
  <blockquote style="color: #ff0000;">
    <p>
      sudo aptitude install texlive-latex-base
    </p>
  </blockquote>
</div>

<span style="font-weight: bold;">&#8211; LaTeX Recomendado</span>: Mucho mas completa que la anterior, aunque no totalmente completa. Sin embargo es la mejor opción para los científicos e ingenieros, pues trae los paquetes más usados por estos.

Para instalarlo deben abrir la consola y escribir:

<div style="text-align: center; color: #990000;">
  <blockquote>
    <p>
      <span style="color: #ff0000;">sudo aptitude install texlive-latex-base texlive-latex-recommended</span><span style="font-weight: bold;"><br /> </span>
    </p>
  </blockquote>
</div>

<span style="font-weight: bold;">&#8211; LaTeX Paqueteria Extra:</span> A este punto la instalación de LaTeX esta casi completa. Lo que necesites es probable que lo encuentres aquí. Pero usa aprox. 800 MB de espacio en el disco duro.

Para instalarlo deben abrir la consola y escribir:

<div style="text-align: center; color: #990000;">
  <blockquote>
    <p>
      <span style="color: #ff0000;">sudo aptitude install texlive-latex-base texlive-latex -recommended texlive-latex-extra</span><span style="font-weight: bold;"><br /> </span>
    </p>
  </blockquote>
</div>

<span style="font-weight: bold;">&#8211; LaTeX Completo: </span><span>E</span>n esta instalación esta todo.

Para instalarlo deben abrir la consola y escribir:

<div style="text-align: center; color: #990000;">
  <blockquote>
    <p>
      <span style="color: #ff0000;">sudo aptitude install texlive-full</span><span style="font-weight: bold;"><br /> </span>
    </p>
  </blockquote>
</div>

<span style="font-weight: bold;"><br /> Comentario Final</span>  
En Linux, el mejor amigo de LaTeX es el editor Kile. Para instalarlo (con la paquetería en español) deberás escribir:

<div style="text-align: center; color: #990000;">
  <blockquote>
    <p>
      <span style="color: #ff0000;">sudo aptitude </span><span style="color: #ff0000;">install kile kile-i18n-es</span><span style="color: #ff0000;"> </span><span style="font-weight: bold;"><br /> </span>
    </p>
  </blockquote>
</div>

Espero que esta información les sea de utilidad.

 [1]: http://es.wikipedia.org/wiki/LaTeX
