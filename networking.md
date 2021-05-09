##### from stackoverflow
You are using return instead of using a callback. You are doing your parsing when the network connection is done; asynchronously.
To synchronize it, you'd need to use semaphores, but that is highly discouraged on the main thread.Instead, do the appropriate things with the result when your completion block is executed. Think of the data task as 'do stuff, come back to me when you're done'.
