# What is servlet in java?

# Java Servlets

A Servlet in Java is a server-side Java program that handles client requests and generates dynamic web content. It runs on a web server or application server and interacts with web clients (typically through HTTP).

## Key Features:
- **Lifecycle**: A servlet's lifecycle includes initialization (`init()`), handling requests (`service()`), and destruction (`destroy()`).
- **Request Handling**: It processes client requests (like form submissions) and generates responses (like HTML pages).
- **Platform Independent**: Being Java-based, servlets are platform-independent.

## Example Use:
A servlet can be used to process a login form, validate user credentials, and generate a response (success or failure page).

## Simple Example:
```java
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.getWriter().println("Hello, World!");
    }
}
```
In this example, when a client sends a GET request to /hello, the servlet responds with "Hello, World!".
