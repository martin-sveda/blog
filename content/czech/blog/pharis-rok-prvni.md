---
hero_title: "Blog"
title: "První rok s MES PHARIS"
date: 2020-10-29T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/pharis/pharis-blue.png"
bg_image: "images/blog_bg.jpg"
categories: ["Pharis"]
tags: ["Management"]
description: "Jaký byl první rok s MES PHARIS? Plný překvapení a změny kam se podíváš."
draft: true
type: "post"
---


Je tomu zhruba rok, co jsem dostal nabídku vést oddělení, které vyvíjí a implementuje
výrobní informační systém [MES PHARIS](https://www.pharis.cz). *Vý-rob-ní. In-for-mač-ní.
Sys-tém.* Všechna tři slova mnou rezonovala celou schůzku. Všechna mám rád. Z dětství
si vybavuji, že když můj táta přišel z práce, tak voněl olejem. Tu vůni řezného oleje
z výroby má po návratu z práce dodnes. Já svůj profesní život strávil v IT. Informační
technologie, mikroprocesory, mechatronické systémy, počítačová grafika, virtuální realita,
desktopové aplikace, webové aplikace. Sám nevím, jestli jsem si ten mix vybral, nebo si mě
jednotlivé role prostě našly. Ať už to bylo jakkoliv, tak jsem všude mohl být součástí
nastavování nebo zavádění nnějakého systému. Vlastně jsem systémy studoval na vysoké. 
Sice kybernetické, ale systém je prostě systém. Mám ta tři slova
asi v krvi takže jsem tu nabídku vzal. Trochu bezhlavě, ale prostě vzal. 

Startovní pozice asi nemohla být horší. Střídal jsem na pozici v podstatě duchovního
otce systému, půlka týmu naštvaná a jednou nohou na odchodu, zákazníci úplně spokojení
taky nebyli - prostě samá pozitiva. Na loňský konec roku budu vzpomínat jako jeden
z nejvíce hektických. Na jedné straně rychle poznat tým, role jednotlivých členů, 
jejich motivaci, strasti a radosti v práci. Na straně druhé vyjednávání s vedením
ohledně nové koncepce a záchrany týmu. Do toho jsem o PHARISu neveděl vůbec nic
a při setkání se zákazníky jsem toho neměl moc co říct. Prostě paráda. Dream job.
Poslední předvánoční den jsem si zasloužil dvojitou dávku punče a od nového roku
jsme do toho pořádně šlápli.

Už ani nevím, čím jsme začli. Asi jsme od začátku nenechali kámen na kameni.

V průběhu roku jsme z řekněme klasické waterfall metodologie přešli na SCRUM. Některé
to asi bolelo a možná i trochu bolí dodnes. Ale většina v tom od začátku viděla přínos.
Mimo Brno máme i dvě kanceláře v Třebíči a Českých Budějovicích. A jestli bylo něco vidět
hned, tak najednou byli kluci co sedí mimo Brno v centru dění. Najednou byli s námi
a věděli, na čem kdo dělá, jak to dělá a jesli je vše ok, nebo potřebuje poradit.
Časem jsme se naučili plánovat a sprinty dokončovat. Z dema na konci sprintů mám
určitě radost nejenom já. A učíme se dodnes, protože když jedete ve SCRUMu, tak je
pořád co zlepšovat.

Přešli jsme na Git. Ano. Git je tu od roku 2005 a my ho začli používat až teď. No a co.
Když jedete roky v TFS tak prostě nemáte potřebu jen tak měnit systém pro správu verzí.
To uděláte, až vám to začne dávat smysl, až to zapadne to širšího kontextu, což
byl u nás SCRUM a začínající důraz na DevOps.

Já DevOps miluju. Nesnáším ruční práci. Alespoň teda ne v IT. Takže jsme začali nasazovat
různé větve do testovacího prostředí, spouštět automatizované testy, vystavovat balíčky.
Postupně se to rozrůstá a v příštím roce budeme mít nasazenou analytiku performance
testů, vizualizace průběhu testů a tak podobně. ELK stack rulez!

Když máte velký systém tak prostě chcete vědět, co se v něm děje, když něco není tak,
jak má být. Hlavně to chcete vědět dřív, než se to dozví zákazník. Takže ruku v ruce
teď upgradujeme *nlog*. Už žádné logy do souborů. Pěktě do Elasticsearch a šup
do Kibany. Důležité logy se budou posílat do cloudu a získáme tak krásný přehled 
o tom, co se kde děje ještě dřív než to nastane. Nebo taky ne, prostě to spadne
a budou problémy. Ale budeme mít nástroj, který nám pomůže s analýzou a následnou
opravou. Tohle bude velký.



Stáhli jsme technologický dluh. Spoustu času jsme strávili refaktoringem jádra systému.
Jeden příklad za všechny? Přesunuli jsme Audittrail z produkční databáze do historizační.
Prostě jsme data, jejichž objem je extrémní přesunuli na místo, kde nám to teď vyhovuje
mnohem víc. Tím se nám produkční databáze zmenšila na 30% původní velikosti, takže
se s ní mnohem líp manipuluje a systém má celkově lepší odezvy. A data v Audittrailu,
(kde najdete záznamy o každé akci v systému) jsme zmenšili. Palec nahoru.


Taky jsme s klukama z marketingu začali dělat na novém webu. Byl nejvyšší čas, už fakt 
dosluhuje. Na úvodním interním brainstormingu jsme se v podstatě shodli jen na tom, 
že potřebujeme někoho, kdo nám s tím fakt pomůže. Profesionály. Tak jsme oslovili kluky a holky 
z [PUXu](https://puxdesign.cz). Dělají nejlepší weby na světě a ten náš se jim fakt 
povedl. Uvidíte na začátku roku 2021. Já ten web miluju od první vteřiny a vsadím se, 
že vám se bude líbit taky.

Na jeden rok toho není málo. Malý krok pro člověka, ale obří skok pro celý tým. Tenhle
tok byl prostě boží a já před vámi smekám a říkám velké díky.

Od ledna zase pokračujeme...











