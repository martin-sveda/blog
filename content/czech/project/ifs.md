---
title: "Implementace ERP IFS v SAAB Czech"
description: "Implementace ERP IFS v SAAB Czech"
draft: false
image : "images/project/ifs.png"
bg_image: "images/featue-bg.jpg"
category: "management"
information:
  - label : "Zaměstnavatel"
    info : "Saab Czech s.r.o."
  - label : "Role"
    info : "Project manager"
---


## O projektu

V SAABu to po stránce přehledu a plánování vypadalo úplně stejně jako v každé jiné
firmě - všechno bylo v Excelu. A fungovalo to tak, že všechny odhady a parciální
výsledky vypadaly výborně. Jakmile ale došlo na finální závěrku tak přišlo rozčarování.

Každá oblast měla svůj vlastní systém - většinou v Excelu. Na pár místech se používaly
jednoúčelové IT systémy nebo programy, jako např. účetnictví, sklady, personalistika. 
Projekty měly své plánovací a reportovací tabulky, výroba také a vykazování hodin se 
dělo několika způsoby, pokud tedy vůbec...

Postupem času to bylo vše neřiditelné a přišli jsme na to, že data naprosto neodpovídají skutečnosti.
Takže přišel na řadu výběr jednoho systému, který by vše sjednotil a data z jednotlivých
firemních procesů agregoval a dostal pod jednu střechu.

V průběhu výběrového řízení jsme se přiklonili k ERP systému IFS. Shodou okolností to byl
naštěstí systém používaný matkou ve Švédsku, takže se schválením na korporátní úrovni
nebyl problém.

Po interních dohodách jsme se rozhodli implementovat následující oblasti:

 - projektové řízení
 - účetnictví a mzdy
 - nákup
 - sklady
 - výroba

### Projektové řízení

Ústřední myšlenkou byla možnost sledovat náklady na jednotlivých částech projektu a možnost
odhadu výsledků projektu na základě dosavadního průběhu. V rámci implementace jsme hledali
optimální kompromis mezi naším stylem řízení projektů, vyplývající ze specifik zbrojního průmyslu,
a standardními funkcemi IFS.


### Účetnictví a mzdy

V oblasti účetnictví byl nejdůležitějším parametrem samozřejmě legislativní rámec a také schopnosti
reportingu směrem k matce, která účtovala a plánovala trochu jiným způsobem.

### Nákup

Proces nákupu byl nastaven tak, aby umožňoval automatické generování požadavků na základě obrátek ve skladu,
minimálního množství a požadavků z výroby a vývoje. Proces měl nastavené limity jednotliých rolí dle
typů projektů a schvalovací workflow.

### Sklady

V oblasti skladového hospodářství jsme v podstatě jen migrovali data ze staršího systému a zaváděli nové
číslování tak, aby vyhovovalo tvorbě knihoven v elektrikářských i strojírenských CAD programech. S tím
souvisela i činnost spočívající v úpravě knihoven těchto programů.

### Výroba

Proces výroby byl navržen tak, aby umožňoval interní výrobu i výrobu v kooperaci. Na základě přenášených dat
z kusovníků byly generovány požadavky na sklad, resp. nákup a výrobní požadavky. Běhm výroby byly na dané
finální výstupy vykazovány hodiny i veškerý materiál, takže bylo možné dohledat materiálové
i personální náklady všech vyráběných položek.


## Přínosy

Obrovským přínosem implementace byla dle mého názoru standardizace všech procesů ve firmě. Jednotlivé
činnosti dostaly smysl a návaznost na další oblasti. Co nejvíce dat se přenášelo automaticky a dostali
jsme tak nástroj, který konečně poskytoval přesné a aktuální údaje o situaci ve firmě.

Moje role v tomto projektu byla jednak organizační a jednak jsem s Tomášem Zezulou (tehdejším finančním ředitelem)
v podstatě nastavoval všechny dotčené procesy.

