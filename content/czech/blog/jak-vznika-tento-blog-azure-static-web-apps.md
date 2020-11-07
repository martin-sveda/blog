---
title: "Jak vzniká tento blog - III. Azure Static Web Apps"
date: 2020-10-25T11:07:10+06:00
#author: Martin Švéda
image : "images/blog/jamstack/Microsoft_Azure_Logo.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo", "Azure"]
description: ""
draft: false
type: "post"
---


Azure Static Web Apps (ASWA) je služba, které umožňuje hostování statických webových stránek v cloudu Azure
a to v úzké provázanosti se službou GitHub. ASWA je tedy připravena pro použití ve workflow, které
odpovídá principům DevOps a to je na tom vlastně celé krásné. 


## Založení účtu Azure

Na stránkách [Azure](https://azure.microsoft.com/cs-cz/free/) si založte svůj free účet Azure. Zdarma
je sice jen na jeden rok, ale ani potom vás náklady této služby určitě nezruinují.

Pro založení budete potřebovat následující:
 - svůj Microsoft účet 
 - telefon pro ověření
 - platební kartu pro ověření a budoucí platby

Nic víc není potřeba - a pokud ano, tak se tím určitě hravě prokoušete.

## Založení Azure Static Web Apps

Po přihlášení ke svému Azure účtu byste na ploše měli vidět ikonu ***Static Web Apps***. Klikněte
na ni a poté přidejte novou webovou aplikaci (***Add***).

Následně budete vyzváni k vyplnění níže uvedeného formuláře:

!["Založení nové Azure Static Web App - krok 1"](/images/blog/jamstack/create-azure-1.png)

Jednotlivé pole mají následující význam:

 - ***Subscription*** - název vašeho předplatného Azure
 - ***Resource-group*** - skupina souvisejících prostředků
 - ***Name*** - název vaší aplikace
 - ***Region*** - vyberte, kde se bude vaše aplikace nacházet
 - ***GitHub accont*** - propojení s vaším GitHub účtem


## Propojení Azure účtu s GitHub Actions

V dalším kroku budete vyzváni k autorizaci Azure do vašeho GitHub účtu. Poté co Azure získá přístup
k vašemu GitHub účtu, vyplníte další podrobnosti, které se týkají
repozitáře, ve kterém jsou uložena zdrojová data vaší výsledné aplikace:

!["Založení nové Azure Static Web App - krok 2"](/images/blog/jamstack/create-azure-2.png)


Jakmile budete mít vyplněno, stiskněte ***Review + Create*** a následně ***Create***.

Poté můžete přejít k záznamům své webové aplikace. Info o nově vytvořené aplikaci může vypadat 
zhruba následovně:


!["Založení nové Azure Static Web App - krok 3"](/images/blog/jamstack/create-azure-2.png)

Z uvedeného obrázku je vidět, že aplikace je hostovaná na adrese `https://zealous-sky-083c63503.azurestaticapps.net`. 
Současně vám Azure vytvořil v master větvi vašeho repozitáře soubor `azure-static-web-apps-zealous-sky-083c63503.yml`,
což je vlastně GitHub actions deployment sktript. 




## Nasazení webové aplikace do Azure

Po autorizaci, kterou jste provedli o krok výše, je vás GitHub účet propojen s vaším účtem Azure. GitHub má tedy
bezpečný přístup do Azure, což si ověříte tak, že ve svém repozitáře přejdete do ***Settings*** - ***Secrets***
a uvidíte, že zde jsou bezpečnostní tokeny vašeho Azure účtu.

V adresáři `.github/workflows/` je uložen deployment skript, který tam byl službou Azure nahrán v průběhu autorizace. 
Originální skript bude potřeba trochu upravit. Níže se podíváme, jak by takový skript mohl vypadat.




Ti, co jsou v deployment skriptech jako doma už dále číst nemusí. Pro ostatní ho celý rozeberu po jednotlivých částech:


### Startovací triggery

Startovací triggery definují, kdy se daný skript, resp. jeho jednotlivé úlohy, spouští.

``` yaml
on:
  push:
    branches:
      - master
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - master
```

V našem případě se úlohy spustí v následujících případech:

 - po pushnutí změn repozitáře do `master` větve
 - po pull requestu do `master` větve 



### Úlohy

Náš deployment skript obsahuje dvě úlohy: `build_and_deploy_job` a `close_pull_request_job`.


#### Build and deploy


``` yaml
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v2
      - uses: jakejarvis/hugo-build-action@master  # ...or replace 'master' with a full version tag, such as: v0.64.1
#        with:
#         # args: --buildDrafts
      - uses: actions/upload-artifact@master
        with:
          name: blog
          path: './public'
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v0.0.1-preview
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_LIVELY_DUNE_02B7DFF03 }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match you app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "./public" # App source code path
          api_location: "api" # Api source code path - optional
          app_artifact_location: "." # Built app content directory - optional
          ###### End of Repository/Build Configurations ######
```

Úloha `build_and_deploy_job` má dva kroky (`steps`) a provede zhruba následující:

 1. Ve virtuállním prostředí GitHubu se vytvoří a spustí linuxový Docker kontejner `ubuntu-latest`
 2. Spustí se akce `actions/checkout`, která do vytvořeného kontejneru stáhne `master` větvi vašeho repozitáře webové 
    aplikace na GitHubu
 3. Spustí se akce `jakejarvis/hugo-build-action@master` (v poslední `master` verzi), která nejprve do virtuálního stroje
    nainstaluje statický generátor [Hugo](https://gohugo.io) a následně vygeneruje vaši webovou aplikaci ze stažených
    zdrojových kódů
 4. Spustí se akce `actions/upload-artifact`, který vygenerované statické stránky zkopíruje do adresáře `./public` 
    virtuálního stroje
 5. Spustí se akce `Azure/static-web-apps-deploy`, která s pomocí _secret tokenů_ nasadí vaši aplikaci do vašeho 
    Azure repozitáře

#### Úklid

``` yaml
close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v0.0.1-preview
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_LIVELY_DUNE_02B7DFF03 }}
          action: "close"
```

Úloha `close_pull_request_job` dělá přesně to, co má ve svém názvu - uzavře daný pull request.


Po aplikaci všech výše uvedených úloh a kroků by vaše webová aplikace měla být nasazena a funkční.


### Kompletní deployment skript

Celý vzorový skript tedy vypadá následovně:

```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - master
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - master

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v2
      - uses: jakejarvis/hugo-build-action@master  # ...or replace 'master' with a full version tag, such as: v0.64.1
#        with:
#         # args: --buildDrafts
      - uses: actions/upload-artifact@master
        with:
          name: blog
          path: './public'
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v0.0.1-preview
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_LIVELY_DUNE_02B7DFF03 }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match you app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "./public" # App source code path
          api_location: "api" # Api source code path - optional
          app_artifact_location: "." # Built app content directory - optional
          ###### End of Repository/Build Configurations ######

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v0.0.1-preview
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_LIVELY_DUNE_02B7DFF03 }}
          action: "close"
```

***Pozn.:*** _Uvedený skript a mnohé podobné najdete všude na internetu. Tento vychází přímo z dokumentace Microsoftu._


## Související články

 - [Jak vzniká tento blog - I. Úvod a motivace]({{< ref "jak-vznika-tento-blog-uvod.md" >}} "Jak vzniká tento blog - I. Úvod a motivace")
 - [Jak vzniká tento blog - II. HUGO statický generátor webu]({{< ref "jak-vznika-tento-blog-hugo-staticky-generator-webu.md" >}} "Jak vzniká tento blog - II. HUGO statický generátor webu")


