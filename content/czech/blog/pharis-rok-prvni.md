---
hero_title: "Blog"
title: "Rok Ďábla"
date: 2020-10-29T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/pharis/teampharis.png"
bg_image: "images/blog_bg.jpg"
categories: ["Pharis"]
tags: ["Management"]
description: "Jaký byl první rok s MES PHARIS? Plný překvapení a změny kam se podíváš."
draft: true
type: "post"
---

## Bylo nebylo...

Je tomu zhruba rok, co jsem dostal nabídku vést oddělení, které vyvíjí a implementuje
výrobní informační systém [MES PHARIS](https://www.pharis.cz). *Vý-rob-ní. In-for-mač-ní.
Sys-tém.* Všechna tři slova mnou rezonovala celou schůzku. Všechna mám rád. Pamatuji si,
že když můj táta přišel z práce, tak voněl olejem. Tu vůni řezného oleje
z výroby má po návratu z práce dodnes. Kdykoliv vstoupím do výrobní haly, tak se zhluboka
nadechnu. Připomíná mi to dětství. Já svůj profesní život strávil v IT. Informační
technologie, mikroprocesory, mechatronické systémy, počítačová grafika, virtuální realita,
desktopové aplikace, webové aplikace. Sám nevím, jestli jsem si ten mix vybral, nebo si mě
jednotlivé role prostě našly. Ať už to bylo jakkoliv, tak jsem všude mohl být součástí
nastavování nebo zavádění nějakého systému. Vlastně jsem systémy studoval na vysoké. 
Kybernetické. Ale systém je prostě systém. Mám ta tři slova
asi v krvi takže jsem tu nabídku vzal. Trochu bezhlavě, ale prostě vzal. 

Na startu jsem střídal duchovního otce systému, takže nic jednoduchého. Na loňský konec 
roku budu vzpomínat jako na jeden z nejvíce hektických. Na jedné straně rychle poznat 
tým, role jednotlivých členů, jejich motivaci, strasti a radosti v práci. Na straně 
druhé vyjednávání s vedením ohledně nové koncepce oddělení a rozvoje týmu. Do toho 
jsem o PHARISu neveděl vůbec nic a při setkání se zákazníky jsem toho neměl moc co 
říct. Prostě paráda. Poslední předvánoční den jsem si zasloužil dvojitou 
dávku punče a od nového roku jsme do toho pořádně šlápli.

## Kde začít?

Už ani nevím, čím jsme začali. Asi jsme od začátku nenechali kámen na kameni.

V průběhu roku jsme z klasické waterfall metodologie přešli na SCRUM. Některé
to asi bolelo a možná i trochu bolí dodnes. Ale většina v tom od začátku viděla přínos.
Mimo Brno máme i dvě kanceláře v Třebíči a Českých Budějovicích. A jestli bylo něco vidět
hned, tak najednou byli kluci, co sedí mimo Brno v centru dění. Najednou byli s námi
a věděli, na čem kdo dělá, jak to dělá a jestli je vše ok, nebo potřebuje poradit.
Časem jsme se naučili plánovat a jednotlivé cíle sprintu plnit. Z dema na konci sprintů mám
určitě radost nejenom já. Zcela jistě se v tom ještě pořád učíme chodit, protože když 
jedete ve SCRUMu, tak je pořád co zlepšovat.

Přešli jsme na Git. Ano. Git je tu od roku 2005 a my ho začli používat až teď. No a co.
Když jedete roky v TFS, tak prostě nemáte potřebu jen tak měnit systém pro správu verzí.
To uděláte, až vám to začne dávat smysl, až to zapadne to širšího kontextu, což
byl u nás SCRUM a začínající důraz na DevOps.

Já DevOps miluju. Nesnáším ruční práci. Teda alespoň ne v IT. Takže jsme začali nasazovat
různé větve do testovacího prostředí, spouštět automatizované testy, vystavovat balíčky.
Postupně se to rozrůstá a v příštím roce budeme mít nasazenou analytiku performance
testů, vizualizace průběhu celého procesu a tak podobně. ELK stack rulez!

Když máte velký systém tak prostě chcete vědět, co se v něm děje, když něco není tak,
jak má být. Hlavně to ale chcete vědět dřív, než se to dozví zákazník. Takže ruku v ruce
teď upgradujeme [NLog](https://nlog-project.org/). Už žádné logy do souborů. Pěkně do 
Elasticsearch a šup do Kibany. Důležité logy se budou posílat do cloudu a získáme tak 
krásný přehled o tom, co se kde děje ještě dřív než to nastane. Nebo taky ne, prostě 
to spadne a budou problémy. Ale teď budeme mít nástroj, který nám mnohem lépe pomůže 
s analýzou a následnou opravou. Tohle bude velký.

Stáhli jsme technologický dluh. Spoustu času jsme strávili refaktoringem jádra systému.
Kalendáře, repository, CLR funkce, API, zeštíhlení hlavního klienta... Jeden příklad za 
všechny? Přesunuli jsme Audittrail z produkční databáze do historizační.
Prostě jsme data, jejichž objem je extrémní, přesunuli na místo, kde nám to teď vyhovuje
mnohem víc. Tím se nám produkční databáze zmenšila na 30% původní velikosti, takže
se s ní mnohem líp manipuluje a systém má celkově lepší odezvy. A data v Audittrailu,
kde najdete záznamy o každé akci v systému, jsme zkomprimovali, takže jsme dosáhli
další úspory. Palec nahoru.

Zavedli jsme API. Tím jak PHARIS dospívá ho otevíráme implementátorům. Dáváme jim možnost
si některé věci upravit mimo náš systém bez zásahů do hlavní větve. Postupně
budeme API rozšiřovat a určitě to bude i cesta k rozdělení aplikace do více nezávislých
celků.


## Chceme být lépe vidět

Taky jsme s klukama z marketingu začali dělat na novém webu. Byl nejvyšší čas, už fakt 
dosluhuje. Na úvodním interním brainstormingu jsme se v podstatě shodli jen na tom, 
že potřebujeme někoho, kdo nám s tím fakt pomůže. Profesionály. Tak jsme oslovili kluky a holky 
z [PUXu](https://puxdesign.cz). Dělají nejlepší weby na světě a ten náš se jim fakt 
povedl. Uvidíte na začátku roku 2021. Já ten web miluju od první vteřiny a vsadím se, 
že vám se bude líbit taky.

Jsme i víc vidět na LinkedInu, byť v tomhle si ještě úplně jistí nejsme. Ale pracujeme na tom
a doufám, že o nás bude slyšet čím dál víc.


## Co bude dál?

Na jeden rok toho není málo. Můj hrdina by k tomu asi řekl, že malý krok pro člověka, ale 
obří skok pro celý tým. Tenhle rok byl prostě boží a já před vámi, před celým týmem
MES PHARIS, smekám a říkám velké díky.

Od ledna zase pokračujeme...




