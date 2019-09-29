# Microsoft商城网页

#### 引用框架插件：bootstrap  Jquery  iScroll.js

示例：![](.\images\16720405657274.png)

设置响应式加载图片

```js
$(function(){
    $('[data-toggle="tooltip"]').tooltip();
    var items=$(".carousel-inner .item");
    /*监听屏幕的大小改变*/
    $(window).on("resize",function(){
        var width=$(window).width();
        if(width>=768){/*说明非移动端*/
            $(items).each(function(index,value){
                var item=$(this);
                var imgSrc=item.data("largeImage");
                console.log(imgSrc);
                item.html($('<a href="javascript:;" class="pcImg"></a>').css("backgroundImage","url('"+imgSrc+"')"));
            });
        }
        else{
            $(items).each(function(index,value){
                var item=$(this);
                var imgSrc=item.data("smallImage");
                item.html('<a href="javascript:;" class="mobileImg"><img src="'+imgSrc+'" alt="..."></a>');
            });
        }
    }).trigger("resize");

    var startX,endX;
    var carousel_inner=$(".carousel-inner")[0];
    var carousel=$(".carousel");

    carousel_inner.addEventListener("touchstart",function(e){
        startX= e.targetTouches[0].clientX;
    });
    carousel_inner.addEventListener("touchend",function(e){
        endX= e.changedTouches[0].clientX;
        if(endX-startX > 0){
            /*上一张*/
            carousel.carousel('prev');
        }
        else if(endX-startX < 0){
            /*下一张*/
            carousel.carousel('next');
        }
    });

    /*计算产品块导航项的原始宽度*/
    var ul=$(".wjs_product .nav-tabs");
    var lis=ul.find("li");
    var totalWidth=0;//总宽度
    lis.each(function(index,value){
        totalWidth=totalWidth+$(value).innerWidth();
        console.log($(value).innerWidth());
    });
    ul.width(totalWidth);
    var myScroll = new IScroll('.tabs_parent',{
        scrollX: true, scrollY: false
    });
});
```

