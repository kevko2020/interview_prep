# Python threads/processes

### Import

    import  threading
    import  multiprocessing  as  mp

## Threads

    # Create a thread with an optional name
    thread = threading.Thread(target=func, name='thread_name') 
    thread.start() # Start the thread
    thread.join() # Wait for the thread to finish
    thread.active_count() # num of active threads
    threading.current_thread().getName() # get the name of the current thread
    thread.is_alive() # Check if thread is running
    thread.daemon = True # Keep the thread running even if its parent thread exits
    if  __name__ == '__main__': # only run if you are the main thread
    

## Locks

    # Normal Lock
    lock = threading.Lock()
    lock.acquire(blocking=False) # default True
    lock.release() # release the lock
    with lock:
	    # do something
	# Re-entrant Lock (RLock) # Can be acquired multiple times
	lock = threading.RLock()
	
## Condition Variable
	# Requires a mutex
    cv = threading.Condition(lock=lock)
    with lock:
	    while (condition): # not your turn
		    cv.wait()
		# your turn to do some work
		cv.notify(n=1) # wake up n threads; default is 1
		cv.notify_all() # wake up all threads
## Semaphore

    semaphore = threading.Semaphore(1) # creates semaphore initialized to 1
    with semaphore:
	    # do something

## Queue

    import queue
    q = queue.Queue(maxsize=5) # Creates a queue of size 5
    q.put(item) # puts an item on the queue and blocks if the queue is full
    q.put_nowait(item) # puts item on the queue # puts an item and raises exception if queue is full
    q.get() # remove an item from the queue
    q.qsize() # get size of queue

## Processes

    os.getpid() # get the current process id
    mp.Process(target=func, args=(arg1,)).start() # Create a process and start it
    mp.Queue(5) # Shared queue between processes

## Barrier

    barrier = threading.Barrier(10) # creates a barrier that waits for 10 threads
    # first group does something
    barrier.wait()
    # then second group does something

## Thread Pool

    from concurrent.futures import ThreadPoolExecutor
    pool = ThreadPoolExecutor(max_workers=5)
    for arg in range(100):
	    pool.submit(function, arg)
    pool.shutdown() # can omit if using the context manager (with ThreadPoolExecutor(max_workers=5) as pool:)

## Process Pool

    from concurrent.futures import ProcessPoolExecutor
    with ProcessPoolExecutor(max_workers=5) as pool:
	    for arg in range(100):
			pool.submit(function, arg)
    

## Future

    future = pool.submit(function) # creates a future
    future.result() # get the result of the future



