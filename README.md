# sass_test
Sass初始练习书写

//utf-8编码格式，确保编译scss Line 2: Invalid GBK character "\xE7"

/*sass编写中100_即100%*/
//$height100_:100%;
//$absolute:absolute;
//$relative:relative;
//$none:none;
//$block:block;
//$fl:left;
//$fr:right;
//$center:counter;
//$table:table;

/* 要注意表单元素并不继承父级 font 的问题 */

body,
button,
input,
select,
textarea {
font: 12px/1.5 "Microsoft YaHei", "Arial", "黑体", "宋体", sans-serif;
}

input,
select,
textarea {
font-size: 100%;
}
/* 去掉 table cell 的边距并让其边重合 */

table {
border-collapse: collapse;
border-spacing: 0;
}
/* ie bug：th 不继承 text-align */

th { text-align: inherit; }
/* 去除默认边框 */

fieldset,
img { border: $none; }
/* ie6 7 8(q) bug 显示为行内表现 */

iframe { display: $block; }
/* 去掉列表前的标识，li 会继承 */

ul, ol { list-style: $none; }
/* 默认不显示下划线，保持页面简洁 */

ins, a,
a:hover { text-decoration: $none; }
/* 去除 ie6 & ie7 焦点点状线 */

a:focus,
*:focus { outline: $none; }
/* 设置显示和隐藏，通常用来与 js 配合 */

.hide { display: $none; }

.block {
display: $block;
}

@charset "utf-8";

$pcFont: "Microsoft Yahei", "Helvetica Neue", Helvetica, Arial, sans-serif;

$defaultColor: #333;

$mobileFont:  "Microsoft Yahei", "Helvetica Neue", Helvetica, Arial, sans-serif, '微软雅黑';

$browser: null;



%display {

    display:inline-block;

    *display:inline;

    *zoom:1;

}

%ext-indent {

    font-size:0;

    text-indent:-99999em;

    overflow:hidden;

}

%box-sizing {

    -webkit-box-sizing:border-box;

    -moz-box-sizing:border-box;

    -o-box-sizing:border-box;

    box-sizing:border-box;

}

// 绝对居中

@mixin center($width, $height) {

    position: absolute;

    left:50%;

    top:50%;

    width:$width;

    height:$height;

    margin:(-$height / 2) 0 0 (-$width / 2);

}

// 设置动画名称

@mixin animation($aniName) {

    -webkit-animation:$aniName;

    -moz-animation:$aniName;

    -o-animation:$aniName;

    animation:$aniName;

}

// 设置延迟执行时间

@mixin animation-delay($time) {

    -webkit-animation-delay:$time;

    -moz-animation-delay:$time;

    -o-animation-delay:$time;

    animation-delay:$time;

}

// 设置阴影

@mixin box-shadow($shadow...) {

    -webkit-box-shadow:$shadow;

    -moz-box-shadow:$shadow;

    -o-box-shadow:$shadow;

    box-shadow:$shadow;

}

// 圆角

@mixin border-radius($radius) {

    -webkit-border-radius:$radius;

    -moz-border-radius:$radius;

    -o-border-radius:$radius;

    border-radius:$radius;

}

// 设置过渡

@mixin transition($transition...) {

    -webkit-transition:$transition;

    -moz-transition:$transition;

    -o-transition:$transition;

    transition:$transition;

}

// 设置旋转位置

@mixin transform-origin($origin...) {

    -webkit-transform-origin:$origin;

    -moz-transform-origin:$origin;

    -o-transform-origin:$origin;

    transform-origin:$origin;

}

@mixin transform($transform...) {

    -webkit-transform:$transform;

    -moz-transform:$transform;

    -o-transform:$transform;

    transform:$transform;

}



// 设置关键帧

@mixin keyframes($name) {

    @-webkit-keyframes #{$name} {

        $browser: '-webkit-'; @content;

    }

    @-moz-keyframes #{$name} {

        $browser: '-moz-'; @content;

    }

    @-o-keyframes #{$name} {

        $browser: '-o-'; @content;

    }

    @keyframes #{$name} {

        $browser: ''; @content;

    }

}





/* ********************重置样式 reset******************** */



/* *********PC端********** */

*{

    margin:0;

    padding:0;

}

ul, ol {

    list-style:none;

    margin:0;

    padding:0;

}

body {

    font:14px/1.5 $pcFont;

    width:100%;

    color: $defaultColor;

    overflow-x:hidden;

}

h1,h2,h3,h4,h5,h6 {

    font-weight:normal;

}

/* 清除点击出现虚拟框 */

a{

    outline:none;

    text-decoration:none;

    -webkit-tap-highlight-color:rgba(0,0,0,0);

    &:focus{

        outline:0;

    }

    &:link, 

    &:visited {

        color: $defaultColor;

        text-decoration:none;

    }

}

a img {

    border:none;

}

input, textarea, select {

    outline:none;

    font:12px/1.5 $pcFont;

}



/* 清除浮动 */

.clearfix {

    *zoom:1;

    &:after {

        display:block;

        content:"\200B";

        clear:both;

        height:0;

    }

}





/* *********移动端********** */

body, dl, dd, h1, h2, h3, h4, h5, h6, p, form, figure, figcaption{

//不建议使用 *

    margin:0;

    padding:0;

}

/* 改变盒子模型 */

section, article, nav, aside, footer, header, div, p, ul, li, input, textarea {

    display: block;

    @extend %box-sizing;

}

html, body {

    -webkit-user-select: none;

    /* 禁止选中文本 */

    user-select: none;

    -webkit-text-size-adjust: 100%;

    /* iphone禁用文字大小调整 */

    -ms-text-size-adjust: 100%;

}

html {

    font-size:625%;

}

body{

    font:.16rem/1.6 $mobileFont; 

    color:#333;

    -webkit-overflow-scrolling: touch;

}

h1, h2, h3, h4, h5, h6{

    font-weight:normal;

}

/* 清除点击虚拟框 */

a, div, p, span, ul, li, i, img, input {

    outline:0;

    text-decoration:none;

    -webkit-tap-highlight-color:rgba(0,0,0,0);

}

a:focus{

    outline:0;

}

a:link,a:visited{

    color:$defaultColor;

    text-decoration:none;

}

a img{

    border:0 none;

}

a, img {

    -webkit-touch-callout: none;

    /* 禁止长按链接与图片弹出菜单 */

}

input, textarea, select {

    outline: none;

    color: $defaultColor;

    font-family: $mobileFont;

}

input {

    /* 清除 iphone 中 input 默认样式 */

    -webkit-appearance: none;

}

/* 清除浮动 1*/

.clearfix {

    *zoom:1;

    &:after {

        display:block;

        content:"\200B";

        clear:both;

        height:0;

    }

}

/* 清除浮动 2*/

.clearfix {

    *zoom:1;

    &:before &:after {

    content:""; 

    display:table; 

    }

    &:after {

        clear:both;

    }

}

可以利用sublime ctrl+b进行转换css；；或者koala编译等
