# 数据结构(四)之队列结构

另外一个受限的数据结构: 队列. 它也是一种受限的线性结构.

### 一. 认识队列

#### 队列结构

队列(Queue)，它是一种运算受限的线性表,先进先出(FIFO First In First Out)

- 队列是一种受限的线性结构
- 受限之处在于它只允许在表的前端（front）进行删除操作，而在表的后端（rear）进行插入操作

生活中类似的队列结构

- 生活中类似队列的场景就是非常多了, 比如在电影院, 商场, 甚至是厕所排队.

- 优先排队的人, 优先处理. (买票, 结账, WC)

  

队列在程序中的应用

- 打印队列:
  - 有五份文档需要打印, 这些文档会按照次序放入到打印队列中.
  - 打印机会依次从队列中取出文档, 优先放入的文档, 优先被取出, 并且对该文档进行打印.
  - 以此类推, 直到队列中不再有新的文档.
- 线程队列:
  - 在进行多线程开发时, 我们不可能无限制的开启新的线程.
  - 这个时候, 如果有需要开启线程处理任务的情况, 我们就会使用线程队列.
  - 线程队列会依照次序来启动线程, 并且处理对应的任务.

### 二. 队列实现

我们需要创建自己的类, 来表示一个队列

```js
// 自定义队列
function Queue() {
    var items = []
    
    // 队列操作的方法
}
```



#### 队列的操作

- 队列有哪些常见的操作呢?

  - `enqueue(element)`：向队列尾部添加一个（或多个）新的项。
  - `dequeue()`：移除队列的第一（即排在队列最前面的）项，并返回被移除的元素。
  - `front()`：返回队列中第一个元素——最先被添加，也将是最先被移除的元素。队列不做任何变动（不移除元素，只返回元素信息——与`Stack`类的`peek`方法非常类似）。
  - `isEmpty()`：如果队列中不包含任何元素，返回`true`，否则返回`false`。
  - `size()`：返回队列包含的元素个数，与数组的`length`属性类似。

- 现在, 我们来实现这些方法. (其实已经比较简单了)

- enqueue方法

  

  ```javascript
  // enter queue方法
  this.enqueue = function (element) {
      items.push(element)
  }
  ```

- dequeue方法

  - 注意: 从队列中删除元素不可以删除最后一个元素了.
  - 因为, 先进入队列中的元素, 先从队列中取出. 因此, 应该删除第一个元素

  

  ```javascript
  // delete queue方法
  this.dequeue = function () {
      return items.shift()
  }
  ```

- front()方法

  

  ```javascript
  // 查看前端的元素
  this.front = function () {
      return items[0]
  }
  ```

- isEmpty方法

  

  ```javascript
  // 查看队列是否为空
  this.isEmpty = function () {
      return items.length == 0
  }
  ```

- size方法

  

  ```javascript
  // 查看队列中元素的个数
  this.size = function () {
      return items.length
  }
  ```

#### 完整的代码

- 我们来看一下队列完整的代码

  

  ```javascript
  // 自定义队列
  function Queue() {
      var items = []
  
      // 队列操作的方法
      // enter queue方法
      this.enqueue = function (element) {
          items.push(element)
      }
  
      // delete queue方法
      this.dequeue = function () {
          return items.shift()
      }
  
      // 查看前端的元素
      this.front = function () {
          return items[0]
      }
  
      // 查看队列是否为空
      this.isEmpty = function () {
          return items.length == 0
      }
  
      // 查看队列中元素的个数
      this.size = function () {
          return items.length
      }
  }
  ```

#### 队列的使用

- 我们来简单使用一下我们封装的Queue

  

  ```javascript
  // 创建队列对象
  var queue = new Queue()
  
  // 在队列中添加元素
  queue.enqueue("abc")
  queue.enqueue("cba")
  queue.enqueue("nba")
  
  // 查看一下队列前端元素
  alert(queue.front())
  
  // 查看队列是否为空和元素个数
  alert(queue.isEmpty())
  alert(queue.size())
  
  // 从队列中删除元素
  alert(queue.dequeue())
  alert(queue.dequeue())
  alert(queue.dequeue())
  ```

### 三. 优先级队列

> 前面, 我们实现了一种普通的队列. 队列中元素的处理顺序和插入的顺序密切相关.
>
> 但是, 还有一种比较常见的场景是和插入顺序无关, 而和元素本身的优先级有关系的队列.
>
> 这种队列就是优先级队列.

#### 优先级队列的介绍

- 优先级队列的特点:
  - 我们知道, 普通的队列插入一个元素, 数据会被放在后端. 并且需要前面所有的元素都处理完成后才会处理前面的数据.
  - 但是优先级队列, 在插入一个元素的时候会考虑该数据的优先级.(和其他数据优先级进行比较)
  - 比较完成后, 可以得出这个元素正确的队列中的位置. 其他处理方式, 和队列的处理方式一样.
  - 也就是说, 如果我们要实现优先级队列, 最主要是要修改添加方法. (当然, 还需要以某种方式来保存元素的优先级)
- 优先级队列应用也非常广泛
  - 一个现实的例子就是机场登机的顺序
    - 头等舱和商务舱乘客的优先级要高于经济舱乘客。
    - 在有些国家，老年人和孕妇（或带小孩的妇女）登机时也享有高于其他乘客的优先级。
  - 另一个现实中的例子是医院的（急诊科）候诊室。
    - 医生会优先处理病情比较严重的患者。
    - 通常，护士会鉴别分类，根据患者病情的严重程度放号。
  - 计算机中, 我们也可以通过优先级队列来重新排序队列中任务的顺序
    - 比如每个线程处理的任务重要性不同, 我们可以通过优先级的大小, 来决定该线程在队列中被处理的次序.

