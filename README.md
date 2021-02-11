# csrf-xhr

Automatically add Rails CSRF tokens into XMLHttpRequest headers.

## How to Use

Load `csrf-xhr.js` in a `<script>` anywhere after the `<meta name="csrf-token">`
that Rails adds to the page.

From now on, any XMLHttpRequest whose destination URL is your local origin
(including both relative URLs as well as URLs which explicitly have the same
origin as the current page) will have an `"X-CSRF-Token"` token set to the
contents of the `<meta name="csrf-token">` that [Rails generates in the page's
`<head>`](http://stackoverflow.com/questions/9996665/rails-how-does-csrf-meta-tag-work).

[jQuery-ujs](https://github.com/rails/jquery-ujs) does this for you;
this does it for you even if you aren't using jQuery.

## Webpacker Instructions

1. Install

`yarn add csrf-xhr`

2. Import:
```js
// application.js 
import("csrf-xhr")
```

3. Ensure Correct Order in Layout file:
```erb
<-- e.g. app/views/layouts/application.html.erb -->

<meta name="csrf-token">
<%= javascript_pack_tag "application" %>  <-- Must come AFTER the above csrf meta tag -->
```

## Motivation

This was created to decouple [`elm-rails`](https://github.com/NoRedInk/elm-rails/)
from CSRF token management.
