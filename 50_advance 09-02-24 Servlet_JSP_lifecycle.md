## Servlet Lifecycle ##
![picture](https://i.ibb.co/xDSRQ3Y/image.png)

* when we start tomcat the very first method that will run in the servlet is init method 

**(Q) Give me any prictical example what code can you write in init method?
(Ans)** Open file or database connection code

**(Q) What method can you write in destroy method?
(Ans)** Database closing connection

## JSP Lifecycle ##
![picture](https://i.ibb.co/hX5jFzg/image.png)

* The java code that we write in the JSP is converted into a servlet using " JSP Translater " .
* Once the servlet is generated then the init() method in the servlet will run first.and this method will run only once and it will run first.
* Services mthod(doGet,doPost) can run any number of times. Finaly when the destroy method is called lifecycle of JSP comes to an end.

**What are Servlets ?**
Servlet is a java class that extends HttpServlet. It is used to develop backend code of the application.

**What are JSP ?**
Java Server Pages provides a feature to write partial java code inside jsp for easily development of software.