---
layout: info
icon: fa-solid fa-bars-progress
order: 3
toc: true
cusp: 
    heading: Projects
    content: These are various projects that I've developed across the past few years, sorted chronologically (newest to oldest!).<br>For more, see my <a href = "https://github.com/phthallo/">GitHub</a> profile.
---

>  SACE Thrive
> - Self motivated learning (operating with self direction, working through challenges, demonstrating initiative)
> - Quality thinking (being creative, taking opportunities, activating curiosity)
{: .prompt-tip }

{% assign projects = site.data.projects %}
<div id="project-post-list" class = "px-xl-1">
{% for project in projects %}
<article class="card-wrapper card">
<div class="project-preview col-md-12 row g-0 flex-md-row-reverse">
    <a href = "{{ project[1].blog }}"><img style = "display: cover" src="/assets/img/projects/project-{{ project[1].img }}" alt="{{ project[1].alt }}"></a>
    <div class="card-body d-flex flex-column">
        <a href = "{{ project[1].blog }}" class = "project-links">
            <h1 class="card-title my-2 mt-md-0">
                <span data-bs-toggle="tooltip" data-bs-placement="right" data-bs-original-title="{{ project[1].tooltip }}">
                {{ project[1].title }}
                </span>
            </h1>
        </a>
            <div class="card-text content mt-0 mb-3">
                <p>{{ project[1].content }}</p>
            </div>
        <div class="post-meta align-items-end">
            <div class="me-auto">
                <i class="far fa-calendar fa-fw me-1"></i>
                <time>{{ project[1].date }}</time> 
                <i class="fa-solid fa-tag fa-fw me-1"></i> 
                <span class="categories">
                {% for tag in project[1].tag %}
                    <a href = "/tags/{{ tag }}">{{ tag }}</a>
                    {% unless forloop.last %},{% endunless %}
                {% endfor %}
                </span>
                <i class="fa-solid fa-code-branch fa-fw me-1"></i> 
                        <a href = "{{ project[1].repo }}">repo</a>
            </div>
        </div>
    </div>
</div>
</article>
{% endfor %}
</div>

