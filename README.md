# MyBlog

Public repository so I can post design philosophy on my projects.

This is a Jekyll site for a GitHub Pages project site. The repository is `rsiena/MyBlog`, so the site base URL is `/MyBlog`. There is no custom domain.

## Local build

GitHub documents Ruby 3.1 for the `github-pages` gem. From the repository root:

```bash
bundle install
JEKYLL_ENV=production bundle exec jekyll build
```

Preview on localhost without the `/MyBlog` prefix:

```bash
bundle exec jekyll serve --baseurl ""
```

Ruby 3 does not ship `webrick`. If `jekyll serve` cannot find it, run `bundle add webrick` locally. Do not commit that gem: the GitHub Pages builder does not need it, and an extra dependency makes `bundle check` warn during the branch build.

The committed Gemfile pins `github-pages` 232, which currently provides Jekyll 3.10.0. Check [pages.github.com/versions.json](https://pages.github.com/versions.json) before changing the pin.

## Publish with GitHub Pages

Pages is not turned on in this repository yet. After this change is on `main`, an admin turns it on. Do not enter a custom domain.

In the repository:

1. Open **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Set the branch to **main** and the folder to **/ (root)**.
4. Save.

This repository does not include a GitHub Actions workflow. Do not set the source to **GitHub Actions**. GitHub's built-in Jekyll build is the publishing source for this site. Saving the setting needs admin access to the repository. GitHub also requires that an admin with a verified email address has pushed to the publishing branch.

No workflow permissions are required. There is no `pages: write` or `id-token: write` grant in this repository.

The addresses below are the ones that build will publish. They are not live until Pages is enabled and that build succeeds.

- https://rsiena.github.io/MyBlog/
- https://rsiena.github.io/MyBlog/2026/11/08/the-specification-comes-first/

The post file is `_posts/2026-11-08-The-specification-comes-first.md`. Its front matter sets that permalink directly.
