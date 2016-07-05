#1、阶乘
##1.0递归的形象解释

```
  天下有奇族人姓计，长生不老。一日其孙问其父：吾之18代祖名何？
  
  其父不明，父问其父
  
  其父不明，父问其父
  
  其父不明，父问其父
  
  其父不明，父问其父
  
  ...
  
  晌后，其18代祖回其子：你猜 
  
  然其回其子：你猜
  
  然其回其子：你猜
  
  然其回其子：你猜
  
  然其回其子：你猜
  
  ……
  终，计姓末代孙知其18代祖名“你猜”
  
  
  此奶，递归
```
##1.2、递归的实例
### 求阶乘的递归
```
  function jc(num){

     if(num == 1 ){
        //此处为必须的出口
        return 1
      }
      return num*jc(num-1)
  }
/以上为阶乘的递归写法
```

### 为求和的递归
```
function sum(num){
    if(num == 1){
        //此处为出口
        return 1
     }
     return num  +  sum(num - 1)
}
/求和
```
### 为斐波拉切数列的递归


斐波拉切数列
规律...
fb(5)=5;
fb(7)=13,
fb(9)=34
·····
```
function fb(num){
    if(num == 1 || num ==2){
       return 1
      //出口
     }
     return fb(num-1) + fb(num -2)
}
```

# 2、单页面开发的方法 之 队列机制 -->微信单页面项目


>该项目它一些精华的地方，重要性逐步降低：

### 2.1. 它用到队列任务机制，实现一个一步一步的路由，相当于是一个状态机。
### 2.2 、进度条插件的使用，用了第三方插件：Pace.js
### 2.3、我们用到手势库的框架
```
hammer.js --->进行手势的操作
```
### 2.4、用到了canvas,进行一些操作
### 2.5、 其他的就是css布局上的一些操作

## 具体内容即实现方法
### 项目为微信项目，（单页面）核心模块，即进行手势操作，完成摊煎饼的整个过程。
#### 核心路由模块： -->单页面进行不同模块的显示和隐藏，并在相应的页面进行操作，实现相关的功能。

## 代码设计核心：任务队列
```
### 以下为代码设计：
    var taskQuene = ['首页', '锅底页', '胡面', '打鸡蛋', '把鸡蛋摊开', '涂酱', 
                      '画番茄酱','撒葱花','包煎饼', '进入分享页']; -->任务队列

    var taskQueneMap = {
    	//核心路由模块的映射存储列表
    	'首页': homeModule,
    	'锅底页': potModule,
    	'胡面': panModule,
    	'打鸡蛋': eggModule
    	....
      ...
      ..
    };-->映射存储列表
    
    
            基础模块,后面的模块均以此为基类进行创建，实现继承，并对于同名的不同属性方法，进行相关的重载
          var homeModule = {
                	enter: function(){
                		this.ready();//该模块以及准备好了
                	},
                	leave:function(){
                
                	},
                	ready: function(){
                
                	}
            };-->基类1
            
            potModule = {
              	enter: function(){
              		this.ready();//该模块以及准备好了
              	},
              	leave:function(){
              
              	},
              	ready: function(){
              
              	}
            };-->基类2
    
    //--->  代码设计如上，之后进行具体实现
```   
## 具体实现：
```
### 第一步： 实现一个加载进度条
    可以利用很多第三方插件去实现，但是要找一个最好：简单、方便、可配置
    Pace.js   --> 很好用的进度条插件
### 第二步:监听触控的操作
    使用第三方插件进行监听
    hammer.js-->一移动端手势库
    用以监听相关的点击，拖拽，拖动等手势操作
### 第三步：移动端的JQ库
    使用第三方移动端专用的库 
    zepto.js库-->移动端jquery库
### 第四步：监听手势触摸的延迟，提高移动端的手势操作的流畅性。
    fastclick.js-->第三方移动触摸监听
    处理移动端 click 事件 300 毫秒延迟的问题
    Zepto的设计目的是提供 jQuery 的类似的API，但并不是100%覆盖 jQuery。 Zepto设计的目的是有一个5-10k的通用库、下载并快速执行、有一个熟悉通用的API，
    所以你能把你主要的精力放到应用开发上。
    
### 第五步：核心代码
  功能实现的主要逻辑以及方法
  //任务队列
	var sceneQueue = ["home", "pan", "cake", "egg", "yolk", "sauce", "chilli", "onion", "crackers", "cover_down", "cover_up", "cover", "share"];
	//状态队列的实现
	sceneQueue.current = null;
	sceneQueue.index = -1;
	sceneQueue.next = function () {
	    sceneQueue.current && sceneQueue.current.exit 
        && sceneQueue.current.exit.call(sceneQueue.current);
	    sceneQueue.index++;
	    var scene = sceneMap[sceneQueue[sceneQueue.index]];
	    scene && scene.enter();
	    sceneQueue.current = scene;
	};
	
	
```


