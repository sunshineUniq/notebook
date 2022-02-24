## Systemjs模块化解决方案

在微前端架构中，微应用被打包为模块，但浏览器不支持模块化，需要使用 systemjs 实现浏览器中的模块化。

systemjs 是一个用于实现模块化的 JavaScript 库，有属于自己的模块化规范。

在开发阶段我们可以使用 ES 模块规范，然后使用 webpack 将其转换为 systemjs 支持的模块。

案例：通过 webpack 将 react 应用打包为 systemjs 模块，在通过 systemjs 在浏览器中加载模块。

webpack 编译es6 动态引入 import() 时不能传入变量，例如dir =’path/to/my/file.js’ ； import(dir) , 而要传入字符串 import(‘path/to/my/file.js’)，这是因为webpack的现在的实现方式不能实现完全动态。

var a = ()=> {

Eval(var b = )

}

f4b17bd66ae2326d282fe878be098abaa48f70df

e47ec7e36b43601f97e69288c2610a98a3893d18

[6b341d4e55f](https://bitbucket.agoralab.co/projects/NEON/repos/rte_portal/pull-requests/41/commits/6b341d4e55ff5a3c12c022cd64389ee8b68baf5f)

[f4b17bd66ae](https://bitbucket.agoralab.co/projects/NEON/repos/rte_portal/pull-requests/41/commits/f4b17bd66ae2326d282fe878be098abaa48f70df)

[e47ec7e36b4](https://bitbucket.agoralab.co/projects/NEON/repos/rte_portal/pull-requests/41/commits/e47ec7e36b43601f97e69288c2610a98a3893d18)

[ae85284537d](https://bitbucket.agoralab.co/projects/NEON/repos/rte_portal/pull-requests/41/commits/ae85284537d0a0a21e4ba1dc2527535960a7842e)

[08eda6bc889](https://bitbucket.agoralab.co/projects/NEON/repos/rte_platform/commits/08eda6bc8895541a786cdf0caf8d81bcb8e8ddb1)

[fee162854bf](https://bitbucket.agoralab.co/projects/NEON/repos/rte_platform/commits/fee162854bfa6cff2a1a79885476b900d6005624)feat: use rteHttpGet fetch and fix eslintrc path

git --no-pager diff fee162854bf 08eda6bc889 |grep '^[+-]' | wc -l

git --no-pager diff fee162854bf 08eda6bc889 |grep '^diff' | wc -l





git --no-pager diff e47ec7e36b4 08eda6bc889 |grep '^[+-]' | wc -l



git --no-pager diff e47ec7e36b4 ae85284537d |grep '^diff' | wc -l

git --no-pager diff 6b341d4e55f f4b17bd66ae |grep '^[+-]' | wc -l

