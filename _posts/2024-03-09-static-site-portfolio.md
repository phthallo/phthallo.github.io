---
title: making websites for fun and profit
author: Annabel
date: 2024-03-09 21:47:00 +/-TTTT
categories:
  - general
tags:
  - productivity
image: 
  path: /assets/img/posts/website-failure.png
  alt: Build failure whilst attempting to deploy the website at 12:26am. Oops.
cusp: 
    heading: Wow! A custom panel 
    content: They're sticky - meaning they stay on the page as you scroll.

---

Two days ago, I made the spontaneous decision to create a website that was 1. functional and 2. relatively nice looking? [^1] 
Front-end development isn't my strong suit I settled on the [Chirpy theme](https://github.com/cotes2020/jekyll-theme-chirpy) for Jekyll. 

[Jekyll](https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers) is a static-site generator written in the programming language Ruby. It's suitable for blogs, but


# Modifications
Originally, I opted to use the Chirpy starter template then built on top of that to customise the site to what I needed. 

## Custom Panels

```html
{% raw %}
  <section id="custom-panel" class = "cusp">
    <h2 class="panel-heading">{{page.cusp.heading}}</h2>
    <ul class="content list-unstyled ps-0 pb-1 ms-1 mt-2">
      {{page.cusp.content}}
    </ul>
  </section>
{% endraw %}
```

```css
.cusp {
        padding-left: 0rem !important;
        border-left: 0px !important;
        padding-top: 1rem;
        border-top: 1px solid var(--main-border-color);
        border-bottom: 1px solid var(--main-border-color);
}
```

```html
{% raw %}
<aside aria-label="Panel" id="panel-wrapper" class="col-xl-3 ps-2 mb-5 text-muted">
  <div class = "access">
  <!-- default panel content -->
  {% include_cached update-list.html lang=lang %}
  {% include_cached trending-tags.html lang=lang %}
</div>
  <div class = "access toc">
  <!-- custom panel content -->
  {% for _include in layout.panel_includes %}
      {% assign _include_path = _include | append: '.html' %}
      {% include {{ _include_path }} lang=lang %}
  {% endfor %}
  </div>
  </aside>
{% endraw %}
```


## The Lorem Ipsum (tm)
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus sit amet nulla ut nibh interdum tincidunt. Etiam imperdiet tincidunt risus, et sagittis lectus semper vel. Suspendisse potenti. Phasellus eros nisl, posuere id bibendum porta, vestibulum vel lorem. Quisque tempus condimentum elit eget elementum. Integer faucibus, mi ut consectetur vulputate, nisl est tempus lorem, et consequat erat nisi vel nibh. Ut posuere magna ex, at hendrerit diam malesuada a. Nulla accumsan, enim id rutrum ullamcorper, lacus nulla malesuada orci, sed gravida libero velit vel eros. Morbi consectetur urna a nibh luctus, et consequat leo consectetur. Phasellus blandit leo et nibh dignissim vestibulum. Nunc tristique lobortis odio pharetra viverra. Praesent sit amet libero massa. Aenean luctus id arcu sed posuere. Praesent id mauris nec purus finibus elementum eget non mi. Nam mollis, mauris et fringilla faucibus, libero nulla venenatis urna, quis imperdiet neque risus ac purus.

Nam orci velit, hendrerit et hendrerit non, accumsan nec ante. Nullam ut lobortis justo. Ut porta facilisis efficitur. Sed eu dictum tortor. Nullam sed lacinia mi. Nulla eu cursus risus, eget malesuada felis. Nam auctor tortor ut quam facilisis elementum. Nam ultrices turpis non sapien congue venenatis. Sed maximus ornare neque ac consectetur.

Sed sed mi fringilla lorem tincidunt pulvinar at eu nunc. Duis consectetur diam ut nisl dapibus, nec ornare tortor faucibus. Aenean tristique, lorem et eleifend rhoncus, nisl augue hendrerit urna, ut volutpat ex metus sit amet est. Proin et velit nec nulla varius convallis. Pellentesque facilisis, orci sit amet feugiat porttitor, nulla neque commodo metus, sit amet viverra purus risus non urna. Phasellus gravida, erat in tempus porttitor, nisl magna tincidunt ipsum, sit amet tempor est massa at ligula. Vestibulum id turpis luctus, pretium lorem ut, lobortis nisl. Sed ipsum velit, mollis sed quam eget, euismod efficitur ipsum. Nullam dapibus tempus sem, in tincidunt ex porttitor et. In at molestie risus, ut congue libero. Etiam ultricies et dolor a imperdiet. Aenean luctus ante quis lorem egestas consequat. Donec quis viverra magna, sed venenatis nisl.

Pellentesque id magna faucibus, feugiat nulla vel, ultrices felis. Maecenas egestas libero ut egestas accumsan. Cras eget mauris venenatis, porta dui nec, consequat metus. Cras venenatis risus sit amet sodales ultricies. Nulla sit amet eros tempus, finibus lacus vel, ornare risus. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Praesent molestie nisl mi, in ultrices elit euismod sed. Fusce mattis orci in mattis faucibus. Praesent vel accumsan lectus. Suspendisse nec urna magna. Suspendisse eu est pellentesque lorem dignissim auctor.

Pellentesque volutpat erat et enim ullamcorper, vel faucibus augue molestie. Vestibulum blandit non lorem eu varius. Maecenas facilisis diam tortor, nec accumsan orci tincidunt in. Quisque at arcu non sem sollicitudin convallis a quis ipsum. Donec non convallis ante. Sed in mollis eros, ut gravida dui. Nam ut diam dolor. Sed ornare diam non arcu dignissim varius. Maecenas et tellus tortor. In hendrerit eu ante a tincidunt. Interdum et malesuada fames ac ante ipsum primis in faucibus. Ut consectetur, ligula vitae tincidunt mollis, purus magna rhoncus sapien, nec placerat elit diam nec neque. Donec nec velit sed sapien scelerisque gravida. Nulla malesuada, nunc eget tincidunt vehicula, nulla ante rutrum felis, a sollicitudin eros urna vel ipsum. Donec eu scelerisque ante.




[^1]: I tried it about a [about a year ago](https://github.com/phthallo/studio). It fulfilled maybe one of the criteria. 