# Bookmarklets

Os [bookmarklets](https://pt.wikipedia.org/wiki/Bookmarklet) são bookmarks (marcadores) que incorporam javascript, quando você clica no marcador, o javascript é executado no contexto da página carregada no momento. O que isso significa é que em um browser (navegador) moderno, os bookmarklets podem ser usados para modificar páginas, analisar sua estrutura e fazer uma série de outras coisas úteis e interessantes.

## IMDB

`https://www.imdb.com/title/tt0325805`

```javascript
javascript: (function () {
  var elements = {};
  elements.title = document.querySelector("h1 > span").innerText;
  elements.Year = document.querySelector(
    "div.sc-52d569c6-0.kNzJA-D > ul > li:nth-child(1) > a"
  ).innerText;
  elements.director = document.querySelector(
    "ul > li:nth-child(1) > div > ul > li > a"
  ).innerText;
  elements.rating = document.querySelector(
    "span.sc-bde20123-1.iZlgcd"
  ).innerText;
  elements.sinopse = document.querySelector(
    "p > span.sc-2eb29e65-0.hOntMS"
  ).innerText;
  elements.genre = Array.from(
    document.querySelectorAll("div.ipc-chip-list__scroller > a")
  )
    .map(function (a) {
      return a.innerText;
    })
    .join(", ");
  var output = "";
  for (var key in elements) {
    if (Array.isArray(elements[key])) {
      output += key + ": " + JSON.stringify(elements[key]) + "\n";
    } else {
      output += key + ": " + elements[key] + "\n";
    }
  }
  var tempInput = document.createElement("textarea");
  tempInput.value = output;
  document.body.appendChild(tempInput);
  tempInput.select();
  document.execCommand("copy");
  document.body.removeChild(tempInput);
  alert(output);
  console.log("Output copied to clipboard:\n", output);
})();
```

### OUTPUT

```console
title: Amigos do Alheio
Year: 2003
director: Ridley Scott
rating: 7.3
sinopse: A phobic con artist and his protégé are on the verge of pulling off a lucrative swindle when the former's teenage daughter arrives unexpectedly.
genre: Comedy, Crime, Drama
```

---

## Listar imagens de uma página

```javascript
javascript: x = "";
for (y = 0; y < document.images.length; y++) {
  x += "<img src=" + document.images[y].src + "><br>";
}
if (x != "") {
  document.write("<center>" + x + "</center>");
  void document.close();
} else {
  alert("Não existem imagens!");
}
```

---

## Htm Link

```javascript
javascript: void prompt(
  "link to this page",
  unescape('<a href="') +
    location.href +
    unescape('">') +
    document.title +
    unescape("</a>")
);
```

### OUTPUT

```console
<a href="https://www.imdb.com/title/tt0325805/">Amigos do Alheio (2003) - IMDb</a>
```

---

## Markdown Link

```javascript
javascript: var $jscomp = $jscomp || {};
$jscomp.scope = {};
$jscomp.createTemplateTagFirstArg = function (b) {
  return (b.raw = b);
};
$jscomp.createTemplateTagFirstArgWithRaw = function (b, a) {
  b.raw = a;
  return b;
};
(function () {
  var b = "[" + document.title + "](" + location.href + ")",
    a = document.createElement("textarea");
  a.style.position = "fixed";
  a.style.left = "0";
  a.style.top = "0";
  a.style.width = "2em";
  a.style.height = "2em";
  a.style.padding = "0";
  a.style.border = "none";
  a.style.outline = "none";
  a.style.boxShadow = "none";
  a.style.background = "transparent";
  a.value = b;
  document.body.appendChild(a);
  a.select();
  b = !1;
  try {
    b = document.execCommand("copy");
  } catch (c) {
    console.error("Failed to copy text: ", c);
  }
  document.body.removeChild(a);
  b
    ? alert("Markdown link copied to clipboard!")
    : alert("Failed to copy markdown link to clipboard");
})();
```

### OUTPUT

```console
[Amigos do Alheio (2003) - IMDb](https://www.imdb.com/title/tt0325805/)
```

---

## copyAllLinks

`https://www.imdb.com/title/tt0325805`

```javascript
javascript: (function () {
  var b = document.querySelectorAll("a");
  var c = [];
  for (var a = 0; a < b.length; a++) {
    c.push(b[a].href);
  }
  navigator.clipboard.writeText(c.join("\n"));
})();
```

## List All Links

```javascript
javascript: x=open('','Z6','width=600,height=400,scrollbars,resizable,menubar'); y=document.links;with(x.document){write('<base target=_blank>'); for(z=0;z<y.length;z++){write(y[z].toString().link(y[z])+'<br>')}; void(close())}
```

## Github PWSH Repos

```javascript
javascript:void(open(window.location.href.replace(/^(.*)$/, '$1?tab=repositories&q=&type=source&language=powershell%27)));
```

## Github Show Gists

```javascript
javascript:void(open(window.location.href.replace('https://', 'https://gist.')));
```

## Show BeatPort Big image

```javascript
javascript:void(open(window.location.href.replace(/95x95/, '1400x1400')));
```

## Pesquisar neste site (Google)

```javascript
javascript:void(q=prompt('Qual é a palavra-chave?%27,%27%27));if(q)void(hn=location.hostname);void(location.href=%27http://www.google.com/search?q=site:%27+hn+%27 %27+escape(q))
```

## Edit Page

```javascript
javascript:document.body.contentEditable = 'true'; document.designMode='on'; void 0
```

## ImgPath

```javascript
javascript:function%20listImages()%7Bfor(var%20b%3Ddocument.getElementsByTagName(%22img%22)%2Ca%3D%5B%5D%2Cc%3D0%3Bc%3Cb.length%3Bc%2B%2B)a.push(b%5Bc%5D.src)%3BcopyToClipboard(a.join(%22%5Cn%22))%3Balert(%22List%20of%20image%20paths%20copied%20to%20clipboard!%22)%7Dfunction%20copyToClipboard(b)%7Bvar%20a%3Ddocument.createElement(%22textarea%22)%3Ba.style%3D%22position%3A%20absolute%3B%20left%3A%20-1000px%3B%20top%3A%20-1000px%22%3Ba.value%3Db%3Bdocument.body.appendChild(a)%3Ba.select()%3Bdocument.execCommand(%22copy%22)%3Bdocument.body.removeChild(a)%7DlistImages()%3Bvoid+0
```

## No img

```javascript
javascript:(function(){var a=Array.prototype.slice;var b=a.call(document.getElementsByTagName('img'));var c=a.call(document.getElementsByTagName('iframe'));var d=a.call(document.getElementsByTagName('object'));var e=b.concat(c).concat(d);for(var i=0;i<e.length;i++){e[i].style.visibility='hidden'};var f=document.getElementsByTagName('*');for(var i=0;i<f.length;i++){var g=f[i].attributes.style;var h=g?g.value+%27;%27:%27%27;f[i].setAttribute(%27style%27,h+%27background-image:%20none%20!important%27)};return%20false})();
```

## img full path parse

```javascript
javascript:n='';for(i=0;i%3Cdocument.images.length;i%2B%2B)%7Bn%2B='%3Cimg%20src='%2Bdocument.images%5Bi%5D.src%2B'%3E%20'%2Bdocument.images%5Bi%5D.src%2B'%20'%2Bdocument.images%5Bi%5D.width%2B'%20x%20'%2Bdocument.images%5Bi%5D.height%2B'%2C%20'%2Bdocument.images%5Bi%5D.fileSize%2B'%20Bytes%3Cbr%3E%3Cbr%3E'%7D;if(n!='')%7Bdocument.write('%3Cp%20style=font-size:11px;font-family:verdana%2Csans;%3E'%2Bn%2B'%3C/p%3E');void(document.close())%7Delse%7Balert('i%20see%20no%20images')%7D
```

## Show tooltips for link destinations

Adds tooltips to every link element so that when hovered they show the link destination in the tooltip.

```javascript
javascript: (function () {  function insertcss() {    var t = document.createElement("STYLE");    (t.innerHTML =      '.qtip{display:inline-block;position:relative;cursor:pointer;border-bottom:.05em dotted #3bb4e5;box-sizing:border-box;font-style:normal;transition:all%20.25s%20ease-in-out}.qtip:hover{color:#069;border-bottom:.05em%20dotted%20#069}.qtip:before{background:rgba(0,0,0,.85);box-shadow:0%201px%203px%20rgba(0,0,0,.3);text-shadow:1px%201px%201px%20rgba(0,0,0,.5)}.dark-mode%20.qtip:before{background:rgba(87,87,87,.5);box-shadow:0%201px%203px%20rgba(219,219,219,.3);text-shadow:0%200%203px%20rgba(255,255,255,.5)}.qtip{--tooltip-color:rgba(0,%200,%200,%200.85)}.qtip{--tooltip-color:rgba(87,%2087,%2087,%200.5)}.qtip:before{content:attr(data-tip);font-size:14px;position:absolute;color:#fff;line-height:1.2em;padding:.5em;font-style:normal;min-width:120px;text-align:center;opacity:0;visibility:hidden;transition:all%20.3s%20ease-in-out;font-family:sans-serif;letter-spacing:0;font-weight:600}.qtip:after{width:0;height:0;border-style:solid;content:%22%22;position:absolute;opacity:0;visibility:hidden;transition:all%20.3s%20ease-in-out}.qtip:hover:after,.qtip:hover:before{visibility:visible;opacity:1}.qtip.tip-top:before{top:0;left:50%;transform:translate(-50%,calc(-100%%20-%208px));box-sizing:border-box;border-radius:3px}.qtip.tip-top:after{border-width:8px%208px%200%208px;border-color:var(--tooltip-color)%20transparent%20transparent%20transparent;top:-8px;left:50%;transform:translate(-50%,0)}.qtip.tip-bottom:before{bottom:0;left:50%;transform:translate(-50%,calc(100%%20+%208px));box-sizing:border-box;border-radius:3px}.qtip.tip-bottom:after{border-width:0%208px%208px%208px;border-color:transparent%20transparent%20var(--tooltip-color)%20transparent;bottom:-8px;left:50%;transform:translate(-50%,0)}.qtip.tip-left:before{left:0;top:50%;transform:translate(calc(-100%%20-%208px),-50%);box-sizing:border-box;border-radius:3px}.qtip.tip-left:after{border-width:8px%200%208px%208px;border-color:transparent%20transparent%20transparent%20var(--tooltip-color);left:-8px;top:50%;transform:translate(0,-50%)}.qtip.tip-right:before{right:0;top:50%;transform:translate(calc(100%%20+%208px),-50%);box-sizing:border-box;border-radius:3px}.qtip.tip-right:after{border-width:8px%208px%208px%200;border-color:transparent%20var(--tooltip-color)%20transparent%20transparent;right:-8px;top:50%;transform:translate(0,-50%)}'),%20%20%20%20%20%20document.body.appendChild(t);%20%20}%20%20function%20replacelinks()%20{%20%20%20%20for%20(var%20t%20=%20document.querySelectorAll(%22a%22),%20r%20=%200;%20r%20%3C%20t.length;%20r++)%20{%20%20%20%20%20%20var%20o%20=%20t[r].innerHTML,%20%20%20%20%20%20%20%20e%20=%20t[r].getAttribute(%22href%22);%20%20%20%20%20%20t[r].innerHTML%20=%20%60%3Ci%20class=%22qtip%20tip-top%22%20data-tip=%22${e}%22%3E${o}%3C/i%3E%60;%20%20%20%20}%20%20}%20%20insertcss();%20%20replacelinks();})();
```

## Wiki Search

```javascript
javascript:(function() {                  function se(d) {                      return d.selection ?%20d.selection.createRange().text%20:%20d.getSelection()%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20}%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20s%20=%20se(document);%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20for%20(i=0;%20i%3Cframes.length%20&&%20(s==null%20||%20s==%27%27);%20i++)%20s%20=%20se(frames[i].document);%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20(!s%20||%20s==%27%27)%20s%20=%20prompt(%27Enter%20search%20terms%20for%20Wikipedia%27,%27%27);%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20open(%27https://en.wikipedia.org%27%20+%20(s%20?%20%27/w/index.php?title=Special:Search&search=%27%20+%20encodeURIComponent(s)%20:%20%27%27)).focus();%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20})();
```

## search links

```javascript
javascript:(function(){var%20x,n,nD,z,i;%20function%20htmlEscape(s){s=s.replace(/&/g,'&');s=s.replace(/>/g,'>');s=s.replace(/</g,'<');return%20s;}%20function%20attrQuoteEscape(s){s=s.replace(/&/g,'&');%20s=s.replace(/"/g,%20'"');return%20s;}%20x=prompt("show%20links%20with%20this%20word/phrase%20in%20link%20text%20or%20target%20url%20(leave%20blank%20to%20list%20all%20links):",%20"");%20n=0;%20if(x!=null)%20{%20x=x.toLowerCase();%20nD%20=%20window.open().document;%20nD.writeln('<html><head><title>Links%20containing%20"'+htmlEscape(x)+'"</title><base%20target="_blank"></head><body>');%20nD.writeln('Links%20on%20<a%20href="'+attrQuoteEscape(location.href)+'">'+htmlEscape(location.href)+'</a><br>%20with%20link%20text%20or%20target%20url%20containing%20"'%20+%20htmlEscape(x)%20+%20'"<br><hr>');%20z%20=%20document.links;%20for%20(i%20=%200;%20i%20<%20z.length;%20++i)%20{%20if%20((z[i].innerHTML%20&&%20z[i].innerHTML.toLowerCase().indexOf(x)%20!=%20-1)%20||%20z[i].href.toLowerCase().indexOf(x)%20!=%20-1%20)%20{%20nD.writeln(++n%20+%20'.%20<a%20href="'%20+%20attrQuoteEscape(z[i].href)%20+%20'">'%20+%20(z[i].innerHTML%20||%20htmlEscape(z[i].href))%20+%20'</a><br>');%20}%20}%20nD.writeln('<hr></body></html>');%20nD.close();%20}%20})();
```

## Dir Viewer

```javascript
javascript:var links=getImageURLS();if(!links.length){alert("This page..");}else{document.write('<html><head><meta http-equiv="Content-Type" content="text/html;charset=utf-8"><title>BSlideShow:'+document.location.href+'</title><style type="text/css">A{text-decoration:none;}BODY,TD,DIV{white-space:nowrap;font-family:calibri;font-size:24px;}</style><script type=\"text/javascript">'+buildJSImageArray(links)+'var imgindex=0;var imgs=new Array();function next(){if(imgindex<urls.length-1)imgindex++;else{imgindex=0;}loadImage();}function prev(){if(imgindex>0)imgindex--;else{imgindex=urls.length-1;}loadImage();}function waitForImage(){var img=imgs[imgindex];if((typeof img).toLowerCase()=="object"){if(!img.complete){var chr=document.getElementById("bgal_body").innerHTML;if(chr=="")newchar="|";else{var chars="|/-\\\\";var pos=chars.indexOf(chr);newchar=(pos==chars.length-1?chars.charAt(0):chars.charAt(pos+1));}document.getElementById(%22bgal_body%22).innerHTML=newchar;setTimeout(%22waitForImage();%22,250);}else{displayImage();}}}function%20loadImage(){preload(imgindex);setTitle(imgindex+1,urls.length,imgs[imgindex].src,%22%22);waitForImage();}function%20preload(index){if(index%3E=urls.length)return;if(!imgs[index]||imgs[index].src!=urls[index]){imgs[index]=new%20Image();imgs[index].src=urls[index];}var%20x=imgindex+5;if(x%3Eurls.length)x=x-urls.length;if(index%3Cx){if(imgs[index].complete)preload(index+1);else%20imgs[index].onload=new%20Function(%22preload(%22+(index+1)+%22);%22);}}function%20displayImage(){var%20img=imgs[imgindex];if((typeof%20img).toLowerCase()==%22object%22&&img.complete){var%20winW=(window.innerWidth||document.body.offsetWidth)-(window.innerWidth?32:38);var%20winH=(window.innerHeight||document.body.offsetHeight)-(window.innerHeight?47:42);var%20imgW=img.width;var%20imgH=img.height;if(imgW%3EwinW||imgH%3EwinH){if((winW/imgW)%3C(winH/imgH)){imgH=(imgH/imgW)*winW;imgW=winW;}else{imgW=(imgW/imgH)*winH;imgH=winH;}}var%20halfW=imgW/2;if(img.width&&img.height){document.getElementById(%22bgal_body%22).innerHTML=\%27%3Cimg%20border=%220%22%20src=%22\%27+img.src+\%27%22%20id=%22bgal_img%22%20style=%22margin-top:8px;cursor:pointer;%22%20width=%22\%27+imgW+\%27%22%20usemap=%22#imgmap%22%20height=%22\'+imgH+\'%22%3E%3Cbr/%3E%3Cmap%20name=%22imgmap%22%20id=%22imgmap%22%3E%3Carea%20shape=%22rect%22%20coords=%220,0,\'+halfW+\',\'+imgH+\'%22%20href=%22javascript:prev()%22%3E%3Carea%20shape=%22rect%22%20coords=%22\'+halfW+\',0,\'+imgW+\',\'+imgH+\'%22%20href=%22javascript:next()%22%3E%3C/map%3E\';setTitle(imgindex+1,urls.length,img.src,%22%C2%A0(%22+img.width+%22x%22+img.height+%22)%22);}else{document.getElementById(%22bgal_body%22).innerHTML=\'%3Ca%20href=%22javascript:next()%22%3E%3Cimg%20border=%220%22%20src=%22\'+img.src+\'%22%20id=%22bgal_img%22%20style=%22margin-top:8px;cursor:pointer;%22%3E%3C/a%3E\';setTitle(imgindex+1,urls.length,img.src,%22%22);}}}function%20setTitle(number,total,imgurl,extra){var%20imgname=imgurl.replace(/([^\\/]+)?\\//g,%22%22);document.getElementById(%22bgal_head%22).innerHTML=%22%3Cstrong%3E%22+number+%22/%22+total+%22%3C/strong%3E%C2%A0-%C2%A0%3Ca%20href=\\\%22%22+imgurl+%22\\\%22%3E%22+unescape(imgname)+%22%3C/a%3E%22+extra;}window.onresize=displayImage;%3C/script%3E%3Cbody%20onload=%22loadImage()%22%20style=%22margin:4px;padding:0px;%22%3E%3Ccenter%3E%3Ctable%20id=%22bgal_wrap%22%20style=%22border:1px%20solid%20#999;width:1%;padding:4px;margin:0px%20auto;%22%20align=%22center%22%3E%3Ctr%3E%3Ctd%3E%3Ctable%20border=%220%22%20cellpadding=%220%22%20cellspacing=%220%22%20width=%22100%%22%3E%3Ctr%3E%3Ctd%20align=%22left%22%20style=%22padding:0px%204px;%22%3E%3Ca%20href=%22javascript:prev()%22%3E%E2%86%90%20%3C/a%3E%3C/td%3E%3Ctd%3E%3Cdiv%20id=%22bgal_head%22%20style=%22text-align:center;%22%3E%3C/div%3E%3C/td%3E'+'%3Ctd%20align=%22right%22%20style=%22padding:0px%204px;%22%3E%3Ca%20href=%22javascript:next();%22%3E%20%E2%86%92%3C/a%3E%3C/td%3E'+'%3C/tr%3E%3C/table%3E%3Cdiv%20id=%22bgal_body%22%20style=%22text-align:center;font-family:monospace;%22%3E%3C/div%3E%3C/td%3E%3C/tr%3E%3C/table%3E%3C/center%3E%3C/body%3E%3C/html%3E');%20document.close();}function%20getImageURLS(){var%20urls=new%20Array();%20for(var%20x=0;%20x%3Cdocument.links.length;%20x++){a=document.links[x].href;%20%20if(!in_array(urls,a)&&a.match(/\.(jpe|jpeg|jpg|bmp|tif|gif|png)$/i)){urls[urls.length]=a;}}return%20urls;}function%20buildJSImageArray(array){var%20js=%22var%20urls=new%20Array();%22;%20for(var%20x=0;%20x%3Carray.length;%20x++){js+=%22urls[urls.length]='%22+array[x].replace(%22'%22,%22\\'%22)+%22';%22;}return%20js;}function%20in_array(array,value){for(var%20x=0;%20x%3Carray.length;%20x++){if(array[x]==a){return%20x+1;}}return%20false;}
```

## thumb gallery

```javascript
javascript:var sHTML="<html><head><title>gallery</title><body><center><table border=0>";var y=0;for(x=0;x<document.links.length;x++){a=document.links[x].href; if (a.match(/jpe|jpeg|jpg|bmp|tiff|tif|bmp|gif|png/i)){sHTML+='<td style="border-style:solid;border-width:1px"><a target="_new" href="'+a+'"><img border="0" width="100" src="'+a+'"></a></td>'; if (!((x+1)%5)) sHTML+="</tr><tr>"}};this.innerHTML=sHTML+"</table></center></body></html>";
```

## thumb

```javascript
javascript:(function(){function I(u){var t=u.split('.'),e=t[t.length-1].toLowerCase();return {gif:1,jpg:1,jpeg:1,png:1,mng:1}[e]}function hE(s){return s.replace(/&/g,'&').replace(/>/g,'>').replace(/</g,'<').replace(/"/g,'"');}var q,h,i,z=open().document;z.write('<p>Images linked to by '+hE(location.href)+':</p><hr>');for(i=0;q=document.links[i];++i){h=q.href;if(h&&I(h))z.write('<p>'+q.innerHTML+' ('+hE(h)+')<br><img src="'+hE(h)+'">');}z.close();})()
```

## Remove CSS

```javascript
javascript:(function()%7Bvar i,x;for(i=0;x=document.styleSheets%5Bi%5D;++i)x.disabled=true;%7D)();
```

## READ

```javascript
javascript:(function(){_readableOptions={text_font:"quote(Open Sans Light), quote(Lucida Sans Unicode), quote(Lucida Grande), Arial, Helvetica, sans-serif",text_font_monospace:"quote(Lucida Console), quote(Andale Mono), Monaco, monospace",text_font_header:"Tinos",text_size:"24px",text_line_height:"1.75",box_width:"30em",color_text:"#FDFDFD%22,color_background:%22#000000%22,color_links:%22#99CCFF%22,text_align:%22normal%22,base:%22blueprint%22,custom_css:%22#box,#menu,#rtl_box{background-color:transparent}::-webkit-scrollbar,::-webkit-scrollbar-corner{background:#000!important}#floating{top:1em}#floating%20a{padding:0;color:#708090!important}#floating_close{font-size:0}#floating_close:before{content:quote(%C3%97);font-size:24px;padding-left:.45em;padding-right:.45em;margin-right:.7em;border:2px%20solid;border-radius:50%}#box_inner%20#menu%20a:hover,#floating%20a:hover{color:#a9a9a9!important}#menu,#rtl_box{border:2px%20solid%20#708090;border-radius:32px}#menu%20a,#rtl_box%20a{color:#708090;border-bottom:1px%20solid%20inherit;vertical-align:sub}@media%20(max-width:920px){#floating{right:%20-5px;}#floating%20a,#floating%20a:before{margin:0!important}}%22};if(document.getElementsByTagName(%22body%22).length%3E0);else{return}if(window.$readable){if(window.$readable.bookmarkletTimer){return}}else{window.$readable={}}window.$readable.bookmarkletTimer=true;window.$readable.options=_readableOptions;if(window.$readable.bookmarkletClicked){window.$readable.bookmarkletClicked();return}_readableScript=document.createElement(%22script%22);_readableScript.setAttribute(%22src%22,%22//rdbl.us/target.js?rand=%22+encodeURIComponent(Math.random()));document.getElementsByTagName(%22body%22)[0].appendChild(_readableScript)})();
```

## tota11y

```javascript
javascript:(function(){var%20tota11y=document.createElement('SCRIPT');tota11y.type='text/javascript';tota11y.src='https://khan.github.io/tota11y/dist/tota11y.min.js';document.getElementsByTagName('head')[0].appendChild(tota11y);})();
```

## Instagram Photo

```javascript
javascript:(function(){;!function(e)%7Bvar t=%7B%7D;function n(a)%7Bif(t%5Ba%5D)return t%5Ba%5D.exports;var r=t%5Ba%5D=%7Bi:a,l:!1,exports:%7B%7D%7D;return e%5Ba%5D.call(r.exports,r,r.exports,n),r.l=!0,r.exports%7Dn.m=e,n.c=t,n.d=function(e,t,a)%7Bn.o(e,t)%7C%7CObject.defineProperty(e,t,%7Benumerable:!0,get:a%7D)%7D,n.r=function(e)%7B"undefined"!=typeof Symbol&&Symbol.toStringTag&&Object.defineProperty(e,Symbol.toStringTag,%7Bvalue:"Module"%7D),Object.defineProperty(e,"__esModule",%7Bvalue:!0%7D)%7D,n.t=function(e,t)%7Bif(1&t&&(e=n(e)),8&t)return e;if(4&t&&"object"==typeof e&&e&&e.__esModule)return e;var a=Object.create(null);if(n.r(a),Object.defineProperty(a,"default",%7Benumerable:!0,value:e%7D),2&t&&"string"!=typeof e)for(var r in e)n.d(a,r,function(t)%7Breturn e%5Bt%5D%7D.bind(null,r));return a%7D,n.n=function(e)%7Bvar t=e&&e.__esModule?function()%7Breturn%20e.default%7D:function()%7Breturn%20e%7D;return%20n.d(t,%22a%22,t),t%7D,n.o=function(e,t)%7Breturn%20Object.prototype.hasOwnProperty.call(e,t)%7D,n.p=%22%22,n(n.s=0)%7D(%5Bfunction(e,t,n)%7B%22use%20strict%22;n.r(t);var%20a=function(e,t)%7Breturn(a=Object.setPrototypeOf%7C%7C%7B__proto__:%5B%5D%7Dinstanceof%20Array&&function(e,t)%7Be.__proto__=t%7D%7C%7Cfunction(e,t)%7Bfor(var%20n%20in%20t)Object.prototype.hasOwnProperty.call(t,n)&&(e%5Bn%5D=t%5Bn%5D)%7D)(e,t)%7D;function%20r(e,t)%7Bif(%22function%22!=typeof%20t&&null!==t)throw%20new%20TypeError(%22Class%20extends%20value%20%22+String(t)+%22%20is%20not%20a%20constructor%20or%20null%22);function%20n()%7Bthis.constructor=e%7Da(e,t),e.prototype=null===t?Object.create(t):(n.prototype=t.prototype,new%20n)%7DObject.create;Object.create;var%20o=function()%7Bfunction%20e(e,t)%7Bthis._program=e,this._module=t%7Dreturn%20e.prototype.image=function(e)%7Bthis._program.setImageLink(e),this._program.foundImage=!0,this._program.foundByModule=this._module.getName(),window.open(this._program.imageLink)%7D,e.prototype.video=function(e)%7Bvar%20t=function(e)%7Bvar%20t=new%20URL(e);return%20t.host=%22scontent.cdninstagram.com%22,t.href%7D(e);window.open(t),this._program.foundByModule=this._module.getName(),this._program.foundVideo=!0,this._program.alertNotInInstagramPost=!0%7D,e%7D(),i=function()%7Bfunction%20e()%7B%7Dreturn%20e.prototype.error=function(e,t)%7Bvar%20n=this.getName();console.error(n+%22()%22,%22%5Binstantgram%5D%20%22+t.VERSION,e)%7D,e%7D(),s=function(e)%7Bfunction%20t()%7Breturn%20null!==e&&e.apply(this,arguments)%7C%7Cthis%7Dreturn%20r(t,e),t.prototype.getName=function()%7Breturn%22ImageVideoInStories%22%7D,t.prototype.execute=function(e)%7Bvar%20t=!1,n=null;try%7Bif(e.isStory)%7Bvar%20a=document.querySelector(%22body%22),r=a.querySelectorAll(%22video%20%3E%20source%22),i=a.querySelectorAll(%22button%5Baria-label%5D%22)%5B0%5D.nextElementSibling.querySelector(e.mediaImageElExpression)%7C%7Ca.querySelector(e.mediaImageElExpressions.img),s=%22%22;r.length%3E0?(s=r%5B0%5D.src,n=%22video%22):(s=i.src,n=%22image%22);var%20u=new%20o(e,this);if(s&&(u%5Bn%5D(s),t=!0),!1===t&&e.videos.length%3E0)%7Bvar%20d=e.videos%5B0%5D.src;if(!d&&e.videos%5B0%5D.children)d=e.videos%5B0%5D.children%5B0%5D.src;d&&(u.video(d),t=!0)%7D%7D%7Dcatch(t)%7Bthis.error(t,e)%7Dreturn%20t%7D,t%7D(i);function%20u(e)%7Bvar%20t=e%5BObject.keys(e).find(function(e)%7Breturn%20e.includes(%22Instance%22)%7C%7Ce.includes(%22Fiber%22)%7D)%5D;return%20t%7C%7Cnull%7Dfunction%20d(e)%7Bvar%20t=window,n=e.getBoundingClientRect();return%20n.bottom%3E0&&n.right%3E0&&n.left%3Ct.innerWidth&&n.top%3Ct.innerHeight%7Dvar%20l=function(e)%7Bfunction%20t()%7Breturn%20null!==e&&e.apply(this,arguments)%7C%7Cthis%7Dreturn%20r(t,e),t.prototype.getName=function()%7Breturn%22VideoInPostAndModal%22%7D,t.prototype.execute=function(e)%7Bvar%20t=!1;try%7Bif(e.isPost)%7Bvar%20n=void%200,a=void%200;if(1===e.videos.length&&(n=e.videos%5B0%5D.src,a=e.videos%5B0%5D),e.videos.length%3E1)%7Bvar%20r=Array.from(e.videos).filter(d);null!==r%5B0%5D.getAttribute(%22loop%22)&&(n=r%5B0%5D.src,a=r%5B0%5D)%7Dif(n)%7Bvar%20i=new%20o(e,this);-1!==n.indexOf(%22blob:%22)?(n=function(e)%7Bvar%20t=u(e),n=null==t?void%200:t.return.memoizedProps.fallbackSrc;return%20n%7C%7Cnull%7D(a),i.video(n)):i.video(n),t=!0%7D%7Delse;%7Dcatch(t)%7Bthis.error(t,e)%7Dreturn%20t%7D,t%7D(i);function%20m(e,t)%7Bvar%20n,a,r=!1,o=%22%22,i=(t%7C%7Ce%5B0%5D.closest(%27%5Brole=%22presentation%22%5D%27)).parentElement,s=Array.from(i.querySelectorAll(%22button%5Baria-label%22)).filter(function(e)%7Breturn%20e.parentElement===i%7D),d=1===s.length&&%22left%22===(null===(n=u(s%5B0%5D))%7C%7Cvoid%200===n?void%200:n.return.memoizedProps.direction),l=1===s.length&&%22right%22===(null===(a=u(s%5B0%5D))%7C%7Cvoid%200===a?void%200:a.return.memoizedProps.direction);return%20r%7C%7C(1===s.length&&l&&(o=e%5B0%5D.src,r=!0),1===s.length&&d&&(o=e%5B1%5D.src,r=!0),3===e.length&&(o=e%5B1%5D.src,r=!0)),o%7Dfunction%20g(e)%7Bvar%20t=%5B%5D;for(t.push(e);e.parentNode;)t.unshift(e.parentNode),e=e.parentNode;return%20t%7Dfunction%20c(e)%7Breturn%22user-avatar%22===e.getAttribute(%22data-testid%22)%7C%7C%22span%22===e.parentElement.localName%7C%7C%22a%22===e.parentElement.localName%7C%7Cg(e).filter(function(e)%7Breturn%22HEADER%22===e.nodeName%7D).length%3E0%7Dvar%20p=function(e)%7Bfunction%20t()%7Breturn%20null!==e&&e.apply(this,arguments)%7C%7Cthis%7Dreturn%20r(t,e),t.prototype.getName=function()%7Breturn%22ImageInPostAndModal%22%7D,t.prototype.execute=function(e)%7Bvar%20t=!1;try%7Bif(e.isPost)%7Bvar%20n=void%200,a=document.querySelector(%27article%5Brole=%22presentation%22%5D%27),r=a.querySelector(%27%5Brole=%22presentation%22%5D%27)%7C%7Ca;if(r)%7Bvar%20i=%5B%5D;a.querySelectorAll(%22img%22).forEach(function(e)%7Bd(e)&&!c(e)&&i.push(e)%7D),1===e.images.length&&(n=e.images%5B0%5D.src,t=!0),t%7C%7C1!==i.length%7C%7C(n=i%5B0%5D.src,t=!0),t%7C%7C(n=m(i,r)),n?((new%20o(e,this)).image(n),t=!0):e.context=%7BhasMsg:!0,msg:%22index#program#screen@alert_dontFound%22%7D%7D%7D%7Dcatch(t)%7Bthis.error(t,e)%7Dreturn%20t%7D,t%7D(i),f=function(e)%7Bfunction%20t()%7Breturn%20null!==e&&e.apply(this,arguments)%7C%7Cthis%7Dreturn%20r(t,e),t.prototype.getName=function()%7Breturn%22ImageOnScreen%22%7D,t.prototype.execute=function(e)%7Bvar%20t=!1;try%7Bvar%20n=void%200,a=Array.from(document.querySelectorAll('article%5Brole=%22presentation%22%5D')).filter(d);a.reverse();var%20r=a%5B0%5D;if(r)%7Bfor(var%20i=r.querySelectorAll(%22img%22),s=%5B%5D,u=0;u%3Ci.length;u++)%7Bvar%20l=i%5Bu%5D;d(l)&&!c(l)&&s.push(l)%7Dif(1===s.length&&(n=s%5B0%5D.src),!n)n=m(s,r.querySelector('div%5Brole=%22presentation%22%5D'));n?((new%20o(e,this)).image(n),t=!0):e.context=%7BhasMsg:!0,msg:%22index#program#modal@alert_dontFound%22%7D%7D%7Dcatch(t)%7Bthis.error(t,e)%7Dreturn%20t%7D,t%7D(i),h=%7Blangs:%7B%22de-DE%22:%7B%22helpers.localize_defaultlang%22:%22Ausgew%C3%A4hlte%20Sprache:%20$%7BLANG_DEFAULT%7D%20%5Cn%20Weitere%20Informationen%20zu%20den%20unterst%C3%BCtzten%20Sprachen%20findest%20du%20auf%20http://theus.github.io/instantgram%22,%22modules.update@oudated_outdated%22:%22%5Binstantgram%5D%20ist%20veraltet.%20Bitte%20besuche%20die%20Seite%20http://theus.github.io/instantgram%20f%C3%BCr%20ein%20Update.%22,%22modules.update@oudated_localInfo%22:%22%5Binstantgram%5D%20Installierte%20Version%20$%7Bdata.version%7D%20%7C%20Neue%20Version:%20$%7Bdata.gitVersion%7D%22,%22modules.update@determineIfGetUpdateIsNecessary_contacting%22:%22%5Binstantgram%5D%20sucht%20nach%20neuen%20verf%C3%BCgbaren%20Updates%E2%80%A6%22,%22modules.update@determineIfGetUpdateIsNecessary_updated%22:%22%5Binstantgram%5D%20wurde%20aktualisiert.%22,%22modules.update@determineIfGetUpdateIsNecessary_@alert_found%22:%22%5Binstantgram%5D%20hat%20ein%20neues%20Update%20gefunden.%5CnBitte%20besuche%20die%20Seite%20http://theus.github.io/instantgram,%20um%20das%20Update%20zu%20installieren.%22,%22index@alert_onlyWorks%22:%22%5Binstantgram%5D%20funktioniert%20nur%20mit%20instagram.com.%22,%22index#program#modal@alert_dontFound%22:%22%5Binstantgram%5D%20konnte%20kein%20Bild%20in%20diesem%20Post%20finden.%20Bitte%20%C3%B6ffne%20den%20Link%20in%20einem%20neuen%20Tab.%22,%22index#program#post@alert_dontFound%22:%22Ops,%20%5Binstantgram%5D%20konnte%20leider%20kein%20Bild%20finden%20%20:-(%22,%22index#program#screen@alert_dontFound%22:%22%5Binstantgram%5D%20hat%20mehr%20als%201%20Bild%20gefunden.%20Bist%20du%20in%20der%20Profilansicht?%20Falls%20ja,%20%C3%B6ffne%20bitte%20zuerst%20einen%20einzelnen%20Post%20und%20f%C3%BChre%20%5Binstantgram%5D%20erneut%20aus.%22,%22index#program@alert_dontFound%22:%22Ops,%20hast%20du%20einen%20Instagram%20Post%20ge%C3%B6ffnet?%20Zum%20Beispiel%20instagram.com/p/82jd828jd%22%7D,%22en-US%22:%7B%22helpers.localize_defaultlang%22:%22%5Binstantgram%5D%20set%20language:%20$%7BLANG_DEFAULT%7D%20%5Cn%20For%20more%20information%20about%20available%20languages%20please%20check%20http://theus.github.io/instantgram%22,%22modules.update@oudated_outdated%22:%22%5Binstantgram%5D%20is%20outdated.%20Please%20check%20http://theus.github.io/instantgram%20for%20available%20updates.%22,%22modules.update@oudated_localInfo%22:%22%5Binstantgram%5D%20Installed%20version:%20$%7Bdata.version%7D%20%7C%20New%20update:%20$%7Bdata.gitVersion%7D%22,%22modules.update@determineIfGetUpdateIsNecessary_contacting%22:%22%5Binstantgram%5D%20is%20looking%20for%20available%20updates%E2%80%A6%22,%22modules.update@determineIfGetUpdateIsNecessary_updated%22:%22%5Binstantgram%5D%20updated%20your%20current%20version.%22,%22modules.update@determineIfGetUpdateIsNecessary_@alert_found%22:%22%5Binstantgram%5D%20found%20a%20new%20available%20update.%5CnPlease%20check%20http://theus.github.io/instantgram%20to%20install%20it.%22,%22index@alert_onlyWorks%22:%22%5Binstantgram%5D%20only%20works%20on%20instagram.com.%22,%22index#program#modal@alert_dontFound%22:%22%5Binstantgram%5D%20didn't%20find%20any%20image%20in%20this%20Instagram%20post.%20Please%20try%20to%20open%20the%20link%20in%20a%20new%20tab.%22,%22index#program#post@alert_dontFound%22:%22Ops,%20%5Binstantgram%5D%20couldn't%20find%20any%20image%20%20:-(%22,%22index#program#screen@alert_dontFound%22:%22%5Binstantgram%5D%20found%20more%20than%201%20image.%20Are%20you%20on%20a%20profile%20page?%20If%20yes,%20please%20open%20a%20single%20post%20first%20and%20open%20%5Binstantgram%5D%20again.%22,%22index#program@alert_dontFound%22:%22Ops,%20did%20you%20open%20any%20Instagram%20post?%20Like%20for%20example%20instagram.com/p/82jd828jd%22%7D,%22es-AR%22:%7B%22helpers.localize_defaultlang%22:%22%5Binstantgram%5D%20elegir%20idioma:%20$%7BLANG_DEFAULT%7D%20%5Cn%20Para%20m%C3%A1s%20informaci%C3%B3n%20acerca%20de%20los%20idiomas%20disponibles,%20por%20favor%20visite%20http://theus.github.io/instantgram%22,%22modules.update@oudated_outdated%22:%22%5Binstantgram%5D%20est%C3%A1%20desactualizado.%20Por%20favor%20visite%20http://theus.github.io/instantgram%20para%20ver%20actualizaciones.%22,%22modules.update@oudated_localInfo%22:%22%5Binstantgram%5D%20Versi%C3%B3n%20instalada:%20$%7Bdata.version%7D%20%7C%20Nueva%20actualizaci%C3%B3n:%20$%7Bdata.gitVersion%7D%22,%22modules.update@determineIfGetUpdateIsNecessary_contacting%22:%22%5Binstantgram%5D%20est%C3%A1%20buscando%20nuevas%20actualizaciones%E2%80%A6%22,%22modules.update@determineIfGetUpdateIsNecessary_updated%22:%22%5Binstantgram%5D%20actualiz%C3%B3%20a%20la%20versi%C3%B3n%20actual.%22,%22modules.update@determineIfGetUpdateIsNecessary_@alert_found%22:%22%5Binstantgram%5D%20encontr%C3%B3%20una%20nueva%20actualizaci%C3%B3n%20disponible.%5CnPor%20favor%20visite%20http://theus.github.io/instantgram%20para%20instalarla.%22,%22index@alert_onlyWorks%22:%22%5Binstantgram%5D%20s%C3%B3lo%20funciona%20en%20instagram.com.%22,%22index#program#modal@alert_dontFound%22:%22%5Binstantgram%5D%20no%20encontr%C3%B3%20ninguna%20imagen%20en%20esta%20publicaci%C3%B3n%20de%20Instagram.%20Por%20favor%20intente%20abrir%20el%20link%20en%20una%20nueva%20pesta%C3%B1a.%22,%22index#program#post@alert_dontFound%22:%22Ups,%20%5Binstantgram%5D%20no%20pudo%20encontrar%20ninguna%20imagen%20:-(%22,%22index#program#screen@alert_dontFound%22:%22%5Binstantgram%5D%20encontr%C3%B3%20m%C3%A1s%20de%201%20imagen.%20%C2%BFEst%C3%A1s%20en%20una%20p%C3%A1gina%20de%20perfil?%20Si%20es%20as%C3%AD,%20por%20favor%20ingresa%20en%20una%20publicaci%C3%B3n%20y%20luego%20abre%20%5Binstantgram%5D%20nuevamente.%22,%22index#program@alert_dontFound%22:%22Ups,%20abriste%20alguna%20publicaci%C3%B3n%20de%20Instagram?%20Por%20ejemplo%20instagram.com/p/82jd828jd%22%7D,%22pt-BR%22:%7B%22helpers.localize_defaultlang%22:%22%5Binstantgram%5D%20idioma%20configurado:%20$%7BLANG_DEFAULT%7D%20%5Cnpara%20mais%20informa%C3%A7%C3%B5es%20sobre%20os%20idiomas%20suportados,%20acesse%20http://theus.github.io/instantgram%22,%22modules.update@oudated_outdated%22:%22%5Binstantgram%5D%20est%C3%A1%20desatualizado.%20Acesse%20http://theus.github.io/instantgram%20para%20atualizar%22,%22modules.update@oudated_localInfo%22:%22%5Binstantgram%5D%20vers%C3%A3o%20local:%20$%7Bdata.version%7D%20%7C%20nova%20vers%C3%A3o:%20$%7Bdata.gitVersion%7D%22,%22modules.update@determineIfGetUpdateIsNecessary_contacting%22:%22%5Binstantgram%5D%20est%C3%A1%20procurando%20atualiza%C3%A7%C3%B5es...%22,%22modules.update@determineIfGetUpdateIsNecessary_updated%22:%22%5Binstantgram%5D%20informa%C3%A7%C3%B5es%20locais%20atualizadas%22,%22modules.update@determineIfGetUpdateIsNecessary_@alert_found%22:%22%5Binstantgram%5D%20encontrou%20uma%20atualiza%C3%A7%C3%A3o.%5Cn%20acesse%20theus.github.io/instantgram%20para%20atualizar%22,%22index@alert_onlyWorks%22:%22%5Binstantgram%5D%20somente%20funciona%20no%20instagram.com%22,%22index#program#modal@alert_dontFound%22:%22%5Binstantgram%5D%20n%C3%A3o%20encontrou%20uma%20imagem%20em%20um%20post.%20Tente%20abrir%20o%20link%20em%20uma%20nova%20aba.%22,%22index#program#post@alert_dontFound%22:%22ops,%20%5Binstantgram%5D%20n%C3%A3o%20encontrou%20a%20imagem%20:(%22,%22index#program#screen@alert_dontFound%22:%22%5Binstantgram%5D%20a%20procura%20por%20imagem%20na%20tela%20encontrou%20mais%20de%201%20imagem.%20Voc%C3%AA%20est%C3%A1%20em%20um%20perfil?%20Se%20sim,%20abra%20alguma%20imagem%20antes%20de%20rodar%20o%20%5Binstantgram%5D%22,%22index#program@alert_dontFound%22:%22ops,%20voc%C3%AA%20est%C3%A1%20em%20algum%20post%20do%20instagram?%20ex:%20instagram.com/p/82jd828jd%22%7D%7D%7D,v=%7Bde:%22de-DE%22,pt:%22pt-BR%22,en:%22en-US%22,%22en-GB%22:%22en-US%22%7D%5Bnavigator.language%5D%7C%7C%22en-US%22;function%20y(e,t)%7Bvoid%200===t&&(t=v);try%7Breturn%20h.langs.hasOwnProperty(t)%7C%7C(t=%22en-US%22),h.langs%5Bt%5D%5Be%5D?h.langs%5Bt%5D%5Be%5D:%22%22%7Dcatch(n)%7Breturn%20console.error(%22%5Binstantgram%5D%20LOC%20error:%22,n),%22ops,%20an%20error%20ocurred%20in%20localization%20system.%20Enter%20in%20https://github.com/theus/instantgram/issues/new%20and%20open%20an%20issue%20with%20this%20code:%20'LOC_dont_found_str_neither_default:%5B%22+t+%22-%3E%22+e+%22%5D'%5Cn%20%20%20%20for%20more%20information%20open%20the%20console%22%7D%7Dconsole.info(y(%22helpers.localize_defaultlang%22).replace(%22$%7BLANG_DEFAULT%7D%22,v));var%20_=y;var%20b=%7BregexOriginalImage:/%5C/%5Ba-z%5D+%5Cd+%5Ba-z%5D?x%5Cd+%5Ba-z%5D?/,regexMaxResImage:/%5C/%5Ba-z%5D+%5B1080%5D+%5Ba-z%5D?x%5B1080%5D+%5Ba-z%5D?/,regexPath:/%5E%5C/p%5C//,regexHostname:/instagram%5C.com/,regexStoriesURI:/stories%5C/(.*)+/,regexURL:/(%5B--:%5Cw?@%25&+~#=%5D*%5C.%5Ba-z%5D%7B2,4%7D%5C/%7B0,2%7D)((?:%5B?&%5D(?:%5Cw+)=(?:%5Cw+))+%7C%5B--:%5Cw?@%25&+~#=%5D+)?/%7D;var%20x=window.navigator.userAgent.indexOf(%22Edge%22)%3E-1%7C%7Cwindow.navigator.userAgent.indexOf(%22Edg%22)%3E-1,I=%7Bcover:'img%5Bstyle=%22object-fit:%20cover;%22%5D',srcset:%22img%5Bsrcset%5D%22,img:%22img%22%7D,w=window.location.pathname,S=%7BVERSION:%225.0.0%22,mediaImageElExpressions:I,mediaImageElExpression:x?I.cover:I.srcset,hostname:window.location.hostname,path:w,images:%5B%5D,imagesOnViewPort:%5B%5D,videos:document.querySelectorAll(%22video%22),foundByModule:null,isStory:b.regexStoriesURI.test(w),isPost:b.regexPath.test(w),probablyHasAGallery:%7Bcheck:null,byModule:%22%22%7D,setImageLink:function(e)%7Bthis.imageLinkBeforeParse=e,b.regexMaxResImage.test(e)?this.imageLink=e:this.imageLink=b.regexOriginalImage.test(e)?e.replace(b.regexOriginalImage,%22%22):e%7D,foundVideo:!1,foundImage:!1,imageLink:!1,imageLinkBeforeParse:!1,alertNotInInstagramPost:!1,context:%7BhasMsg:!1,msg:void%200%7D%7D;!function(e,t,n)%7Bfor(var%20a=0;a%3Ce.length;a++)t.call(n,a,e%5Ba%5D)%7D(document.images,function(e,t)%7Bvar%20n=t;!c(n)&&function(e)%7Breturn%20g(e).filter(function(e)%7Breturn%22ARTICLE%22===e.nodeName%7D).length%3E0%7D(n)&&(S.images.push(n),d(n)&&S.imagesOnViewPort.push(n))%7D),b.regexHostname.test(S.hostname)%7C%7Cwindow.alert(_(%22index@alert_onlyWorks%22)),b.regexHostname.test(S.hostname)&&!1===(new%20s).execute(S)&&!1===(new%20l).execute(S)&&!1===(new%20p).execute(S)&&!1===(new%20f).execute(S)&&(S.context.hasMsg=!1),S.context.hasMsg&&window.alert(_(S.context.msg)),!S.alertNotInInstagramPost%7C%7CS.foundVideo%7C%7CS.foundImage%7C%7Cwindow.alert(_(%22index#program@alert_dontFound%22))%7D%5D);})()
```

## Google Translate

```javascript
javascript:var t=((window.getSelection&&window.getSelection())||(document.getSelection&&document.getSelection())||(document.selection&&document.selection.createRange&&document.selection.createRange().text));var e=(document.charset||document.characterSet);if(t!=''){location.href='http://translate.google.com/translate_t?text=%27+t+%27&hl=en&langpair=auto|pt&tbb=1&ie=%27+e;}else{location.href=%27http://translate.google.com/translate?u=%27+escape(location.href)+%27&hl=en&langpair=auto|pt&tbb=1&ie=%27+e;};
```

## adblock

```javascript
javascript:(function()%7BArray.from(document.querySelectorAll('*')).map(ele %3D> %7Bele.style.overflow %3D 'inherit'%3BgetComputedStyle(ele).zIndex>0 %3F ele.remove() %3A null%7D)%7D)()
```

## Gmail

```javascript
javascript:(function(){m='http://mail.google.com/mail/?view=cm&fs=1&tf=1&to=&su=%27+encodeURIComponent(document.title)+%27&body=%27+encodeURIComponent(document.location);w=window.open(m,%27addwindow%27,%27status=no,toolbar=no,width=575,height=545,resizable=yes%27);setTimeout(function(){w.focus();},%20250);})();
```

## Copy SD Styles

> `https://github.com/willwulfken/MidJourney-Styles-and-Keywords-Reference`

```javascript
javascript:tags=[];document.querySelectorAll('th').forEach(function(x){tags.push(x.textContent);});navigator.clipboard.writeText(tags.join(", ")).then(function() {}, function(err) {alert(tags.join(", "));console.error('Async: Could not copy text: ', err);});
```

## Copy Tags Anime

> `https://danbooru.donmai.us/posts?page=14`

```javascript
javascript:skip=["censor", "request", "dark skin", "dark-skin", "tanline", "cum", "speech", "tattoo", "watermark", "web address", "juice", "artist", "name", "blur", "focus", "dated", "signature", "background", "text" ];tags=[]; document.querySelectorAll('.general-tag-list .search-tag, .tag-type-general > a').forEach(function(x){t=x.textContent; for (let x in skip) {if(t.indexOf(skip[x]) != -1) return;}; tags.push(t); }); navigator.clipboard.writeText(tags.join(", ")).then(function() {}, function(err) {alert(tags.join(", "));console.error('Async: Could not copy text: ', err); });
```

## word frequency

```javascript
javascript:(function() {  var blacklist = ["the", "of", "and", "a", "to", "in", "that", "is", "for", "it", "with", "was", "as", "by", "on", "not", "at", "but", "be", "this", "from", "which", "or", "have", "you", "an", "they", "her", "she", "him", "he", "we", "our", "us", "its", "their", "them"];  var text = document.body.innerText.toLowerCase().replace(/[\n\r]+/g, " "); var words = text.match(/\b\w+\b/g);  var counts = {};  words.forEach(function(word) { if(word.length >= 5 && !blacklist.includes(word)) { counts[word] = (counts[word] || 0) + 1;}});  var sorted = Object.keys(counts).sort(function(a, b) { return counts[b] - counts[a];  }); var html = "<h3>Word Frequency:</h3><ul>"; sorted.forEach(function(word) {    html += "<li>" + word + ": " + counts[word] + "</li>";  }); html += "</ul>"; var popup = window.open("", "Word Frequency Count", "width=420,height=600"); popup.document.write(html);})();
```

## Beautify a JSON page

Beautifies a JSON page, for example from an API response.

```js
javascript: !(() => {document.querySelector("pre").innerText = JSON.stringify(JSON.parse(document.querySelector("pre").innerText), null, 2)})()
```

## Show internal and external links

Highlights internal and external links, external: blue, red: internal, orange: the same URL

```js
javascript:!function(){var n,t;for(n=0;t=document.links[n];++n)t.style.color=["blue","red","orange"][e(t,location)];function e(n,t){return n.hostname!=t.hostname?0:a(n.pathname)!=a(t.pathname)||n.search!=t.search?1:2}function a(n){return(n=("/"==n.charAt(0)?"":"/")+n).split("?")[0]}}();
```

## List all links

Lists all links on the current page in a new popup window

```js
javascript:WN7z=open('','Z6','width=400,height=200,scrollbars,resizable,menubar');DL5e=document.links;with(WN7z.document){write('<base target=_blank>');for(lKi=0;lKi<DL5e.length;lKi++){write(DL5e[lKi].toString().link(DL5e[lKi])+'<br><br>')};void(close())}
```

## Load script

Loads a script from a URL into the current page

```js
javascript:{  let s = document.createElement("script");  s.src = prompt("Script location:");  document.body.appendChild(s);}
```


## Open all links

Opens all links on the page after prompting

```js
javascript:(function(){var n_to_open,dl,dll,i; function linkIsSafe(u) { if (u.substr(0,7)=='mailto:') return false; if (u.substr(0,11)=='javascript:') return false; return true; } n_to_open = 0; dl = document.links; dll = dl.length; for(i = 0; i < dll; ++i) { if (linkIsSafe(dl[i].href)) ++n_to_open; } if (!n_to_open) alert ('no links'); else { if (confirm('Open ' + n_to_open + ' links in new windows?')) for (i = 0; i < dll; ++i) if (linkIsSafe(dl[i].href)) window.open(dl[i].href); } })();
```

## Open in WayBack machine

Opens the current page in the wayback machine

```js
javascript: void(location.href = 'http://web.archive.org/web/' + location.href);
```

## Open repo in website
Opens the current GitHub repo in its username.github.io/repo counterpart
```js
javascript:(() => {    let gh = window.location.href.match(/(?:http|https)+:\/\/github\.com\/([^\.\/]+)\/([^\.\/]+)(?:.+)?/);    window.location.href = `https://${gh[1]}.github.io/${gh[2]}`;})();
```


## Remove colors
Removes most colors from the current page allow much better readability
```js
javascript: (function() {var newSS, styles = '* { background: white ! important; color: black !important } :link, :link * { color: #0000EE !important } :visited, :visited * { color: #551A8B !important }';if (document.createStyleSheet) {document.createStyleSheet("javascript:'" + styles + "'");} else {newSS = document.createElement('link');newSS.rel = 'stylesheet';newSS.href = 'data:text/css,' + escape(styles);document.getElementsByTagName("head")[0].appendChild(newSS);}})();
```

## Search site
Search the current site for a search term using google's site: keyword
```js
javascript:(function(){  window.location.href = 'https://google.com/search?q=site:' + new URL(window.location.href).hostname +  ' ' + prompt('What are you searching for?');})();
```

## Speed up video
Constantly tries to speed up the currently playing video.
```js
javascript:setInterval(() => document.querySelector("video").playbackRate = (window.speed || (window.speed = +prompt("New speed", 10))), 50)
```

## Split horizantally
Split the current page horizantally
```js
javascript:document.write('<HTML><HEAD></HEAD><FRAMESET ROWS=\'50%,*\'><FRAME SRC=' + location.href + '><FRAME SRC=' + location.href + '></FRAMESET></HTML>');document.close();
```

## Split vertically
Split the current page vertically
```js
javascript:document.write('<HTML><HEAD></HEAD><FRAMESET COLS=\'50%,*\'><FRAME SRC=' + location.href + '><FRAME SRC=' + location.href + '></FRAMESET></HTML>')
```

## View passwords
View all passwords in forms on the current page
```js
javascript: (function() {var s, F, j, f, i;s = "";F = document.forms;for (j = 0; j < F.length; ++j) {f = F[j];for (i = 0; i < f.length; ++i) {if (f[i].type.toLowerCase() == "password") s += f[i].value + "\n";}}if (s) alert("Passwords in forms on this page:\n\n" + s);else alert("There are no passwords in forms on this page.");})();
```

## Headers
Print headers on the response to the current page in the console
```js
javascript:fetch(location.href).then(r => Object.fromEntries(r.headers.entries())).then(console.table)
```

## Make page editable
Make the page editable

```js
javascript: document.body.contentEditable = 'true';document.designMode = 'on';void 0
```

## Stop page editing
Stop editing the page

```js
javascript: document.body.contentEditable = 'false';document.designMode = 'off';void 0
```

## H2 Tags na Consola

```javascript
javascript:(function() {
  var h2Tags = document.getElementsByTagName('h2');
  for (var i = 0; i < h2Tags.length; i++) {
    console.log(h2Tags[i].textContent.trim());
  }
  console.log('Total <h2> tags:', h2Tags.length);
})();

```
