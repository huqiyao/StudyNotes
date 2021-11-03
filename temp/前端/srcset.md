# srcset

[张鑫旭解说](https://www.zhangxinxu.com/wordpress/2014/10/responsive-images-srcset-size-w-descriptor/)

[MDN详细解释](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)

为了在不同设备尺寸 和 不同分辨率 情况下，都能响应式加载合适的图片



## 三种场景

- 加载不同尺寸的图片（宽度）

  ```html
  <img srcset="pic1.jpg 320w,
               pic2.jpg 480w,
               pic3.jpg 800w"
       sizes="(max-width: 320px) 280px, 
              (max-width: 480px) 480px,
              800px",
       src="pic3.jpg"
       alt=""/>
  ```

  浏览器获得设备大小信息

  sizes= " [查询条件] 图片插槽大小, ..."，设备信息与查询条件惰性匹配，所以顺序调整好

  在srcset中选择最接近插槽大小的图片

  设置src以兼容不支持srcset的浏览器



- 加载相同尺寸，不同像素的图片

  ```html
  <img srcset="pic1.jpg,
               pic2.jpg 1.5x,
               pic3.jpg 2x"
       src="pic1.jpg"
       alt=""/>
  ```

  浏览器获得设备的分辨率(即知道几个设备像素代表一个css像素)

  在srcset中选择最接近设备分辨率的图片

  设置src兼容不支持srcset的浏览器



- 美术设计场景(为不同显示大小的情况，选用处理过构图的图片，如在移动端用只显示主体人物的图片)

  ```html
  <picture>
      <source media="max-width:480px" srcset="pic1.png"></source>
  	<source media="min-width:960px" srcset="pic2.png"></source>
  	<img src="pic3.png" alt=""/>
  </picture>
  ```

  img 标签是必需的，否则不会显示图片

  其中的src，在浏览器不支持或者不匹配媒体查询时，会被用到

  

## 为什么不用css 或 js 实现

当浏览器开始加载一个页面, 它会在主解析器开始加载和解析页面的 CSS 和 JavaScript 之前先下载 (预加载) 任意的图片。这是一个非常有用的技巧，平均下来减少了页面加载时间的20%。但是, 这对响应式图片一点帮助都没有, 所以需要类似 `srcset`的实现方法。因为你不能先加载好img元素后, 再用 JavaScript 检测可视窗口的宽度，如果觉得大小不合适，再动态地加载小的图片替换已经加载好的图片，这样的话, 原始的图像已经被加载了, 然后你又加载了小的图像, 这样的做法对于响应式图像的理念来说，是很糟糕的。

**浏览器解析过程是怎样的？**