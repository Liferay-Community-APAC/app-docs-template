# App docs template

A starting point for an app's documentation, published from its own repository at
`https://liferay-community-apac.github.io/<repository-name>/`. The docs share the main site's
header, footer, styles and search, so readers move between the site and every app's docs as if
it were one site.

## What's here

| Path | What it is |
| --- | --- |
| `docs/_config.yml` | The docs' settings: the app's name, description, address and licence line. |
| `docs/_layouts/default.html` | The page layout: sidebar, breadcrumbs, previous and next links, and the shared header, footer and search. Improve it here, then copy it into each app's docs. |
| `docs/index.md`, `docs/guide/` | Example pages. Replace them with the app's docs. |
| `.github/workflows/pages.yml` | Publishes the docs with the shared workflow whenever `docs/` changes on `main`. |

## Add docs to an app

1. **Start the docs repository from this template**: click **Use this template → Create a new repository**, in the Liferay-Community-APAC organization, and make it public. Name it after the app (for example `liferay-forums`): the name becomes the docs' address, `/<repository-name>/` on the main site's address, so never use the name of one of the main site's own folders (such as `marketplace-apps`, `tutorials`, `community`, `resources`, `get-help`, `ja`, `zh` or `id`), or the repository hides that page. For an app without a code repository of its own, add a folder to the shared [marketplace-app-docs](https://github.com/Liferay-Community-APAC/marketplace-app-docs) repository instead. To add docs to an existing app repository instead, copy `docs/` and `.github/workflows/pages.yml` into it.
2. **Edit the four marked lines in `docs/_config.yml`**: `app_name`, `description`, `baseurl` (`/` and the repository's name) and `footer_note`.
3. **Write the docs in Markdown** in `docs/`. Each page starts with front matter:

    ```yaml
    ---
    title: Installing        # the page's name in the sidebar
    parent: Guide            # the section it belongs to (leave out for a section or top page)
    nav_order: 1             # its position, lower first
    ---
    ```

    Pages can use a table of contents (`1. TOC` then `{:toc}` on the next line), callouts
    (`{: .note }`, `{: .tip }`, `{: .important }` or `{: .warning }` on the line before a paragraph),
    and screenshots (`{: .screenshot }` after an image).
4. **Turn on publishing**: in the repository's **Settings → Pages**, set **Source** to **GitHub Actions**. The repository must be public.
5. **Add the app to the main site**: add an entry to `data/apps.json` in
   [liferay-community-apac.github.io](https://github.com/Liferay-Community-APAC/liferay-community-apac.github.io),
   with `"docs": "<repository-name>/"`, `"search": "<repository-name>/pagefind/"` and
   `"sitemap": "<repository-name>/sitemap.xml"`. That adds it to the homepages and the Marketplace Apps pages,
   includes its pages in the site search, and tells search engines about its sitemap.

## Preview locally

The docs load the header, footer and styles from the main site. To preview them on their own,
set `main_site: https://liferay-community-apac.github.io` in `docs/_config.yml` (don't commit it), then:

```bash
cd docs && jekyll serve --baseurl /my-app
```

Search only works on the published site, where the search index is built.
