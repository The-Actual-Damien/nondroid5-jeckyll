---
layout: post
title: 画像のアスペクト比を維持して拡縮
---

jQueryの場合

```
<script type="text/javascript" src="/path/to/jquery.js"></script>
<script type="text/javascript">
    jQuery.event.add(window, "load", function(){
        var fw = 100;        //fixed width
        var fh = 100;        //fixed height
        var sl = 'img.hoge'; //selector
        $(sl).each(function(){
            var w = $(this).width();
            var h = $(this).height();
            if (w >= h) {
                $(this).width(fw);
            } else {
                $(this).height(fh);
            }
        });
    });
</script>
 
<img src="sample1.jpg" class="hoge">
<img src="sample2.jpg" class="hoge">
<img src="sample3.jpg" class="hoge">
```

javascriptの場合

```
<script>
var maxWidth  = 300;
var maxHeight = 300;
var elements = document.getElementsByTagName("img");
for(i=0;i<elements.length;i++){
  var width  = elements[i].width;
  var height = elements[i].height;
  if (width > height) {
    elements[i].width = Math.min(width, maxWidth);
  } else {
    elements[i].height = Math.min(height, maxHeight);
  }
}
</script>
```
