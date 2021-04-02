---
hero_title: "Blog"
title: "Analýza logů MES PHARIS pomocí ELK stacku"
date: 2021-04-02T19:55:10+06:00
#author: Martin Sveda
image : "images/blog/elk/elk-hero.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo"]
description: "Analýza dvou typů logů MES PHARIS pomocí dockerizovaného ELK stacku v prostředí Windows 10."
draft: true
type: "post"
---


Následující post popisuje istalaci dockerizovaného ELK stacku na lokální počítač a analýzu logů
po zadrhávání systému MES PHARIS při přenosu do datacentra a upgradu systému v IDE.


## Co je to ELK stack?

TBD

 
## Instalace potřebných nástrojů 

### Instalace dockerizovaného ELK stacku

Pro instalaci ELK stacku je potřeba stáhnout a nainstalovat [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows/), 
nebo-li distribuci dockeru pro Windows 10.

Jakmile máme nainstalovaný Docker na svém počítači, spustíme konzoli s právy administrátora a zadáme příkaz `docker pull sebp/elk`, který
nám do místního Docker repozitáře stáhne oficiální image ELK stacku. K uvedenému image je k dispozici podrobná
[dokumentace](https://elk-docker.readthedocs.io/), která popisuje vše potřebné pro provoz ELK stacku.


### Instalace nástroje logstash

Logstash je nástroj, který čte logy v takřka libovolném formátu, transformuje je do požadované podoby množiny záznamů `KEY`:`VALUE`
a odesílá je do databáze Elasticsearch.

Logstash je možné stáhnout z oficiálních [balíčků](https://www.elastic.co/downloads/logstash) na webu Elasticu.

Pro instalaci je doporučeno stažení JVM (Java Virtual Machine) a nastavení proměnných prostředí. Více o postupu instalace je
možné najít v oficiální [dokumentaci](https://www.elastic.co/guide/en/logstash/current/running-logstash-windows.html). Já si JVM
stáhl a vše nastavil a pak mi logstash psal, že to stejně nebylo potřeba, protože si JVM táhne s sebou.



## Normalizace logů

Pro analýzu byly použity dva druhy logů:
 - TRACE.TXT
 - DEBUG.TXT

Pro každý typ logu je potřeba napsat vlastní konfiguraci nástroje `logstash` pro správnou/požadovanou transformaci dat z těchto
logů.


### Transformace TRACE.TXT

Vstupní soubor TRACE.TXT vypadá zhruba následovně:

```
2021-03-24 00:00:04.4320|TRACE||MSSQL|PrepCommand prov: 0, thr: 129. Cmd: SELECT @@SPID (@RETURN_VALUE: Null)
2021-03-24 00:00:04.4320|TRACE||MSSQL|PrepCommand prov: 0, thr: 129. Cmd: set transaction isolation level read committed (@RETURN_VALUE: Null)
2021-03-24 00:00:04.4320|TRACE||MSSQL|PrepCommand prov: 0, thr: 129. Cmd: SELECT MU.*, U.UserName AS CLIENTID FROM [BOARD].[MessageUser] MU JOIN MAIN.[User] U ON MU.UserId = U.RecordId 
											WHERE U.UserAccountType = @UserAccountType AND MU.DateSent >= @DateSent AND U.UserStatus = @UserStatus ORDER BY MU.DateSent DESC (@UserAccountType: 1, @DateSent: 23-03-2021 23:50:04, @UserStatus: 6, @RETURN_VALUE: Null)
2021-03-24 00:00:04.4320|TRACE||MSSQL|Closing MS SQL connection for provider 0, thr: 129
2021-03-24 00:00:05.9946|TRACE||MSSQL|PrepCommand prov: 0, thr: 346. Cmd: SELECT MAX(last_user_update) FROM sys.dm_db_index_usage_stats WHERE database_id = DB_ID() AND OBJECT_ID=OBJECT_ID('[CONF].[PhysicalLevel]') (@RETURN_VALUE: Null)
2021-03-24 00:00:05.9946|TRACE||MSSQL|PrepCommand prov: 0, thr: 346. Cmd: SELECT MAX(last_user_update) FROM sys.dm_db_index_usage_stats WHERE database_id = DB_ID() AND OBJECT_ID=OBJECT_ID('[DEV].[Equipment]') (@RETURN_VALUE: Null)
2021-03-24 00:00:05.9946|TRACE||MSSQL|PrepCommand prov: 0, thr: 346. Cmd: SELECT EA.TagAttributeId FROM DEV.TagsOnEquipment EA
										    WHERE EA.EquipmentId='20f17a43-e7c3-4691-aa88-eb0d144015e3' AND ( EA.TagAttributeId='000000a7-3182-462c-012a-0037a24feac5' ) (@RETURN_VALUE: Null)
2021-03-24 00:00:05.9946|TRACE||MSSQL|PrepCommand prov: 0, thr: 346. Cmd: SELECT EA.TagAttributeId FROM DEV.TagsOnEquipment EA
										    WHERE EA.EquipmentId='9c94ebc7-749f-4b5f-ac80-c6685ae703ea' AND ( EA.TagAttributeId='fbb13408-142f-40ce-8194-6d665e1bf328' ) (@RETURN_VALUE: Null)

```

Log obsahuje relativně smysluplnou strukturu, která má svoje rezervy a šla by udělat pro budoucí strojovou analýzu i lépe. Pozor je třeba si dát
i na to, že jeden záznam logu je někdy přes více řádků.


#### Konfigurace logstash pro zpracování TRACE.TXT

Pro zpracování tohoto logu je třeba vytvořit konfigurační soubor s předpisem pro zpracování tohoto logu. Níže uvádím jeho
výpis i s komentáři.

```docker
# Logstash konfig pro TRACE.TXT
# File -> Logstash -> Elasticsearch pipeline.

# Definice vstupních parametrů /filtrů / předpisu zpracování
#
#
input {
  # Budeme zpracovávat soubor
  file {
    # cesta k souboru s logy
    path 	=> 	[ "d:/msveda/docker/trace.txt" ]
    # zpracování víceřádkových logů - vše, co začíná bílým znakem bude připojeno
    # k předchozímu řádku
    codec => multiline {
      pattern => "^\s"
      what => "previous"
    }
    # soubor se zpracovává od začátku (pozor - logstash si pamatuje, který soubor
    # již zpracoval a kam až došel, takže při opětovném spuštění zpracování logu
    # je potřeba smazat dočasné soubory .sinceXXXXXXX (v adresáři data logstashe)
    start_position => "beginning"
  }
}

# část aplikace filtru na každý vstupní řádek logu
filter {
      # grok je filtr, který parsuje text, hledá v něm dané patterny a vystupují z něj strukturovaná data
      grok {
        # match - hledá daný pattern
        # pro význam jednotlivých předdefinovaných patternů viz
        # https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html
        #
         match => { "message" => "%{DATESTAMP:logdate}\|%{LOGLEVEL:log_level}\|\|%{WORD:actor}\|%{GREEDYDATA:message}" } 
      }
      
      date {
        # na závěr je ještě třeba normalizovat časovou značku - textové pole označit jako primární
        # entitu pro řazení v Elasticsearchi
        match => [ "logdate", "yy-MM-dd HH:mm:ss.SSSS" ]
        target => "@timestamp"
      } 
}


# definice výstup
output {
  # výstup je přesměrován na port elasticsearche
  elasticsearch { 
  hosts => ["localhost:9200"] 
  # jméno indexu pro uložení TRACE logů
  index => "phar2_logs"
  document_type => "phar2_doc"
  }
  
  # pro debug je dobré vypisovat i na stdout (kdo chce vidět, odkomentuje)
  # stdout {}
 }
```

### Transformace DEBUG.TXT

Vstupní soubor DEBUG.TXT vypadá zhruba následovně:

```
2021-03-24 00:00:04.9007|DEBUG||

####### 2021-03-24-00-00-04-9007 - IDE0MPC058 (10.10.201.55) - Client_Log_Debug :
24.03.2021 0:00:03 | VarioIdReader | Stop read


2021-03-24 00:00:04.9320|DEBUG||

####### 2021-03-24-00-00-04-9320 - IDE0MPC058 (10.10.201.55) - Client_Log_Debug :
24.03.2021 0:00:03 | VarioIdReader | Stop read - didn't receive periodic log.


2021-03-24 00:00:07.0572|DEBUG||

####### 2021-03-24-00-00-07-0572 - IDE0MPC008 (10.10.200.108) - Client_Log_Debug :
3/24/2021 12:00:06 AM | VarioIdReader | Start read


2021-03-24 00:00:07.1197|DEBUG||CInputComponentControl.UpdateCurrentInputStates || MaterialId: <null>, newNote: <null>.
2021-03-24 00:00:07.1197|DEBUG||

####### 2021-03-24-00-00-07-1197 - IDE0MPC002 (10.10.200.102) - Client_Log_Debug :
MultipleOperationsSignInManager | ProcessNextSignInFromMultipleOperations || Stav spusteni, session: 02000032-4271-a82b-90c4-00396e58ad27, Hodnoty: 111111111
```

#### Konfigurace logstash pro zpracování DEBUG.TXT

Pro zpracování tohoto logu je třeba vytvořit konfigurační soubor s předpisem pro zpracování tohoto logu. Níže uvádím jeho
výpis i s komentáři.

Za zmínku zde stojí pouze to, že `grok` umí **vyhledávat i mezi více patterny najednou**.

```docker
# Logstash konfig pro DEBUG.TXT
# File -> Logstash -> Elasticsearch pipeline.

# už bez podrobných komentářů - viz trace.conf
input {
  file {
    path 	=> 	[ "d:/msveda/docker/Debug.txt" ]
    codec => multiline {
       pattern => "^%{TIMESTAMP_ISO8601}"
       negate => true
       what => previous
    }
    start_position => "beginning"
  }
}

filter {
      grok {
        # grok umí zpracovat i několik různých patternů
        # pak je třeba mu patterny podhodit jako pole patternů
        # když najde odpovídající záznam v logu, vytvoří strukturu dle jednoho z níže uvedených patternů
         match => { "message" => [ "%{TIMESTAMP_ISO8601:logdate}\|%{LOGLEVEL:log_level}\|\|%{SPACE}####### %{YEAR}-%{MONTHNUM}-%{MONTHDAY}-%{HOUR}-%{MINUTE}-%{SECOND}-%{INT} - %{HOSTNAME:terminal_id} \(%{IP:ip_addr}\) %{GREEDYDATA:message}",
                                   "%{TIMESTAMP_ISO8601:logdate}\|%{LOGLEVEL:log_level}\|\|%{WORD:issuer}\|Outdate table \[BATCH\]\.\[%{WORD:operation}\]%{GREEDYDATA:message}",
                                   "%{TIMESTAMP_ISO8601:logdate}\|%{LOGLEVEL:log_level}\|\|%{WORD:issuer}%{GREEDYDATA:message}" ]
                  } 
      }
      
      date {
        match => [ "logdate", "yy-MM-dd HH:mm:ss.SSSS" ]
        target => "@timestamp"
      } 
}

output {
  elasticsearch { 
  hosts => ["localhost:9200"] 
  index => "oper_debug_logs"
  document_type => "oper_debug_doc"
  }
  
#  stdout {}
 }
```

## Spuštění ELK stacku a transformace logů

### Spuštění ELK stacku

Dockerizovaný ELK stack spustíme z administrátorské konzole následovně:

```bash
$ docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk
```

Počkáme, až vše naběhne a pak v prohlížeči zadáme adresu `http://localhost:5601` a mělo by nám naběnout rozhraní
KIBANA.


### Transformace logů ze souboru do Elasticsearche

Logstash máme nakonfigurovaný z předchozích kapitol, takže spustíme následující dva příkazy:

```bash
$ bin/logstash -f trace.conf.conf
$ bin/logstash -f debug.conf
```
Tyto dva příkazy spustí transfrmaci a přenos logů z našich souborů do Elasticsearche pro jejich další
zpracování. Dle velikosti souboru to může nějakou dobu trvat.

V Kibaně bychom následně měli mít k dispozici dva indexy: `oper_debug_logs` a `phar2_logs`.


## Vizualizace logů v Kibaně

Na hlavní stránce klikneme na odkaz `Manage` a přidáme oba indexy.

Vytvoříme dashboard, vybereme jaký typ vizualizace chceme, umístíme ho na dashboard, na osu X dáme pole `@timestamp`
a na osu Y cokoliv nás napadne vizualizovat ;-)

!["Příklad vizualizovaného logu v Kibaně"](images/blog/elk/elk-example.png)

