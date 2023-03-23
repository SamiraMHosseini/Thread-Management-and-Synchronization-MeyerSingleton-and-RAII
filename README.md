# Thread Management and Synchronization with Meyer Singleton and RAII


This code demonstrates the use of multithreading, synchronization, and the Meyer's Singleton pattern in C++. The main functionality is distributed across multiple threads that run concurrently, while the Meyer's Singleton pattern is used to manage thread count.

Important components:

ThreadCountProxy: This struct implements the Meyer's Singleton pattern. It keeps track of the number of threads and provides static methods to increment, decrement, and wait for all threads to complete.

ThreadCount: This class is a helper class that increments and decrements the thread count using ThreadCountProxy when it is constructed and destructed, respectively.

A, B, C, and D: These classes inherit from BannerBase, which is not shown in the code. They each have an operator() method that takes a std::future<void> reference as an argument. Inside the method, they perform a specific task, check the future's status, and exit the loop if the future is ready.

Controller: This class also inherits from BannerBase and has an operator() method that takes a std::promise<void> rvalue reference as an argument. It sets the promise's value to signal the other threads to stop and waits for all the threads to complete using ThreadCountProxy::WaitUntilThreadsDone().

main(): This function sets up the threads and starts them with the appropriate classes and promises/futures. It also creates a future for the Controller object, which is either launched in deferred mode or async mode, depending on the code version. The program waits for a key press, and when detected, it calls fuController.get() to allow the Controller to signal the other threads to stop and wait for their completion.

# Key points:

1) Meyer's Singleton pattern ensures that there is only one instance of ThreadCountProxy.

2) Threads are created for the classes A, B, C, D, and Controller.

3) Thread synchronization is achieved using std::mutex, std::condition_variable, std::lock_guard, and std::unique_lock.

4) The Controller object is responsible for signaling the other threads to stop and waiting for their completion.
