## i++ & ++i  
int i=1,a=0;
* i++ 先赋值在运算,例如 a=i++,先赋值a=i,后运算i=i+1,所以结果是a==1
* ++i 先运算在赋值,例如 a=++i,先运算i=i+1,后赋值a=i,所以结果是a==2

## sleep 和 wait 区别  
sleep(休眠) 和 wait(等待)

1. 使用限制
sleep 方法可以让让当前线程休眠，时间一到当前线程继续往下执行，在任何地方都能使用，但需要捕获 InterruptedException 异常。<br/>
wait 方法则必须放在 synchronized 块里面，同样需要捕获 InterruptedException 异常，并且需要获取对象的锁。<br/>
而且 wait 还需要额外的方法 notify/ notifyAll 进行唤醒，它们同样需要放在 synchronized 块里面，且获取对象的锁 <br/>

2. 使用场景
sleep 一般用于当前线程休眠，或者轮循暂停操作，wait 则多用于多线程之间的通信。<br/>

3. 所属类
sleep 是 Thread 类的静态本地方法，wait 则是 Object 类的本地方法。<br/>
因为 sleep 是让当前线程休眠，不涉及到对象类，也不需要获得对象的锁，所以是线程类的方法。<br/>
wait 是让获得对象锁的线程实现等待，前提是要楚获得对象的锁，所以是类的方法。

4. 释放锁 
wait 可以释放当前线程对 lock 对象锁的持有，而 sleep 则不会
5. 线程切换 
sleep 会让出 CPU 执行时间且强制上下文切换，而 wait 则不一定，wait 后可能还是有机会重新竞争到锁继续执行的。 


## 多线程4中方式  
1. 继承Thread类，重写run方法
2. 实现Runnable接口，重写run方法，实现Runnable接口的实现类的实例对象作为Thread构造函数的target
3. 通过Callable和FutureTask创建线程
4. 通过线程池创建线程 <br/>

1和2无返回值  3，4 有返回值是个object对象 
```java 
// 1
public class ThreadDemo01 extends Thread{
    public ThreadDemo01(){
        //编写子类的构造方法，可缺省
    }
    public void run(){
        //编写自己的线程代码
        System.out.println(Thread.currentThread().getName());
    }
    public static void main(String[] args){ 
        ThreadDemo01 threadDemo01 = new ThreadDemo01(); 
        threadDemo01.setName("我是自定义的线程1");
        threadDemo01.start();       
        System.out.println(Thread.currentThread().toString());  
    }
}

// 2 
public class ThreadDemo02 {

    public static void main(String[] args){ 
        System.out.println(Thread.currentThread().getName());
        Thread t1 = new Thread(new MyThread());
        t1.start(); 
    }
}

class MyThread implements Runnable{
    @Override
    public void run() {
        // TODO Auto-generated method stub
        System.out.println(Thread.currentThread().getName()+"-->我是通过实现接口的线程实现方式！");
    }   
}

// 3
public class ThreadDemo03 {

    /**
     * @param args
     */
    public static void main(String[] args) {
        // TODO Auto-generated method stub

        Callable<Object> oneCallable = new Tickets<Object>();
        FutureTask<Object> oneTask = new FutureTask<Object>(oneCallable);

        Thread t = new Thread(oneTask);

        System.out.println(Thread.currentThread().getName());

        t.start();

    }

}

class Tickets<Object> implements Callable<Object>{

    //重写call方法
    @Override
    public Object call() throws Exception {
        // TODO Auto-generated method stub
        System.out.println(Thread.currentThread().getName()+"-->我是通过实现Callable接口通过FutureTask包装器来实现的线程");
        return null;
    }   
}

// 4
public class ThreadDemo05{

    private static int POOL_NUM = 10;     //线程池数量

    /**
     * @param args
     * @throws InterruptedException 
     */
    public static void main(String[] args) throws InterruptedException {
        // TODO Auto-generated method stub
        ExecutorService executorService = Executors.newFixedThreadPool(5);  
        for(int i = 0; i<POOL_NUM; i++)  
        {  
            RunnableThread thread = new RunnableThread();

            //Thread.sleep(1000);
            executorService.execute(thread);  
        }
        //关闭线程池
        executorService.shutdown(); 
    }   

}

class RunnableThread implements Runnable  
{     
    @Override
    public void run()  
    {  
        System.out.println("通过线程池方式创建的线程：" + Thread.currentThread().getName() + " ");  

    }  
}  
``` 
## 常用线程池  
线程池名称	描述
1. FixedThreadPool	核心线程数与最大线程数相同 
2. SingleThreadExecutor	一个线程的线程池
3. CachedThreadPool	核心线程为0，最大线程数为Integer. MAX_VALUE
4. ScheduledThreadPool	指定核心线程数的定时线程池 


## 静态代码块 

对于一个类而言，按照如下顺序执行：

1. 执行静态代码块
2. 执行构造代码块
3. 执行构造函数
对于静态变量、静态初始化块、变量、初始化块、构造器，它们的初始化顺序依次是（静态变量、静态初始化块）>（变量、初始化块）>构造器。

```java 
 public class InitialOrderTest {
         /* 静态变量 */
     public static String staticField = "静态变量";
         /* 变量 */
     public String field = "变量";
         /* 静态初始化块 */
     static {
         System.out.println( staticField );
         System.out.println( "静态初始化块" );
     }
         /* 初始化块 */
     {
         System.out.println( field );
         System.out.println( "初始化块" );
     }
         /* 构造器 */
     public InitialOrderTest()
     {
         System.out.println( "构造器" );
     }
 
 
     public static void main( String[] args )
     {
         new InitialOrderTest();
     }
}

/**
 执行顺序 

 静态变量
 静态初始化块
 变量
 初始化块
 构造器
*/


```  

## 线程池  
重要概念：  
核心线程数量，  最大线程数，

