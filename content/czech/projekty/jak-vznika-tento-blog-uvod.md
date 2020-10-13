---
title: "Jak vzniká tento blog - I. Úvod a motivace"
description: "Jak nejléle tvořit web"
draft: false
image : "images/portfolio/work1.jpg"
bg_image: "images/featue-bg.jpg"
categories: ["Psaní"]
tags: ["Hugo", "Azure", "DevOps"]
---

Tento blog se nezrodil z touhy něco psát a sdělovat své myšlenky světu. Spíše jsem v práci
narazil na problém, jak psát dokumentaci k našemu produktu a projektům - a to jak
uživatelskou dokumentaci pro zákazníky, tak interní pro programátory, analytiky
a implementátory.

Nikdy mě nechytl žádný redakční systém typu Wordpress, Drupal, nebo předpřipravené stránky
např. na Webnode. Naopak mě vždycky fascinovala možnost tvořit dokumentaci ze zdrojových
kódů.

Co od takového nástroje očekávám? Shrnout by se to dalo do několika níže popsaných bodů:

 - možnost psát obsah v relativně jednoduchém jazyce bez nutnosti specifických nástrojů
 - podobnost s běžně používanými nástroji ve vývoji (IDE, značkovací jazyk, ...)
 - možnost verzování, schvalování do produkce
 - ???

Ke splnění výše uvedeného měli nejblíže tyto nástroje:

 - kombinace Asciidoc a projektu [Antora](https://antora.org/)
 - reStructuredText a [Sphinx](https://www.sphinx-doc.org/en/master/)
 - wiki
 - Geterátory statických webů, neboli JAM-stack  


Kombinací RST a projektu Sphinx jsem si už jednou prošel - nebylo to špatné, ale bylo vidět, že
koncept je to už zastaralý a vizuální stránka projektu Sphinx taky nenabízela žádné velké možnosti.

Dlouho byl mým favoritem projekt [Antora](https://antora.org/) - Asciidoc je úžasný nástroj/jazyk, který
je mnohem mocnější než __markdown__. Sama definice značkovacího jazyka [Asciidoc](https://asciidoctor.org/docs/asciidoc-writers-guide/)
je mnohem komplexnější než __markdown__ a umožňuje vytvářet opravdu komplikovanou a bohatou dokumentaci.
Nicméně projekt Antora mi přišel složitý na rychlé pochopení a také není tolik rozšířený jako následující
kandidát.

__JAM-stack__ - neboli JavaScript, API & Markup je koncept, který jsem zkoumal hned po odklonu od Antory.
Jak je možné se přesvědčit na stránkách [JAM-stacku](https://jamstack.org/), jedná se o moderní
princip tvorby statických webů s využitím značkovacího jazyka MArkdown. Výhody JAM stack řešení
jsou následující:

- větší výkon / rychlost / odezva stránek,
- větší bezpečnost - web je v podstatě čistě statický,
- snažší integrace do vývojářských procesů,
- a v neposlední řadě široká podpora komunity.

Na výběr je široké množství nástrojů - [Gatsby](https://www.gatsbyjs.com/), [Hugo](https://gohugo.io/), [Jekyll](https://jekyllrb.com/) a další...

Letmo jsem prozkoumal tři výše uvedené a v podstatě naslepo jsem se rozhodl vyzkoušet [Hugo](https://gohugo.io/). 

Pokud se alespoň trochu orientujete v HTML, CSS a JavaScriptu a je vám programování alespoň trochu sympatické, tak
se to vše dá v základu pochopit a úspěšně zprovoznit za jeden delší večer.


