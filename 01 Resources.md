# IO Processing
In IO (Input/Output) processing there are mainly two kinds of processing.
1. Sequencial (Single thread process)
2. Concurrent
    1. Multiprocessing (Parallelism)
    2. Multithreading
    3. Asynchronous processing
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

## 1.3 Async IO
Asynchronous IO (async IO):
* Asynchronous I/O is a form of input/output processing that permits other processing to continue before the transmission has finished.  
* a language-agnostic paradigm (model) that has implementations across a host of programming languages. Here is an article from <strong>real python</strong> to have outlook on <a href="https://realpython.com/async-io-python/">Async IO </a>
<p></p>
<strong>asyncio</strong> - is a python package.
<br>
Coroutines (specialized generator functions) are the heart of async IO in Python.
<p>
<i>Below image: Overview of Synchrounous Vs Multi-threaded Vs Asynchronous</i>
<img src="https://tamerlan.dev/content/images/2022/02/image-4.png" height=400 width=550 align="centre"></img>
</p>
Overview <br></br>

# PyTest
* Pytest <a href="https://realpython.com/pytest-python-testing/#useful-pytest-plugins">Real Python</a>
