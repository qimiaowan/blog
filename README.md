# 我的博客
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
