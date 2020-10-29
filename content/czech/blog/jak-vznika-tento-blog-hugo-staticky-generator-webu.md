---
hero_title: "Blog"
title: "Jak vzniká tento blog - II. HUGO statický generátor webu"
date: 2020-10-18T11:00:00+06:00
author: Martin Sveda
image : "images/blog/jamstack/hugo-logo-wide.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo", "Azure", "DevOps"]
description: "Jak nejlépe tvořit web"
draft: false
type: "post"
---




HUGO je jedním ze statických generátorů webu jejichž strukturu tvoříte pomocí 
samostatných souborů s obsahem ve značkovacím jazyce _markdown_.

Výhodou takového přístupu je to, že je to proklatě jednoduché a můžete se soustředit
jen na to, co je důležité - tedy samotné psaní. Vše ostatní, tedy tvorbu _html_
a stylování za vás obstará jedna z mnoha šablon, kterou pro vzhled svého webu můžete
použít.

Samotný generátor je napsán v jazyce [Go](https://golang.org/), přičemž generování
výsledného webu je opravdu, ale opravdu neuvěřitelně rychlé. Více o vnitřnostech
statického generátoru se můžete dozvědět na stránkách samotného 
projektu [HUGO](https://gohugo.io/).

Vše co budu popisovat níže se můžete samozřejmě dočíst i v [dokumentaci](https://gohugo.io/documentation/)
projektu HUGO, takže budu stručný a budu se soustředit jen na to nejdůležitější.


## Instalace HUGO

Na platformě windows si můžete HUGO nainstalovat pomocí nástroje **chocolatey** a to
prostým zápisem:

``` PowerShell

choco install hugo-extended -confirm

```

Doporučuji nainstalovat HUGO v rozšířené sestavě s procesorem Saas/SCSS - budete to
potřebovat v případě použití komplexnějších šablon.


## Vytvoření nového statického webu

Nový statický web `myblog` vytvoříte příkazem:

``` PowerShell

hugo new site myblog

```

Hugo v podtatě vytvoří základní adresářovou strukturu nového webu a rovnou můžeme začít tvořit
jeho obsah.

Jednodušší bude zase odkázat na ýbornou dokumentaci projektu HUGO, kde je vše krásně vysvětleno.

Samozřejmě nezapomeňte vložit celý projekt do **Gitu**. 

```
.
├── archetypes
├── content
├── data
├── layouts
├── static
├── themes
└── config.toml

```

Pro první krůčky koukněte do adresáře `content`, který obsahuje podadresáře jednotlivých jazykových verzí, které budete
na svém webu používat. Další struktura už v podstatě připomíná členění článů dle hlavních menu nebo submenu na webu.
Příklad je uveden níže.


```
.
├── about
├── projects
├── cyklo
├── blog
├── kontakt
├── ...
├── ...
└── ...

```

Tato úroveň tvoří rozcestník k jednotlivým článkům dané kategorie, takže např. v adresáři `projects` můžete
mít tyto soubory:


```
.
├── _index.md
├── jak-vznika-tento-blog-hugo-staticky-generator-webu.md
├── jak-vznika-tento-blog-uvod.md
├── ...
├── ...
└── ...

```

Samotný soubor, nebo chcete-li článek, pak může vypadat zhruba následovně:


``` markdown
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
samostatných souborů s obsahem ve značkovacím jazyce _markdown_.

Výhodou takového přístupu je to, že je to proklatě jednoduché a můžete se soustředit
jen na to, co je důležité - tedy samotné psaní. Vše ostatní, tedy tvorbu _html_
a stylování za vás obstará jedna z mnoha šablon, kterou pro vzhled svého webu můžete
použít.

....
....
....


```

Jak je vidět, tvorba výsledného článku je opravdu jednoduchá.


## Použití šablony

Vizuální podoba výsledného webu je určena použitou šablonou, resp. _tématem_, který tvoří 
předpis, jakým způsobem bude článek z _markdownu_ převeden do _html_. Hugo má 
[nepřeberné množství šablon](https://themes.gohugo.io/), ze kterých
si každý vybere. Šablony si můžete dále upravovat - některé způsoby nabízí sám Hugo, některé
šablony jsou pro uživatelské úpravy přpraveny a nebo šablonu prostě přepíšete nebo doplníte
o definice, které potřebujete.

Kromě šablon/témat dostupných zdarma na stránkách projektu Hugo jsem objevil i krásné [šablony
pro tvorbu dokumentace](http://demo.themefisher.com/godocs-hugo/) na stránkách Themefisher.



## Generování statického webu

Pokud máme nachystaný obsah a vybranou šablonu, tak už jen zbývá vygenerovat statický web a to jednoduše
příkazem `hugo`, který vygeneruje váš web do adresáře `public`.




## Spuštění lokální verze webu

Chcete-li během psaní mít možnost instantně sledovat změny výsledného webu, spusťte Hugo příkazem:

``` bash

hugo server -D

```

Výsledný web zobrazíte ve svém prohlížeči zadáním adresy `localhost:1313`.

Parametr `-D` řekne generátoru, aby generoval i stránky, které mají příznak **Draft**, tedy
jsou v rozpracovaném stavu.

V následující části se podíváme na to, jak celý web zpřístupnit čtenářům pomocí služby
Azure Static Web.


# Související články
 
 - [Jak vzniká tento blog - I. Úvod a motivace]({{< ref "jak-vznika-tento-blog-uvod.md" >}} "Jak vzniká tento blog - I. Úvod a motivace")
 - [Jak vzniká tento blog - III. Azure Static Web Apps]({{< ref "jak-vznika-tento-blog-azure-static-web-apps.md" >}} "Jak vzniká tento blog - III. Azure Static Web Apps")