#### 优先级队列的实现

- 实现优先级队列相对队列主要有两方面需要考虑:

  - 1. 封装元素和优先级放在一起(可以封装一个新的构造函数)
  - 1. 添加元素时, 将当前的优先级和队列中已经存在的元素优先级进行比较, 以获得自己正确的位置.

- 优先级队列代码实现:

  

  ```javascript
  // 封装优先级队列
  function PriorityQueue() {
      var items = []
  
      // 封装一个新的构造函数, 用于保存元素和元素的优先级
      function QueueElement(element, priority) {
          this.element = element
          this.priority = priority
      }
  
      // 添加元素的方法
      this.enqueue = function (element, priority) {
          // 1.根据传入的元素, 创建新的QueueElement
          var queueElement = new QueueElement(element, priority)
  
          // 2.获取传入元素应该在正确的位置
          if (this.isEmpty()) {
              items.push(queueElement)
          } else {
              var added = false
              for (var i = 0; i < items.length; i++) {
                  // 注意: 我们这里是数字越小, 优先级越高
                  if (queueElement.priority < items[i].priority) {
                      items.splice(i, 0, queueElement)
                      added = true
                      break
                  }
              }
  
              // 遍历完所有的元素, 优先级都大于新插入的元素时, 就插入到最后
              if (!added) {
                  items.push(queueElement)
              }
          }
      }
  
      // 删除元素的方法
      this.dequeue = function () {
          return items.shift()
      }
  
      // 获取前端的元素
      this.front = function () {
          return items[0]
      }
  
      // 查看元素是否为空
      this.isEmpty = function () {
          return items.length == 0
      }
  
      // 获取元素的个数
      this.size = function () {
          return items.length
      }
  }
  ```

- 代码解析:

  - 封装了一个QueueElement, 将element和priority封装在一起.
  - 在插入新的元素时, 有如下情况下考虑:
    - 根据新的元素先创建一个新的QueueElement对象.
    - 如果元素是第一个被加进来的, 那么不需要考虑太多, 直接加入数组中即可.
    - 如果是后面加进来的元素, 需要和前面加进来的元素依次对比优先级.
    - 一旦优先级, 大于某个元素, 就将该元素插入到元素这个元素的位置. 其他元素会依次向后移动.
    - 如果遍历了所有的元素, 没有找到某个元素被这个新元素的优先级低, 直接放在最后即可.

#### 优先级队列的使用

- 我们来简单使用一下我们的优先级队列.

  

  ```javascript
  // 创建优先级队列对象
  var pQueue = new PriorityQueue()
  
  // 添加元素
  pQueue.enqueue("abc", 10)
  pQueue.enqueue("cba", 5)
  pQueue.enqueue("nba", 12)
  pQueue.enqueue("mba", 3)
  
  // 遍历所有的元素
  var size = pQueue.size()
  for (var i = 0; i < size; i++) {
      var item = pQueue.dequeue()
      alert(item.element + "-" + item.priority)
  }
  ```

### 四. 队列面试题

> 击鼓传花是一个常见的面试算法题. 使用队列可以非常方便的实现最终的结果.

#### 击鼓传花的规则

- 原游戏规则:
  - 班级中玩一个游戏, 所有学生围成一圈, 从某位同学手里开始向旁边的同学传一束花.
  - 这个时候某个人(比如班长), 在击鼓, 鼓声停下的一颗, 花落在谁手里, 谁就出来表演节目.
- 修改游戏规则:
  - 我们来修改一下这个游戏规则.
  - 几个朋友一起玩一个游戏, 围成一圈, 开始数数, 数到某个数字的人自动淘汰.
  - 最后剩下的这个人会获得胜利, 请问最后剩下的是原来在哪一个位置上的人?

#### 击鼓传花的实现

- 我们使用队列可以非常方便的实现这个代码.

- 封装函数

  

  ```javascript
  // 实现击鼓传花的函数
  function passGame(nameList, num) {
      // 1.创建一个队列, 并且将所有的人放在队列中
      // 1.1.创建队列
      var queue = new Queue()
  
      // 1.2.通过for循环, 将nameList中的人放在队列中
      for (var i = 0; i < nameList.length; i++) {
          queue.enqueue(nameList[i])
      }
  
      // 2.寻找最后剩下的人
      while (queue.size() > 1) {
          // 将前num-1中的人, 都从队列的前端取出放在队列的后端
          for (var i = 0; i < num; i++) {
              queue.enqueue(queue.dequeue())
          }
  
          // 将第num个人, 从队列中移除
          queue.dequeue()
      }
  
      // 3.获取剩下的一个人
      alert(queue.size())
      var endName = queue.dequeue()
      alert("最终留下来的人:" + endName)
  
      // 4.获取该人在队列中的位置
      return nameList.indexOf(endName)
  }
  ```

- 代码验证:

  ```javascript
  // 验证结果
  var names = ['John','Jack','Camila','Ingrid','Carl'];
  var index = passGame(names, 7) // 数到8的人淘汰
  alert("最终位置:" + index)
  ```

  