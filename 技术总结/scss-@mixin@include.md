使用```@mixin```定义一个样式，可以进行复用，复用参考下面代码

```./common.scss```

```scss
@mixin library_item{
	.....
}
```

```./index.scss```

```scss
@import ./common.scss
  .normal-item{
     @import library_item
  }
```

