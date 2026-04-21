# Reflection Notes

## Commit 1 Reflection
In this step, I learned how to listen for TCP connections using TcpListener::bind("127.0.0.1:7878") and iterate over incoming connections. 
At first, the server only printed "Connection established!", so the browser did not display anything yet, but it showed that the program was already receiving requests.
Then I updated the code by adding handle_connection with TcpStream and BufReader. This helped me see the actual HTTP request sent by the browser.
From this part, I understood that the server first needs to read and understand the request before it can send back a proper response.

## Commit 2 Reflection
In this step, I modified the server to return an actual HTTP response instead of just printing the request. I learned that a valid HTTP response needs a status line, headers, and the body.
I used fs::read_to_string("hello.html") to read the HTML file and send it back to the browser. 
This made the browser finally display a real webpage instead of nothing.
![Commit 2](assets/images/commit2.png)

## Commit 3 Reflection
In this step, I modified the server to respond differently based on the request. 
If the request is for the root path, it returns hello.html with 200 OK. 
Otherwise, it returns 404.html with 404 NOT FOUND.
This split is important because the server must handle valid and invalid requests differently. 
The refactoring is needed so the response is not always the same and becomes more realistic.
![Commit 3](assets/images/commit3.png)


## Commit 4 Reflection
In this step, I simulated a slow response using /sleep by adding a delay. 
I observed that when accessing /sleep, other requests are also delayed.
This happens because the server is single-threaded and can only handle one request at a time. 
While one request is being processed, other requests must wait.
This shows the limitation of a single-threaded server and why multithreading is needed to improve performance.

## Commit 5 Reflection
In this step, I improved the server by using a ThreadPool to handle multiple requests concurrently.
Previously, the server was single-threaded, so one slow request (like /sleep) would block all other requests. 
After using ThreadPool, multiple threads can handle different requests at the same time.
This improves performance because requests no longer need to wait for each other. 
The ThreadPool also limits the number of threads, making it more efficient and preventing resource overload.

## Commit Bonus Reflection
In this step, I created a new function build as a replacement for new in the ThreadPool implementation. 
The build function internally calls new but it provides a clearer and more flexible way to construct the ThreadPool.
This improvement makes the code easier to extend in the future, because additional logic can be added inside build without changing how the ThreadPool is created in other parts of the program.