## CSS命名规范及优缺点总结

> css不同于编程语言，其命名都是全局性质的。在构建大型项目的同时，容易出现覆盖，重复，语意不清等情况。为了解决这些问题，就必须引入css的命名规范和编写风格来解决和约束css的这些缺点。

常见的css命名规范有以下几种：

### OOCSS
   
    引入编程语言的思维，抽象化css,分离结构。
    比如一个按钮组件

    .button {
        color: red;
        border-radios: 20px;
        padding: 10px;
        box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
    }
从复用性（DRY）角度考虑，我们可以写成

    .button {
        color: red;
    }
    .button-radios: {
        border-radios: 20px;
    }
    .p10 {
        padding: 10px;
    }
    .shadow {
        box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
    }

使用OO的思维来编写组件可以大量复用css代码，类名丰富可以增加代码的可读性。但是在大型项目中，很容易出现原子化的情况，并且类名的增多会带来维护和html文件变大的问题。

### SMACSS

SMACSS针对css提出了3条总的原则
* css分类
* 命名规则
* 最小化适配深度

具体到每一条而言，即：

- css分类（Categorizing CSS Rules）
这是SMACSS的核心内容，SMACSS将css分为5个类别，分别为
    1. _base rule_ tag select的样式，定义全局的，最基础的样式（css reset也在其中）。
    2. _lay out_ 描述页面中的各类具体元素。比如层级系统（header sidebar footer）,栅格系统等都属于布局样式。
    3. _module rule_ 可以在各个场景下重复使用的独立模块。
    4._state rule_ 用来描述某一个元素在特定状态下的外观，比如tab页选中可以添加`is-active`，消息组件可以添加`message-success`和`message-error`之类的特定属性。
    5._theme rule_ 可选的主题样式之类的，将需求中的这些样式单独抽离，根据外部条件来动态设置。
- 命名规则（name rules）
    命名规则是说在考虑class命名的时候，体现其对应的类别。
    比如layout rule 用`layout-`或者`l-`的前缀/state rule的时候用`is-`的前缀/theme rule的时候用`theme-`的前缀
- 最小化适配深度
    简而言之就是将耦合度降低到最低程度。
    比如`.button span {}`中有继承选择器，对DOM结构是有一定的依赖程度的。
    当然解耦程度越低越会增加额外的代码阅读负担。

### BEM 
BEM即block element modifier这三块，核心的思想就是组建化，BEM通过块，元素，修饰符的约束来确保类名的唯一。
* Block 所属组件名称
* Element 组件内元素名称
* Modifier 元素或组件修饰符

比如一个表单元素块，按照常规我们会写成如下形式
```
<form class="search full">
    <input type="text" class="field">
    <input type="submit" value="search" class="button">
</form>
```
而按照BEM的规则，我们可以写成如下的代码

```
<form class="search search--full">
    <input type="text" class="search--text__field">
    <input type="submit" value="search" class="search--submit__button">
<form>

```
相比而言代码的可读性也是提高了不少。
公司的项目中是使用了预处理器scss，在scss中嵌套使用BEM规范的话，可以选择使用@at-root来实现
```
<!-- before -->
.block {
    @at-root #{&}__element{

    }
    @at-root #{&}--modifier{

    }
}
```
```
<!-- after -->
.block {

}
.block-element {

}
.block__modifier {

}
```
BEM 通过简单的命名规则使得关联类名元素语义性、可读性更强，利于项目管理和多人协作；同时 BEM 方案中并没有嵌套，所有类名最浅深度，并不会出现嵌套过深难以覆盖的情况，易于维护、复用；缺点则是实际使用中，维护 BEM 的命名确实需要一些成本，很多时候命名反而成了一件难事。