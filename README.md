### About

Simple CSS Marquee.

[![Build Status](https://img.shields.io/travis/com/AlfredoRamos/simple-marquee.svg?style=flat-square)](https://travis-ci.com/AlfredoRamos/simple-marquee)
[![Latest Stable Version](https://img.shields.io/github/tag/AlfredoRamos/simple-marquee.svg?style=flat-square&label=stable)](https://github.com/AlfredoRamos/simple-marquee/releases)
[![Code Quality](https://img.shields.io/codacy/grade/63fcd59694174ec88466aff031a8868b.svg?style=flat-square)](https://app.codacy.com/manual/AlfredoRamos/simple-marquee/dashboard)
[![License](https://img.shields.io/github/license/AlfredoRamos/simple-marquee.svg?style=flat-square)](https://raw.githubusercontent.com/AlfredoRamos/simple-marquee/master/LICENSE)

Generates an animation effect that horizontally scrolls elements, like text or images. It tries to mimic what the obsolete [`<marquee>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/marquee) tag did, using only CSS.

Precompiled CSS files (`marquee.css` and `marquee.min.css`) can be found in [this gist](https://gist.github.com/AlfredoRamos/241ebc49763fd6d8d805878e29b9c804). A live demo is hosted at [Simple Marquee](https://alfredoramos.mx/simple-marquee).

### Dependencies

- Ruby >= 2.4.0
- Bundler

For a list of gem dependencies, see the [Gemfile](https://github.com/AlfredoRamos/simple-marquee/blob/master/Gemfile).

### Build

First off run `bundler install` to install all required gems, then generate the CSS files using `rake` tasks:

**Normal**

```shell
rake build:css
```

**Minified**

```shell
rake build:minify
```

**Both**

```shell
rake build:all
```
