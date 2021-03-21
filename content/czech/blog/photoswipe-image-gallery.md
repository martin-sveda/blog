---
hero_title: "Blog"
title: "Galerie obrázků ve statickém webu pomocí Photoswipe"
date: 2021-01-06T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/photoswipe/photoswipe.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo"]
description: "Implementace galerie obrázků na statickém webu pomocí knihovny Photoswipe."
draft: true
type: "post"
---

Photoswipe je JavaScriptová knihovna pro tvorbu obrázkových galerií. Umožňuje postupné nahrávání
obrázků (lazy loading), ovládání pomocí gest, repsonsivní design, zoomování obrázků a další.
Následující článek vám ukáže, jak Photoswipe použít na statickém webu generovaném pomocí 
[Hugo](https://gohugo.io).




## Nastavení Photoswipe pro použití v Hugo

Pro použití Photoswipe v našem statickém webu, resp. v předlohách pro Hugo je nutné provést
následující:

 - Stáhnutí Photoswipe
 - Vytvoření shortcode
 - Inicializace knihovny v patičce stránek
 - Vložení obrázků do požadovaných stránek 


### Stažení Photoswipe

Pro použití postačí stáhnout aktuálnéí verzi ze stránek [Photoswipe](https://photoswipe.com/).
Knihovna nemá žádné závislosti, takže nic dalšího potřebovat nebudeme.
Knihovnu stáhneme z [GitHubu](https://github.com/dimsemenov/PhotoSwipe). Najdeme zde adresář
`dist`, který celý zkopírujeme do lokálního adresáře `static/plugins/photoswipe` v používaném tématu,
v mém případě tedy do `blog/themes/airspace-hugo/static/plugins/photoswipe`.


### Implementace shortcode gallery.html

Shortcode v Hugo je malý kousek kódu (snippet), který v kontentových souborech (to jsou ty markdowny s nějakým obsahem)
vyvolá jejich implementaci, tedy vygenerování výsledného HTML kódu pomocí šablony definované tímto shortcodem.

Shortcode naší galerie uložíme do souboru `layouts\shortcodes\gallery.html`, který bude mít následující obsah:

```xml
{{ $scratch := newScratch }}

{{ with .Get "title" }}
  <h3>{{ . }}</h3>
{{ end }}

  <div class="gallery" itemscope itemtype="http://schema.org/ImageGallery">


    {{ range (.Page.Resources.Match (printf "%s/*" (.Get "folder"))) }}

    {{ $scratch.Set "thumb" (printf "%s" .Permalink) }}

    {{ $orientation := 1 }}

    {{ $orientation = .Exif.Tags.Orientation }}

      {{ if eq $orientation 1 }}
        {{ $thumbnail := .Resize "200x" }}
        {{ $scratch.Set "thumb" $thumbnail.Permalink }}
          <figure itemscope itemtype="http://schema.org/ImageObject" class="image gallery-item">
            <a href="{{ .Permalink }}" itemprop="contentUrl" data-size="{{ .Width }}x{{ .Height }}" >
              <img src="{{ $thumbnail.Permalink }}" itemprop="thumbnail" alt="galleryImage" class="galleryImage" />
            </a>
            <figcaption itemprop="caption description">
              <span itemprop="copyrightHolder"></span>
            </figcaption>
          </figure> 
      
      {{ else if (eq $orientation 6) }}
        {{ $thumbnail := .Resize "200x r270" }}
        {{ $scratch.Set "thumb" $thumbnail.Permalink }}
        <figure itemscope itemtype="http://schema.org/ImageObject" class="image gallery-item">
          <a href="{{ .Permalink }}" itemprop="contentUrl" data-size="{{ .Height }}x{{ .Width }}" >
            <img src="{{ $thumbnail.Permalink }}" itemprop="thumbnail" alt="galleryImage" class="galleryImage" />
          </a>
          <figcaption itemprop="caption description">
            <span itemprop="copyrightHolder"></span>
          </figcaption>
        </figure> 

      {{ end }}

  {{ end }}

  </div>

```


### Inicializace knihovny Photoswipe v patičce stránek

Abychom mohli Photoswipe využít na každé stránce, je třeba do patičky všech stránek umístit
inicializační kód knihovny.





## Nastavení vlastností dokumentu

Každý dokument, který využívá statického generování obrázkové galerie musí mít nastaveny své 
vlastnosti zhruba následovně:

```yaml
resources:
- src: "*.jpg"
  name: img-:counter
  title: img-title:counter
```

Výše uvedené vlastnosti v podstatě znamenají to, že pro obrázkovou galerii budou
použity soubory `*.jpg`, přičemž při generování odkazů na obrázky budou jakékoliv
nalezené soubory pojmenovány `img-XXXX`, kde `XXXX` bude nahrazeno čísly. Proměnná
`img-title:counter` pak bude nabývat podobných hodnot a může být např. využita pro 
generování doplňujícího titulku obrázku.


## Použití shortcode gallery.html v dokumentu

Pro generování výsledného seznamu obrázků se použije následující shortcode:

```xml
{{ < gallery folder="img" title="Galerie obrázků" > }}
```






