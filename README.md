# Bookmarklets
 Vários bookmarklets uteis

## Copy SD Styles

```javascript
javascript:tags=[];document.querySelectorAll('th').forEach(function(x){tags.push(x.textContent);});navigator.clipboard.writeText(tags.join(", ")).then(function() {}, function(err) {alert(tags.join(", "));console.error('Async: Could not copy text: ', err);});
```

## Copy Tags Anime

```javascript
javascript:skip=["censor", "request", "dark skin", "dark-skin", "tanline", "cum", "speech", "tattoo", "watermark", "web address", "juice", "artist", "name", "blur", "focus", "dated", "signature", "background", "text" ];tags=[]; document.querySelectorAll('.general-tag-list .search-tag, .tag-type-general > a').forEach(function(x){t=x.textContent; for (let x in skip) {if(t.indexOf(skip[x]) != -1) return;}; tags.push(t); }); navigator.clipboard.writeText(tags.join(", ")).then(function() {}, function(err) {alert(tags.join(", "));console.error('Async: Could not copy text: ', err); });
```

## word frequency

```javascript
javascript:(function() {  var blacklist = ["the", "of", "and", "a", "to", "in", "that", "is", "for", "it", "with", "was", "as", "by", "on", "not", "at", "but", "be", "this", "from", "which", "or", "have", "you", "an", "they", "her", "she", "him", "he", "we", "our", "us", "its", "their", "them"];  var text = document.body.innerText.toLowerCase().replace(/[\n\r]+/g, " "); var words = text.match(/\b\w+\b/g);  var counts = {};  words.forEach(function(word) { if(word.length >= 5 && !blacklist.includes(word)) { counts[word] = (counts[word] || 0) + 1;}});  var sorted = Object.keys(counts).sort(function(a, b) { return counts[b] - counts[a];  }); var html = "<h3>Word Frequency:</h3><ul>"; sorted.forEach(function(word) {    html += "<li>" + word + ": " + counts[word] + "</li>";  }); html += "</ul>"; var popup = window.open("", "Word Frequency Count", "width=420,height=600"); popup.document.write(html);})();
```

## IMDB

```javascript
javascript:(function() {    var elements = {};    elements.title = document.querySelector('h1 > span').innerText;    elements.Year = document.querySelector('div.sc-52d569c6-0.kNzJA-D > ul > li:nth-child(1) > a').innerText;elements.realizador = document.querySelector('ul > li:nth-child(1) > div > ul > li > a').innerText;    elements.rating = document.querySelector('span.sc-bde20123-1.iZlgcd').innerText;    elements.sinopse = document.querySelector('p > span.sc-5f699a2-0.kcphyk').innerText;    elements.genre = Array.from(document.querySelectorAll('div.ipc-chip-list__scroller > a'))                    .map(function(a) {                        return a.innerText;                    })                    .join(", ");    var output = "";    for (var key in elements) {        if (Array.isArray(elements[key])) {            output += key + ': ' + JSON.stringify(elements[key]) + '\n';        } else {            output += key + ': ' + elements[key] + '\n';        }    }    var tempInput = document.createElement('textarea');    tempInput.value = output;    document.body.appendChild(tempInput);    tempInput.select();    document.execCommand('copy');    document.body.removeChild(tempInput);    alert('Elements grabbed and copied to clipboard:\n' + output);    console.log('Output copied to clipboard:\n', output);})();
```


## Cine Cartaz

```javascript
javascript: (function () {var elements = {};elements.title = document.querySelector('#hero-movie-Detail > section:nth-child(3) > div > div > div > div > div > p > a').innerText;elements.realizador = document.querySelector('#hero-movie-Detail > section:nth-child(5) > div > div:nth-child(1) > div > div > div > p > a').innerText;elements.sinopse = document.querySelector('div.movie-detail__section-content.block-content > div > div:nth-child(1)').innerText;elements.elenco = Array.from(document.querySelectorAll('#hero-movie-Detail > section:nth-child(5) > div > div:nth-child(2) > div > div > div > p > a')).map(function (a) { return a.innerText; }).join(", "); var output = ""; for (var key in elements) { if (Array.isArray(elements[key])) { output += key + ': ' + JSON.stringify(elements[key]) + '\n'; } else { output += key + ': ' + elements[key] + '\n'; } } var tempInput = document.createElement('textarea'); tempInput.value = output; document.body.appendChild(tempInput); tempInput.select(); document.execCommand('copy'); document.body.removeChild(tempInput); alert(output); console.log('Output copied to clipboard:\n', output);})();
```

## Listar imagens de uma página

```javascript
javascript:x='';for (y=0;y<document.images.length;y++){x+='<img src='+document.images[y].src+'><br>'};if(x!=''){document.write('<center>'+x+'</center>');void(document.close())}else{alert('Não existem imagens!')}
```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```

##

```javascript

```