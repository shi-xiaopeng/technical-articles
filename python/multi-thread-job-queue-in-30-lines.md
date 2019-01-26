原文链接：https://medium.com/@shashwat_ds/a-tiny-multi-threaded-job-queue-in-30-lines-of-python-a344c3f3f7f0

Recently while plotting some data while doing gradient descent on my neural net, i ran across some performance issues. My gradient descent code was something like this. (pseudocode)
```
def gradient_descent():
    # the gradient descent code
    plotly.write(X, Y)
```
Basically the network calls to plot.ly were blocking in nature and were slowing down the rest of the gradient descent function as well.

One possible solution was to start a new thread for each plotly.write call but launching a thread everytime just felt wrong. I didn’t want to use a full blown job queue like celery either because it was rather heavy and i really didn’t need redis persistence for plotting stuff.

The solution?  I wrote a tiny task queue in python which can run the plotly.write calls in a separate thread. Here’s what it looks like.
```
from threading import Thread
import Queue 
import time
class TaskQueue(Queue.Queue):
```
We start off by inheriting from the Queue.Queue class. This gives us access to the get, put methods and the queue behaviour.
```
def __init__(self, num_workers=1):
    Queue.Queue.__init__(self)
    self.num_workers = num_workers
    self.start_workers()
```
While initialising, we can pass in the number of worker threads we would like to keep.
```
def add_task(self, task, *args, **kwargs):
    args = args or ()
    kwargs = kwargs or {}
    self.put((task, args, kwargs))
```
I am storing the task, args, kwargs as tuples in the queue. *args allows you to pass variable number of arguments and **kwargs allows named arguments.
```
def start_workers(self):
    for i in range(self.num_workers):
        t = Thread(target=self.worker)
        t.daemon = True
        t.start()
```
We create threads for each of the workers and fire them off in background mode.

Next the actual worker code.
```
def worker(self):
    while True:
       tupl = self.get()
       item, args, kwargs = self.get()
       item(*args, **kwargs) 
       self.task_done()
```
The worker doesn’t do much but keeps getting the topmost task from the queue and running it along with its arguments. That’s the code for the queue.

We can test out the queue like this:
```
def blokkah(*args, **kwargs):
    time.sleep(5)
    print “Blokkah mofo!”
q = TaskQueue(num_workers=5)
for item in range(1):
    q.add_task(blokkah)
q.join() # wait for all the tasks to finish.
print “All done!”
```
Blokkah being the name of the task we have to do. The queue is in memory and doesn’t do much. The next logical steps would be to run the main queue as a standalone process so that it doesn’t shut down when the main program exits and adding database persistence. But it’s a good example of how complex stuff like job queues can be written starting from a very simple initial version.
```
def gradient_descent():
    # the gradient descent code
    queue.add_task(plotly.write, x=X, y=Y)
```
My gradient descent seems to be working better now after the modification, here’s the full script if you are interested.
```
from threading import Thread
import Queue 
import time

class TaskQueue(Queue.Queue):

    def __init__(self, num_workers=1):
        Queue.Queue.__init__(self)
        self.num_workers = num_workers
        self.start_workers()

    def add_task(self, task, *args, **kwargs):
        args = args or ()
        kwargs = kwargs or {}
        self.put((task, args, kwargs))

    def start_workers(self):
        for i in range(self.num_workers):
            t = Thread(target=self.worker)
            t.daemon = True
            t.start()

    def worker(self):
        while True:
            tupl = self.get()
            item, args, kwargs = self.get()
            item(*args, **kwargs)  
            self.task_done()


def tests():
    def blokkah(*args, **kwargs):
        time.sleep(5)
        print "Blokkah mofo!"

    q = TaskQueue(num_workers=5)

    for item in range(10):
        q.add_task(blokkah)

    q.join()       # block until all tasks are done
    print "All done!"

if __name__ == "__main__":
    tests()
```
