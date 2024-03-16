---
title: making websites for fun and profit
author: Annabel
date: 2024-03-09 21:47:00 +/-TTTT
categories:
  - showcase
tags:
  - webdev
image: 
  path: /assets/img/posts/website-failure.png
  alt: Build failure whilst attempting to deploy the website at 12:26am. Oops.
cusp: 
    heading: Wow! A custom panel 
    content: They're sticky - meaning they stay on the page as you scroll. <br> P.S You can only see me on desktop :P 
---
> SACE Thrive Capabilities
> - Being Intentional
> - Managing Projects
> - Designing with Purpose
> - Operating with Self-Direction
{: .prompt-tip }


Two days ago, I made the spontaneous decision to create a website that was 1. functional and 2. relatively nice looking? [^1] 
Front-end development isn't my strong suit, so I settled on using pre-made themes - in particular, the [Chirpy theme](https://github.com/cotes2020/jekyll-theme-chirpy) for Jekyll. 

[Jekyll](https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers) is an open-source static-site generator written in the programming language Ruby. While it's intended for blogs, it 'builds' and styles each page using HTML and CSS. Unlike no-code site builders (some that come to mind are [Carrd](https://carrd.co) and [Squarespace](https://squarespace.com)) users can freely edit exactly what appears on their website. This means there's a nigh-infinite amount of customisation that can be done. 


## Glossary

| Term | Definition | Example | 
| ---- | ---------- | ------- |
| Open source | Software which has its source code freely available to be modified and distributed at will.<br>This actively encourages derivations and improvements on existing projects, even if the original contributors are no longer active. | This project! |
| HTML | HyperText Markup Language, and how website content in browsers is displayed. |  `<a href = "https://phthallo.github.io">website</a>` renders as <a href = "https://phthallo.github.io">website</a> | 
| CSS | Cascading Style Sheets. Used to style HTML elements (changing size, colour etc) | |

## Building a Portfolio...
Even as a student, I'm aware of the need to develop a strong portfolio when applying to internships and jobs. It's not just a portfolio of your projects that showcase your programming skills, though - your communication skills count for the same, if not more. 

### ...isn't as straightforward as it seems.
![This webpage, open as a Markdown file in the VScode environment](assets/img/posts/website-dev.png)
Setting up the development environment requires one to take initiative; to **operate with self-direction**. It's in the nature of programming to be very hands-on, and I've found I learn best by doing. 

