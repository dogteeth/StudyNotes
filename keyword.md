#### Completion Handler

A completion handler is a closure (“a self-contained block of functionality that can be passed around and used in your code”). It gets passed to a function as an argument and then called when that function is done.


##### @nonescaping closure
When passing a closure as the function argument, the closure gets execute with the function’s body and returns the compiler back. As the execution ends, the passed closure goes out of scope and have no more existence in memory.

##### @escaping closure
When passing a closure as the function argument, the closure is being preserve to be execute later and function’s body gets executed, returns the compiler back. As the execution ends, the scope of the passed closure exist and have existence in memory, till the closure gets executed. 
