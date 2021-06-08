父盒子是伸缩布局， 如果父盒子没有设固定宽度，子盒子的内容超出父盒子会将父盒子撑开

```javascript
  <style>
    .conto1{
      max-width: 500px;
      min-width: 200px;
      width: 50%;
      height: 50%;
      display: flex;
      border: 1px solid red;
    }
    .flexbox{
      flex: 1;
      border: 2px solid yellow;
      display: flex;
      flex-direction: column;
    }
    .flexbox:hover{
      background-color: red;
    }
    .flexbox .top{
      flex: 1;
    }
    .flexbox .bottom{
      height: 22px;
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <div class="conto1">
    <div class="flexbox"></div>
    <div class="flexbox"></div>
    <div class="flexbox"></div>
    <div class="flexbox"></div>
    <div class="flexbox"></div>
    <div class="flexbox">
      <div class="top">1</div>
      <div class="bottom">我是啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊</div>
    </div>
  </div>
</body>
```

解决方案： 给子盒子设置最小宽度

```javascript
    .flexbox{
      min-width: 20px; // width: 0
      flex: 1;
      border: 2px solid yellow;
      display: flex;
      flex-direction: column;
    }
```

