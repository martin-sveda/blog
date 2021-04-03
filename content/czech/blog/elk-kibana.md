---
hero_title: "Blog"
title: "Vizualizace logů MES PHARIS pomocí nástroje Kibana"
date: 2021-04-03T10:55:10+06:00
#author: Martin Sveda
image : "images/blog/elk/elk-hero.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Pharis"]
description: "Vizualizace logů MES PHARIS pomocí nástroje Kibana (ELK stack)."
draft: false
type: "post"
---

Tento post navazuje na předcházející díl [Analýza logů MES PHARIS pomocí nástrojů ELK stacku]({{< ref "docker-elk-stack.md" >}} "Analýza 
logů MES PHARIS pomocí nástrojů ELK stacku"). V tomto díle se podíváme na vizualizaci logů MES PHARIS v nástroji Kibana.


## Vizualizace logů v Kibaně

Abychom mohli logy v Kibaně vizualizovat je, potřeba vytvořit nový index, jehož data budeme vizualizovat. To se provede
následovně: na hlavní obrazovce klikněte na `Manage` - `(Kibana) Index Patterns` - `Create index pattern`.

V dialogovém okně zadejte jméno indexu v Elasticsearch, který se použije v Kibaně, viz obrázek:


!["Tvorba indexu v Kibaně"](/images/blog/elk/elk-ip-1.png)

Na dalším okně vybereme primární pole pro časový filter - tedy `@timestamp`:

!["Výběr primárního časového indexu v Kibaně"](/images/blog/elk/elk-ip-2.png)

Stiskneme `Create index pattern` a máme hotovo - Kibana zobrazí všechna pole v daném indexu, ze kterých
následně můžeme tvořit vizualizace.


## Kontrola logů v Elasticsearch

Úspěšné přenesení a uložení logů do Elasticsearch poznáme jednak podle existence daného indexu a jednak kontrolou dat
uvnitř indexu. Data zobrazíme po kliknutí na `Analytics` - `Discover` v hlavním (hamburgerovém) menu Kibany.

Data by měla být uložena v JSON formátu se zhruba následující podobou:

```json
{
  "_index": "oper_debug_logs",
  "_type": "oper_debug_doc",
  "_id": "eE6HlngBu7D6TvjwV5Db",
  "_version": 1,
  "_score": null,
  "_source": {
    "@timestamp": "2021-03-24T14:14:13.672Z",
    "path": "d:/msveda/docker/Debug.txt",
    "host": "PC5406303",
    "log_level": "DEBUG",
    "ip_addr": "10.10.200.121",
    "tags": [
      "multiline"
    ],
    "message": [
      "2021-03-24 15:14:13.6728|DEBUG||\r\n\r\n####### 2021-03-24-15-14-13-6728 - IDE0MPC021 (10.10.200.121) - Client_Log_Debug :\r\n3/24/2021 3:14:13 PM | VarioIdReader | Stop read\r\n\r\n\r",
      "- Client_Log_Debug :\r\n3/24/2021 3:14:13 PM | VarioIdReader | Stop read\r\n\r\n\r"
    ],
    "logdate": "2021-03-24 15:14:13.6728",
    "terminal_id": "IDE0MPC021",
    "@version": "1"
  },
  "fields": {
    "@timestamp": [
      "2021-03-24T14:14:13.672Z"
    ]
  },
  "sort": [
    1616595253672
  ]
}
```

V uvedeném JSON souboru by měla být vidět všechny pole, které jsme předím definovali v `grok` filtru nástroje `logstash`.



## Tvorba dashboardu


Ukázkový dashboard vytvoříme nad daty o terminálech - budou nás zajímat informace o jednotlivých terminálech a jejich IP adresách.

Klikneme na `Analztics` - `Dashboard` a vytvoříme první dashboard. 

Pro zobrazení záznamů o terminálech se nejlépe hodí tabulka. Klikneme na `Create panel` - `Lens` a typ jako vizualizace zvolíme
`Data table`. Pro vytvoření správné tabulky pak stačí pouze přenést formou Drag & Drop pole `host.keyword` a `ip_addr.keyword`
do vizualizační komponenty a tabulka se automaticky vytvoří.

Pro správné zobrazení je potřeba nastavit ještě pár drobností:

- odstranit z tabulky metriku počítání jednotlivých záznamů
- nastait počet top values na nějakou vysokou hodnotu (jinak nám Kibana zobrazí Top N záznamů a zbytek shlukne pod others)

Výsledná tabulka může vypadat následovně:

!["Tabulka terminálů a jejich IP adres"](/images/blog/elk/elk-data-table.png)


Další možnou vizualizací je zobrazení informací z TRACE.TXT - např. zobrazení událostí, které nastávají v komponentě Repository. 

!["Příklad vizualizovaného logu v Kibaně"](/images/blog/elk/elk-stacked-bar.png)

