---
hero_title: "FMPC - řídicí jednotka palivového čerpadla"
title: "FMPC"
description: "Řídicí jednotka palivového čerpadla"
draft: false
image : "images/project/fmpc.jpg"
bg_image: "images/featue-bg.jpg"
category: "Embedded"
information:
  - label : "Zaměstnavatel"
    info : "UNIS, a.s."
  - label : "Role"
    info : "Projektový manažer"
  - label : "Klient"
    info : "Microturbo, SAFRAN"
---


Řídicí jednotka palivového čerpadla zajišťuje dodávku paliva pro pomocnou energetickou jednotku (APU - Auxiliary Power
Unit), která je určena k dodávce elektrické energie za účelem startování hlavních motorů a k dodávce energie
do palubní sítě.

Jednalo se o vývojový projekt pro spole4nost Microturbo (SAFRAN), na kterém společnost UNIS, a.s. spolupracovala 
s výrobcem čerpadel, společností JIHOSTROJ, a.s., Velešín.



## Požadavky na jednotku

Požadavky společnsti Microturbo (SAFRAN) byly následující:

 - kompaktní rozměry
 - řízení otáček mechanického čerpadla pomocí BLDC (bezkartáčovéhp) motoru
 - operační rozsah teplot od -50°C do +120°C
 - výkon jednotky 60W
 - požadavky na proces vývoje dle standardu DO-178B
 - environmentální požadavky dle DO-160 


## Klíčové vlastnosti projektu

Vývoj firmware jednotky byl prováděn dle požadavků normy DO-178B (Software Considerations in Airborne Systems and Equipment 
Certification). S vývojem dle této normy jsme do té doby neměli prakticky žádné zkušenosti, takže jsme si museli
projít úskalím složitého vývoje dle tohoto standardu.

V podstatě to znamenalo, že každý řádek, který se v kódu objevil, musel být trasovatelný a to od systémových až po
nízkoúrovňové požadavky, konkretizující celou specifikaci. Stejně tak muselo být zajištěno, že každý řádek
zdrojových souborů projde testy.

V projektu muselo být tedy definováno a splněno:

- specifikace systémových, vysoko-úrovňových a nízko-úrovňových požadavků
- trasovatelnost mezi jednotlivými požadavky a zdrojovým kódem
- pokrytí kódu (code coverage)
- testovatelnost od nízkoúrovňových až po systémové požadavky

Zvláštní důraz byl také kladen na tzv. configuration management, což znamenalo, že všechny změny v průběhu projektu - a to
jak požadavků, tak kódu nebo testů - musely být zaznamenané, zdůvodněné a musely projít formálním procesem
schvalování.

Naprostou většinu procesů jsme museli teprve nastavovat v průběhu projektu. Vzhledem k tomu, že podobný projekt v historii
společnosti (a ani v České republice) do té doby nikdy neprobíhal, tak jsme v tom si na vše podstatné museli přijít sami.
Nutno podotknout, že jsme měli pomocnou ruku ze společnosti Miroturbo (SAFRAN), ale i tam se s tím solidně prali. Jen
na to měli mnohem více lidí a přeci jen rozvinutější letecký průmysl, takže se měli na koho obrátit.




