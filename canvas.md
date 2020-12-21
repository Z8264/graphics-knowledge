# canvas 知识文档
## HTMLCanvasElement

| 属性   | 描述     |
| ------ | -------- |
| height | 画布高度 |
| width  | 画布宽度 |

| 方法       | 参数                           | 描述             |
| ---------- | ------------------------------ | ---------------- |
| getContext | contextType, contextAttributes | 上下文环境       |
| toBlob     | callback, mimeType, quality    | Blob 对象        |
| toDataURL  | mimeType, quality,             | data URI，base64 |


## CanvasRenderingContext2D

| 属性                     | 可选值                                                  | 描述               |
| ------------------------ | ------------------------------------------------------- | ------------------ |
| canvas                   | -                                                       | 当前上下文的canvas |
| fillStyle                | [color], [gradient], [pattern]                          | 填充样式           |
| font                     | eg. `12px sans-serif`                                   | 字体字号           |
| globalAlpha              | [0~1]                                                   | 全局透明度         |
| globalCompositeOperation |                                                         | 混合模式           |
| lineCap                  | `buzz`, `round`, `square`                               | 线条端点样式       |
| lineDashOffset           | [number]                                                | 设置虚线偏移量     |
| lineJoin                 | `miter`, `round`, `bevel`                               | 线条转角样式       |
| lineWidth                | [number]                                                | 线宽               |
| miterLimit               | [number]                                                | `miter`，转角长度  |
| shadowBlur               | [number]                                                | 阴影模糊程度       |
| shadowColor              | [color]                                                 | 阴影颜色           |
| shadowOffsetX            | [number]                                                | 阴影水平偏移       |
| shadowOffsetY            | [number]                                                | 阴影垂直偏移       |
| strokeStyle              | [color], [gradient], [pattern]                          | 路径或形状描边     |
| textAlign                | `left`, `right`, `center`, `start`, `end`               | 文本对齐方式       |
| textBaseline             | `top`, `hanging`, `middle`, `alphabetic`, `ideographic` | 对齐的基线         |
### 画布状态

| 方法    | 参数 | 描述                       |
| ------- | ---- | -------------------------- |
| save    | -    | 保存当前画布状态，放在栈顶 |
| restore | -    | 从栈顶弹出画布状态         |

### 矩形绘制

| 方法       | 参数       | 描述     |
| ---------- | ---------- | -------- |
| clearRect  | x, y, w, h | 清除像素 |
| strokeRect | x, y, w, h | 矩形描边 |
| fillRect   | x, y, w, h | 填充矩形 |

### 路径

| 方法      | 参数 | 描述                             |
| --------- | ---- | -------------------------------- |
| beginPath | -    | 开始一个新的路径                 |
| closePath | -    | 闭合路径，把起点和终点用直线连接 |

| 方法             | 参数                         | 描述               |
| ---------------- | ---------------------------- | ------------------ |
| moveTo           | x, y                         | 移动到，路径起始点 |
| lineTo           | x, y                         | 绘制直线           |
| arcTo            | x1, y1, x2, y2, radius       | 绘制圆弧           |
| bezierCurveTo    | cp1x, cp1y, cp2x, cp2y, x, y | 绘制贝塞尔曲线     |
| quadraticCurveTo | cpx, cpy, x, y               | 绘制二次贝塞尔曲线 |

| 方法    | 参数                                                                  | 描述     |
| ------- | --------------------------------------------------------------------- | -------- |
| arc     | x, y, radius, startAngle, endAngle, anticlockwise                     | 圆弧路径 |
| ellipse | x, y, radiusX, radiusY, rotation, startAngle, endAngle, anticlockwise | 椭圆路径 |
| rect    | x, y, width, height                                                   | 矩形路径 |

| 方法              | 参数           | 描述                                                |
| ----------------- | -------------- | --------------------------------------------------- |
| fill              | fillRule, path | 填充                                                |
| stroke            | path           | 描边                                                |
| clip              | fillRule, path | 剪裁                                                |
| drawFocusIfNeeded | element, path  | 指定元素处于focus状态，让当前路径或指定路径轮廓高亮 |

| 方法            | 参数 | 描述                   |
| --------------- | ---- | ---------------------- |
| isPointInPath   | -    | 某个点是否在当前路径中 |
| isPointInStroke | -    | 某个点是否在描边路径中 |

### 虚线
| 方法        | 参数     | 描述         |
| ----------- | -------- | ------------ |
| getLineDash | -        | 获取虚线设置 |
| setLineDash | segments | 设置虚线     |

### 坐标系转换

| 方法         | 参数             | 描述                       |
| ------------ | ---------------- | -------------------------- |
| rotate       | angle            | 旋转                       |
| scale        | x, y             | 缩放                       |
| translate    | x, y             | 对坐标系整体位移           |
| transform    | a, b, c, d, e, f | 对坐标系进行变化，效果累加 |
| setTransform | a, b, c, d, e, f | 重组当前坐标系变化         |

### 文字

| 方法        | 参数                 | 描述             |
| ----------- | -------------------- | ---------------- |
| fillText    | text, x, y, maxWidth | 填充文字         |
| strokeText  | text, x, y, maxWidth | 描边文字         |
| measureText | text                 | 返回测量文本数据 |


### 图像

| 方法            | 参数                                                         | 描述                                  |
| --------------- | ------------------------------------------------------------ | ------------------------------------- |
| drawImage       | image, [sx, sy, sWidth, sHeight, ] dx, dy, [dWidth, dHeight] | 图像                                  |
| createImageData | width, height, imagedata                                     | 创建一个新的ImageData对象             |
| getImageData    | sx, sy, sWidth, sHeight                                      | 返回一个ImageData对象                 |
| putImageData    | imagedata, dx, dy, dirtyX, dirtyY, dirtyWidth, dirtyHeight   | 将给定ImageData对象的数据绘制到位图上 |

### 渐变&纹理
| 方法                 | 参数                   | 描述             |
| -------------------- | ---------------------- | ---------------- |
| createLinearGradient | x0, y0, x1, y1         | 创建线性渐变对象 |
| createRadialGradient | x0, y0, r0, x1, y1, r1 | 创建径向渐变对象 |
| createPattern        | image, repetition      | 创建纹理对象     |

## 示例


``` html
<canvas id="canvas" width="600" height="300"></canvas>```
```

``` javascript
const canvas = document.getElementById('canvas')
const ctx = canvas.getContext('2d');
ctx.font = '38pt Arial';
ctx.fillStyle = 'cornflowerblue';
ctx.strokeStyle = 'blue';
ctx.fillText('Hello Canvas', canvas.width/2 -150, canvas.height/2- + 15);
ctx.strokeText('Hello Canvas', canvas.width/2 - 150, canvas.height/2 + 15);
```

