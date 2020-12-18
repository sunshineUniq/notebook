- 安装

```jsj s
npm install redux-saga
```

- 使用实例

  - 场景：点击按钮，请求接口

  - 按钮点击事件：点击按钮，派发一个新的action

    ```
    class UserComponent extends React.Component {
      ...
      onSomeButtonClicked() {
        const { userId, dispatch } = this.props
        dispatch({type: 'USER_FETCH_REQUESTED', payload: {userId}})
      }
      ...
    }
    ```

  - 使用saga监听USER_FETCH_REQUESTED， 触发接口请求

    ```js
    // saga.js
    import {call, put, takeEvery, takeLatest} from 'react-sage/effects'
    import Api from '...'
    
    // 请求用户信息
    function *fetchUser(action){
      try{
        const user = yield call(Api.fetchUser, action.payload.userId)
        yield put({type: "USER_FETCH_SUCCEEDED", user: user})
      }catch(error){
    		yield pur({type: "USER_FETCH_FAILED", message: error.message})
      }
    }
    
    // 监听所有的USER_FETCH_REQUESTED
    function *mySaga(){
      yield takeEvery('USER_FETCH_REQUESTED', fetchUser)
    }
    
    // 监听USER_FETCH_REQUESTED， 如果前一次的fetch pending, 取消前面pending的fetch, 只处理最后一次的fetch
    function *mySaga(){
      yield takeLastest('USER_FETCH_REQUESTED', fetchUser)
    }
    ```

  - run saga: 需要使用redux-saga将我们写的saga 关联到redux store	

    ```javascript
    import { createStore, applyMiddleware } from 'redux'
    import createSagaMiddleware from 'redux-saga'
    
    import reducer from './reducers'
    import mySaga from './sagas'
    
    // create the saga middleware
    const sagaMiddleware = createSagaMiddleware()
    // mount it on the Store
    const store = createStore(
      reducer,
      applyMiddleware(sagaMiddleware)
    )
    
    // then run the saga
    sagaMiddleware.run(mySaga)
    
    // render the application
    ```

    

