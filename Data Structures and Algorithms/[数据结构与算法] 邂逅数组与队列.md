
@[TOC](   数据结构与算法一   )


学习完部分大数据知识之后, 大数据阶段的学习就暂时告一段落了. 为了能够有机会进入大厂修习, 因此特别在这段时间里通过学习[韩顺平老师的数据结构与算法来](https://www.bilibili.com/video/av54029771?from=search&seid=977205517467992060)复习下数据结构与算法. 与其说是复习不如说是预习,嘿嘿.我将不同于以往的写博方式, 重新和大家一起认识下数据结构. 去发现其中的奥秘~~~

<font color=red>  本期关键词: 线性结构, 非线性结构, 二维数据, 稀疏数组, 队列, 循环队列
 </font>
 
在学习数据结构与算法之前我们需要了解**数据结构与算法的重要性**

- 算法是程序的灵魂. 是能够支撑一个程序高效运行的关键. 
- 算法就是解题的方法论. 如果说设计模式学习的是思维模式, 那么算法就是学习解决编程问题的方法论, 具有良好思维模式和方法论的程序员才是当下需要的, 被定义为"出色程序员"的那类人.
- 学习数据结构与算法能让你在同类人之中脱颖而出


然后我们可以了解一下**数据结构与算法的关系**, 对其有一个初步的认识
- 数据结构是研究数据的组织方式, 是算法的基础
- 算法是解决编程问题的方法论, 是程序的灵魂
- 程序= 数据结构+算法

# 线性结构与非线性结构
首先我们去了解数据结构, 然后以数据结构为基础, 再去了解算法吧
数据结构是有分类的, 它分为**线性结构和非线性结构**
线性结构最为**最常用的数据结构**, 是**一个有序的数据元素集合, 特点是元素间具有一对一的[线性关系](https://baike.baidu.com/item/%E7%BA%BF%E6%80%A7%E5%85%B3%E7%B3%BB/1653156?fr=aladdin)**. 

另外, 线性结构有两种存储: **线性存储结构和链式存储结构**
<font color=red>  基于顺序存储结构存储的线性表称为顺序表, 其元素存储顺序是连续的;
基于链式存储结构存储的线性表称为链表, 其元素存储顺序不一定是连续的, 且元素中存放数据元素以及相邻元素的地址信息</font>
<font color=blue>  我们**常见的线性结构: 数组, 链表,栈和队列**
 </font>
那么, 我想我们应该好奇非线性结构是什么东东了,非线性结构就是当前元素**可能有 多个 直接前驱 和 直接后继元素**
<font color=blue>  **常见的非线性结构有: 数组(二维or多维), 广义表, 树结构, 图结构**
 </font>


# 稀疏数组及五子棋问题
**需求**
如何保存五子棋记录? 我们能够比较容易的想到使用二维数组

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108152455728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)
**问题**
可以看到二维数组中很多数据都是默认值0, 因此可以采用稀疏数组的方式存储数据

**稀疏数组( SparseArray )**
当一个数组大部分数据元素为0 or 同一个值时, 采取稀疏数组	

**稀疏数组的处理方法**
- 记录数组一共有几行几列，有多少个不同的值
- 把具有不同值的元素的行列及值记录在一个小规模的数组中，从而缩小程序的规模
- 如下图,  **稀疏数组的第一行存放二维数组行数, 列数, 有效数据的个数; 第二行及以后存放的是有效数据所在行数, 列数和值**


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108153424876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

**因此五子棋存盘问题可以转换成如下问题**
- 使用稀疏数组，来保留类似前面的二维数组(棋盘、地图等等)
- 把稀疏数组存盘，并且可以从新恢复原来的二维数组数

**整体思路图解**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108153105337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

## 二维数组与稀疏数组的转化

**代码实现**
> 根据思路,一步步实现即可

```java
/**
 * 稀疏数组与二维数组的转换
 *
 * @author TimePause
 * @create 2020-01-08 16:08
 */
public class SparseArray {
    public static void main(String[] args) {
        /**
         * 二维数组转稀疏数组
         * 1. 遍历原始二维数据, 得到有效数据个数sum
         * 2. 根据sum创建稀疏数组 sparseArray[sum+1][3], 3代表列数且为固定
         * 3. 将二维数组中的数据存放到稀疏数组
         */
        // 表示棋子的二维数组
        int[][] chessArray1 = new int[11][11];
        chessArray1[1][2] = 1;
        chessArray1[2][3] = 2;
        //遍历二维数组
        int sum = 0;
        for (int[] row : chessArray1) {
            for (int data : row) {
                if (data != 0) {
                    sum++;
                }
                System.out.print(data + "\t");
            }
            System.out.println();
        }
        System.out.println("二维数组的有效元素个数" + sum);
        //System.out.println(chessArray1.length); 取得二维数组行数
        //System.out.println(chessArray1[0].length); 取得二维数组列数

        // 创建稀疏数组, 本质仍是二维数据
        int[][] sparseArray = new int[sum + 1][3];
        sparseArray[0][0] = chessArray1.length;
        sparseArray[0][1] = chessArray1[0].length;
        sparseArray[0][2] = sum;
        // 将二维数据的有效值赋值给稀疏数组(第二行以后)
        int count = 1; //对行计数
        for (int i = 0; i < chessArray1.length; i++) {
            for (int j = 0; j < chessArray1[i].length; j++) {
                if (chessArray1[i][j] != 0) {
                    // 第一列有:效数据元素所在行.第二列: 有效数据元素所在列,第三列: 有效数据元素的值
                    sparseArray[count][0] = i;
                    sparseArray[count][1] = j;
                    sparseArray[count][2] = chessArray1[i][j];
                    count++;
                }
            }

        }
        System.out.println("==============稀疏数组遍历结果====================");
        for (int[] row : sparseArray) {
            for (int data : row) {
                System.out.print(data + "\t");
            }
            System.out.println();
        }

        /**
         * 稀疏数组转二维数组
         * 1. 读取稀疏数组第一行数据, 根据第一行数据创建原始的第二行数据, 比如chess2=int[11][11]
         * 2. 在去读稀疏数组后几行数据, 并赋值给原始的二维数组即可
         */
        int[][] chessArray2 = new int[sparseArray[0][0]][sparseArray[0][1]];
        // 遍历稀疏数组第二列数据, 注意i从1开始!!!
        System.out.println("==============稀疏数组转二维数组====================");
        for (int i = 1; i < sparseArray.length; i++) {
            chessArray2[sparseArray[i][0]][sparseArray[i][1]] = sparseArray[i][2];
        }

        for (int[] row: chessArray2) {
            for (int data : row) {
                System.out.print(data + "\t");
            }
            System.out.println();
        }


    }
}

```
**运行结果**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108191552788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

## 遍历二维数组的两种方式
>通过上面的代码学习, 我们可以总结出二维数组遍历的两种方式
```java
int[][] chessArray1 = new int[11][11];
//...赋值省略

//方式一: 增强for循环
 for (int[] row : chessArray1) {
            for (int data : row) {
                if (data != 0) {
                    sum++;
                }
                System.out.print(data + "\t");
            }
            System.out.println();
        }

//方式二
 int count = 1; //对行计数
        for (int i = 0; i < chessArray1.length; i++) {
            for (int j = 0; j < chessArray1[i].length; j++) {    
            	    System.out.print(chessArray1[i][j] + "\t");
            }
			 System.out.println();
        }
```


# 队列和银行排队问题
## 银行排队问题
在生活中, 我们在银行排队中需要去取票机取票, 按照取票的顺序(由小到大)进行排队, 
银行有n个窗口, 每次每个窗口处理完业务处理完业务后, 都会叫下一个大的码号, 而且会不断的有人加入这个队列, 如何模拟?


## 队列与队列模拟
下面我们来学习**线性结构的一种数据结构: 队列**
<font color=red>  队列是一个有序表, 编程上可以通过数组和链表来实现 </font>
- **遵循先入先出原则**. 先进入对列的先出去; 后进入的后出去.相当于取火车票时的排队
- 结构图
**由下图我们可以清楚的看到, 当队列有元素进入, rear会增加(rear++); 当队列有元素出去, front会增加(front++)**
**<font color=red>  队列为空时, front=rear, 队列满时, rear=MaxSize-1 (MaxSize为数组最大容量) </font>**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108195320896.png)


