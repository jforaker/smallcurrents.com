# Small Currents

Static Astro + TypeScript homepage, reproduced from the Fable “Flow (Paper)” HTML export. Plain CSS; no client JavaScript. The current-line SVG in `public/assets/` is copied byte for byte from the export. Font families and weights use the export’s Google Fonts stylesheet.

## Develop and build

Use Node.js 22.18.0 (pinned in `.nvmrc` and used by CI). Run `nvm use` if you manage Node with nvm. Corepack uses the Yarn version pinned in `package.json`.

```sh
corepack enable
yarn install --immutable
yarn dev
yarn build
yarn preview
```

Production files are generated in `dist/`. `public/CNAME` is copied into that output.

## GitHub Pages

Repository: `jforaker/smallcurrents.com`.

1. In **Settings → Pages → Build and deployment**, select **GitHub Actions** as the source.
2. Push to `main` (or run **Deploy to GitHub Pages** manually). The workflow builds with the lockfile and publishes `dist/` using GitHub’s Pages artifact deployment.
3. In **Settings → Pages → Custom domain**, enter `smallcurrents.com` and save **before changing DNS**. With Actions deployments, the repository’s CNAME file alone does not configure this setting.
4. After DNS resolves and GitHub issues the certificate, enable **Enforce HTTPS**.

DNS has not been changed. Until the custom domain is pointed at GitHub, the site may not be reachable at its intended URL.

## Squarespace DNS (configure later)

In the domain’s **DNS → DNS Settings → Custom records**, add these records. Use the default TTL (or 1 hour).

| Host | Type | Data |
| --- | --- | --- |
| `@` | `A` | `185.199.108.153` |
| `@` | `A` | `185.199.109.153` |
| `@` | `A` | `185.199.110.153` |
| `@` | `A` | `185.199.111.153` |
| `www` | `CNAME` | `jforaker.github.io` |

Optional IPv6 records (add all four alongside the A records):

| Host | Type | Data |
| --- | --- | --- |
| `@` | `AAAA` | `2606:50c0:8000::153` |
| `@` | `AAAA` | `2606:50c0:8001::153` |
| `@` | `AAAA` | `2606:50c0:8002::153` |
| `@` | `AAAA` | `2606:50c0:8003::153` |

Replace conflicting Squarespace website/parking A or AAAA records at `@` and any existing `www` CNAME. Preserve email MX, SPF, DKIM, DMARC, and other unrelated records. The `www` target must not include the repository name. GitHub redirects `www` to the configured apex domain. Allow up to 24 hours for propagation.

Source: [GitHub Pages custom-domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).
