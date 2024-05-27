# IO Processing
In IO (Input/Output) processing there are mainly two kinds of processing.
1. Sequencial (Single thread process)
2. Concurrent
<table>
<tr><td>Data</td><td>Data</td></tr>
<tr><td>Multiprocessing (Parallelism)</td><td><li>concurrency<li>library: import multiprocessing</td></tr>
<tr><td>Multithreading</td><td><li>import threading<li>concurrency.futures</ul></td></tr>
<tr><td>Asynchronous processing</td><td><li>import asyncio</td></tr>
</table>
<p>Here in this article you can have a good understanding of what is the <a href="https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism">difference</a>.
<p align="centre">
<img src="https://files.realpython.com/media/Screen_Shot_2018-10-17_at_3.18.44_PM.c02792872031.jpg" alt="AsyncIO Overview Image" height=300 width=400></img>
</p>

# 1. Concurrency
## 1.1 Multithreading
Threads share the same memory and space and execute concurrently <br>
Use case : IO bound tasks
## 1.2 Multiprocessing
More process run in parallel, here processes run in separate memory spaces. <br>
Use case : CPU-bound tasks 
<br></br>
<img src="https://media.licdn.com/dms/image/D5612AQHG77oKct76lQ/article-cover_image-shrink_423_752/0/1692946169635?e=1722470400&v=beta&t=QDT5dIZNzP9gAb_L_tkwMyfTnfJmsgNzzxf9wHWhKn0"></img>

The <a href="https://docs.python.org/3/library/concurrency.html">standard library "Concurrency"</a> supports 
1. Multiprocessing, 
2. Threading and 
3. Concurrent.futures( thread pool executors)
<p> This is a <a href="https://superfastpython.com/threadpoolexecutor-vs-threads/">good article</a> to under stand difference between threading and threadpoolexecutor
<p>
<img src="https://superfastpython.com/wp-content/uploads/2021/12/Differences-Between-ThreadPoolExecutor-and-Thread.jpg"></img>

## 1.3 Async IO
Asynchronous IO (async IO):
* Asynchronous I/O is a form of input/output processing that permits other processing to continue before the transmission has finished.  
* a language-agnostic paradigm (model) that has implementations across a host of programming languages. Here is an article from <strong>real python</strong> to have outlook on <a href="https://realpython.com/async-io-python/">Async IO </a>
<p></p>
<strong>asyncio</strong> - is a python package.<br>
Please go through <a href="https://medium.com/@moraneus/mastering-pythons-asyncio-a-practical-guide-0a673265cf04">this page</a> for better understanding.
<br>
Coroutines (specialized generator functions) are the heart of async IO in Python.
<p>
<i>Below image: Overview of Synchrounous Vs Multi-threaded Vs Asynchronous</i>
<img src="https://tamerlan.dev/content/images/2022/02/image-4.png" height=400 width=550 align="centre"></img>
</p>
Overview <br></br>
async IO is a single-threaded, single-process design: it uses cooperative multitasking. In other words that async IO gives a feeling of concurrency despite using a single thread in a single process. <br>
Coroutines (a central feature of async IO) can be scheduled concurrently, but they are not inherently concurrent.<br>
To reiterate, async IO is a style of concurrent programming, but it is not parallelism. It’s more closely aligned with threading than with multiprocessing but is very much distinct from both of these and is a standalone member in concurrency’s bag of tricks.

```
import asyncio

async def count():
    print("One")
    await asyncio.sleep(1)
    print("Two")

async def main():
    await asyncio.gather(count(), count(), count())

if __name__ == "__main__":
    import time
    s = time.perf_counter()
    asyncio.run(main())
    elapsed = time.perf_counter() - s
    print(f"{__file__} executed in {elapsed:0.2f} seconds.")
```
```
(venv) PS ~> py .\r_asyncio.py
One
One
One
Two
Two
Two
~\r_asyncio.py executed in 1.01 seconds.

```
When each task reaches await asyncio.sleep(1), the function yells up to the event loop and gives control back to it, saying, “I’m going to be sleeping for 1 second. Go ahead and let something else meaningful be done in the meantime.”<br>
asyncio.sleep() - is used to stand in for a non-blocking call (but one that also takes some time to complete).<br>
There’s also a strict set of rules around when and how you can and cannot use async/await.

---
Links for information
* <a href="https://testdriven.io/blog/fastapi-crud/#objectives"> AsyncIO with FastAPI</a>


