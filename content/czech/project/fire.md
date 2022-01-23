---
title: "FIRE - univerzální HW platforma pro speciální vozy"
description: "FIRE - univerzální HW platforma s řídicí jednotkou, displejem a I/O moduly pro speciální vozy"
draft: false
image : "images/project/fire.jpg"
bg_image: "images/blog_bg.jpg"
category: "Automotive"
information:
  - label : "Zaměstnavatel"
    info : "UNIS, a.s."
  - label : "Role"
    info : "Project manager"
  - label : "Klient"
    info : "THK Polička"
  - label : "Doba realizace"
    info : "5 let"
  - label : "Velikost týmu"
    info : "12"
---


## O projektu

Projekt FIRE zahrnoval dlouhodobý vývoj a výrobu modulů pro speciální hasičské vozy
vyráběné společností THK Polička.

Jednalo se o následující moduly:

 - DISP 64 a DISP84 - řídicí jednotky s displejem pro ovládání jednotlivých funkcí systému
 - FCU - Foam Control Unit - jednotka řízení přiměšování hasicí pěny
 - EXP - univerzální I/O modul
 - REL - modul se spínatelnými výkonovými relé
 - KLAV - univerzální klávesnice

## Technické řešení

FIRE byl postaven jako univerzální a modulární systém, kde spolu jednotlivé moduly komunikují
po sběrnici CAN. Řízení mohlo probíhat jak z přední, tak zadní části vozu současně - tzn. že
obě řídicí jednotky pracovali v redundantním módu a informace a spouštěné funkce na jedné
řídicí jednotce se automaticky zobrazovali na druhé.

Řešení bylo postaveno na MCU od firmy Microchip. Řídicí jednotka s displejem obsahovala
procesor od firmy Intel.



