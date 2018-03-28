### 小结
- **可以使用变量**
```SCSS
$topMargin:5px;
// 注：变量也可以引用变量
```
- **选择器可以嵌套书写**
```SCSS
#content{
  .article{
     h1{
       color:#333;
     }
     p{
       margin-top:5px;
     }
  }
  .aside{
    background:#ff0;
  }
}
```
- **父选择器 `&`**
```SCSS
// 用于嵌套书写时，想要完成伪类选择器等情况
#item a{
  img{
    url:"xxx.jpg";
  }
  &:hover{
    color:#f00;
  }
}
```
- **群组选择器嵌套**
```SCSS
.container{
  h1,h2,h3{
    color:#333;
  }
}
nav,aside{
  a{
    color：blue;
  }
}
```
- **子组合选择器、同层组合选择器（ > 、 + 和 ~ ）**
```SCSS
article{
  ~ article{}
  > section{}
  dl > {
    dt{}
    dd{}
  }
}
```
- **属性嵌套**
```SCSS
nav{
  border:{
    style:solid;
    width:1px;
    color:#333;
  }
}
```
- **设置默认值 `!default`**
- **混合器 `@mixin`、`@include`**
```SCSS
@mixin rounded-corners{
  -moz-border-radius:5px;
  -webkit-border-radius:5px;
  border-radius:5px;
}
notice {
  @include rounded-corners;
  background:#333;
}
// 混合器可以传递参数，并且可以设置参数默认值
```
- **继承选择器 `@extend`**
```SCSS
.error{
  color:red;
}
.seriousError{
  @extend .error;
  border-width:3px;
}
```
