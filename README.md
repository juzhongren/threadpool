创建线程池学习与体会
========================
  线程池的作用主要是为了把线程复用，执行完一个任务，并不被销毁，而是可以继续执行其他的任务。<br>
  线程池，就是存放线程的池子，池子里存放了很多可以复用的线程。<br>
### 作用： ###

1.对线程进行统一管理

2.降低系统资源消耗。通过复用已存在的线程，降低线程创建和销毁造成的消耗

3.提高响应速度。当有任务到达时，无需等待新线程的创建便能立即执行

4.提高线程的可管理性。线程是稀缺资源，如果无限制的创建，不仅会消耗大量系统资源，还会降低系统的稳定性，使用线程池可以进行对线程进行统一的分配、调优和监控

### 七大参数： ###

1.核心线程数

2.最大线程数

3.线程空闲时的存活时间

4.线程空闲时的存活时间的时间单位

5.任务缓存队列，用来存放等待执行的任务

6.线程工厂，创建新线程时使用的线程工厂

7.任务拒绝策略

## 线程池的组成主要分为 3 个部分，这三部分配合工作就可以得到一个完整的线程池： ##

### 1、任务队列，存储需要处理的任务，由工作的线程来处理这些任务 ###
      1、通过线程池提供的 API 函数，将一个待处理的任务添加到任务队列，或者从任务队列中删除
      2、已处理的任务会被从任务队列中删除
      3、线程池的使用者，也就是调用线程池函数往任务队列中添加任务的线程就是生产者线程
### 2、工作的线程（任务队列任务的消费者） ，N个 ###
      1、线程池中维护了一定数量的工作线程，他们的作用是是不停的读任务队列，从里边取出任务并处理
      2、工作的线程相当于是任务队列的消费者角色，
      3、如果任务队列为空，工作的线程将会被阻塞 (使用条件变量 / 信号量阻塞)
      4、如果阻塞之后有了新的任务，由生产者将阻塞解除，工作线程开始工作
### 3、管理者线程（不处理任务队列中的任务），1个 ###
      1、它的任务是周期性的对任务队列中的任务数量以及处于忙状态的工作线程个数进行检测
      2、当任务过多的时候，可以适当的创建一些新的工作线程
      3、当任务过少的时候，可以适当的销毁一些工作的线程
