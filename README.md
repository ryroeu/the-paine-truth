# The Paine Truth

An independent editorial journal built with Jekyll and served by GitHub Pages. The site uses a single stylesheet, system fonts, and no JavaScript. The archive, subject index, RSS feed, and sitemap update on publication.

## Publish an essay

1. Open [Pages CMS](https://app.pagescms.org/) and sign in as `ryroeu`. On the first visit, install the Pages CMS GitHub App for **only** `the-paine-truth`. Open the repository on `main`; the editor reads `.pages.yml` automatically.
2. Open **Essays** and create a new entry. Enter a headline, one-sentence standfirst, byline, date, and one or more subjects. Paste Markdown into **Essay and endnotes**. On the first save, Pages CMS generates the filename from the publication date and headline.
3. Once the copy and citations are ready, turn on **Publish to the website** and save. That commit triggers a GitHub Pages rebuild. Check the [deployment](https://github.com/ryroeu/the-paine-truth/actions) and open the new essay from the home page. Reopen an entry to edit it and save again. Keep the filename and publication date stable once published so existing links keep working.

The **Publish to the website** switch controls whether an entry appears on the site. Every commit in this public repository is readable, including unpublished entries and their history. Keep private drafts and source material in a private editor or the ignored local `_drafts/` folder. Paste a private draft into Pages CMS only when it is ready to become public. A future date suppresses a post until a build runs on or after that date; saving it does not schedule a build.

### Markdown and sourcing

The layout supplies the headline. Start section headings with `##` and give inline images descriptive alt text. Insert a note marker such as `[^1]` after the claim it supports and put the definition on its own line near the end of the file. Jekyll collects notes under **Endnotes** and adds links back to the text.

```markdown
A sentence that draws on a source.[^1]

[^1]: Author or institution, *Title*, publication date, and page or section. [Stable source link](https://example.org).
```

The snippet above illustrates the syntax. For an actual source, use a stable primary-document or archive link where available and add enough detail for a reader to find the passage. [Article front matter template](docs/essay-template.md).

### Write directly in Markdown

Use the template above and save to `_posts/YYYY-MM-DD-short-slug.md`. Set `published: true` when you commit a ready-to-publish essay to `main`. Add new subjects to both `_data/subjects.yml` and `.pages.yml` to make them available in site navigation and the editor.

## Local preview

Use Ruby 3.3 with Bundler, matching [GitHub Pages’ Jekyll environment](https://pages.github.com/versions/).

```sh
bundle install
bundle exec jekyll serve --baseurl ''
```

Open [http://localhost:4000](http://localhost:4000). Add `--drafts --unpublished` for a local preview of `_drafts/` and entries marked `published: false`. Leave those flags out for a public-build preview.

## Hosting and DNS

[Repository Pages settings](https://github.com/ryroeu/the-paine-truth/settings/pages) should publish from **Deploy from a branch**, `main`, `/ (root)`. The canonical origin in `_config.yml` is `https://thepainetruth.com`. GitHub supplies the base path from its Pages configuration.

Use `thepainetruth.com` as the custom domain. GitHub’s [account Pages settings](https://github.com/settings/pages) can verify ownership with a TXT record in Route 53. Keep that TXT record after verification. Attach the custom domain to the repository before pointing web traffic at it.

| Route 53 record name | Type | Values |
| --- | --- | --- |
| Leave blank (zone apex) | A | 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 |
| www | CNAME | ryroeu.github.io. |

Use one A record with four values and one CNAME. The `www` address redirects to the apex once GitHub has provisioned both names. Enable **Enforce HTTPS** under repository Pages settings after the certificate is ready. [GitHub Pages custom domain guide](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

GitHub Pages is free for this public repository. The AWS domain renewal and Route 53 DNS charges are billed separately.
