This is a [Hugo Components](https://gohugo.io/hugo-modules/) that packages a variety of libaries commonly in use at InterExchange.

- [Bootstrap v4](https://github.com/twbs/bootstrap)
- [jQuery](https://github.com/jquery/jquery)
- [js-cookie](https://github.com/js-cookie/js-cookie)

You need the Hugo extended version and Go to use this component.

## Development

We may want to add more libaries to these modules over time.

Following the [Use Hugo Modules Docs](https://gohugo.io/hugo-modules/use-modules/) to learn more about the system.

1. Add Module to config.toml


## Usage

### CSS Bundles

Add the component to your Hugo site's config:

```toml
[module]
  [[module.imports]]
    path = "github.com/interexchange/hugo-modules"
```

#### Twitter Bootstrap

The Bootstrap SCSS will be mounted in `assets/scss/bootstrap`, so you can then import either all:

```scss
@import "bootstrap/bootstrap";
```

Or only what you need:


```scss
@import "bootstrap/functions";
@import "bootstrap/variables";
@import "bootstrap/mixins";
@import "bootstrap/root";
@import "bootstrap/reboot";
@import "bootstrap/type";
@import "bootstrap/images";
@import "bootstrap/code";
@import "bootstrap/grid";
@import "bootstrap/tables";
@import "bootstrap/forms";
@import "bootstrap/buttons";
@import "bootstrap/transitions";
@import "bootstrap/dropdown";
@import "bootstrap/button-group";
@import "bootstrap/input-group";
@import "bootstrap/custom-forms";
@import "bootstrap/nav";
@import "bootstrap/navbar";
@import "bootstrap/card";
@import "bootstrap/breadcrumb";
@import "bootstrap/pagination";
@import "bootstrap/badge";
@import "bootstrap/jumbotron";
@import "bootstrap/alert";
@import "bootstrap/progress";
@import "bootstrap/media";
@import "bootstrap/list-group";
@import "bootstrap/close";
@import "bootstrap/toasts";
@import "bootstrap/modal";
@import "bootstrap/tooltip";
@import "bootstrap/popover";
@import "bootstrap/carousel";
@import "bootstrap/spinners";
@import "bootstrap/utilities";
@import "bootstrap/print";
```


### JS Bundles

#### Twitter Bootstrap

The Bootstrap JS bundles will be mounted in `assets/js/bootstrap`. Within Hugo pages
you can import it as follows to deliver one combined JS file for your site.

```html
{{ $bootstrap := resources.Get "js/bootstrap/bootstrap.bundle.js" }}
{{ $your_js := resources.Get "js/your_js/main.js" }}
{{ $defaultJS := slice $bootstrap $your_js | resources.Concat "js/global.js" }}
{{ $globalJS := $defaultJS | resources.Minify | resources.Fingerprint }}

<script src="{{ $globalJS.Permalink }}" integrity="{{ $globalJS.Data.Integrity }}"></script>
```

#### JS Cookies

## Versions

This repository is a fork of https://github.com/gohugoio/hugo-mod-bootstrap-scss-v4 to explore bootstrap js, inspired by https://github.com/denolteholding/hugo-mod-bootstrap-scss-js-v5.

Please refer to the original repository for proper update cycles and maintenance.
