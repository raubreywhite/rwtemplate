# pkgdowntemplate

Shared **pkgdown house style** for the rwhite.no R packages — Newsreader + Source
Sans 3 typography, the warm brand-red palette, a light editorial navbar with a
`packages` switcher, and a common footer. Build it once; every site inherits it.

This package only ships theme assets — it is infrastructure, not a user-facing
package.

## Use it in a package

1. Declare `pkgdowntemplate` as a website dependency in the package's
   `DESCRIPTION`, as an **inline GitHub ref** (CI installs `Config/Needs/website`
   entries directly with pak, so a bare package name will *not* resolve):

   ```
   Config/Needs/website: raubreywhite/pkgdowntemplate
   ```

2. Point the package's `_pkgdown.yml` at the template:

   ```yaml
   template:
     package: pkgdowntemplate

   # keep your own url + reference: / articles: groups below
   ```

3. Rebuild: `pkgdown::build_site()`.

That's it — fonts, colours, navbar, and footer all come from here. Per-package
overrides still work: anything you set in your own `_pkgdown.yml` wins.

## Home-page hero

The home page uses a full-width hero band driven by params in the consuming
package's `_pkgdown.yml`:

```yaml
template:
  package: pkgdowntemplate
  params:
    hero:
      overline: "R package · Cohort construction"
      title: "Build cohorts with provenance."
      lede: >
        A short one- or two-sentence pitch. <em>HTML is allowed</em> here.
      cta:
        primary:   { text: "Get started",          href: "articles/cohort.html" }
        secondary: { text: "Browse the reference →", href: "reference/index.html" }
```

Set no `hero:` and the page falls back to pkgdown's normal home. Below the hero,
author "What's inside" cards and an optional gallery in the package's `index.md`:

```markdown
<p class="rw-section">What's inside</p>

<div class="rw-cards">
<div class="rw-card"><div class="rw-card-num">01</div><h3>Title</h3><p>Blurb.</p></div>
<div class="rw-card"><div class="rw-card-num">02</div><h3>Title</h3><p>Blurb.</p></div>
<div class="rw-card"><div class="rw-card-num">03</div><h3>Title</h3><p>Blurb.</p></div>
</div>
```

## What's inside

```
inst/pkgdown/
  _pkgdown.yml              navbar + footer structure, fonts, palette + Bootstrap
                            variable overrides (template > bslib)
  extra.scss                custom CSS rules, added after Bootstrap
  templates/content-home.html   full-width hero + content/sidebar home layout
```

## Editing the look

- **Colours / fonts / Bootstrap variables** → `_pkgdown.yml` (`template > bslib`).
- **Component styling** (hero, code blocks, reference index, footer strip) →
  `extra.scss` (the `$rw-*` tokens are defined at its top).
- **Packages menu / footer links** → `_pkgdown.yml` components.

## Lineage

The component architecture is adapted from
[niphr/cstemplate](https://github.com/niphr/cstemplate) (the cs* family house
style), re-skinned end to end into the rwhite.no brand: warm ink and brand-red
in place of navy/coral, Newsreader + IBM Plex Mono in place of Spectral +
JetBrains Mono, and an `.rw-*` component namespace.
