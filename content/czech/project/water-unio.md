---
title: "Sada IoT zařízení"
#description: "IoT zařízení pro měření růýných fyzikálních veličin"
draft: false
image : "images/project/water-unio.jpg"
bg_image: "images/blog_bg.jpg"
category: "Electronics"
information:
  - label: "Zaměstnavatel"
    info: "UNIS, a.s."
  - label: "Role"
    info: "Produktový manažer"
---



Vývoj několika typů IoT zařízení pro měření fyzikálních veličin:

 - GPS sledování pohybu a náklonů zařízení
 - UNIO - univerzální snímač proudu a napětí na svorkách
 - WATER UNIO - rozšíření modulu UNIO o měření výšky vodní hladiny s pomocí hydrostatického snímače
 - UZ - ultrazvukový měřič vzdálenosti

Součástí projektu byl i vývoj cloudových platforem a mobilních aplikací:

 - cloudová platforma založená na Thingsboard a MES PHARIS pro sledování a vizualizaci naměřených dat
 - Android aplikace pro sledování pohybu GPS snímačů
 - Android aplikace pro sledování měření výšky vodní hladiny


Všechny snímače byly postaveny na MCU platformě STM32L, jako OS pro firmware byl použit FreeRTOS
a komunikace probíhala pomocí rádiové sítě Sigfox.


## GPS IoT snímač

GPS snímač odesílá v pravidelných intervalech informaci o poloze snímače do cloudu. Snímač lze nastavit tak,
aby reagoval na různou intenzitu pohybu, detekoval náklony a posílal data jen za určitých podmínek.


## UNIO



Snímač WATER UNIO měří v pravidelných intervalech měřit hladinu vody např. ve studni. Změřená data jsou odesílána 
do cloudu, kde dojde k jejich zpracování a vizualizaci.

Informace o výšce hladiny je možné si prohlédnout na webu, nebo v aplikaci na mobilním telefonu.


## WATER UNIO

Snímač WATER UNIO měří v pravidelných intervalech měřit hladinu vody např. ve studni. Změřená data jsou odesílána 
do cloudu, kde dojde k jejich zpracování a vizualizaci.

Informace o výšce hladiny je možné si prohlédnout na webu, nebo v aplikaci na mobilním telefonu.




## Klíčové parametry projektu

V průběhu roku 2017 došlo k velkému rozmachu IoT - všude se o Internetu věcí mluvilo jako o dalším zlomu
v oblasti konektivity snímačů a rádiového přenosu dat. Podle předpokladů mělo být během následujících
pěti let nainstalováno a provozováno 20 miliard IoT zařízení.

S kolegou jsme se vyčlenili z Divize letecké a pokročilého řízení a bylo nám umožněno
založit vlastní sekci s názvem *Embedded systems & IoT solutions*. Nabrali jsme jednoho kmenového
(a mimochodem výborného) programátora firmware, jednoho vývojáře elektroniky a několik studentů - brigádníků
z Fakulty aplikované informatiky UTB Zlín a začali vymýšlet IoT zařízení.

V rámci této sekce jsme postupně vyvinuli několik zařízení:

 - Průmyslový GPS snímač polohy s detekcí specifických pohybů
 - Osobní GPS snímač s SOS tlačítkem
 - Ultrazvukový snímač vzdálenosti
 - IoT jednotka univerzálních vstupů a výstupů (UNIO)


Největší uplatnění měla nakonec jednotka UNIO, kterou jsme v rámci hledání a vymýšlení
jejího uplatnění vybavili hydrostatickýcm snímačem tlaku. Tak vznikla jednotka WATER UNIO,
která sloužila k měření výšky hladiny. Typickou aplikací bylo měření ve studnách nebo
hloubkových vrtech v místech, kde bylo obtížné nasadit některý z konvenčních snímačů.

Spolu se snímačem WATER-UNIO jsme vyvinuli i webovou aplikaci pro management zařízení a agregaci dat. Uživatelé
pak měli k dispozici webové rozhraní a mobilní aplikaci.







