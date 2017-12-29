
## CSS长度单位
<!-- 理解 rm、rem、pt、px、% 这 些单位的区别 -->
> css中只有两种类型的单位长度：相对长度和绝对长度。
相对长度是指一个长度相对于另一个长度的属性。
绝对长度指的是一个固定的长度值，代表着一个真实的物理尺寸。

### 绝对长度单位
#### pt
pt就是point，是一个标准的长度单位。定义上1pt=1/72英寸，因此他们我们所熟悉的厘米一样，可以明确的指出1pt的长度是多少。（1pt=1/72inch=0.35146mm）
### 相对长度单位
#### em
>em相对于当前对象内文本的**字体尺寸**，会继承父级元素的字体大小。如果当前对行内文本的字体尺寸没有被人为设置，则相对于浏览器的默认字体尺寸。通常而言，浏览器的默认字体大小基本都是16px。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css单位</title>
    <style>
        div {
            font-size: 2em;
        }
    </style>
</head>
<body>
测试文字 body (16px)
<div class="div1">
    测试文字 div1 (32px)
    <div class="div2">
        测试文字 div2 (64px)
        <div class="div3">
            测试文字 div3 (128px)
        </div>
    </div>
</div>
</body>
</html>
```
效果如下：
![em展示效果](/imgs/css1.png)
####rem
em是根据父级元素的**字体**大小而变化的，但是如果嵌套多层后，它的大小就很难计算了。rem就是用来解决这个问题的，它与em的区别就是rem是相对于根元素而言，因此他不受父类的影响，在新的现代浏览器上都得到了良好的支持。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css单位</title>
    <style>
        div {
            font-size: 2rem;
        }
    </style>
</head>
<body>
测试文字 body (16px)
<div class="div1">
    测试文字 div1 (32px)
    <div class="div2">
        测试文字 div2 (32px)
        <div class="div3">
            测试文字 div3 (32px)
        </div>
    </div>
</div>
</body>
</html>
```
![rem展示效果](/imgs/css2.png)

####px（pixel）
px是相对于一个设备像素（屏幕分辨率）的长度单位，通常而言Windows用户所使用的分辨率一般都是96像素/英寸；而MAC用户所使用的分辨率一般是指72像素/英寸。由于pt在定义上是1/72英寸的关系，所以在72dpi的系统上时1pt=1px，但是在96dpi的规则下明显不适用，像素密度明显变低。所以转换公式就变成了1px=0.75pt。因为这个原因，在许多时候都建议屏幕显示的设计使用px作为字体的单位。
#### %（百分比）
百分比是相对于包含它最近的父元素的高度和宽度所言（继承）
![百分比展示效果](/imgs/css3.png)
