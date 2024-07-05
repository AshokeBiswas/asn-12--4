Q1. What is multiprocessing in Python? Why is it useful?
Multiprocessing in Python refers to the ability to create and run multiple independent processes concurrently. Each process runs in its own memory space, enabling true parallelism on multi-core systems. It is particularly useful for CPU-bound tasks, such as complex computations, where utilizing multiple cores can significantly improve performance and reduce execution time.

Q2. Differences between multiprocessing and multithreading
Multiprocessing:

Creates multiple processes, each with its own memory space.
True parallelism on multi-core CPUs.
Higher memory and process management overhead.
Better for CPU-bound tasks.
Multithreading:

Creates multiple threads within a single process, sharing the same memory space.
Concurrency but not true parallelism (due to Python's Global Interpreter Lock, GIL).
Lower memory and management overhead.
Better for I/O-bound tasks.
Q3. Python code to create a process using the multiprocessing module
Here's an example of creating a simple process using the multiprocessing module:

python
Copy code
import multiprocessing

def worker():
    """Function to run in the process."""
    print("Worker process executing.")

if __name__ == "__main__":
    # Create a new process
    process = multiprocessing.Process(target=worker)
    
    # Start the process
    process.start()
    
    # Wait for the process to complete
    process.join()
    
    print("Main process exiting.")
Q4. What is a multiprocessing pool in Python? Why is it used?
A multiprocessing pool in Python is a high-level interface that allows you to manage a pool of worker processes. It is used to parallelize the execution of a function across multiple input values, distributing the tasks among the worker processes efficiently. This is particularly useful for tasks that can be executed independently and concurrently.

Q5. Creating a pool of worker processes in Python using the multiprocessing module
Here's how you can create and use a pool of worker processes with the multiprocessing.Pool class:

python
Copy code
import multiprocessing

def worker(num):
    """Function to execute in the worker process."""
    print(f"Worker process handling number: {num}")

if __name__ == "__main__":
    # Create a pool of 4 worker processes
    with multiprocessing.Pool(processes=4) as pool:
        # Map the worker function to a range of numbers
        pool.map(worker, range(1, 5))
Q6. Python program to create 4 processes, each process printing a different number
Here's a Python program that creates 4 processes, each printing a different number using the multiprocessing module:

python
Copy code
import multiprocessing

def print_number(num):
    """Function to print a number."""
    print(f"Process {num}: Number {num}")

if __name__ == "__main__":
    # Create a list to hold the process objects
    processes = []
    
    # Create 4 processes
    for i in range(1, 5):
        process = multiprocessing.Process(target=print_number, args=(i,))
        processes.append(process)
        process.start()
    
    # Wait for all processes to complete
    for process in processes:
        process.join()

    print("All processes completed.")
In this program:

Four processes are created using multiprocessing.Process, each assigned to the print_number function with a different number as an argument.
Each process starts and then the main process waits for all to complete using process.join().
