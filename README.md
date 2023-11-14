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
## Learning Resources
* https://web.dev/articles/speed-script-loading#toc-aggressive-optimisation
