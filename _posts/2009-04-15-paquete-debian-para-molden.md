---
title: Paquete Debian para Molden
author: muammar
excerpt: ' '
layout: post
permalink: /?p=67
categories:
  - Computación
  - Química
---
Todos aquellos que nos hemos  dedicado a la Química Teórica/Computacional reconocemos a <a href="http://www.cmbi.ru.nl/molden/" target="_blank">Molden</a> como una herramienta, en algunos casos, fundamental. Es por ello que he creado un paquete Debian para esta aplicación.

Es necesario comentar que debido al copyright de esta aplicación, no puede incluirse en los repositorios oficiales de Debian.  A continuación pego el copyright:

> **Copyright (C) 1991 CMBI.**
> 
> Permission to copy and use the MOLDEN software and its documentation for private usage, is hereby granted to **non profit** organisations. No part of the software code may be reused without specific permission of the CMBI.
> 
> The MOLDEN software is provided &#8220;as is&#8221; without explicit or implied warranty.
> 
> The author should be cited in any work based on this material.
> 
> **Commercial** users (non-acedemic,for-profit organisations) are required to receive authorization to download and use MOLDEN by printing, completing, signing and fax-ing the ** [ COMMERCIAL_LICENSE-AGREEMENT][1]** to the CMBI at Fax. nr. +31 024 3652977. This document is also available as file from the CMBI Anonymous ftp site;<tt> ftp.cmbi.ru.nl</tt>

El uso de estos paquetes es solo de tipo académico. Si quieres descargarlos puedes agregar estas líneas a tu repositorio:

**AMD64**:

> deb http://proyectociencia.org/debian amd64/

**i386:**

> deb http://proyectociencia.org/debian i386/

Luego de agregarlos, actualizas APT con:

> \# aptitude update

o

> \# apt-get update

Una vez actualizado APT, puedes instalar molden simplemente ejecutando:

> \# aptitude install molden

o

> \# apt-get install molden

Los paquetes están firmados con <a href="http://pgp.mit.edu:11371/pks/lookup?search=muammarelkhatib%40gmail.com&op=vindex" target="_blank">mi llave digital</a>. Estos paquetes deberían funcionar en Debian y Ubuntu. En caso de que consigan algún error, por favor escriban a cualquiera de mis correos. Por otro lado,  pronto publicaré el source de esta aplicación.

Espero que les sean útil estos paquetes.

 [1]: http://www.cmbi.ru.nl/molden/COMMERCIAL_LICENSE.html