# Reflection Notes

## Commit 1 Reflection
In this step, I learned how to listen for TCP connections using TcpListener::bind("127.0.0.1:7878") and iterate over incoming connections. 
At first, the server only printed "Connection established!", so the browser did not display anything yet, but it showed that the program was already receiving requests.
Then I updated the code by adding handle_connection with TcpStream and BufReader. This helped me see the actual HTTP request sent by the browser.
From this part, I understood that the server first needs to read and understand the request before it can send back a proper response.