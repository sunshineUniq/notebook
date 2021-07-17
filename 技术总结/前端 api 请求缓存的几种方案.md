#### 数据缓存

第一次请求数据后保存在本地，后续使用数据就从缓存里获取

```javascript
const dataCache = new Map()
async getData(keys) {
  const data = dataCache.get(keys);
	if(!data){
		const res = await request.get('/api')
		// 数据处理
    data = ...; 
    // 设置数据缓存
    dataCache.set(keys, data)
	}
  return data
}
```



#### promise缓存

```javascript
const promiseCache = new Map()
getData() {
  const key = 'home'
  let promise = promiseCache.get(key)
  if(!promise){
    promise = request.get('/getData').then((res) => {
      // 对res进行操作
    }).catch((error) => {
      // 请求出错，将改promise从cache中删除，以避免第二次请求继续出错
      promiseCache.delete(key)
      return Promise.reject(error)
    })
  }
  return promise
}
```

#### 多promise缓存

```javascript
const querys = {
	wares: 'getWares',
  names: 'getNames',
}

const promiseCache = new Map()
async queryAll(queryApiName){
  // 判断传入的是否是数组
  const queryIsArray = Array.isArray(queryApiName)
  // 统一处理成数组
  const apis = queryIsArray? queryApiName : [queryApiName]
  const promiseApi = []
  apis.forEach((api)=> {
    let promise = promiseCache.get(api)
    if(promise){
      promiseApi.push(promse)
    }else{
      promise = request.get(querys[api]).then((res) => {
        // 对res进行操作
        // 。。。
      }).catch((error) => {
        promiseCache.detele(api)
        return Promise.reject(error)
      })
    }
     promiseCache.set(api, promise)
     promiseApi.push(promise)
  })
  return Promise.all(promiseApi).then(res => {
    return queryIsArray? res : res[0]
  })
}
```

#### 添加时间有关的缓存

约定个时间清除旧数据

采用类做数据缓存，并添加过期时长

- 定义持久化类

```javascript
class ItemCache() {
  construct(data, timeout){
    this.data = data;
    this.timeout = timeout;
    this.cacheTime = new Date().getTime()
  }
}
```



