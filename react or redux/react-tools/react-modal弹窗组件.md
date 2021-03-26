```javascript
$ npm install --save react-modal
$ yarn add react-modal
```

```javascript
/*
  * react-modal最终生成的DOM默认是作为body的子元素。
  *   以此例来说，最终位置
  *   <div className="App">
        <div onClick={this.toggle}>点我</div>
      </div>
 
      Modal单独生成的DOM（位置可变，下面有说）
      <div portal>
        ...
      </div>
  *
  * Modal单独生成的DOM，4层div
  * |div Portal 没有默认样式
  *
  *   |div  overlay 有默认的内联样式
  *       position: fixed;
          top: 0px;
          left: 0px;
          right: 0px;
          bottom: 0px;
          background-color: rgba(255, 255, 255, 0.75);
  *
  *       |div content 有默认的内联样式
  *           绝对定位等一大推
  *
  *           |div 指<Modal></Model>标签中包含的自定义元素
  * */

```

```javascript
 <div id="App">
        <button onClick={this.openModal}>打开模态框</button>
        <button onClick={this.openRef}>测试获取DOM节点</button>
        <Modal
          isOpen={this.state.showModal}   // modal容器是否显示
          overlayClassName="overlay"   // 指定div overlay的classname。（可覆盖默认样式）
          className="content"   // 指定div content的classname。（可覆盖默认样式）
          style={{ overlay: {}, content: {} }}  // div overlay和content的样式，也可以直接在这里指定。
          onAfterOpen={this.handleAfterOpenFunc}  // 在模态框打开后，执行的函数
 
          // 当请求关闭模态框时，执行的函数！
          // （模态框不一定会关闭，因为是否关闭取决于isOpen特性，如果在当前函数中，改变了isOpen:false，才会关闭）
          //   只有两种情况，才会执行目标函数。
          //   1，当shouldCloseOnOverlayClick为true时，在div overlay上点击，会触发
          //   2，当shouldCloseOnEsc为true时，并且选中了div content
          //        也就是说，如果shouldFocusAfterRender也为true，按esc键就会触发。
          //        或者，shouldFocusAfterRender为false时，手动选中div content，按esc键就会触发。
          onRequestClose={this.handleAfterCloseFunc}
          closeTimeoutMS={1000} // 指定，在发出关闭命令后，模态框延迟关闭的时间，默认0
          shouldCloseOnOverlayClick={true}   // 指定在div overlay上点击，是否关闭模态框，默认true
          shouldFocusAfterRender={false}  //指定模态框出现后，是否被默认选中，默认true
          shouldCloseOnEsc={true}  // 指定按esc键，是否关闭模态框，默认true（要选中div content，才有效）
          shouldReturnFocusAfterClose={false} // 指定是否应将焦点恢复到，显示前具有焦点的元素，默认true
 
          overlayRef={node => this.overlayRef = node}   // 可以获取div overlay的整个DOM节点
          contentRef={node => this.contentRef = node}   // 可以获取div content的整个DOM节点
          parentSelector={this.getParent}   // 配合指定的方法，指定"Modal单独生成的DOM"的父级元素，该demo中，指定到了div App中
          ariaHideApp={false}   //如果没有添加到某个DOM节点中，就会显示警告，为了不显示警告，设置为false，默认true。
 
          // portalClassName="protal"   // 指定div Portal的classname（因为没有默认样式，所以一般不用指定）。
          // contentLabel="一个demo"   // 显示在div content的自定义属性:aria-label="通告给屏幕的内容"。
        >
          <button onClick={this.closeModal}>关闭模态框</button>
        </Modal>
      </div>
    );

```

990 0.8w

1190 1.2w