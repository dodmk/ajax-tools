# ajax-tools

<img src="./icons/ajax-tools.png" width="300">  

[![](https://img.shields.io/chrome-web-store/v/kphegobalneikdjnboeiheiklpbbhncm.svg?logo=Google%20Chrome&logoColor=white&color=blue&style=flat-square)](https://chrome.google.com/webstore/detail/ajax-interceptor-tools/kphegobalneikdjnboeiheiklpbbhncm)   
一个拦截ajax请求并修改返回结果的chrome插件。  

**主要功能：**   
- [x] 支持XMLHttpRequest、fetch  
- [x] 支持正则表达式、HTTP请求方法匹配  
- [x] 支持拦截404请求，修改响应结果 
- [x] 支持返回结果Json、JavaScript方式编辑（内置mock.js） 
- [x] 支持JavaScript方式时通过arguments拿到原始接口信息，简单编程增加mock场景  

## 安装
谷歌商店：https://chrome.google.com/webstore/detail/ajax-interceptor-tools/kphegobalneikdjnboeiheiklpbbhncm  
直接下载：https://raw.githubusercontent.com/PengChen96/ajax-tools/master/kphegobalneikdjnboeiheiklpbbhncm.crx

## 使用
![o1.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a88c304eadc54915bd7a75ea2fe3ee86~tplv-k3u1fbpfcp-watermark.image?)  
![o2.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bc051954c02946148e4dc750c9fb3ace~tplv-k3u1fbpfcp-watermark.image?)  

### 通过JS编辑返回结果
代码是通过`new Function(responseText)`生成函数然后执行，所以JS方式返回结果就是return的值。

示例：
```js
const data = [];
for (let i = 0; i < 10; i++) {
  data.push({ id: i });
}
return {
  data
}
```
**支持 [mock.js](https://github.com/nuysoft/Mock/wiki/Getting-Started) 生成数据**

示例：
```js
const data = Mock.mock({
    // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
    'list|1-10': [{
        // 属性 id 是一个自增数，起始值为 1，每次增 1
        'id|+1': 1
    }]
});
return {
  data
}
```

**支持通过arguments拿到原始接口信息，可以简单编程增加mock场景**
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/25494da9e62d4e34ba66fce28987124a~tplv-k3u1fbpfcp-watermark.image?)  
示例：
```js
let { method, payload, originalResponse } = arguments[0];
if (method === 'get') { // 请求方式
  // do something
}
if (payload) { // 入参 { queryStringParameters，requestPayload }
  // do something
}
return originalResponse;
```

## License
MIT License.
