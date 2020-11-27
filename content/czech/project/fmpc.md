---
title: "FMPC - řídicí jednotka palivového čerpadla"
description: "Projekt certifikace řídicího jednotky palivového čerpadla"
draft: false
image : "images/project/fmpc.jpg"
bg_image: "images/blog_bg.jpg"
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
do palubní sítě letadel a vrtulníků.

Jednalo se o vývojový projekt pro společnost Microturbo (SAFRAN), na kterém společnost UNIS, a.s. spolupracovala 
s výrobcem čerpadel, společností JIHOSTROJ, a.s., Velešín. Finálním produktem byla e-APU, jež měla být
instalována do vrtulníků Augusta-Westland.



## Požadavky na jednotku

Požadavky zákazníka byly následující:

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
zdrojových souborů projde testy a to za plného pokrytí všech podmínek a možných stavů.

V projektu muselo být tedy definováno a splněno:

- specifikace systémových, vysoko-úrovňových a nízko-úrovňových požadavků
- trasovatelnost mezi jednotlivými požadavky a zdrojovým kódem
- pokrytí kódu (code coverage)
- testovatelnost od nízkoúrovňových až po systémové požadavky

Zvláštní důraz byl také kladen na tzv. configuration management, což znamenalo, že všechny změny v průběhu projektu - a to
jak požadavků, tak kódu nebo testů - musely být zaznamenané, zdůvodněné a musely projít formálním procesem
schvalování.

Naprostou většinu procesů jsme nastavovali teprve v průběhu projektu. Vzhledem k tomu, že podobný projekt v historii
společnosti (a ani v České republice) do té doby nikdy neprobíhal, tak jsme na vše podstatné museli přijít sami.
Nutno podotknout, že jsme měli pomocnou ruku ze společnosti Miroturbo (SAFRAN), ale i tam se s tím solidně prali. Jen
na to měli mnohem více lidí a přeci jen rozvinutější letecký průmysl, takže se měli na koho obrátit.

Projekt byl nakonec dotažen do úspěšného konce a dodnes je to jediný projekt/produkt, který společnost UNIS, a.s.
certifikovala dle standardu DO-178B.


