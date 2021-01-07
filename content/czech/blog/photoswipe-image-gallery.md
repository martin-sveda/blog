---
hero_title: "Blog"
title: "Galerie obrázků ve statickém webu pomocí Photoswipe"
date: 2021-01-06T11:07:10+06:00
#author: Martin Sveda
image : "images/blog/pharis/.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo"]
description: "Implementace galerie obrázků na statickém webu pomocí knihovny Photoswipe."
draft: true
type: "post"
---

Bla bla bla

## Prerekvizity

[Photoswipe](https://photoswipe.com/). 





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

## Implementace shortcode gallery.html

Galerie je generována pomocí shortcode, který je uložen v adresáři `layouts\shortcodes\gallery.html`.

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

## Inicializace knihovny Photoswipe v patičce stránek

Bla bla bla