**利用数组模拟队列**
- **队列本身是有序列表**，若使用数组的结构来存储队列的数据，则队列数组的声明如下图, 其中 maxSize 是该队列的最大容量。

- 因为队列的输出、输入是分别从前后端来处理，因此需要两个变量 front及 rear分别记录队列前后端的下标，**front 会随着数据输出而改变，而 rear则是随着数据输入而改变**，如图所示:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108195320896.png)


### 队列


**数组模拟队列代码**


- 在创建队列这个实体类时, 需要一个构造函数, 构造函数无返回值. 
且在构造函数中front=rear=-1, 队列用一个数组模拟, 队列长=maxSize
- 执行入队, 需要判断是否队满; 指定出队和查询需要判断是否队空; 
- 队空条件 `rear==front,` 队满条件 `rear==maxSize-1`,不符合条件需要抛出异常
- `throw new RuntimeException()`可以在运行时抛出我们指定的异常, 配合try()...catch()可以实现异常的定制显示而且不会中断程序的执行
- `scanner.next().charAt(0)` 用于接收下一行输出的第一个字符
```java
package ah.sz.tp.algorithm1;

import java.util.Scanner;

/**
 * 数组模拟队列
 *
 * @author TimePause
 * @create 2020-01-08 20:15
 */
public class AarryQueueDemo {
    public static void main(String[] args) {
        // 创建一个队列实体, 且元素个数为3
        ArrayQueue queue=new ArrayQueue(3);
        // 定义键盘输入的数值
        char key=' ';
        Scanner scanner = new Scanner(System.in);
        // 定义一个循环是否终止的变量
        boolean flag=true;
        while (flag){
            //显示菜单
            System.out.println("s(show): 显示当前队列数据");
            System.out.println("a(add): 向当前队列添加数据");
            System.out.println("g(get): 向当前队列取出数据");
            System.out.println("h(head): 显示当前队列头数据");
            System.out.println("e(exit): 执行退出操作");
            //读取我们输入的第一个字符
            key = scanner.next().charAt(0);
            switch (key) {
                case 's':
                    try {
                        queue.showQueueData();
                    } catch (Exception e) {
                        // 这里使用try..catch...的作用是,不会中断程序的运行,手动打印异常信息
                        System.out.println("队空,无法显示所有数据~~~");
                    }
                    break;
                case 'h':
                    try {
                        queue.showHeadData();
                    } catch (Exception e) {
                        System.out.println("队空,无法显示头数据~~~");
                    }
                    break;
                case 'a':
                    try {
                        System.out.println("请输入入队的数据");
                        int n = scanner.nextInt();
                        queue.addQueue(n);
                    } catch (Exception e) {
                        System.out.println("队满,无法添加数据~~~");
                    }
                    break;
                case 'g':
                    try {
                        int res = queue.getQueue();
                        System.out.println("取出的数据为:"+res);
                    } catch (Exception e) {
                        System.out.println("队空,无法获取数据~~~");
                    }
                    break;
                case 'e':
                    flag = false;
                    break;
                default:
                    break;
            }
        }
        System.out.println("已退出, 欢迎下次使用~~~");
    }
}

class ArrayQueue {
    private int maxSize; //数组最大容量
    private int front;  //队列头
    private int rear;  //队列尾
    private int[] arr; //该数组用于模拟队列, 存放队列元素


    public  ArrayQueue(int maxSize) {// 构造函数无需定义返回值!!!
        this.maxSize = maxSize;
        this.front = -1;  //指向队列的头部, 实际上指向队列头的前一个位置.-1实际上是因为数组下标从0开始
        this.rear = -1;   //指定队列的尾部, 最后一个数据
        this.arr = new int[maxSize];
    }

    //判断队列是否为空, 条件是判断front==rear
    public boolean isNull() {
        return front == rear;//首先对进行是否等值的判断, 然后将结果输出
    }

    //判断队列是否为满, 条件是判断rear==maxSize-1
    public boolean isFull() {
        return rear == maxSize - 1;
    }

    // 入队操作, 需要判断是否队满
    public void addQueue(int n) {
        if (isFull()) {
            throw new RuntimeException("队满, 无法进行入队操作");
           // System.out.println("队满, 无法进行入队操作");
        }
        rear++;
        arr[rear] = n;
    }

    //出队操作, 需要判断是否队空
    public int getQueue() {
        if (isNull()) {
            throw new RuntimeException("队空,无法进行入队操作");
           // System.out.println("队空,无法进行入队操作");
        }
        front++;
        return arr[front];//因为rear在上, front在下,front+1后,便会自动跳过上一条数据
    }

    // 显示头数据, 仍需要判空
    public int showHeadData() {
        if (isNull()) {
            throw new RuntimeException("队空,无法进行显示头数据操作");
           // System.out.println("队空,无法进行显示头数据操作");
        }
        return arr[front + 1];
    }

    // 显示所有数据
    public void showQueueData() {
        if (isNull()) {
            throw new RuntimeException("队空, 无法显示所有数据");
            //System.out.println("队空, 无法显示所有数据");
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "]=" + arr[i]);
        }
    }

}

```

