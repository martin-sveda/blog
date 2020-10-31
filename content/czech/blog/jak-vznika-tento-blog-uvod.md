---
hero_title: "Blog"
title: "Jak vzniká tento blog - I. Úvod a motivace"
date: 2020-10-11T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/jamstack/Jamstack_Logo_Original.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo", "Azure", "DevOps"]
description: "Shrnutí úprav šablony"
draft: false
type: "post"
---




Tento blog vlastně vznikl jako experiment s JAM stackem. Vůbec nebylo mým cílem sdílet světu nějaké 
své převratné myšlenky - spíše jsem narazil na otázku, jak psát co možná nejjednodušeji, nejefektivněji
a přitom vizuálně atraktivní dokumentaci k našemu produktu a projektům. A to jak uživatelskou 
dokumentaci pro zákazníky, tak interní pro programátory, analytiky a implementátory.

Nikdy mě neoslovil žádný redakční systém typu Wordpress, Drupal, nebo předpřipravené stránky typu
Webnode. Naopak mě vždycky fascinovala možnost tvořit dokumentaci ze zdrojových
kódů, mít možnost je verzovat a týmově na nich spolupracovat.

Od nástroje, který jsem hledal, jsem očekával zhruba následující:

 - možnost psát obsah v relativně jednoduchém jazyce bez nutnosti specifických nástrojů,
 - schopnost generování částí dokumentace přímo ze zdrojových kódů, 
 - podobnost s běžně používanými nástroji ve vývoji (IDE, značkovací jazyk, ...),
 - možnost verzování, schvalování do produkce.
 
Provedl jsem tedy krátký průzkum, přičemž zamýšlenou filosofii a požadavky nejvíce splňovaly
následující nástroje:

 - kombinace Asciidoc a projektu [Antora](https://antora.org/),
 - reStructuredText a [Sphinx](https://www.sphinx-doc.org/en/master/),
 - wiki,
 - geterátory statických webů, neboli JAM-stack.


## reStructuredText a Sphinx
Kombinací RST a projektu Sphinx jsem si už jednou prošel - nebylo to špatné, ale bylo vidět, že
koncept je to už zastaralý a vizuální podoba generované dokumentace taky každého úplně neoslnila.

RST je značkovací jazyk podobný markdownu, možná trochu mocnější a svého času byl oblíbený
v komunitě kolem Pythonu. Na jednom projektu jsme s pomocí RST a Sphinxu psali vývojářskou
i uživatelskou dokumentaci do jednoho staticky generovaného webu. Zákazník dostal přístup do
své části, kde si mohl přečíst, jak zařízení používat, jak ho konfigurovat, upgradovat firmware
apod.

Zajímavou vlastností bylo automatické generování popisu konfiguračních registrů ze zdrojového
kódu - měli jsme tedy vždy aktuální dokumentaci k tomu, co a jak je možné konfigurovat. V části 
vývojářské dokumentace jsme pak měli popis interních struktur a architektury celého řešení,
které bylo doplněno o podrobnější info do části generované Doxygenem.

Mělo to pouze dvě nevýhody:

  - značkovací jazyk RST byl prostě jiný než markdown a museli jste se ho nejprvě naučit (ok, to nebyla
    žádná raketová věda),
  - vizuálně ten výsledný web prostě nevypadal dobře,
  - na výběr bylo pouze omezené množství šablon/témat výsledného webu.

Suma sumárum, dnes bych do této cesty již neinvestoval.


## Antora

Projekt [Antora](https://antora.org/) byl dlouho mým favoritem, protože sama definice
značkovacího jazyka [Asciidoc](https://asciidoctor.org/docs/asciidoc-writers-guide/)
je mnohem širší než _markdown_ a umožňuje vytvářet opravdu komplikovanou a bohatou dokumentaci.

Nicméně projekt Antora mi přišel složitý na rychlé pochopení a také mi přišlo, že není v komunitě
fanoušků _docs as code_ dostatečně rozšířený, abych si na něj bez obav v delším horizontu vsadil.


## JAM stack

_JAM-stack_ - neboli JavaScript, API & Markup je koncept, který jsem zkoumal hned po odklonu od Antory.
Jak je možné se přesvědčit na stránkách [JAM-stacku](https://jamstack.org/), jedná se o moderní
princip tvorby statických webů s využitím značkovacího jazyka _markdown_. Výhody JAM stack řešení
jsou následující:

- web je staticky generovaný a proto je odezva webu velmi, ale velmi, rychlá,
- větší bezpečnost - web je v podstatě čistě statický a tudíž není moc prostoru pro chybu v kódu na straně serveru,
- snadněji se integruje do vývojářských procesů,
- a v neposlední řadě má širokou podpora komunity.

Na výběr je také velké množství nástrojů - [Gatsby](https://www.gatsbyjs.com/), [Hugo](https://gohugo.io/), 
[Jekyll](https://jekyllrb.com/) a další...

Letmo jsem prozkoumal tři výše uvedené a v podstatě bez jasného vítěze této plytké analýzy jsem se 
rozhodl vyzkoušet [Hugo](https://gohugo.io/). Jak to dopadlo se dozvíte 
v [další části]({{< ref "jak-vznika-tento-blog-hugo-staticky-generator-webu.md" >}} "Další část článku") článku...





