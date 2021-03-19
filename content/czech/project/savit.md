---
title: "SAVIT  - simulátor lehkých střelných zbraní"
description: "SAVIT - simulátor lehkých střelných zbraní"
draft: false
image : "images/project/savit.jpg"
bg_image: "images/featue-bg.jpg"
category: "Military"
information:
  - label : "Zaměstnavatel"
    info : "Saab Czech s.r.o."
  - label : "Role"
    info : "Project manager"
---


## O projektu

SAVIT, neboli Small Arms Virtual Indoor Simulator. Byl to můj první projekt, který jsem dostal na starosti,
když jsem přišel do společnosti SAAB Czech, což je dceřinná společnost Švédské zbrojovky SAAB. Pobočka
ve Slavkově u Brna byla přímo podřízena BU (Bussiness Unit) SAAB Training & Simulations v Huskvarně.

Duchovním otcem simulátoru SAVIT byl Martin Jandl, se kterým jsem v roli projektového manažera spolupracoval.
Bylo to jedno z nejintezivnějších období - s Martinem jsme vedli nekonečné diskuze o podobě a technickém
řešení simulátoru, kdy jsme hledali balanc mezi jeho propracovaným designem, geniálním produktem a cenou
a časem, za který půjde jeho myšlenky realizovat. Kromě Martina tam byli samozřejmě i další skvělí kolegové,
ale Martin byl rozhodně ten nejvýraznější.


## Technické řešení

SAVIT se skládal ze tří hlavních částí - replik zbraní, generátoru scény a vyhodnocovacího modulu.

### Repliky zbraní

V rámci prvního projektu jsme měli zákazníkovi dodat celkem 12 různých typů zbraní - pistole Glock, lehké
útočné pušky AK47, M4, MP-5, samopaly M60 a G3, granátomet RPG a další... Všechny repliky musely být
k nerozeznání od originálu - tzn. že musely nejenom stejně vypadat a vážit, ale musely se i shodně ovládat
a při střele generovat zpětný ráz.

Všechny repliky se kompletně navrhovali ve strojním oddělení, kde vznikaly 3D modely a výkresy, které
pak šly do výroby. U některých typů zbraní byly použity originální nakupované díly, ale mnohé byly
kompletně navržené a vyrobené ve Slavkově. Pro generování zpětného rázu se používalo stlačené CO2
v malé tlakové nádobě, která byla umístěna v zásobníku.

Každá replika byla protkána komplikovanou elektronikou, která snímala všechna data ze sensorů, vyhodnocovala
je a na jejich základě pak řídila chování zbraně. Autorem elektroniky byl z největší části Laďa
Hubík a na spolupráci s ním taky strašně rád vzpomínám.

### Genererátor scény (Image Generator)

Generátor scény zobrazoval virtuální tréninkovou scénu na velkém projekčním plátně, před nímž stáli střelci,
kteří mířili do virtuálního prostoru. Pro věrnost zobrazení a tréninku byly ve výpočetním modelu uvažovány
optické jevy, vliv prostředí a specifické balistiky odpovídající dané zbrani i náboji.

Původní IG bylo napsané týmem ve Slavkově, ale časem už nešlo držet krok s moderními IG, které
byly na trhu k dispozici. Z několika možných variant jsme se časem přiklonili k Unity 3D, které se
pro zobrazení scény používá dodnes.


### Vyhodnocovací modul

Vyhodnocovací modul sledoval výsledky jednotlivých aktérů tréninku. Každý účastník tréninku mohl
sledovat svůj progres v průběhu cvičení, nastřílené body a další charakteristiky důležité pro
správný nácvik střelby - náklon zbraně, strhávání, rozptyl apod.

Instruktor mohl jednotlivé pokusy zobrazit v přehledném vyhodnocovacím reportu, kde byly všechny
parametry graficky znázorněny.



## Reference

[VIDEO: Vyrábí technologie pro armádu. Střelba je maximálně realistická](https://www.idnes.cz/brno/zpravy/armada-vyroba-technologie-saab-virtualni-simulator.A151023_170123_brno-zpravy_vh)

[Vojáci testují nový střelecký simulátor. Jméno má po padlém kamarádovi](https://www.idnes.cz/zpravy/nato/simulator-strelby-tabor-42-mechanizovany-svatovaclavsky-afghanistan-saab-armada-vojaci.A201016_111528_zpr_nato_inc)