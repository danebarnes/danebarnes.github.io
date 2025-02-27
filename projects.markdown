---
layout: default
title: Projects
permalink: /projects/
---

<div class="page-content">
  <div class="wrap">
    <header class="intro">
      <h1 id="page-title" class="intro-title">{{ page.title | markdownify | strip_html }}</h1>
    </header>

    <div class="inner">
      <div class="initial-content">
        <div class="posts">
          <ul class="post-list">
            {% for project in site.projects %}
              <li class="post-item">
                <header class="post-header">
                  <span class="post-meta">{{ project.date | date: "%B %d, %Y" }}</span>
                  <h2 class="post-title">
                    <a class="post-link" href="{{ project.url }}">{{ project.title }}</a>
                  </h2>
                </header>
                {% if project.excerpt %}
                <div class="post-excerpt">
                  {{ project.excerpt }}
                </div>
                {% endif %}
              </li>
            {% endfor %}
          </ul>
        </div>
      </div>
    </div>

  </div>
</div>
