## 可能你会觉得获取可视区宽高不是很简单吗
> 原生js获取高度不就是就window.innerHeight一句话的事，可是真的这么简单吗
### 来看个测试页面,如果页面带有横向纵向的滚动条，我们打印出各个高度进行查看对比
> 顺便你也可以看看document.body和document.documentElement在各个浏览器的差异;document.documentElement返回的是整个文档的根节点即 html标签；document.body 返回的是DOM对象里的body子节点，即 body 标签
```js
console.log('document.documentElement.clientHeight-' + document.documentElement.clientHeight);
console.log('document.documentElement.scrollHeight-' + document.documentElement.scrollHeight);
console.log('document.documentElement.offsetHeight-' + document.documentElement.offsetHeight);
console.log('document.body.clientHeight-' + document.body.clientHeight);
console.log('document.body.scrollHeight-' + document.body.scrollHeight);
console.log('document.body.offsetHeight-' + document.body.offsetHeight);
console.log('window.innerHeight-' + window.innerHeight);
```

1. ie8下各个值

![image](https://note.youdao.com/yws/api/personal/file/B96D15BBD4B94E918E4E4ECD18DBA701?method=download&shareKey=b919e21ede3b3a1d4de1208d3953096c)

2. ie9下各个值

![image](https://note.youdao.com/yws/api/personal/file/4F73E4B3B4D84B30A196F93D42970543?method=download&shareKey=c44deef19255b7283976aa1e33a61f4c)

3. ie10跟ie9一样不列图了
5. ie11下各个值

![image](https://note.youdao.com/yws/api/personal/file/42904268B0324DCAAE557D0A663E5A38?method=download&shareKey=647fd400a996ff97b70d4ff4a6f9980e)
6. 火狐浏览器下各个值

![image](https://note.youdao.com/yws/api/personal/file/C96821CF793B458F8392B100913A070C?method=download&shareKey=6d5b9f601db4b9e32dce052ae068be84)

7. chorme浏览器下各个值

![image](https://note.youdao.com/yws/api/personal/file/91788A33D9674B7D894EE4C1B046301F?method=download&shareKey=5263d06058fd51dda41de66d14b98bd1)


#### 通过以上各图对比不难看出（先排除ie8）
> window.innerHeight = document.documentElement.clientHeight + 滚动条高度； 

> 如果没有滚动条则window.innerHeight = document.documentElement.clientHeight
#### 在来说说ie8
> ie8比较特殊不支持window.innerHeight并且html还自带有2像素的边框;
可以通过document.documentElement.offsetHeight - 2 * 2得到window.innerHeight的值

> 所以ie8的window.innerHeight = document.documentElement.offsetHeight - 2 * 2 = document.documentElement.clientHeight + 滚动条高度。

> 如果没有滚动条window.innerHeight =  document.documentElement.offsetHeight - 2 * 2 = document.documentElement.clientHeight

## 所以获取可视区的高度不是简单的window.innerHeight，真正的可视区高度不应该包括滚动条
```js
/**
*  获取视口宽高 兼容兼容到ie8
*  @param {boolean} flag 标识返回的宽高是否包含滚动条
*  @return {object} {widht: xxx, height: xxx} 视口宽高
/ 
function getViewPort (flag) {
    if (typeof flag === 'undefined') {
        return {
            width: document.documentElement.clientWidth,
            height: document.documentElement.clientHeight
        };
    }
    if (flag === true) {
        // ie8 html 有2像素边框 上下, 左右 4像素
        return {
            width: window.innerWidth || document.documentElement.offsetWidth - 2 * 2,
            height: window.innerHeight || document.documentElement.offsetHeight - 2 * 2
        };
    }
}
```

## 获取文档的宽高呢
> 通过以上各图的对比，整个文档的高度，可以通过document.documentElement.scrollHeight来获取各个浏览器都比较一致，你也不必纠结到底是用document.body 还是用document.documentElement; 用clientHeight还是offsetHeight

```js
/**
*  获取文档宽高 兼容兼容到ie8
* 
*  @return {object} {widht: xxx, height: xxx} 视口宽高
/ 
function getDocumentPort (flag) {
    return {
        width: document.documentElement.scrollWidth,
        height: document.documentElement.scrollHeight
    };
}

