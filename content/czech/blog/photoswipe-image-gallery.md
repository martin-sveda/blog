---
hero_title: "Blog"
title: "Galerie obrázků ve statickém webu pomocí Photoswipe"
date: 2021-03-23T19:55:10+06:00
#author: Martin Sveda
image : "images/blog/photoswipe/photoswipe.png"
bg_image: "images/blog_bg.jpg"
categories: ["Psaní"]
tags: ["Hugo"]
description: "Implementace galerie obrázků na statickém webu pomocí knihovny Photoswipe."
draft: false
type: "post"
---

Photoswipe je JavaScriptová knihovna pro vkládání obrázkových galerií na web. Umožňuje postupné nahrávání
obrázků (lazy loading), ovládání pomocí gest, repsonsivní design, zoomování obrázků a další.
Následující článek vám ukáže, jak Photoswipe použít na statickém webu generovaném pomocí 
[Hugo](https://gohugo.io).




## Nastavení Photoswipe pro použití v Hugo

Pro použití Photoswipe ve statickém webu je nutné provést
následující:

 - Stáhnutí Photoswipe
 - Vytvoření Hugo shortcode
 - Inicializace knihovny Photoswipe v patičce stránek
 - Vložení obrázkové galerie do požadovaných stránek 


### Stažení Photoswipe

Pro použití postačí stáhnout aktuální verzi [Photoswipe](https://photoswipe.com/) z 
[GitHubu](https://github.com/dimsemenov/PhotoSwipe). Najdeme zde adresář
`dist`, který celý zkopírujeme do lokálního adresáře `static/plugins/photoswipe` v používaném tématu -
v mém případě tedy do `blog/themes/airspace-hugo/static/plugins/photoswipe`.


### Implementace shortcode gallery.html

Shortcode v Hugo je malý kousek kódu (snippet), který v kontentových souborech (to jsou ty markdowny s nějakým obsahem)
provede vygenerování výsledného HTML kódu pomocí šablony definované tímto shortcodem.

Shortcode naší galerie uložíme do souboru `layouts\shortcodes\gallery.html`, který bude mít následující obsah:

```html
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


### Inicializace knihovny Photoswipe

Před použitím je potřeba knihovnu inicializovat. V adresáři `themes\airspace-hugo\static\plugins\photoswipe\` 
vytvoříme soubor `initphotoswipe.js` a vložíme tam následující kód:

```javascript
var initPhotoSwipeFromDOM = function(gallerySelector) {

    // parse slide data (url, title, size ...) from DOM elements 
    // (children of gallerySelector)
    var parseThumbnailElements = function(el) {
        var thumbElements = el.childNodes,
            numNodes = thumbElements.length,
            items = [],
            figureEl,
            linkEl,
            size,
            item;

        for(var i = 0; i < numNodes; i++) {

            figureEl = thumbElements[i]; // <figure> element

            // include only element nodes 
            if(figureEl.nodeType !== 1) {
                continue;
            }

            linkEl = figureEl.children[0]; // <a> element

            size = linkEl.getAttribute('data-size').split('x');

            // create slide object
            item = {
                src: linkEl.getAttribute('href'),
                w: parseInt(size[0], 10),
                h: parseInt(size[1], 10)
            };



            if(figureEl.children.length > 1) {
                // <figcaption> content
                item.title = figureEl.children[1].innerHTML; 
            }

            if(linkEl.children.length > 0) {
                // <img> thumbnail element, retrieving thumbnail url
                item.msrc = linkEl.children[0].getAttribute('src');
            } 

            item.el = figureEl; // save link to element for getThumbBoundsFn
            items.push(item);
        }

        return items;
    };

    // find nearest parent element
    var closest = function closest(el, fn) {
        return el && ( fn(el) ? el : closest(el.parentNode, fn) );
    };

    // triggers when user clicks on thumbnail
    var onThumbnailsClick = function(e) {
        e = e || window.event;
        e.preventDefault ? e.preventDefault() : e.returnValue = false;

        var eTarget = e.target || e.srcElement;

        // find root element of slide
        var clickedListItem = closest(eTarget, function(el) {
            return (el.tagName && el.tagName.toUpperCase() === 'FIGURE');
        });

        if(!clickedListItem) {
            return;
        }

        // find index of clicked item by looping through all child nodes
        // alternatively, you may define index via data- attribute
        var clickedGallery = clickedListItem.parentNode,
            childNodes = clickedListItem.parentNode.childNodes,
            numChildNodes = childNodes.length,
            nodeIndex = 0,
            index;

        for (var i = 0; i < numChildNodes; i++) {
            if(childNodes[i].nodeType !== 1) { 
                continue; 
            }

            if(childNodes[i] === clickedListItem) {
                index = nodeIndex;
                break;
            }
            nodeIndex++;
        }



        if(index >= 0) {
            // open PhotoSwipe if valid index found
            openPhotoSwipe( index, clickedGallery );
        }
        return false;
    };

    // parse picture index and gallery index from URL (#&pid=1&gid=2)
    var photoswipeParseHash = function() {
        var hash = window.location.hash.substring(1),
        params = {};

        if(hash.length < 5) {
            return params;
        }

        var vars = hash.split('&');
        for (var i = 0; i < vars.length; i++) {
            if(!vars[i]) {
                continue;
            }
            var pair = vars[i].split('=');  
            if(pair.length < 2) {
                continue;
            }           
            params[pair[0]] = pair[1];
        }

        if(params.gid) {
            params.gid = parseInt(params.gid, 10);
        }

        return params;
    };

    var openPhotoSwipe = function(index, galleryElement, disableAnimation, fromURL) {
        var pswpElement = document.querySelectorAll('.pswp')[0],
            gallery,
            options,
            items;

        items = parseThumbnailElements(galleryElement);

        // define options (if needed)
        options = {

            // define gallery index (for URL)
            galleryUID: galleryElement.getAttribute('data-pswp-uid'),

            getThumbBoundsFn: function(index) {
                // See Options -> getThumbBoundsFn section of documentation for more info
                var thumbnail = items[index].el.getElementsByTagName('img')[0], // find thumbnail
                    pageYScroll = window.pageYOffset || document.documentElement.scrollTop,
                    rect = thumbnail.getBoundingClientRect(); 

                return {x:rect.left, y:rect.top + pageYScroll, w:rect.width};
            }

        };

        // PhotoSwipe opened from URL
        if(fromURL) {
            if(options.galleryPIDs) {
                // parse real index when custom PIDs are used 
                // http://photoswipe.com/documentation/faq.html#custom-pid-in-url
                for(var j = 0; j < items.length; j++) {
                    if(items[j].pid == index) {
                        options.index = j;
                        break;
                    }
                }
            } else {
                // in URL indexes start from 1
                options.index = parseInt(index, 10) - 1;
            }
        } else {
            options.index = parseInt(index, 10);
        }

        // exit if index not found
        if( isNaN(options.index) ) {
            return;
        }

        if(disableAnimation) {
            options.showAnimationDuration = 0;
        }

        // Pass data to PhotoSwipe and initialize it
        gallery = new PhotoSwipe( pswpElement, PhotoSwipeUI_Default, items, options);
        gallery.init();
    };

    // loop through all gallery elements and bind events
    var galleryElements = document.querySelectorAll( gallerySelector );

    for(var i = 0, l = galleryElements.length; i < l; i++) {
        galleryElements[i].setAttribute('data-pswp-uid', i+1);
        galleryElements[i].onclick = onThumbnailsClick;
    }

    // Parse URL and open gallery if it contains #&pid=3&gid=1
    var hashData = photoswipeParseHash();
    if(hashData.pid && hashData.gid) {
        openPhotoSwipe( hashData.pid ,  galleryElements[ hashData.gid - 1 ], true, true );
    }
};
```


### Umístění Photoswipe JS skriptů v patičce stránek

Abychom mohli Photoswipe použít na webu, je třeba do patičky všech stránek umístit
inicializační kód knihovny, který najdete níže ve snippetu. Tento kód umístěte do vhodného
shortcode, tedy např. `footer.html`. V případě šablony Airspace Hugo jej najdete v
adresáři `themes/airspace/hugo/layouts/partials/footer.html`.


```html
<!-- PHOTOSWIPE -->

{{- if .HasShortcode "gallery" -}}
  <!-- Root element of PhotoSwipe. Must have class pswp. -->
  <div class="pswp" tabindex="-1" role="dialog" aria-hidden="true">
  <!-- Background of PhotoSwipe.
     It's a separate element, as animating opacity is faster than rgba(). -->
  <div class="pswp__bg"></div>
  <!-- Slides wrapper with overflow:hidden. -->
  <div class="pswp__scroll-wrap">
    <!-- Container that holds slides.
      PhotoSwipe keeps only 3 of them in DOM to save memory.
      Don't modify these 3 pswp__item elements, data is added later on. -->
    <div class="pswp__container">
      <div class="pswp__item"></div>
      <div class="pswp__item"></div>
      <div class="pswp__item"></div>
    </div>
    <!-- Default (PhotoSwipeUI_Default) interface on top of sliding area. Can be changed. -->
    <div class="pswp__ui pswp__ui--hidden">
    <div class="pswp__top-bar">
      <!--  Controls are self-explanatory. Order can be changed. -->
      <div class="pswp__counter"></div>
      <button class="pswp__button pswp__button--close" title="Close (Esc)"></button>
      <button class="pswp__button pswp__button--share" title="Share"></button>
      <button class="pswp__button pswp__button--fs" title="Toggle fullscreen"></button>
      <button class="pswp__button pswp__button--zoom" title="Zoom in/out"></button>
      <!-- Preloader demo http://codepen.io/dimsemenov/pen/yyBWoR -->
      <!-- element will get class pswp__preloader--active when preloader is running -->
      <div class="pswp__preloader">
      <div class="pswp__preloader__icn">
        <div class="pswp__preloader__cut">
        <div class="pswp__preloader__donut"></div>
        </div>
      </div>
      </div>
    </div>
    <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
      <div class="pswp__share-tooltip"></div>
    </div>
    <button class="pswp__button pswp__button--arrow--left" title="Previous (arrow left)">
    </button>
    <button class="pswp__button pswp__button--arrow--right" title="Next (arrow right)">
    </button>
    <div class="pswp__caption">
      <div class="pswp__caption__center"></div>
    </div>
    </div>
    </div>
  </div>
  <link rel="stylesheet" href="/plugins/photoswipe/photoswipe.css">
  <link rel="stylesheet" href="/plugins/photoswipe/default-skin/default-skin.css">

  <script src="/plugins/photoswipe/photoswipe.min.js"></script>
  <script src="/plugins/photoswipe/photoswipe-ui-default.min.js"></script>
  <script src="/plugins/photoswipe/initphotoswipe.js"></script>
  <script>initPhotoSwipeFromDOM('.gallery');</script>


<!-- PHOTOSWIPE style -->
<style>
.gallery{
  width: 100%;
  display: block;
  margin:0 auto;
}

/* Extra Small Devices, Phones */ 
@media only screen and (min-width : 480px) {
  .gallery {
    column-count: 1;
    column-gap: 3px;
  }
}
/* Small Devices, Tablets */
@media only screen and (min-width : 768px) {
  .gallery {
    column-count: 3;
    column-gap: 3px;
  }
}

/* Medium Devices, Desktops */
@media only screen and (min-width : 992px) {
  .gallery { /* Masonry container */
      column-count: 3;
      column-gap: 0px;
  }
}

/* Large Devices, Wide Screens */ 
@media only screen and (min-width : 1200px) {
  .gallery{
    column-count: 3;
    column-gap: 3px;
    width: 100%;
  }
}


.gallery-item { /* Masonry bricks or child elements */
    background-color: #eee;
    display: inline-block;
    /* margin: 0 0 0.2rem; */
    margin: 0.2rem;
    width: auto;
}
</style>
{{- end -}}

```


### Vložení obrázků na stránku

Pokud chceme na generovanou stránku vložit obrázkovou galerii, musíme nastavit
tzv. front-matter dokumentu a to zhruba následovně:

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

Nakonec obrázkovou galerii umístíme na požadované místo ve stránce a to tak, že do kódu
stránky uvedeme následující snippet:

```html
{{ < gallery folder="img" title="Galerie obrázků" > }}
```

A to je vše... Veškeré ukázky kód a popis najdete na mnoha místech na webu, není to žádná věda.

