# Inky-for-VAEs

Inky-for-VAEs is an Inky clone that removes the excess of HTML elements

# Inky

Inky is an HTML-based templating language that converts simple HTML into complex, responsive email-ready HTML. Designed for [Foundation for Emails](https://get.foundation/emails).

Give Inky simple HTML like this:

```html
<row>
  <columns large="6"></columns>
  <columns large="6"></columns>
</row>
```

And get complicated, but battle-tested, email-ready HTML like this:

```html
<table class="row">
  <tbody>
    <tr>
      <th class="small-12 large-6 columns first">
        <table>
          <tr>
            <th class="expander"></th>
          </tr>
        </table>
      </th>
      <th class="small-12 large-6 columns first">
        <table>
          <tr>
            <th class="expander"></th>
          </tr>
        </table>
      </th>
    </tr>
  </tbody>
</table>
```

## Installation

```bash
npm install inky-for-vaes --save-dev
```

## Usage

Inky can be used standalone, as a Gulp plugin, or with a CLI. You can also access the `Inky` parser class directly.

### Standalone

```js
var inky = require('inky');

inky({
  src: 'src/pages/**/*.html',
  dest: 'dist'
}, function() {
  console.log('Done parsing.');
});
```

### With Gulp

```js
var inky = require('inky')

function parse() {
  gulp.src('src/pages/**/*.html')
    .pipe(inky())
    .pipe(gulp.dest('dist'));
}
```

### Command Line

Install [foundation-cli](https://github.com/foundation/foundation-cli) to get the `foundation` command.

## Plugin Settings

- `src` (String): Glob of files to process. You don't need to supply this when using Inky with Gulp.
- `dest` (String): Folder to output processed files to. You don't need to supply this when using Inky with Gulp.
- `components` (Object): Tag names for custom components. See [custom components](#custom-components) below to learn more.
- `columnCount` (Number): Column count for the grid. Make sure your Foundation for Emails project has the same column count in the Sass as well.
- `cheerio` (Object): cheerio settings (for available options please refer to [cheerio project at github](https://github.com/cheeriojs/cheerio)).

## Custom Elements

Inky simplifies the process of creating HTML emails by expanding out simple tags like `<row>` and `<column>` into full table syntax. The names of the tags can be changed with the `components` setting.

Here are the names of the defaults:

```js
{
  button: 'button',
  row: 'row',
  columns: 'columns',
  container: 'container',
  inky: 'inky',
  blockGrid: 'block-grid',
  menu: 'menu',
  menuItem: 'item'
}
```

## Programmatic Use

The Inky parser can be accessed directly for programmatic use. It takes in a [Cheerio](https://github.com/cheeriojs/cheerio) object of HTML, and gives you back a converted Cheerio object.

```js
var Inky = require('inky-for-vaes').Inky;
var cheerio = require('cheerio');

var options = {};
var input = '<row></row>';

// The same plugin settings are passed in the constructor
var i = new Inky(options);
var html = cheerio.load(input)

// Now unleash the fury
var convertedHtml = i.releaseTheKraken(html);

// The return value is a Cheerio object. Get the string value with .html()
convertedHtml.html();
```
