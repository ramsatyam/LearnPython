# Multithreading
Navigation:
1. <a href="#basics">Basics</a>
2. <a href="#synchronization">Synchronization</a>
3. <a href="#inter-thread-communication">Interthread Communication</a>
## Basics
Keywords:
```
t = Thread(target=<func_name>)
t = Thread(target = <class_name>.<func_name>)
t.start()
```
Example:
* Creating a thread by extending Thread Class. We have to define run function which is execution direclty then instance is defined and started.
```
from threading import *
import time
class Mythread(Thread):
    def run(self):
        for i in range(10):
            print("2. Child thread-1")
            time.sleep(1)
t = Mythread()
t.start()
for i in range(10):
    print("2. Main thread")
print("Name of the running thread:", current_thread().name)
```

### Thread Identification Number (ident)
```
current_thread().ident
t.ident
active_count()
```
### Naming threads
```
current_thread().getName()
t = Thread(target =<calss>.<func>, name = <name_for_thread>)
```
### List of name of active threads
```
i = enumerate()
for t in i:
   print("Thread name: ", t.name)
```
### To check if thread is alive or not
```
<thread>.isalive() -> returns True or False
print(t.name , is alive:', t.isalive())
```
### join() method:
If thread wants to wait until completing some other thread then we should go for `join()` method.<br>
We can use with time period also, if we want to wait for some time period `t.join(5)` waits for 5 seconds.
```
t.start()
t.join() # Main function executes this so it will wait for 't' thread to complete.

t.start()
t.join(5) # main will wait 5 seconds and continues.
```
### Daemon Threads
#### Example 01
```
# Creating thread by extending thread class
from threading import *
import time


class Mythread(Thread):
    def run(self):
        for i in range(5):
            print("2. Child thread-1")
            time.sleep(1)
t = Mythread()
t.start()
t.join()
for i in range(5):
    print("2. Main thread")
print("Name of the running thread:", current_thread().name)
print("Name of Mythread:", t.name)
```
Example 02
```
class Newclass01:
    def func01(self):
        for _ in range(5):
            print( 'New class 01 func 01 executing')
            time.sleep(0.5)
    def func02(self):
        for _ in range(5):
            print('New class 01 func 02 executing')
            time.sleep(0.5)
    def func03(self):
        for _ in range(5):
            print('New class 01 func 03 executing')
            time.sleep(0.5)
obj1 = Newclass01()
t2 = Thread(target=obj1.func01)
t3 = Thread(target=obj1.func02, name="t3 Thread")
t4 = Thread(target=obj1.func03, name ="t4 Thread")
t2.start()
t3.start()
t4.start()

# ========>print thread name and identification number<====
print("t2 thread name:", t2.name,'identification',t2.ident)
print("t3 thread name", t3.name)
print("t3 thread name", t4.name)

# ========>Print active number of threads<====
print('Active Thread Count:', active_count())

# ========>Print active thread names<====
enum = enumerate()
for i in enum:
    print ('Thread name',i.name)
```
#### Default Nature
## 2 Synchronization
If multiple threads get executed then there may be a chance of data inconsistency problems.<br>
To overcome this problem we go for synchronization. In synchronization threads will be executed one by one. Synchronization means at a time only one thread.<br>
In python, we can implement synchronization by using the following
1. Lock
2. RLock
3. Semaphore
* Synchronization using Lock concept
* Problem with simple Lock
* Difference with Lock and RLock
* Synchronization using Semaphore
* Bounded Semaphore
* Difference between Lock and Semaphore
### 2.1 Synchronization using Lock concept
```
# Synchronization using Lock
import time
from threading import Lock, Thread
I = Lock()
def wish(name):
    I.acquire()
    for i in range(3):
        print('Hello: ', end='')
        time.sleep(2)
        print(name)
    I.release()
t1 = Thread(target=wish, args=('Name1',))
t2 = Thread(target=wish, args= ('Name2',))
t3 = Thread(target=wish, args=('name3',))
t1.start()
t2.start()
t3.start()
```
#### Problem with simple Lock
Standard Lock object doesn't care which thread is currently holding that lock. If the lock is held and any thread attempts to acquire lcok, then it will be clocked, even the same thread is already holding that lock.<br>
Below program will be bocked because it is trying to acquire the lock repititively.
```
from threading import Lock, Thread
def factorial(number):
    I.acquire()
    if number > 1:
        print('Entered Loop')
        return number * factorial(number-1)
    else:
        I.release()
        return 1
print(factorial(6))
```
#### 2.2 Synchronization using RLock (Reentrant Lock)
To Overcome above problem we can use RLock. Reentrant means the thread can acquire the same lock again and again. If the Rlock is held by any other thread then only the thread will be blocked.<br>
Note:
* Rlock keeps track of recursion level. The number of acquire() calls and release() calls should be matched.
* Only owner thread can acquire the lock multiple times.
```
from threading import Thread, RLock
IR = RLock()
def factorial(number):
    IR.acquire()
    if number == 0:
        result = 1
    else:
        print('Entered Loop')
        result =  number * factorial(number-1)
    IR.release()
    return result
def results(n):
    print("The factorial of ",n,"is", factorial(n))
t1 = Thread(target=results, args=(5,))
t2 = Thread(target=results, args=(7,))
t1.start()
t2.start()
```
#### Difference with Lock and RLock
<table><th>Lock</th><th>RLock</th>
<tr><td><li> Lock object can be acquired by only one thread at a time. Even owner thread also cannot acquire multiple times.</td>
<td><li> RLock object can be acquired by only one thread, but owner thread can acquire same lock object multiple times</td></tr>
<tr><td><li> Not suitable to execute recursive functions and nested access calls</td>
<td><li> Best suited to execute recursive functions and nested access calls</td></tr>
<tr><td><li> In this case RLock object will care only Locked or unlocked and it never takes care about owner thread and recursion level.</td>
<td><li> In this case RLock will take care whether Locked or unlocked and owner thread information, recursion level.</td></tr>
</table>

