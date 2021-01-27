### ReactDOM.render

```javascript
function render(element, container, callback) {
	// TODO: 入参校验
  return legacyRenderSubtreeIntoContainer(null, element, container, false, callback);
}
```

legacyRenderSubtreeIntoContainer

```javascript
function legacyRenderSubtreeIntoContainer(parentComponent, children, container, forceHydrate, callback) {
      var root = container._reactRootContainer;
  	var fiberRoot;
    if(!root){
         root = container._reactRootContainer = legacyCreateRootFromDOMContainer(container, forceHydrate);
    	fiberRoot = root._internalRoot;
        // TODO: ....
    }else{
         fiberRoot = root._internalRoot;
    	// TODO:
        
    }
     return getPublicRootInstance(fiberRoot);
}
```

legacyCreateRootFromDOMContainer

```javascript
function legacyCreateRootFromDOMContainer(container, forceHydrate){
    return createLegacyRoot(container, shouldHydrate ? {
   		 hydrate: true
  		} : undefined);
}
```

createLegacyRoot

```javascript
function createLegacyRoot(container, options) {
  return new ReactDOMBlockingRoot(container, LegacyRoot, options);
}
```

ReactDOMBlockingRoot

```javascript
function ReactDOMBlockingRoot(container, tag, options) {
  this._internalRoot = createRootImpl(container, tag, options);
}
```

createRootImpl

```javascript
function createRootImpl(container, tag, options) {
    // ...
    var root = createContainer(container, tag, hydrate);
    // ...
      return root;
}
```

createContainer

```javascript
function createContainer(containerInfo, tag, hydrate, hydrationCallbacks) {
  return createFiberRoot(containerInfo, tag, hydrate);
}
```

createFiberRoot

```javascript
function createFiberRoot(containerInfo, tag, hydrate, hydrationCallbacks) {
  var root = new FiberRootNode(containerInfo, tag, hydrate);
  var uninitializedFiber = createHostRootFiber(tag);
  root.current = uninitializedFiber;
  uninitializedFiber.stateNode = root;
  initializeUpdateQueue(uninitializedFiber);
  return root;
}
```

