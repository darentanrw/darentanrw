# Jinchao Li's Homepage

TODO:

- [ ] change sidebar to topbar, social icons to footer, then remove sidebar
- [ ] card style for listing images with texts (left-right in PC, top-bottom in mobile)
- [ ] encrypt some posts

## Build

1. Install [Node.js][nodejs] and [Ruby Gem][ruby], then run:

    ```sh
    gem install --user-install bundler jekyll
    ```

2. Install the dependencies:

    ```sh
    # rm -rf node_modules && jekyll clean  # clean
    npm i && npm run build  # build js assets
    bundle  # install jekyll packages
    ```

3. Local preview:

    ```sh
    bundle exec jekyll s  # visit http://localhost:4000/
    ```

4. Test

    ```sh
    bundle exec htmlproofer _site --disable-external --check-html --allow_hash_href
    ```

## Deploy

- To deploy in [Github Pages][github_pages]:

  - Fork or upload the repository to Github
  - `Settings` > `Pages` > select the `Branch` to `main` or your branch

- To deploy in [Vercel][vercel], add new project, import the repository, then configure with:

  - `Framework Preset`: `Jekyll`
  - `Build and Output Settings` > OVERRIDE `Build Command`:

    ```sh
    npm i && npm run build && JEKYLL_ENV=production bundle exec jekyll b -d "_site"
    ```

## Credits

Powered by [Chirpy Jekyll Theme][chirpy], a minimal, responsive and feature-rich Jekyll theme for technical writing.

This theme is mainly built with [Jekyll][jekyllrb] ecosystem,
[Bootstrap][bootstrap], [Font Awesome][icons] and some other [wonderful tools][lib].

<details>
  <summary>
    <i>Click to view features</i>
  </summary>
  <p>

- Dark / Light Theme Mode
- Localized UI language
- Pinned Posts
- Hierarchical Categories
- Trending Tags
- Table of Contents
- Last Modified Date of Posts
- Syntax Highlighting
- Mathematical Expressions
- Mermaid Diagram & Flowchart
- Dark / Light Mode Images
- Embed Videos
- Disqus / Utterances / Giscus Comments
- Search
- Atom Feeds
- Google Analytics
- SEO & Performance Optimization

  </p>

</details>

[nodejs]: https://nodejs.org/
[ruby]: https://jekyllrb.com/docs/installation/
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/wiki/
[jekyllrb]: https://jekyllrb.com/
[bootstrap]: https://getbootstrap.com/
[icons]: https://fontawesome.com/
[lib]: https://github.com/cotes2020/chirpy-static-assets/
[github_pages]: https://pages.github.com/
[vercel]: https://vercel.com/