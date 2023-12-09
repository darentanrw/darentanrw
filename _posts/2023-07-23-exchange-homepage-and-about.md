---
title: Exchange Homepage and About
author: jcli
date: 2023-07-23 10:00:00 +0800
categories: [Blogging, Tutorial]
tags: [homepage]
render_with_liquid: false
---

To change the default site homepage as `About`, and the original paginator homepage as `Blog`. It may be difficult since [pagination](https://jekyllrb.com/docs/pagination/) only works within `index.html`, see similar [issue](https://github.com/cotes2020/jekyll-theme-chirpy/issues/711).

1. Modify the front matters with permalink:

    - Create a new folder, e.g. `/projects/`, and move `index.html` inside it.
    - Add `permalink: /` in the front matter of `/_tabs/about.md`.

2. Add `paginate_path` in `/_config.yml` to point to the folder `/projects/`

    ```diff
    + paginate_path: "/projects/page:num/"
    ...
    - permalink: /posts/:title/
    + permalink: /projects/:title/
    ```

3. Add `BLOG` as a new tab or navigation item, refer to this [issue](https://github.com/cotes2020/jekyll-theme-chirpy/issues/855).

    - Modify `/_includes/sidebar.html`

        ```html
        <!-- home -->
        - <li class="nav-item{% if page.layout == 'home' %}{{ " active" }}{% endif %}">
        + <li class="nav-item{% if page.url == '/' | relative_url %}{{ " active" }}{% endif %}">
        <a href="{{ '/' | relative_url }}" class="nav-link">
            <i class="fa-fw fas fa-home"></i>
            <span>{{ site.data.locales[include.lang].tabs.home | upcase }}</span>
        </a>
        </li>
        + <!-- blog -->
        + <li class="nav-item{% if page.url == '/projects/' | relative_url %}{{ " active" }}{% endif %}">
        +   <a href="{{ '/projects/' | relative_url }}" class="nav-link">
        +     <i class="fa-fw fas fa-pen"></i> 
        +     <span>BLOG</span>
        +   </a>
        + </li>
        <!-- the real tabs -->
        {% for tab in site.tabs %}
        +     {% if tab.url == '/' | relative_url %}{% continue %}{% endif %}
        ```

    - Modify `/_includes/topbar.html`

        ```html
        - {% if paths.size == 0 or page.layout == 'home' %}
        -   <!-- index page -->
        + {% if paths.size == 0 %}
        +   <!-- home page -->
        ...
        -           {% elsif page.layout == 'category' or page.layout == 'tag' %}
        +           {% elsif page.layout == 'category' or page.layout == 'tag' or page.layout == 'home' %}
        ```

4. Replace `page.layout == 'home'` with `page.url == '/' or page.url == site.baseurl` if needed, including `_layouts/page.html`, `_includes/head.html`, `/_includes/sidebar.html`, and `_includes/topbar.html`.

5. (Optional) Modify your style in `/_tabs/about.md`. For example, this demo we disable `title`, `post-meta` and `tails` in the homepage by assigning bool values `has_title`, `has_meta` and `has_tail` to skip related part in `_layouts/page.html` and `_layouts/post.html`.
