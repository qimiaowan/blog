# My blog
## 1. 对于闭包的理解
#### 内部函数在全局环境下被调用，并且内部函数影响到父函数的变量的时候，就一定产生闭包；
####                        例如：
####                        function add(){
####                           var a = 1;
####                           return function(){
####                               return a++;
####                           }
####                       }
####                       var b = add();
####                       console.log(b());//1
####                       console.log(b());//2
####
####                      闭包如果在外部被调用并且影响外部的函数变量时候，函数内部会形成AO对象。
####                       当执行完毕以后，执行环境销毁，但是活动对象由于被闭包函数引用，所以仍然保留。
####                       所以就会出现如上的答案

## 2. 寄生组合继承 记录：
#### function Parent (name) {
####    this.name = name;
#### }
#### Parent.prototype.getName = function () {
 ####   console.log(this.name)
#### }
#### function Child (name, age) {
####    Parent.call(this, name);   
####    this.age = age;
####
#### }
#### var child1 = new Child('dd', '18');
### 上面这个问题就是 访问不到Parent原型，这个问题可以用下面方法解决

#### function Parent (name) {
####    this.name = name;
#### }
#### Parent.prototype.getName = function () {
 ####   console.log(this.name)
#### }
#### function Child (name, age) {
####    Parent.call(this, name);   
####    this.age = age;
#### }
#### function f(){}
#### f.prototype = Parent.prototype;
#### Child.prototype = new f();
#### var child1 = new Child('dd', '18');
### 这样就可以了。

## 3. es5实现数组去重 记录：
#### [1,2,3,1,4,1,2,4,1].filter(function(ele,index,arr){
#### 
   ####  return index === arr.indexOf(ele);
####
#### })
### 原理也很简单 filter中 返回的是新数组，只要条件是true的 即可添加。

## 4.html5里面的scrollIntoView应用 2018.5.24
####  不传参数的情况下 类似a锚点
### 如果传参数 有2种格式 一种是布尔值 一种是对象 首先是布尔值：
#### 如果传true 元素的顶端将和其所在滚动区的可视区域的顶端对齐。若为false，元素的底端将和其所在滚动区的可视区域的底端对齐
#### 对象的话  首先ie是不支持的 
####   test.scrollIntoView({
####        block: 'start',
####        behavior: 'smooth'
####     });
#### Object型参数，这个对象有两个选项，也就是对象里面的key。block与之前的Boolean型参数一致，不过值不再是true和false，是更语义化的start和end。
#### 另一个选项是behavior,MDN上给出三个可取的值，分别是auto、instant与smooth。这个选项决定页面是如何滚动的，实测auto与instant都是瞬间跳到相应的#### 位置,smooth是有动画效果的
### 下面是个例子：
#### <script>
####        const scrollIntoView = document.querySelector(".scrollIntoView");
####        const chunk = document.querySelector(".chunk");
####        const scrollIntoViewIfNeededT = document.querySelector(".scrollIntoViewIfNeeded-top");
####        const scrollIntoViewIfNeededB = document.querySelector(".scrollIntoViewIfNeeded-bottom");
####       scrollIntoView.addEventListener("click",fun,false);
####        scrollIntoViewIfNeededT.addEventListener("click",funa,false);
####        scrollIntoViewIfNeededB.addEventListener("click",funb,false);
####        function fun(){
####            chunk.scrollIntoView(true);
####        }
####        function funa(){
####            chunk.scrollIntoViewIfNeeded(true); //在看不到chunk 的情况下点击才有效 会居中
####        }
####        function funb(){
####            chunk.scrollIntoViewIfNeeded(false); //在看不到chunk 的情况下点击才有效 会在上面也可能下面 看哪边离的近
####        }
####    </script>


 
