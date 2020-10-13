---
title: "Jak vzniká tento blog - II. HUGO statický generátor webu"
description: "Jak nejléle tvořit web"
draft: false
image : "images/projects/jamstack.png"
bg_image: "images/featue-bg.jpg"
categories: ["Psaní"]
tags: ["Hugo", "Azure", "DevOps"]
---

HUGO je jedním ze statických generátorů webu jejichž strukturu tvoříte pomocí 
samostatných souborů s obsahem ve značkovacím jazyce **markdown**.

Výhodou takového přístupu je to, že je to proklatě jednoduché a můžete se soustředit
jen na to, co je důležité - tedy samotné psaní. Vše ostatní, tedy tvorbu **html**
a stylování za vás obstará jedna z mnoha šablon, kterou pro vzhled svého webu můžete
využít.

Samotný generátor je napsán v jazyce [Go](https://golang.org/), přičemž generování
výsledného webu je opravdu, ale opravdu neuvěřitelně rychlé. Více se můžete
dozvědět na stránkách samotného projektu [HUGO](https://gohugo.io/).

Vše co budu popisovat níže se můžete samozřejmě dočíst i v [dokumentaci](https://gohugo.io/documentation/)
projektu HUGO, takže budu stručný a budu se soustředit jen na to nejdůležitější.


## Instalace HUGO

Na platformě windows si můžete HUGO nainstalovat pomocí nástroje **chocolatey** a to
prostým zápisem:

``` PowerShell

choco install hugo-extended -confirm

```

Doporučuji rovnou instalovat HUGO v rozšířené sestavě s procesorem Saas/SCSS - budete to
potřebovat v případě použití komplexnějších šablon.


## Vytvoření nového statického webu

Nový statický web `myawesome` vytvoříte příkazem:

``` PowerShell

hugo new site myawesomesite

```

Hugo v podtatě vytvoří základní adresářovou strukturu nového webu a můžeme začít tvořit
jeho obsah.

Jednodušší bude zase odkázat na ýbornou dokumentaci projektu HUGO, kde je vše krásně vysvětleno.

Samozřejmě nezapomeňte vložit celý projekt do **Gitu**. 



## Spuštění lokální verze webu

Lokální verzi webu spustíte příkazem:

``` PowerShell

hugo server -D

```

Parametr `-D` řekne generátoru, aby generoval i stránky, které jsou s příznakem **Draft**, tedy
v rozpracovaném stavu.
