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

demo

```javascript
import React from 'react'
import Modal from 'react-modal'
import SVGA from 'svgaplayerweb';
import './index.scss'
const titleFinishReview = 'https://web-data.zmlearn.com/image/rCpxZzq1JfNxWUKFtwLaG5/title_finishreview%403x.png'

export default function FinishTaskAlert({
  isOpen
}) {
  const renderSvga = () => {
    const player = new SVGA.Player('#finishZmgReviewSvga')
    const parser = new SVGA.Parser('#finishZmgReviewSvga')
    console.log('player', player);
    console.log('parser', parser);
    parser.load('https://web-data.zmlearn.com/media/gx1cmZ7acSbbh7HgdiEKH1/finish_zmg_review.svga', function (videoItem) {
      player.loops = 1; // 设置循环播放次数是1,0是无限播放
      player.clearsAfterStop = false;
      player.fillMode = 'Backward';
      player.setVideoItem(videoItem);
      player.startAnimation();
    })
  }

  return (
    <Modal className="finish-zmg-review-task-alert" ariaHideApp={false} isOpen={isOpen} onAfterOpen={() => { renderSvga() }}>
      <img src={titleFinishReview} className="title-review-img" />
      <div id="finishZmgReviewSvga" className="finish-svga-wrapper"></div>
      <p className="svga-desc">复习完成了，奖励5个能量果</p>
    </Modal>
  )
}
```

注意：modal上的svga初始化在onAfterOpen内进行不然 获取不到dom元素