# Marketing site

> A marketing website built from every marketing block of the library.

Built with [Sovrium](https://sovrium.com) — a configuration-as-code interpreter: one config
file in, a complete self-hosted web application out.

## Use this template

Click **Use this template** on GitHub to copy this app into your own repository (clean
history, yours to modify), or scaffold it locally:

```bash
curl -fsSL https://sovrium.com/install | sh
sovrium init my-marketing-site --template marketing-site
```

## What's inside

Eleven pages, each a stack of blocks from the Sovrium library — heroes, logo walls, feature
grids, figures, testimonials, pricing tables, FAQs, team, blog lists, a long read with its
outline, contact forms, a newsletter sign-up and two pages for lost visitors. Each file
under [`library/block/`](./library/block) starts with the line naming the block and the
version it came from.

Copy in square brackets — `[Product]`, `[Primary action]` — is a placeholder: replace it
with your own words, and delete the blocks a page does not need. The blog sections read the
`posts` table and the live figures read `orders`; point them at your own tables with
`sovrium library add block/<name> --set table=<yours>`.

The site speaks English and French. Every word that changes with the language is a key in
[`config/languages.yaml`](./config/languages.yaml), and the blocks cite it as `$t:<key>`:
`/en/…` and `/fr/…` serve a page in that language, and the switcher in the header opens the
same page in the other one. The home hero, the pricing page, the headers and the footers
are translated; add a key and its two values to translate the rest.

The contact forms post to the `contact` form in [`config/forms/`](./config/forms), which
writes each message to the `messages` table. Only the owner reads it: sign in at `/login`
with the `AUTH_ADMIN_EMAIL` and `AUTH_ADMIN_PASSWORD` you set, then open the admin. The
newsletter blocks post to the `newsletter` form the same way, into a `subscribers` table.

## Run locally

```bash
curl -fsSL https://sovrium.com/install | sh
cp .env.example .env
sovrium seed app.yaml        # needs SOVRIUM_SEED_PASSWORD in .env
sovrium start app.yaml --watch
```

Zero-config: embedded SQLite, local file storage, no variable required to boot.
[`.env.example`](./.env.example) lists the optional ones this app reads.
The first administrator comes from `AUTH_ADMIN_EMAIL` and `AUTH_ADMIN_PASSWORD` on the
first start, or from `sovrium admin create <email>`.
`--watch` reloads the app each time you save a config file.

## Deploy

Ship it to Sovrium Cloud from this directory: sign in once, then deploy. The CLI finds or
creates the app it deploys to, checks the variables it needs, bundles and uploads it, and
ends only once the app answers at its address.

```bash
sovrium login
sovrium deploy
```

Any other host works the same way: run the `sovrium` binary with this config (see the
[deployment guides](https://sovrium.com/en/docs/installation)).

> **The demo accounts are for trying the app, not for running it.** The seed gives every
> account it creates, the admin included, the one password in `SOVRIUM_SEED_PASSWORD`, and
> their addresses are in `seed/`. Before anyone else can reach the app, choose a long
> password or skip the seed, and change or delete the demo admin.

## About this repository

This repository is **auto-published from the
[Sovrium monorepo](https://github.com/sovrium/sovrium)** on every release
(source: [`src/templates/marketing-site`](https://github.com/sovrium/sovrium/tree/main/src/templates/marketing-site)).
Issues are welcome here; please send code contributions upstream to the monorepo so the
template stays in sync with the engine. The pinned engine release lives in
`.sovrium-version`.

License: [MIT](./LICENSE). The Sovrium engine itself is licensed separately
([BSL 1.1](https://github.com/sovrium/sovrium/blob/main/LICENSE.md)).
