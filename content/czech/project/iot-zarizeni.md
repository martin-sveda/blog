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
  - label: "Velikost týmu"
    info: "5"
  - label: "Doba realizace"
    info: "2 roky"

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


## IoT zařízení 

Všechny snímače byly postaveny na MCU platformě STM32L, jako OS pro firmware byl použit FreeRTOS
a komunikace probíhala pomocí rádiové sítě Sigfox.


### GPS IoT snímač

GPS snímač odesílá v pravidelných intervalech informaci o poloze snímače do cloudu. Snímač lze nastavit tak,
aby reagoval na různou intenzitu pohybu, detekoval náklony a posílal data jen za určitých podmínek.


### UNIO

Snímač UNIO dokáže v nastavených intervalech měřit následující veličiny:

- proud (4 - 20mA) a napětí (0 - 10V) na svých svorkách
- teplotu okolí
- náklon zařízení

Kromě měření výše uvedených veličin byl snímač vybaven i možností spínaného napájení externího zařízení. 

### WATER UNIO

Snímač WATER UNIO měří v pravidelných intervalech měřit hladinu vody např. ve studni. Změřená data jsou odesílána 
do cloudu, kde dojde k jejich zpracování a vizualizaci.

Informace o výšce hladiny je možné si prohlédnout na webu, nebo v aplikaci na mobilním telefonu.


### UZ snímač

Ultrazvukový snímač vzdálenosti, který se může použít např. pro měření hladiny řek nebo naplněnost kontejneru.


## Cloudová platforma a mobilní aplikace

Informace o změřených veličinách byly posílány do cloudových platforem Thingsboard nebo MES PHARIS, kde došlo
k procesingu a vizualizaci dat.

Stejné možnosti byly dostupné i v mobilních aplikacích na platformě Android.






