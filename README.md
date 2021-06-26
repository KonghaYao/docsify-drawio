# docsify-drawio

This is a docsify plugin that can convert drawio xml Data to a picture in your docs.

## First - write your drawio File Path in Your Markdown File

```md
[filename](https://cdn.jsdelivr.net/npm/docsify-drawio/test.drawio ':include :type=code')
```

## Second - Add Some Script in your docsify html File.

!! It must put after your window.$docsify 

```html
<script src="https://cdn.jsdelivr.net/npm/docsify-drawio/viewer.min.js"></script>
<script src='https://cdn.jsdelivr.net/npm/docsify-drawio/drawio.js'></script>
```

## Third - Add A Markdown render function in your $docsify.

```js
window.$docsify = {
    // You just have to copy it to Your own html File
    markdown: {
      renderer: {

        code: function (code, lang) {
          if (lang === 'drawio') {
            if (window.drawioConverter) {
              console.log('drawio 转化中')
              return window.drawioConverter(code)
            } else {
              return `<div class='drawio-code'>${code}</div>`
            }
          } else {
            return this.origin.code.apply(this, arguments);
          }
        }
      }
    },
  };

```

## Some detail

Because I haven't find a smaller plugin to convert drawio File to HTML, so I use the js File from  [viewer.min.js](https://github.com/jgraph/drawio/blob/dev/src/main/webapp/js/viewer.min.js) to convert it.

And I put this File to npm repo, so that I could use it by jsdelivr or other cdn.
