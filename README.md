```js
 function load(url){
    var ajax = new XMLHttpRequest();
    ajax.open('GET', url, false);
    ajax.onreadystatechange = function ()
    {
        var script = ajax.response || ajax.responseText;
        if (ajax.readyState === 4)
        {
            switch(ajax.status)
            {
                case 200:
                    eval.apply( window, [script] );
                    console.log("library loaded: ", url);
                    break;
                default:
                    console.log("ERROR: library not loaded: ", url);
            }
        }
    };
    ajax.send(null);
}
```
 ### initialize a single load 
> load('plugins/script.js');

var s =["resources/codemirror/mode/xml/xml.js","resources/codemirror/mode/php/php.js","resources/codemirror/mode/clike/clike.js"];
### initialize a full load of scripts
```js
if (s.length > 0)
{
    for (i = 0; i < s.length; i++)
    {
        load(s[i]);
    }
}
```

## Support both modern and old browsers
```js
!function(e,t,r){function n(){for(;d[0]&&"loaded"==d[0][f];)c=d.shift(),c[o]=!i.parentNode.insertBefore(c,i)}for(var s,a,c,d=[],i=e.scripts[0],o="onreadystatechange",f="readyState";s=r.shift();)a=e.createElement(t),"async"in i?(a.async=!1,e.head.appendChild(a)):i[f]?(d.push(a),a[o]=n):e.write("<"+t+' src="'+s+'" defer></'+t+">"),a.src=s}(document,"script",[
  "//other-domain.com/1.js",
  "2.js"
])
```

## Modern approach | Promises

```js
      const loadScript = function () {
          let cache = {};
          return function (src) {
              return cache[src] || (cache[src] = new Promise((resolve, reject) => {
                  let s = document.createElement('script');
                  s.defer = true;
                  s.src = src;
                  s.onload = resolve;
                  s.onerror = reject;
                  document.body.append(s);
              }));
          }
      }();
```

### Calling above function
```js
      Promise.all([
          loadScript('resources/codemirror/mode/xml/xml.js'),
          loadScript('resources/codemirror/mode/php/php.js'),
          loadScript('resources/codemirror/mode/clike/clike.js'),
      ]).then(() => {
          
          // do something
          var codeSelector=document.getElementById("code");
          var editor = CodeMirror.fromTextArea(codeSelector, {
              mode: "application/x-httpd-php",
              matchTags: {bothTags: true},
              theme:"default",
              styleActiveLine: true,
              lineNumbers: true,
              lineWrapping: true,
              foldGutter: true,
              gutters: ["CodeMirror-linenumbers", "CodeMirror-foldgutter"],
              matchBrackets: true,
              indentUnit: 4,
              extraKeys: {"Alt-F": "findPersistent"},
              indentWithTabs: true
          });
          //editor.options.mode="text/x-go";
          //console.log(editor.options.mode,editor.options.gutters);
      });
```
## Learning Resources
* https://web.dev/articles/speed-script-loading#toc-aggressive-optimisation
