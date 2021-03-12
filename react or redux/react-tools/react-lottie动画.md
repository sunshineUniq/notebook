```
npm install --save react-lottie
```

Import pinjump.json.json as animation data

```javascript
// UncontrolledLottie.jsx
import React, { Component } from 'react'
import Lottie from 'react-lottie'
import animationData from '../lotties/4203-take-a-selfie.json'
 
class UncontrolledLottie extends Component {
 
 
  render(){
 
    const defaultOptions = {
      loop: true,
      autoplay: true, 
      animationData: animationData,
      rendererSettings: {
        preserveAspectRatio: 'xMidYMid slice'
      }
    };
 
    return(
      <div>
        <h1>Lottie</h1>
        <p>Base animation free from external manipulation</p>
        <Lottie options={defaultOptions}
              height={400}
              width={400}
        />
      </div>
    )
  }
}
 
export default UncontrolledLottie
```

`animationData`一个带有导出的动画数据的对象，在本例中为json文件

`autoplay` -一个布尔值，确定是否一旦准备就绪就开始播放

`loop`一个布尔值或数字，它确定动画是否重复或应该重复多少次

`rendererSettings`配置数据

```javascript
// ControlledLottie.jsx
import React, { Component } from 'react'
import Lottie from 'react-lottie'
import animationData from '../lotties/77-im-thirsty.json'
 
class ControlledLottie extends Component {
  state = {isStopped: false, isPaused: false}
 
  render(){
    const buttonStyle = {
      display: 'inline-block',
      margin: '10px auto',
      marginRight: '10px',
      border: 'none',
      color: 'white',
      backgroundColor: '#647DFF',
      borderRadius: '2px',
      fontSize: '15px'
 
    };
 
    const defaultOptions = {
      loop: true,
      autoplay: true, 
      animationData: animationData,
      rendererSettings: {
        preserveAspectRatio: 'xMidYMid slice'
      }
    };
 
    return(
      <div className="controlled">
        <h1>Controlled Lottie</h1>
        <p>Uses state manipulation to start, stop and pause animations</p>
        <Lottie options={defaultOptions}
              height={400}
              width={400}
              isStopped={this.state.isStopped}
              isPaused={this.state.isPaused}
        />
        <button style={buttonStyle} onClick={() => this.setState({isStopped: true})}>Stop</button>
        <button style={buttonStyle} onClick={() => this.setState({isStopped: false, isPaused: false })}>Play</button>
        <button style={buttonStyle} onClick={() => this.setState({isPaused: !this.state.isPaused})}>Pause</button>
      </div>
    )
  }
}
 
export default ControlledLottie
```

`isStopped`一个布尔值，指示动画是否处于活动状态

`isPaused`一个布尔值，指示动画是否已暂停