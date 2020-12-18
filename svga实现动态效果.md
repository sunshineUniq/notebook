SVGA 是一种同时兼容 iOS / Android / Flutter / Web 多个平台的动画格式。

## Install

- ### Prebuild JS

Add `<script src="https://cdn.jsdelivr.net/npm/svgaplayerweb@2.3.1/build/svga.min.js"></script>` to your.html

- ### NPM

1. `npm install svgaplayerweb --save`
2. Add `require('svgaplayerweb')` to `xxx.js`

## 使用

- add div tag

```javascript
<div id="demoCanvas" style="styles..."></div>
```

- load animation

```javascript
var player = new SVGA.Player('#demoCanvas');
var parser = new SVGA.Parser('#demoCanvas'); // Must Provide same selector eg:#demoCanvas IF support IE6+
parser.load('rose_2.0.0.svga', function(videoItem) {
    player.setVideoItem(videoItem);
    player.startAnimation();
})
```

## 自动播放

```javascript
<div src="rose_2.0.0.svga" loops="0" clearsAfterStop="true" style="styles..."></div>
```

## API

```javascript
player.setImage('http://yourserver.com/xxx.png', 'ImageKey');
player.setText('Hello, World!', 'ImageKey');
player.setText({ 
    text: 'Hello, World!', 
    family: 'Arial',
    size: "24px", 
    color: "#ffe0a4",
    offset: {x: 0.0, y: 0.0}
}, 'ImageKey'); // customize text styles.
```