Some facts: 
- This website is hosted on [GitHub Pages](https://pages.github.com/). I can also run it on my computer and preview the content in my browser before I deploy my changes to the actual website. This is known as the local development environment.
- Setting up the development environment requires installation of the **Ruby programming language, Ruby's package installer, the GCC Compiler and the Make software.** This is what's used to install the tools needed to use Jekyll locally.
- Jekyll isn't actually officially supported on Windows 10, and neither is GCC and Make. This is as  most tools are built for Linux and its various distributions (the predominant operating system in the software field). Luckily, I had them previously installed on my system from another project[^2].
- I also use **Git**, an industry-standard version control system to track and record the changes I make to files. I use this to 'push' my changes to GitHub, where the repository for this website is stored. GitHub then builds and deploys it to the [phthallo.github.io](https://phthallo.github.io) domain (as seen in the first image of this post![^3])

## Making modifications
I chose to personalise portions of this site to demonstrate my own technical ability, as well as to portray more of myself to potential employers/other people reviewing my website as an example of **designing with purpose**.


### Custom Panels
For instance, I chose to add custom panels (an example of which can be seen on this page, if you're reading this on desktop!) These panels can accompany any page and display additional custom information. 

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
### Projects Tab
Additionally, I also decided that being able to display all my projects in one page would provide a concise summary of the work that I've done so far, which could then be expanded on in a blog post like this one. 



### Theme



## The Lorem Ipsum (tm)
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus sit amet nulla ut nibh interdum tincidunt. Etiam imperdiet tincidunt risus, et sagittis lectus semper vel. Suspendisse potenti. Phasellus eros nisl, posuere id bibendum porta, vestibulum vel lorem. Quisque tempus condimentum elit eget elementum. Integer faucibus, mi ut consectetur vulputate, nisl est tempus lorem, et consequat erat nisi vel nibh. Ut posuere magna ex, at hendrerit diam malesuada a. Nulla accumsan, enim id rutrum ullamcorper, lacus nulla malesuada orci, sed gravida libero velit vel eros. Morbi consectetur urna a nibh luctus, et consequat leo consectetur. Phasellus blandit leo et nibh dignissim vestibulum. Nunc tristique lobortis odio pharetra viverra. Praesent sit amet libero massa. Aenean luctus id arcu sed posuere. Praesent id mauris nec purus finibus elementum eget non mi. Nam mollis, mauris et fringilla faucibus, libero nulla venenatis urna, quis imperdiet neque risus ac purus.

Nam orci velit, hendrerit et hendrerit non, accumsan nec ante. Nullam ut lobortis justo. Ut porta facilisis efficitur. Sed eu dictum tortor. Nullam sed lacinia mi. Nulla eu cursus risus, eget malesuada felis. Nam auctor tortor ut quam facilisis elementum. Nam ultrices turpis non sapien congue venenatis. Sed maximus ornare neque ac consectetur.

Sed sed mi fringilla lorem tincidunt pulvinar at eu nunc. Duis consectetur diam ut nisl dapibus, nec ornare tortor faucibus. Aenean tristique, lorem et eleifend rhoncus, nisl augue hendrerit urna, ut volutpat ex metus sit amet est. Proin et velit nec nulla varius convallis. Pellentesque facilisis, orci sit amet feugiat porttitor, nulla neque commodo metus, sit amet viverra purus risus non urna. Phasellus gravida, erat in tempus porttitor, nisl magna tincidunt ipsum, sit amet tempor est massa at ligula. Vestibulum id turpis luctus, pretium lorem ut, lobortis nisl. Sed ipsum velit, mollis sed quam eget, euismod efficitur ipsum. Nullam dapibus tempus sem, in tincidunt ex porttitor et. In at molestie risus, ut congue libero. Etiam ultricies et dolor a imperdiet. Aenean luctus ante quis lorem egestas consequat. Donec quis viverra magna, sed venenatis nisl.

Pellentesque id magna faucibus, feugiat nulla vel, ultrices felis. Maecenas egestas libero ut egestas accumsan. Cras eget mauris venenatis, porta dui nec, consequat metus. Cras venenatis risus sit amet sodales ultricies. Nulla sit amet eros tempus, finibus lacus vel, ornare risus. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Praesent molestie nisl mi, in ultrices elit euismod sed. Fusce mattis orci in mattis faucibus. Praesent vel accumsan lectus. Suspendisse nec urna magna. Suspendisse eu est pellentesque lorem dignissim auctor.

Pellentesque volutpat erat et enim ullamcorper, vel faucibus augue molestie. Vestibulum blandit non lorem eu varius. Maecenas facilisis diam tortor, nec accumsan orci tincidunt in. Quisque at arcu non sem sollicitudin convallis a quis ipsum. Donec non convallis ante. Sed in mollis eros, ut gravida dui. Nam ut diam dolor. Sed ornare diam non arcu dignissim varius. Maecenas et tellus tortor. In hendrerit eu ante a tincidunt. Interdum et malesuada fames ac ante ipsum primis in faucibus. Ut consectetur, ligula vitae tincidunt mollis, purus magna rhoncus sapien, nec placerat elit diam nec neque. Donec nec velit sed sapien scelerisque gravida. Nulla malesuada, nunc eget tincidunt vehicula, nulla ante rutrum felis, a sollicitudin eros urna vel ipsum. Donec eu scelerisque ante.




[^1]: I tried it about a [about a year ago](https://github.com/phthallo/studio). It fulfilled maybe one of the criteria. 
[^2]: Gotta love [msys2](https://www.msys2.org/).
[^3]: The build failed here because I forgot to add alt text to my photos, which is essential towards increasing the accessibility of my website. 