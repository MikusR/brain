# Bookmarklet — copy selection + URL as Markdown link

made by gpt5

```js
(function () {
  function mdEscape(str) {
    return String(str || "")
      .replace(/\\/g, "\\\\")
      .replace(/\[/g, "\\[")
      .replace(/\]/g, "\\]")
      .replace(/\s+/g, " ")
      .trim();
  }

  var selection =
    (window.getSelection && window.getSelection().toString()) || "";
  var linkText = selection || document.title || window.location.hostname;
  linkText = mdEscape(linkText);

  var url = window.location.href;
  var md = "[" + linkText + "](" + url + ")";

  function copyToClipboard(text) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(text).catch(function () {
        // fallback if permission denied
        fallbackCopy(text);
      });
    } else {
      fallbackCopy(text);
    }
  }

  function fallbackCopy(text) {
    var ta = document.createElement("textarea");
    ta.value = text;
    // avoid page jump / visible focus
    ta.style.position = "fixed";
    ta.style.left = "-9999px";
    document.body.appendChild(ta);
    ta.select();
    try {
      document.execCommand("copy");
    } catch (e) {
      console.error("Copy failed", e);
      alert("Copy failed — see console for details.");
    }
    document.body.removeChild(ta);
  }

  copyToClipboard(md);
})();
```

```bookmarklet
javascript:(function(){function m(s){return String(s||'').replace(/\\/g,'\\\\').replace(/\[/g,'\\[').replace(/\]/g,'\\]').replace(/\s+/g,' ').trim()}var t=(window.getSelection&&window.getSelection().toString())||'';var l=t||document.title||window.location.hostname;var md='['+m(l)+']('+location.href+')';function c(x){if(navigator.clipboard&&navigator.clipboard.writeText){navigator.clipboard.writeText(x).catch(function(){f(x)})}else f(x)}function f(x){var ta=document.createElement('textarea');ta.value=x;ta.style.position='fixed';ta.style.left='-9999px';document.body.appendChild(ta);ta.select();try{document.execCommand('copy')}catch(e){console.error('Copy failed',e);alert('Copy failed — see console.')}document.body.removeChild(ta)}c(md);})();
```
