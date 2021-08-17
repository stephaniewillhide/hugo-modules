This is a [Hugo Components](https://gohugo.io/hugo-modules/) that packages a variety of libaries commonly in use at InterExchange.

- [Bootstrap v4](https://github.com/twbs/bootstrap)
- [jQuery](https://github.com/jquery/jquery)
- [js-cookie](https://github.com/js-cookie/js-cookie)
- [Font Awesome](https://github.com/FortAwesome/Font-Awesome/)

You need the Hugo extended version and Go to use this component.

## Development

We may want to add more libaries to these modules over time.

Following the [Use Hugo Modules Docs](https://gohugo.io/hugo-modules/use-modules/) to learn more about the system.

### 1. Add Module to config.toml

```
[[module.imports]]
path="github.com/FortAwesome/Font-Awesome" # source repository
```

### 2. Find the paths you need to mount

```
[[module.imports.mounts]]
source = "scss" # source repository directory
target = "assets/scss/font-awesome" # module asset location
```

```
[[module.imports.mounts]]
source = "js" # source repository directory
target = "assets/js/font-awesome" # module asset location
```

### 3. Start Hugo to configure module files

```
hugo
```

### 4. This will have updated two files

```
modified:   go.mod
modified:   go.sum
```

### 5. Check tag version in `go.mod`, you may need to modify this

This was the default
```
github.com/FortAwesome/Font-Awesome v4.7.0+incompatible // indirect
```

Changed to the most recent version, which doesn't have the v prefix
```
github.com/FortAwesome/Font-Awesome 5.15.4 // indirect
```

### 6. Remove the go.sum lines related to the library, run hugo again

```
git co go.sum
hugo
```

### 7. Create a commit

```
git commit -m "Added Font Awesome Support"
```

### 8. Tag a new version

```
git tag v1.0.5
```

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

#### Font Awesome

You will also need to specify the versions you wish you use

```scss
$fa-font-path: "/webfonts/fontawesome"; // we store the fonts under a namespaced directory

@import 'font-awesome/fontawesome'; // github.com/interexchange/hugo-modules
@import 'font-awesome/solid';
@import 'font-awesome/regular';
@import 'font-awesome/brands';
```

### JS Bundles

#### Twitter Bootstrap

The Bootstrap JS bundles will be mounted in `assets/js/bootstrap`. Within Hugo pages
you can import it as follows to deliver one combined JS file for your site.

```html
{{ $bootstrap := resources.Get "js/bootstrap/bootstrap.bundle.js" }}
{{ $site := resources.Get "js/site.js" }}
{{ $defaultJS := slice $bootstrap $site | resources.Concat "js/global.js" }}
{{ $globalJS := $defaultJS | resources.Minify | resources.Fingerprint }}

<script src="{{ $globalJS.Permalink }}" integrity="{{ $globalJS.Data.Integrity }}"></script>
```

#### JQuery

```html
{{ $jquery := resources.Get "js/jquery/jquery.min.js" }}
{{ $site := resources.Get "js/site.js" }}
{{ $defaultJS := slice $jquery $site | resources.Concat "js/global.js" }}
{{ $globalJS := $defaultJS | resources.Minify | resources.Fingerprint }}

<script src="{{ $globalJS.Permalink }}" integrity="{{ $globalJS.Data.Integrity }}"></script>
```

#### JS Cookies

```html
{{ $jscookie := resources.Get "js/js-cookie/js.cookie.js" }}
{{ $site := resources.Get "js/site.js" }}
{{ $defaultJS := slice $jscookie $site | resources.Concat "js/global.js" }}
{{ $globalJS := $defaultJS | resources.Minify | resources.Fingerprint }}

<script src="{{ $globalJS.Permalink }}" integrity="{{ $globalJS.Data.Integrity }}"></script>
```

#### All Libraries


```html
{{ $jscookie := resources.Get "js/js-cookie/js.cookie.js" }}
{{ $jquery := resources.Get "js/jquery/jquery.min.js" }}
{{ $bootstrap := resources.Get "js/bootstrap/bootstrap.bundle.js" }}
{{ $site := resources.Get "js/site.js" }}
{{ $defaultJS := (slice $jscookie $jquery $bootstrap $site) | resources.Concat "js/global.js" }}
{{ $globalJS := $defaultJS | resources.Minify | resources.Fingerprint }}

<script src="{{ $globalJS.Permalink }}" integrity="{{ $globalJS.Data.Integrity }}"></script>
```

## Versions

This repository is a fork of https://github.com/gohugoio/hugo-mod-bootstrap-scss-v4 to explore bootstrap js, inspired by https://github.com/denolteholding/hugo-mod-bootstrap-scss-js-v5.

Please refer to the original repository for proper update cycles and maintenance.
