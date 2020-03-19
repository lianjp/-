## HTML方面

`备注： + 代表被问到的次数，没有 + 代表自己整理了，但没被问到`

#### 1.HTML5 有哪些新元素？

​	常用的如header、footer、main、nav和新的音频元素audio、video图像元素canvas、svg等



#### 2.HTML开头的DOCTYPE有什么用

​	告诉浏览器以何种模式来渲染文档，如果不写会以混乱模式解析



## css方面

#### 1.自适应布局的方法+

​	rem/calc/vw/lib-flexble  原理：所有尺寸都以rem为单位，用js根据视口宽度动态改变html根元素的font-size大小。



#### 2.flex布局及常用的属性++

* justify-content设置在容器上，定义子元素在主轴上的对齐方式

  flex-start/flex-end/center

* align-items设置在容器上，定义子元素在交叉轴上的对齐方式

  flex-start/flex-end/center

* flex-wrap定义子元素是否换行

  nowrap/wrap/wrap-reverse



#### 3.position有那些值，各个值有哪些区别+

* static 默认值，没有定位
* relative：相对定位，保留原来的位置
* absolute：绝对定位，相对于最近一级定位不是static的父元素定位，不保留原来的位置
* fixed：相对于浏览器视口定位
* sticky：粘性定位，当元素在屏幕内，表现为relative，就要滚出显示器屏幕的时候，表现为fixed。



#### 4.盒模型++

​	由content+padding+border+margin构成。有2种解析形式，标准盒模型content-box：设置宽高是指content部分的宽高。IE盒模型border-box：设置宽高是指content+padding+border部分的宽高。可以用过box-sizing属性设置解析形式。



#### 5.css3新增选择器

* 属性选择器 (a[foo = "bar"])
* 伪类选择器 (a: hover, li:nth-child(n))



#### 6.css权重

​	!important > 内联样式 > id > class > 伪类



#### 7.css3动画效果有哪些？

​	transform（2/3D转换）/transition（缓动）/animation（动画）



#### 8.transform里有哪些对元素的操作

​	旋转，平移，放大，倾斜等



#### 10.垂直居中+

* 绝对定位和负margin

  ```css
  #foo{
      position:relative;
  }
   
  #bar{
      position:absolute;
      top:50%;
      left:50%;
      height：100px;
      width:100px;
      margin:-50px 0 0 -50px;
  }
  ```

* 绝对定位+transform

  ```css
  #bar{      
          position:absolute;
          left:50%;    /* 定位父级的50% */
          top:50%;
          transform: translate(-50%,-50%); /*自己的50% */
      }
  ```

* flexbox

  ```css
  #foo {
      display: flex;
      justify-content:center;
      align-items:center;
  }
  
  ```




#### 11.如何设置元素的bfc？+

1. overflow：hidden；
2. display：inline-block；
3. display；flow-root；



#### 12.伪元素和伪类的区别？+

![区别](https://github.com/lianjp/-/blob/master/%E4%BC%AA%E7%B1%BB%E5%8F%8A%E4%BC%AA%E5%85%83%E7%B4%A0%E7%9A%84%E5%8C%BA%E5%88%AB.jpg)
