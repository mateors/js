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
