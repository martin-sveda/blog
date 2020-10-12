---
title: "Převod rozvrhovače MES PHARIS do cloudu"
description: "Jak jsme předělávali část PHARIS do cloudu"
draft: false
image : "images/portfolio/work1.jpg"
bg_image: "images/featue-bg.jpg"
categories: ["Programování"]
tags: ["Azure", "Docker"]
category: "Programování"
information:
  - label : "Client"
    info : "UNIS, a.s."
  - label : "What We Did"
    info : "Website Redesign"
  - label : "Nástroje"
    info : "ASP .NET, C++, C#, Docker, Azure Container Registry"
  - label : "Dokončeno"
    info : "2020"
---

Rozvrhovač výroby je jedním z modulů výrobního informačního systému MES PHARIS, který
má za úkol na základě předaných dat provést optimální rozvržení výroby - tedy posloupnost jednotlivých
výrobních operací na všech výrobních strojích.

Rozvrhovač musí během optimalizace zahrnout do výpočtu následující omezení: 

 - aktuální situaci ve výrobě (jaké výrobní příkazy jsou aktuálně na výrobních zařízeních)
 - dostupnost materiálu,
 - pracovní kalendáře (dobu, kdy je daný prostředek k dispozici),
 - dostupnost lidských zdrojů,
 - plánované odstávky,
 - a další.


## Výchozí situace

Historicky byl rozvrhovač výroby napsán v jazyce C++ a k dispozici byla výhradně binárka pro OS Linux. 
Vzhledem k tomu, že na oddělení vývoje neměl nikdo s Linuxem moc zkušeností, řešilo se to tak, že
se v systému vyhradil celý virtuální stroj s OS Linux a na ten se ručně nahrála relativně malá binárka
plánovače.

Komunikace mezi hlavním serverem MES PHARIS a rozvrhovačem - tedy předání výpočetní úlohy - probíhalo
na základě výměny vstupního a výstupního souboru. Vstupní i výstupní byl v podstatě databázová tabulka
s popisem úlohy. Výměna dat pak probíhala přes souborový systém, který byl mezi oběma systémy sdílen.

Uvedené řešení mělo následující nevýhody:

 - velký virtuální stroj pro relativně malou binárku,
 - velmi pracná (ruční) distribuce a aktualizace rozvrhovače
 - předávání dat přes namapovaný souborový systém.


