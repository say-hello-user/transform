# transform
自己对于css3 3d动画的主要几个知识理解

### 最主要的坐标轴图

![image](https://github.com/say-hello-user/transform/blob/master/img.png)

X轴，y轴，z轴的中心默认相对于元素的中心位置

旋转，平移的正负相对于坐标轴的正方向 顺时针为正 逆时针为负

例如 translateZ(45deg) 为正 相对于Z轴正方向视角的顺时针旋转 45度

 transform: rotateX(90deg) translateZ(150px);
 
 后面的坐标方向会在前面的影响下改变  例如上述语句  是坐标轴先沿着x轴的顺时针方向旋转90 此时该元素的坐标轴也整体沿着x轴的顺时针方向旋转90 所以此时translateZ(150px)是在之前旋转之后的方向上 沿着Z轴平移了150像素
 
 如果说rotateX/rotateY/rotateZ可以帮助理解三维坐标，则translateZ则可以帮你理解透视位置。

我们都知道近大远小的道理，对于没有rotateX以及rotateY的元素，translateZ的功能就是让元素在自己的眼前或近或远。比方说，我们设置元素perspective为201像素，如下：

perspective: 201px;
则其子元素，设置的translateZ值越小，则子元素大小越小（因为元素远去，我们眼睛看到的就会变小）；translateZ值越大，该元素也会越来越大，当translateZ值非常接近201像素，但是不超过201像素的时候（如200像素），该元素的大小就会撑满整个屏幕（如果父辈元素没有类似overflow:hidden的限制的话）。因为这个时候，子元素正好移到了你的眼睛前面，所谓“一叶蔽目，不见泰山”，就是这么回事。当translateZ值再变大，超过201像素的时候，该元素看不见了——这很好理解：我们是看不见眼睛后面的东西的！

例子代码: 

####旋转木马

```html
<div class="stage">
    <div class="container">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
    </div>
</div>
```

```css
 .stage{
          width: 800px;
          height: 200px;
          border:1px solid red;
          perspective: 800px;
          position: relative;
          margin: auto;
      }
        .container{
            transform-style: preserve-3d;
            width: 128px;
            height: 100px;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -64px;
            margin-top: -50px;
        }
      .container > div{
          width: 128px;
          height: 100px;
          color: white;
          text-align: center;
          font-size: 20px;
          position: absolute;
          top: 0px;
          left: 0px;
          background-color: red;
      }
      .container > div:nth-child(1){
          transform: rotateY(0deg) translateZ(195px);
      }
      .container > div:nth-child(2){
          transform: rotateY(40deg) translateZ(195px);
      }
      .container > div:nth-child(3){
          transform: rotateY(80deg) translateZ(195px);
      }
      .container > div:nth-child(4){
          transform: rotateY(120deg) translateZ(195px);
      }
      .container > div:nth-child(5){
          transform: rotateY(160deg) translateZ(195px);
      }
      .container > div:nth-child(6){
          transform: rotateY(200deg) translateZ(195px);
      }
      .container > div:nth-child(7){
          transform: rotateY(240deg) translateZ(195px);
      }
      .container > div:nth-child(8){
          transform: rotateY(280deg) translateZ(195px);
      }
      .container > div:nth-child(9){
          transform: rotateY(320deg) translateZ(195px);
      }
```

效果:

![image](https://github.com/say-hello-user/transform/blob/master/1.png)

####正方体

```html
<div class="stage2">
    <div class="rectContainer">
        <div class="page1"></div>
        <div class="page2"></div>
        <div class="page3"></div>
        <div class="page4"></div>
        <div class="page5"></div>
        <div class="page6"></div>
    </div>
</div>
```

```css
  .stage2{
          width: 800px;
          height: 600px;
          border:1px solid blue;
          perspective: 800px;
          position: relative;
          margin: auto;
      }
        .rectContainer{
            width: 300px;
            height: 300px;
            position: absolute;
            left: 50%;
            margin-left: -150px;
            top: 50%;
            margin-top: -150px;
            transform-style: preserve-3d;
            transform: rotateY(245deg) rotateX(45deg);
        }
        .page1,.page2,.page3,.page4,.page5,.page6{
            width: 300px;
            height: 300px;
            position: absolute;
            left: 0px;
            top: 0px;
        }
        .page1{
            transform: rotateY(0deg) translateZ(150px);
            background-color: red;
        }
      .page2{
          transform: rotateY(0deg) translateZ(-150px);
          background-color: blue;
      }
      .page3{
          transform: rotateX(90deg) translateZ(150px);
          background-color: yellow;
      }
      .page4{
          transform: rotateX(90deg) translateZ(-150px);
          background-color: #FFE1FF;
      }
      .page5{
          transform: rotateY(90deg) translateZ(150px);
          background-color: black;
      }
      .page6{
          transform: rotateY(90deg) translateZ(-150px);
          background-color: #B2DFEE;
      }
```

效果:

![image](https://github.com/say-hello-user/transform/blob/master/2.png)

