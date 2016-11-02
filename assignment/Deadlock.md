## Deadlock ##

### 死锁停在第几次的截图 ###

![](https://raw.githubusercontent.com/nickxiaowei/markdownpicture/master/deadlock_1.png)

### 产生死锁的4个必要条件 ###

**死锁就是两个或者多个进程，互相请求对方占有的资源**

* **互斥条件**

   一个资源每次只能被一个进程使用

* **请求与保持条件**

   一个进程因请求资源而阻塞时，对已获得的资源保持不放

* **不剥夺条件**

   进程已获得的资源，在未使用完之前，不能强行剥夺

* **循环等待条件**

   若干进程之间形成一种头尾相接的循环等待资源关系

### 对程序产生死锁的解释 ###

#### 程序代码如下： ####

**Deadlock.java**

```java
class A{
	synchronized void methodA(B b){
		b.last();
	}

	synchronized void last(){
		System.out.println("Inside A.last()");
	}
}

class B{
	synchronized void methodB(A a){
		a.last();
	}

	synchronized void last(){
		System.out.println("Inside B.last()");
	}
}


class Deadlock implements Runnable{
	A a=new A();
	B b=new B();

	Deadlock(){
		Thread t = new Thread(this);
		int count = 20000;

		t.start();
		while(count-->0);
		a.methodA(b);
	}

	public void run(){
		b.methodB(a);
	}

	public static void main(String args[]){
		new Deadlock();
	}
}
```

**Deadlock.bat**

```
cd /d %~dp0
@echo off
:start
set /a var+=1
echo %var%
java Deadlock
if %var% leq 1000 GOTO start
pause
```

#### 对上述程序产生死锁的解释 ####

分析Deadlock中的一段代码：

```java
Thread t = new Thread(this);
int count = 20000;
t.start();
while(count-->0);
a.methodA(b);
```

可以知道，main线程是在`while(count-->0);`这段忙等待时间之后，再调用对象**a**的`a.methodA(b)`函数，申请了**b**的资源，而这个`while`的忙等待过程，实际上消耗了main线程的时间片。
然后**t**线程的话，一直是处在后台的，在`t.start()`之后就被加入到了调度队列中。
那么假设**count**的设置和分配给**main线程**的时间片大致相同，让main线程开始调用**a**的`a.methodA(b)`函数，然而还没有调用完，时间片已经用完了，那么**main线程**就被迫中止了。
然后**t线程**开始运行，**t线程**的`run()`调用了对象**b**的`b.methodB(a)`，但是这个时候**a**正在**main线程**中执行`a.methodA(b)`函数，由于关键字**synchronized**，线程被阻塞。
又回到**main线程**，继续调用**a**的`a.methodA(b)`函数，这个时候**b**正在**t线程**中执行`b.methodB(a)`，和上面同理，线程被阻塞了，于是两个进程开始互相请求对方占有的资源，造成了死锁。