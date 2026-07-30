# Yuxin Wang Academic Website

This repository contains the bilingual Hugo academic website for Yuxin Wang.

## Run locally on macOS

Install the prerequisites:

```bash
brew install hugo git go
```

Hugo must be the Extended edition. Confirm with:

```bash
hugo version
```

From this repository, start the local site:

```bash
hugo server
```

Open `http://localhost:1313/` for English or `http://localhost:1313/zh/` for Chinese.

## Deploy to GitHub Pages

The initial deployment uses the default address:

`https://yuxinwang-econ.github.io/`

1. Create the public repository `YuxinWang-econ/YuxinWang-econ.github.io` if it does not already exist.
2. Push this source to the repository's `main` branch.
3. In GitHub, open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **GitHub Actions**.
5. Leave **Custom domain** empty during the initial deployment.
6. Run the **Deploy website to GitHub Pages** workflow, or push a commit to `main`.

The workflow uses the base URL supplied by GitHub Pages, builds the Hugo site, and publishes the generated `public` directory. Verify the English and Chinese pages at the default address before beginning custom-domain work.

## Configure the custom domain later

Do not perform these steps until the default GitHub Pages deployment has been verified.

First add and verify `yuxinwang-econ.com` in the repository's **Settings → Pages** section. Then configure Cloudflare DNS.

In Cloudflare, remove conflicting default records and add these DNS records:

| Type | Name | Content | Proxy status |
|---|---|---|---|
| A | `@` | `185.199.108.153` | DNS only |
| A | `@` | `185.199.109.153` | DNS only |
| A | `@` | `185.199.110.153` | DNS only |
| A | `@` | `185.199.111.153` | DNS only |
| CNAME | `www` | `YuxinWang-econ.github.io` | DNS only |

Do not add a wildcard DNS record. Keep the records DNS-only while GitHub verifies the domain and provisions its HTTPS certificate. DNS changes can take up to 24 hours to propagate. Once GitHub makes the option available, select **Enforce HTTPS**.

After the custom domain is active, change `baseURL` in `config/_default/hugo.yaml` to `https://yuxinwang-econ.com/`. The deployment workflow can continue using the base URL supplied by GitHub Pages.

## Edit content

All public copy is in Markdown:

- English homepage: `content/_index.en.md`
- Chinese homepage: `content/_index.zh.md`
- Research pages: `content/research.en.md` and `content/research.zh.md`
- CV pages: `content/cv.en.md` and `content/cv.zh.md`
- Contact pages: `content/contact.en.md` and `content/contact.zh.md`

Navigation and language settings are in `config/_default/languages.yaml`. Shared site settings are in `config/_default/hugo.yaml`.

Replace `static/uploads/Yuxin_Wang_CV.pdf` when the CV changes, keeping the filename unchanged so existing links continue to work.

Future sections can be added later as new Markdown files without changing the current navigation until the content is ready.
