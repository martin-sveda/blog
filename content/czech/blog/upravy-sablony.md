---
title: "Úpravy šablony v tomto webu"
date: 2020-10-11T11:07:10+06:00
author: Martin Sveda
image : "images/blog/blog-post-2.jpg"
bg_image: "images/featue-bg.jpg"
categories: ["Programování"]
tags: ["Hugo"]
description: "Shrnutí úprav šablony"
draft: false
type: "post"
---

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quas officiis cumque, harum dicta necessitatibus
reprehenderit, delectus molestiae, impedit alias adipisci distinctio voluptas. Tempora modi amet voluptate
at provident soluta consequatur.

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores quibusdam sed, neque recusandae, est
odit. A facere tempore soluta laborum.


Byly provedeny následující úpravy:

## Tlačítko v hero obrázku hlavní stránky

Originální definice:

``` html
/airspace-hugo/layouts/index.html

<!-- banner -->
{{ if $data.homepage.banner.enable }}
{{ with $data.homepage.banner }}
<section class="slider {{if .bg_overlay}}overly{{end}}" style="background-image: url('{{ .bg_image | absURL }}');">
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="block">
          <h1>{{ .title | markdownify }}</h1>
          <p>{{ .content | markdownify }}</p>
          {{ if .button.enable }}
          {{ with .button }}
          <a href="{{ .link | relLangURL }}" target="_blank" class="btn btn-main animated fadeInUp">{{ .label }}</a>
          {{ end }}
          {{ end }}
        </div>
      </div>
    </div>
  </div>
</section>
{{ end }}
{{ end }}
<!-- /banner -->
```

Nová definice:

``` html
/airspace-hugo/layouts/index.html

<!-- banner -->
{{ if $data.homepage.banner.enable }}
{{ with $data.homepage.banner }}
<section class="slider {{if .bg_overlay}}overly{{end}}" style="background-image: url('{{ .bg_image | absURL }}');">
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="block">
          <h1>{{ .title | markdownify }}</h1>
          <p>{{ .content | markdownify }}</p>
          {{ if .button.enable }}
          {{ with .button }}
          <a href="{{ .link | relLangURL }}" class="btn btn-main animated fadeInUp">{{ .label }}</a>
          {{ end }}
          {{ end }}
        </div>
      </div>
    </div>
  </div>
</section>
{{ end }}
{{ end }}
<!-- /banner -->
```


## Barva tlačítka

Původní definice

``` css
.feature {
	background: url("../img/featue-bg.jpg");
	background-position: 50% 94px;
	display: block;
	position: relative;
	background-attachment: fixed;
	background-repeat: no-repeat;
	background-position: center center;
	background-size: cover;
	padding: 100px 0;

	h2 {
		margin-bottom: 30px;
	}

	p {
		color: #8d8f92;
		margin-bottom: 20px;
	}

	.btn-view-works {
		background: $secondary-color;
		color: #fff;
		padding: 10px 20px;
	}
}

```

Nová definice:

``` css
.feature {
	background: url("../img/featue-bg.jpg");
	background-position: 50% 94px;
	display: block;
	position: relative;
	background-attachment: fixed;
	background-repeat: no-repeat;
	background-position: center center;
	background-size: cover;
	padding: 100px 0;

	h2 {
		margin-bottom: 30px;
	}

	p {
		color: #8d8f92;
		margin-bottom: 20px;
	}

	.btn-view-works {
		background: $secondary-color; /* Change !!! */
		color: #fff;
		padding: 10px 20px;
	}
}

```


## Page Title

Soubor `page-title.html` byl přepsán.

