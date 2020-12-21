---
hero_title: "Blog"
title: "Rok Ďábla"
date: 2020-11-24T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/pharis/teampharis.png"
bg_image: "images/blog_bg.jpg"
categories: ["Pharis"]
tags: ["Management"]
description: "Jaký byl první rok s MES PHARIS? Plný překvapení a změny kam se podíváš."
draft: false
type: "post"
---

## Bylo nebylo...

Je tomu zhruba rok, co jsem dostal nabídku vést oddělení, které vyvíjí a implementuje
výrobní informační systém [MES PHARIS](https://www.pharis.cz). *Vý-rob-ní. In-for-mač-ní.
Sys-tém.* Všechna ta slova mám rád. Pamatuji si,
že když můj táta přišel z práce, tak voněl olejem a tu vůni řezného oleje
z výroby má po návratu z práce dodnes. 

Kdykoliv vstoupím do výrobní haly, tak se zhluboka
nadechnu. Připomíná mi to dětství. Já svůj profesní život strávil v IT - informační
technologie, mikroprocesory, mechatronické systémy, počítačová grafika, virtuální realita,
desktopové aplikace, webové aplikace. Sám nevím, jestli jsem si ten mix vybral, nebo si mě
jednotlivé role prostě našly. Ať už to bylo jakkoliv, tak jsem všude mohl být součástí
nastavování nebo zavádění nějakého systému. Vlastně jsem systémy studoval na vysoké škole. 
Kybernetické. Systém je prostě systém. Mám ta tři slova
asi v krvi takže jsem tu nabídku vzal. Trochu bezhlavě, ale prostě vzal. 

Na startu jsem střídal duchovního otce systému, takže nic jednoduchého. Na loňský konec 
roku budu vzpomínat jako na jeden z nejvíce hektických. Na jedné straně jsem musel rychle 
poznat tým, role jednotlivých členů, jejich motivaci, strasti a radosti v práci. Na straně 
druhé vyjednávání s vedením ohledně nové koncepce oddělení a rozvoje týmu. Do toho 
jsem o PHARISu nevěděl vůbec nic a při setkání se zákazníky jsem neměl moc co 
říct. Prostě paráda. Poslední předvánoční den jsem si zasloužil dvojitou 
dávku punče a od nového roku jsme do toho pořádně šlápli.


## Kde začít?

Už ani nevím, čím jsme začali. Asi jsme od začátku nenechali kámen na kameni.

V průběhu roku jsme z klasické waterfall metodologie přešli na SCRUM. Některé
to asi bolelo a možná i trochu bolí dodnes. Ale většina v tom od začátku viděla přínos.
Mimo Brno máme i dvě kanceláře v Třebíči a Českých Budějovicích. A jestli bylo něco vidět
hned, tak najednou byli kluci, co sedí mimo Brno, v centru dění. Najednou byli s námi
a věděli, na čem kdo dělá, jak to dělá a jestli je vše ok, nebo potřebuje poradit.
Časem jsme se naučili plánovat a jednotlivé cíle sprintu plnit. Z dema na konci sprintů mám
určitě radost nejenom já. Zcela jistě se v tom ještě pořád učíme chodit, protože když 
jedete ve SCRUMu, tak je pořád co zlepšovat.

Přešli jsme na Git. Ano. Git je tu od roku 2005 a my ho začli používat až teď. No a co.
Když jedete roky v TFS, tak prostě nemáte potřebu jen tak měnit systém pro správu verzí.
To uděláte, až vám to začne dávat smysl, až to zapadne to širšího kontextu, což
byl u nás SCRUM a začínající důraz na DevOps.

DevOps miluju. Nesnáším ruční práci. Teda alespoň ne v IT. Takže jsme začali nasazovat
různé větve do testovacího prostředí, spouštět automatizované testy, vystavovat balíčky.
Postupně se to rozrůstá a v příštím roce budeme mít nasazenou analytiku performance
testů, vizualizace průběhu celého procesu a tak podobně. ELK stack rulezz!

Když máte velký systém, tak prostě chcete vědět, co se v něm děje, když něco není tak,
jak má být. Hlavně to ale chcete vědět dřív, než se to dozví zákazník. Takže ruku v ruce
teď upgradujeme [NLog](https://nlog-project.org/). Už žádné logy do souborů. Pěkně do 
Elasticsearch a šup do Kibany. Důležité logy se budou posílat do cloudu a získáme tak 
krásný přehled o tom, co se kde děje ještě dřív, než to nastane. Nebo taky ne, prostě 
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

Zavedli jsme API. Tím, jak PHARIS dospívá, ho otevíráme implementátorům. Dáváme jim možnost
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


## Máme nové funkce

Dokáže někdo uvěřit, že v tom všem byl i čas na nové funkcionality?

Asi nejvíc jsou za tento rok vidět dva moduly - __KANBAN__ a __Just In Sequence__. Dobře,
neříkejme tomu KANBAN, ale prostě jen _pokročilé řízení materiálových požadavků
ve výrobě_. To znamená, že výrobou se teď prohánějí operátoři s tablety, kteří jezdí
od jednoho stanoviště k druhému a přiváží a odváží materiál nebo výrobky přesně
tam, kam jim PHARIS řekne. 

A Just In Sequence? Dalo by se říct _pěkně popořádku..._ Aby to bylo úplně jasný - až
uvidíte, jak si to nějaký anglický aristokrat maže na golf, tak budete vědět, že některé díly 
do tý jeho nejluxusnější káry na světě byly vyrobeny _just in sequence_, tedy přesně 
tak, jak to PHARIS naplánoval.

Do toho spousta zákaznických úprav, jejichž množství by se v odrážkách nevešlo ani na tři 
strany papíru. Zapracovali jsme i na novém klientovi pro Androidí tablety. Boom!

A pokud byste fakt chtěli řešit kvalitu v automotive, tak vás může oslovit proces 
__kontroly prvního kusu__. My ho pro jednoho 
našeho zákazníka dokázali implementovat během pár týdnů.


## Co bude dál?

Na jeden rok toho není málo. Ten rok byl poznamenaný COVIDem a všichni jsme se báli,
co to pro nás bude znamenat. Technicky, obchodně a hlavně lidsky.
Museli jsme se naučit efektivně pracovat z domu, lépe plánovat, přizpůsobit tomu 
všemu procesy i nástroje.

Dalo by se říct, že malý krok pro člověka, ale obří skok pro celý tým. Tenhle rok měl 
prostě grády a já před vámi, před celým týmem
MES PHARIS, smekám a říkám velké díky.

Od ledna do toho zase pořádně šlápnem...




