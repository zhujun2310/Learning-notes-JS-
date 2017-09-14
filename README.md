# Learning-notes-JS-
-闭包closure（好处、弊端、应用场景）
  ·闭包是指有权访问另一个函数作用域中的变量的函数（高程3）；
  ·当函数可以记住并访问所在的词法作用域时，就产生了闭包，即使函数是在当前词法作用域之外执行（你不知道的javascript上卷）；
  ·优点：保护函数内的变量安全，加强封装
  ·缺点：内存常驻，使用不当很容易造成内存泄漏
  ·应用场景：模拟快级作用域，对象中创建私有变量
  ·闭包例子：
      function foo(){
        var a = 2;
        function bar(){
          console.log(a);
        }
        return bar;
      }
      var baz = foo();
      baz();//2   这就是闭包
  -内存泄漏
    ·内存泄漏是指一块被分配的内存既不能使用，又不能被回收，知道浏览器进程结束。
    ·当页面中元素被移除或者替换时，若元素绑定的事件仍没有被移除，在ie中不会作出恰当处理，此时需要手工移除事件，不然会存在内存泄漏。
    ·例子：
    function foo(){
      var e = document.getElementById('someElement');
      e.onclick = function(){
        alert(e.id);
      }
    }
    //由于页面始终会保存对DOM元素的引用，内存不会被回收，就会导致内存泄漏
    //修改为
    function foo(){
      var e = document.getElementById('someElement');
      var id = e.id;
      e.onclick = function(){
        alert(id);
      }
      e = null;
    }
    //这样解除对DOM的引用，确保正常回收其占用内存
  
-原型、原型链
  ·所有的引用类型（数组、对象、函数）都具有对象特质，即可自由扩展属性（除‘null’外）
  ·所有的引用类型（数组、对象、函数）都有一个-proto-（隐式原型）属性，属性值是一个普通的对象
  ·所有的函数都有一个prototype（显示原型）属性，属性值也是一个普通的对象
  ·所有引用类型，-proto-属性值都指向它的构造函数的prototype属性值
  ·当试图查找一个对象的某个属性时，如果这个对象本身没有这个属性，就会去它的-proto-（即它的构造函数prototype）中查找，如果没有找到会一层一层 -       proto（构造函数prototype）查找下去，这样层层链接起来就构成了原型链，遍历原型链之后还是没有找到，会返回undefined
  
-new一个对象的过程
  ·创建一个新对象
  ·this指向这个新对象
  ·执行代码（对this赋值）
  ·返回this；