### 2.3 Synchronization using Semaphore
In the case of Lock and RLock, at a time only one thread is allowed to execute. If at a time number of threads are to be allowed to access, then we cannot use Lock or RLock, we should go for Semaphore.<br>
Semaphores can be used to limit the access to the shared resources with limited capacity.<br>
Semaphores use `s = Semaphore(counter)` as syntax where counter is number of threads that can have parallel access.
```
import time
from threading import Lock, Thread, RLock, Semaphore
s = Semaphore(3)
def wish(name):
    s.acquire()
    for i in range(5):
        print('Hello :', end='')
        time.sleep(2)
        print(name )
    s.release()
t1 = Thread(target=wish, args=('Name 1',))
t2 = Thread(target=wish, args=('Name 2',))
t3 = Thread(target=wish, args=('Name 3',))
t4 = Thread(target=wish, args=('Name 4',))
t5 = Thread(target=wish, args=('Name 5',))
t1.start()
t2.start()
t3.start()
t4.start()
t5.start()
```
#### Bounded Semaphore
A normal semaphore is an unlimited semaphore, it allows us to call release() method any number of times to increment counter. The number of release() calls can exceed the number of acquire() calls also.<br>
Bounded Semaphore is exactly same as a semaphore except that number of release() calls should not exceed the number of acquire() calls, otherwise we will get <br>
<strong> valueError: Semaphore released too many times.</strong><br>
Note: It is recomended to used BoundedSemaphore over normal semaphore to prevent simple programming mistakes.

#### Difference between Lock and Semaphore
<table><th>Lock</th><th>Semaphore</th>
<tr><td><li> Lock object can be acquired by only one thread</td>
<td><li> Semaphore object can be acquired by fixed number of threads, specified by counter value.</td></tr>
</table>

## 3. Inter Thread Communication
Whenever threads are required to communicate with each other, we use interthread communication.
In python it can be implemented in three ways.
1. Event
2. Condition
3. Queue
#### 3.1 Interthread communication using Event Objects
Event object is the simplest communication mechanism between the threads. One thread signals an event and other thread waits for it.<p>
`event = threading.Event()`<p>
Event manage internal flag that can set() and clear()

##### Methods of Event Class:
<table>
<th>S.no<th>Method<th>Comment
<tr><td>1.<td>set()<td>Internal flag value become True and it represents GREEN  signal for all waiting threads.
<tr><td>2.<td>clear()<td>Internal flag value become False and it represents RED signal for all waiting threads.
<tr><td>3.<td>isSet()<td> This method can be used whether the event is set or not.
<tr><td>4.<td>wait() | wait(seconds)<td> Thread can wait until event is set.
</table>

#### 3.2 Interthread communication using Condition Objects
Condition is more advanced version of Event Object for interthread communication. Condition is always associated to RLock().<br>
A Condition has acquire() and release() methods that call the corresponding methods of the associated lock.
##### Methods of Condition:
<table>
<th>S.no<th>Method<th>Comment
<tr><td>1.<td>acquire()<td>To acquire condition object before producing or consuming items ie. thread acquiring internal lock.
<tr><td>2.<td>release()<td>To release condition object after producing or consuming items ie. thread releases internal lock.
<tr><td>3.<td>wait() | wait(time)<td> To wait until getting notification or time expired.
<tr><td>4.<td>notify()<td> To give notification for one waiting thread.
<tr><td>5.<td>notifyAll()<td> To give notification for all waiting threads.
</table>

```
from threading import Thread, Condition
def rec_func(c):
    c.acquire()
    print('Receiver: Waiting for price')
    c.wait()
    print('Receiver:',data_transer[-1],' received as price')
    c.release()
def emitter(c):
    c.acquire()
    print('Emitter: Price calculation is being done')
    data_transer.append(599)
    c.notify()
    print('Emitter: Price value sent using condition notification')
    c.release()
c = Condition()
data_transer = []
t1 = Thread(target=rec_func, args=(c,))
t2 = Thread(target=emitter, args=(c,))
t1.start()
t2.start()
```

#### 3.3 Interthread communication using Queue Objects
Queues concept is the most advanced mechanism for interthread communication and to share data between them.<br>
Queue internally has condition and that condition has RLock. Hence whenever we are using Queue we are not required to worry about synchronization.<br>
```
import queue
q = queue.Queue()
```
##### Important Methods of Queue:
1. put() -> Put an item into queue.
2. get() -> Remore and return an item from the queue.
##### Types of Queue:
1. FIFO<br>
First In First Out
```
import queue
q = queue.Queue()
q.put(25)
q.put(20)
q.put(15)
q.put(10)
while not q.empty():
    print(q.get(), end=' ')
```
```25 20 15 10 ```

2. LIFO<br>
Last in First out.
```
import queue
ql = queue.LifoQueue()
ql.put(25)
ql.put(20)
ql.put(15)
ql.put(10)
while not ql.empty():
    print(ql.get(), end=' ')
```

3. Priority Queue <br>
Elements are inserted based on some priority order.
```
import queue
qp = queue.PriorityQueue()
qp.put(25)
qp.put(20)
qp.put(15)
qp.put(10)
while not qp.empty():
    print(qp.get(), end=' ')
```
If data is non numeric, then we have to provide data in tuple form.
```
import queue
qp = queue.PriorityQueue()
qp.put((8, 'Eight'))
qp.put((6, 'six'))
qp.put((7,'seven'))
qp.put((3,'Three'))
while not qp.empty():
    print(qp.get()[1],end=' ')
```