**结果展示**
1. 定义了一个最大值为maxSize=3的队列, 首先执行查询和入队操作
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108220857371.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)
三个元素都入队后, 查看入队情况
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108220941555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

2. 一次取出数据元素
在这里的演示中可以看到, 先入队的元素先出队,直至队空
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108221042362.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)
3. 但是在队空以后重新添加元素出现了问题
**无法再次向这个队列添加入队元素**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020010822121676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

**问题分析及优化**
问题: 数组使用一次便不可用, 不能复用
优化: 改进成一个环形队列, 取模: %


### 循环队列


- <font color=red>  **开始时(队空时), front=rear(=0)** </font>
- <font color=red>  **队列满时, (rear + 1)% maxSize=front** </font>
- **<font color=red>   队列中有效数据的个数(队列长度为):  (rear+maxSize-front)%maxSize**
- **由于数组下标从0开始, 相对于上面的队列, 相当于 front直接指向了第一个元素, 而rear指向了最后一个元素的后一个元素**
(而原来队列的规则是:front指向队列头的前一个位置, 而 rear指向了队列的最后一个数据   )
</font>

**示意图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200109111022872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)



**循环队列实现代码**

- 在进行队列转循环队列时需要注意
- 队空 `rear==front`, 队满 `(rear + 1)% maxSize=front` ,队列中有效数据的个数 `(rear+maxSize-front)%maxSize`
- 入队时 rear直接加入` arr[rear] = n`, 然后rear指针后移(取模)`rear = (rear + 1) % maxSize`
- 出队时:1. 将front保存到一个临时变量 2. front后移(取模)  `front = (front + 1) % maxSize`3. 将临时保存的变量返回
- 数据遍历显示时 `for (int i = front; i < front+circleQueueSize(); i++) `, 注意i的初始值和结束值
- **创建一个循环队列实体, 且有效数据长度为 maxSize-1**
  
  
```java
package ah.sz.tp.algorithm1;

import java.util.Scanner;

/**
 * 数组模拟队列
 *
 * @author TimePause
 * @create 2020-01-09 11:30
 */
public class CircleQueueDemo {
    public static void main(String[] args) {
        // 创建一个循环队列实体, 且有效数据长度为 maxSize-1
        CircleQueue queue = new CircleQueue(4);
        // 定义键盘输入的数值
        char key = ' ';
        Scanner scanner = new Scanner(System.in);
        // 定义一个循环是否终止的变量
        boolean flag = true;
        while (flag) {
            //显示菜单
            System.out.println("s(show): 显示当前队列数据");
            System.out.println("a(add): 向当前队列添加数据");
            System.out.println("g(get): 向当前队列取出数据");
            System.out.println("h(head): 显示当前队列头数据");
            System.out.println("e(exit): 执行退出操作");
            //读取我们输入的第一个字符
            key = scanner.next().charAt(0);
            switch (key) {
                case 's':
                    try {
                        queue.showQueueData();
                    } catch (Exception e) {
                        // 这里使用try..catch...的作用是,不会中断程序的运行,手动打印异常信息
                        System.out.println("队空,无法显示所有数据~~~");
                    }
                    break;
                case 'h':
                    try {
                        queue.showHeadData();
                    } catch (Exception e) {
                        System.out.println("队空,无法显示头数据~~~");
                    }
                    break;
                case 'a':
                    try {
                        System.out.println("请输入入队的数据");
                        int n = scanner.nextInt();
                        queue.addQueue(n);
                    } catch (Exception e) {
                        System.out.println("队满,无法添加数据~~~");
                    }
                    break;
                case 'g':
                    try {
                        int res = queue.getQueue();
                        System.out.println("取出的数据为:" + res);
                    } catch (Exception e) {
                        System.out.println("队空,无法获取数据~~~");
                    }
                    break;
                case 'e':
                    flag = false;
                    break;
                default:
                    break;
            }
        }
        System.out.println("已退出, 欢迎下次使用~~~");
    }
}

class CircleQueue {
    private int maxSize; //数组最大容量
    private int front;  //队列头 front=0, 指向第一个元素
    private int rear;  //队列尾 rear=0,指向最后一个元素的最后一个元素
    private int[] arr; //该数组用于模拟队列, 存放队列元素


    public CircleQueue(int maxSize) {// 构造函数无需定义返回值!!!
        this.maxSize = maxSize;
        this.arr = new int[maxSize];
        // front=rear=0.为默认值, 因此可以省略
    }

    //判断队列是否为空
    public boolean isNull() {
        return front == rear;//首先对进行是否等值的判断, 然后将结果输出
    }

    //判断队列是否为满
    public boolean isFull() {
        return (rear + 1) % maxSize == front;
    }

    // 入队操作, 需要判断是否队满
    public void addQueue(int n) {
        if (isFull()) {
            throw new RuntimeException("队满, 无法进行入队操作");
        }
        // 因为rear指向的最后一个元素的后一个元素,所以在入队是直接加入
        arr[rear] = n;
        // 后移, 必须考虑取模!!!
        rear = (rear + 1) % maxSize;
    }

    //出队操作, 需要判断是否队空
    public int getQueue() {
        if (isNull()) {
            throw new RuntimeException("队空,无法进行入队操作");
        }

        //出队时, 需要分析front指向队列的第一个元素
        // 步骤: 1. 将front保存到一个临时变量 2. front后移(取模) 3. 将临时保存的变量返回
        int temp = arr[front];
        front = (front + 1) % maxSize;
        return temp;

    }

    // 显示头数据, 仍需要判空
    public int showHeadData() {
        if (isNull()) {
            throw new RuntimeException("队空,无法进行显示头数据操作");
        }
        return arr[front];
    }

    // 显示所有数据, 需要求出有效数据的长度!!!
    public void showQueueData() {
        if (isNull()) {
            throw new RuntimeException("队空, 无法显示所有数据");
        }
        // 这里注意i=front, 而不是front+circleQueueSize()!!!
        for (int i = front; i < front+circleQueueSize(); i++) {
            System.out.println("arr[" + i % maxSize + "]=" + arr[i % maxSize]);
        }

    }

    // 循环队列有效数据的长度
    public int circleQueueSize() {
        return (rear + maxSize - front) % maxSize;
    }

}

```

**结果演示**

查看队列是否为空->添加元素至队满->查看元素->**取出所有元素至队空->查看是否能够重新加入该元素->查看这些元素**

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020010911571892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)

---
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200109151346675.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMzcxNTU2,size_16,color_FFFFFF,t_70)
