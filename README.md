### About

Simple SASS Grid System

[![Build Status](https://img.shields.io/travis/com/AlfredoRamos/simple-marquee.svg?style=flat-square)](https://travis-ci.com/AlfredoRamos/simple-marquee)
[![Latest Stable Version](https://img.shields.io/github/tag/AlfredoRamos/simple-marquee.svg?style=flat-square&label=stable)](https://github.com/AlfredoRamos/simple-marquee/releases)
[![Code Quality](https://img.shields.io/codacy/grade/4880dfbf94f040f5900b2b840ddd5bd6.svg?style=flat-square)](https://www.codacy.com/app/AlfredoRamos/simple-marquee)
[![License](https://img.shields.io/github/license/AlfredoRamos/simple-marquee.svg?style=flat-square)](https://raw.githubusercontent.com/AlfredoRamos/simple-marquee/master/LICENSE)

Precompiled CSS files (`marquee.css` and `marquee.min.css`) can be found in [this gist](https://gist.github.com/AlfredoRamos/241ebc49763fd6d8d805878e29b9c804). A live demo is hosted at [Simple Marquee](https://alfredoramos.github.io/simple-marquee).

### Dependencies

- Ruby >= 2.2.0
- Bundler [[info](https://bundler.io/)]

For a list of gem dependencies, see the [Gemfile](https://github.com/AlfredoRamos/simple-marquee/blob/master/Gemfile).

### Build

First off run `bundler install` to install all required gems, then generate the CSS files using `rake` tasks:

**Normal**

```shell
rake build:css
```

**Minified**

```shell
rake build:minified
```

**Both**

```shell
rake build:all
```
