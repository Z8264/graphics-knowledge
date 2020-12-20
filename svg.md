# SVG 知识文档

## SVG 属性

### viewBox

```
viewBox="x, y, width, height"
```
### preserveAspectRatio

```
preserveAspectRatio = "alignment [meet | slice]"
```

| alignment | 可选值                 |
| --------- | ---------------------- |
| x         | `xMin`, `xMid`, `xMax` |
| y         | `yMin`, `yMid`, `mMax` |

| 说明符 | 描述                       |
| ------ | -------------------------- |
| meet   | 缩放适应（保持高比例）     |
| slice  | 剪裁图片（保持高比例）     |
| none   | 平铺（不保留图像宽高比例） |


## 形状

| 元素     | 描述   | 属性                        |
| -------- | ------ | --------------------------- |
| line     | 直线   | x1, y1, x2, y2              |
| rect     | 矩形   | x, y, width, height, rx, ry |
| circle   | 圆形   | cx, cy, r                   |
| ellipse  | 椭圆   | cx, cy, rx, ry              |
| polyline | 折线   | points                      |
| polygon  | 多边形 | points                      |

## 路径

| 命令 | 名称                            | 描述                 |
| ---- | ------------------------------- | -------------------- |
| M    | moveto                          | 移动                 |
| L    | lineto                          | 绘制直线             |
| H    | horizontal lineto               | 水平直线             |
| V    | vertical lineto                 | 垂直直线             |
| C    | curveto                         | 三次贝塞尔曲线       |
| S    | smooth curveto                  | 平滑三次方贝塞尔曲线 |
| Q    | quadratic Bezier curve          | 二次方贝塞尔曲线     |
| T    | smooth quadratic Bezier curveto | 平滑二次方贝塞尔曲线 |
| A    | elliptical Arc                  | 椭圆弧线             |
| Z    | closepath                       | 闭合路径             |

## 样式

填充与边框

| 属性              | 可选值                    | 描述                   |
| ----------------- | ------------------------- | ---------------------- |
| stroke            | [color]                   | 线颜色                 |
| stroke-width      | [number]                  | 线宽                   |
| stroke-opacity    | [0~1]                     | 线透明度               |
| stroke-dasharray  | [number array]            | 虚线                   |
| stroke-dashoffset | [number]                  | 虚线开始的位置         |
| stroke-linecap    | `butt`, `round`, `square` | 线头尾形状             |
| stroke-linejoin   | `miter`, `round`, `bevel` | 链接线形状             |
| stroke-miterlimit |                           | 相交处显示宽度与线宽比 |
| fill              | [color]                   | 填充颜色               |
| fill-opacity      | [0~1]                     | 填充透明度             |
| fill-rule         | `nonzero`, `evenodd`      | 填充规则               |


## 文字

元素 text & tspan

```
<text x="" y="">
    TEXT <tspan> text </tspan>
</text>
```

坐标

| 属性 | 描述   |
| ---- | ------ |
| x    | 横坐标 |
| y    | 纵坐标 |

样式

| 属性            | 可选值                                          | 描述     |
| --------------- | ----------------------------------------------- | -------- |
| font-family     |                                                 | 字体     |
| font-size       |                                                 | 字号     |
| font-weight     | `bold`, `normal`                                | 粗细     |
| font-style      | `italic`,`normal`                               | 样式     |
| text-decoration | `none`, `underline`, `overline`, `line-through` | 装饰     |
| word-spacing    |                                                 | 单词间距 |
| letter-spacing  |                                                 | 字母间距 |

对齐方式

| 属性        | 可选值                   | 描述         |
| ----------- | ------------------------ | ------------ |
| text-anchor | `start`, `middle`, `end` | 文本对齐方式 |

文本长度

| 属性         | 可选值                        | 描述         |
| ------------ | ----------------------------- | ------------ |
| textLength   | [number]                      | 文本长度     |
| lengthAdjust | `spacing`, `spacingAndGlyphs` | 字符间距模式 |

纵向文本

| 属性                       | 可选值   | 描述                                 |
| -------------------------- | -------- | ------------------------------------ |
| writing-mode               | `tb`     | top to bottom                        |
| glphy-orientation-vertical | [number] | 默认值为90，即纵向排列的字符旋转90度 |

文本路径 textPath

```
<defs>
    <path id="path" d="..."/>
</defs>

<text>
    <textPath xlink:href="#path">
        ...
    </textPath>
</text>
```

## 文档结构

| 元素   | 描述                                                                   |
| ------ | ---------------------------------------------------------------------- |
| g      | 用来组合对象的容器，添加到 g 元素的属性会被其所有的子元素继承。        |
| use    | 在 SVG 文档内取得目标节点，并复制它们。                                |
| defs   | 定义需要重复使用的图形元素，在 defs 元素中定义的图形元素不会直接呈现。 |
| symbol | 用来定义一个图形模板对象，它可以用一个 use 元素实例化。                |
| image  | 图像信息                                                               |


## 接口方法

### SVGLocatable （svg / g)

| 方法/属性                         | 描述                                            |
| --------------------------------- | ----------------------------------------------- |
| getBBox()                         | 元素的位置和边界，{x,y,width,height}            |
| getCTM()                          | 返回SVBMatrix，当前元素到最近坐标系统的变换     |
| getScreenCTM()                    | 返回SVBMatrix，当前元素到屏幕坐标系统的变换     |
| getTransformToElement(SVGElement) | 返回SVBMatrix，当前元素到指定元素坐标系统的变换 |

### SVGPathElement (path)

| 方法/属性                  | 描述                                 |
| -------------------------- | ------------------------------------ |
| getTotalLength()           | 计算路径长度                         |
| getPointAtLength(distance) | 返回距离起点 distance 单位的点 {x,y} |

### SVGAnimatedPoints (polygon / polyline)

| 方法/属性 | 描述                         |
| --------- | ---------------------------- |
| points    | 返回一个SVGPointList，点列表 |

