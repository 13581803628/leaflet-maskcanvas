# Leaflet MaskCanvas

一个基于 canvas 的 leaflet 图层，用来展示大量覆盖数据集。

__特性__:

* 基于 Canvas tile 图层
* 即便对于大量数据都有高性能，因为采用了 [四叉树](https://en.wikipedia.org/wiki/Quadtree) 原理
* 自定义颜色和圆大小

## 演示

查看在线案例 http://domoritz.github.com/vbb-coverage/.

## 用法

### 安装

* 添加 MaskCanvas 和 Quadtree 库。

```html
<script src="QuadTree.js"></script>
<script src="L.TileLayer.MaskCanvas.js"></script>
```

你也可以使用包管理器 [bower](http://bower.io/) 来安装这个插件: `bower install leaflet.maskcanvas`

* 初始化 maskCanvas 图层

```javascript
L.TileLayer.maskCanvas();
```

* 为这个图层设置数据集

```javascript
layer.setData(data);
```

* 最后，将图层添加到地图上

```javascript
map.addLayer(layer);
```

数据格式是一个简单数组: `[lat, lng]` 。举个例子 `[[51.50,-0.28],[51.51,-0.07],[51.51,-0.07],[51.54,-0.29]]`。我建议你使用异步方式加载数据，这样做可以可以保持页面持续响应。当数据一旦加载到页面上，你就可以把它绘制到图层中并显示它。

### 可选选项

MaskCanvas 图层支持所有的 [Leaflet canvas 图层参数](http://leafletjs.com/reference.html#tilelayer-options)，这些参数都可以传给  `L.TileLayer.maskCanvas`。你可能想去设置这个图层。

其他可用选项:

```javascript
var layer = L.TileLayer.maskCanvas({
       radius: 5,  // 以像素为单位或者以米为单位的半径，详见 useAbsoluteRadius
       useAbsoluteRadius: true,  // true: 半径单位为米， false:半径单位为像素
       color: '#000',  // 这个图层的颜色
       opacity: 0.5,  // 未覆盖区域的透明度
       noMask: false,  // true:正常填充圆，false:蒙版圆 mask
       lineColor: '#A00'   // noMask 设置为 true 时有效，圆的轮廓颜色

});
```
## Leaflet 1.0-dev

对于即将来临的leaflet新版本，有一些基于 L.GridLayer 的实现更改。
你所需要做的就是用 `L.GridLayer.maskCanvas` 替换 `L.TileLayer.maskCanvas`。

新的leaflet 1 .0-Dev版本的 `L.GridLayer.maskCanvas` 像之前的一样支持相同的选项。
另外，你可以为每个数据点指定不同的渲染半径，就像你在例子中看到的那样 http://loggia.at/leaflet-maskcanvas/demo/index-1.0-dev.html

## 截屏

![screenshot](https://raw.github.com/domoritz/leaflet-maskcanvas/master/screenshot.png "Screenshot showing mask canvas layer")

## 开发者

使用 `python -m SimpleHTTPServer` 指令来本地运行演示例子，并且随后打开地址 http://0.0.0.0:8000/demo 。

## 相关知识

四叉树的实现主要来自于 https://github.com/jsmarkus/ExamplesByMesh/tree/master/JavaScript/QuadTree 并且轻微更改。由 Mike Chambers 组织实现。
