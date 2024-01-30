# Servlet

#### INDEX
* [What is a Servlet?](#what-is-a-servlet)
* [Configuration of Apache Tomcat with Eclipse IDE](#configuration-of-apache-tomcat-with-eclipse-ide)
* [How to create servlet using Servlet Interface](#configuration-of-apache-tomcat-with-eclipse-ide)
    * [Servlet Interface Methods](#servlet-interface-methods)
    * [My First Servlet Program](#first-servlet-program)
* [GenericServlet](#genericservlet)
* [HttpServlet](#httpservlet)
* [LifeCycle Of Servlet](#life-cycle-of-servlet)
* [How to fetch data of form using servlet](#how-to-fetch-data-of-form-using-servlet)

### What is a Servlet ?
- Servlet is just a simple java program that runs on server, not only capable of handling request but also generating dynamic response.
- Servlet in layman's terms is a server side program that is stored in server.

### Working of Servlet
![Servlet Architecture](/java/servlet/img/servletArchitecture.png)

### Configuration of Apache Tomcat with Eclipse IDE
* Download the lastest version of Apache Tomcat Server click here to [DOWNLOAD](https://tomcat.apache.org/).
* After downloading the Apache Tomcat Server just extract it in your desired location.
* Afte extracting you will some folder among those bin is an important one because this folder contains startup and shutdown files to start & stop the server.
* Another important folder is conf folder which contains configuration of Tomcat basically this folder contains files which can be used to add users, change roles or other important thing likr changing the port which is quite useful. For eg:- /home/ocean/softwares/apache-tomcat-10.1.17/conf/ contains server.xml here we change the port number. To configure user we have tomcat-users.xml For eg. /home/ocean/softwares/apache-tomcat-10.1.17/conf contains tomcat-users.xml.
* Now open you Eclipse IDE
    * Server Configuration:- Go to Window tap -> Preferences -> Click on Server from the list in which
    you will see Runtime Environment -> Add your Tomcat Server (select parent directory of bin i.e /home/ocean/softwares/apache-tomcat-10.1.17).
    * Go to Window tap -> Show View -> now see for server tab if not found click on others and search for server.
    * After clicking on server you see this **No servers are available. Click this link to create a new server.** Click this link and create your server (select the version of tomcat you have installed).
* <p><span style="color:red;">!! IMPORTANT</span> :- If you used older version of Apache Tomcat then the <em>Servlet & Jsp Apis</em> are located in <strong><u>javax package</u></strong> but if you are using newer version of Apache Tomcat then <em>Servlet & Jsp Apis </em>are located in <Strong><u>jakarta package</strong></u>.</p>

### How to create servlet using Servlet Interface
![Servlet Interface Working](/java/servlet/img/servletInterface.png)

### Servlet Interface Methods
* Life Cycle Methods
    * init() -> This method is used for initialization.
    * service() -> This method is used for logic or request processing.
    * destroy() -> This method is used for object destruction.
* Non-Life Cycle Methods
    * getServletConfig() -> This method is used to get ServletConfig's object.
    * getServletInfo() -> This method provides the information about our servlet.

### First Servlet Program

**MyFirstServlet.java**
```java
package com.learningservlet.servlets;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import jakarta.servlet.Servlet;
import jakarta.servlet.ServletConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;

public class MyFirstServlet implements Servlet {

	// Servlet Life Cycle Methods
	ServletConfig config;

	public void init(ServletConfig config) {
		// This is used to initialize servlet objects
		this.config = config;
		System.out.println("Creating object");
	}

	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		// This is method is used for logic like request processing
		System.out.println("Servicing..");

		// Set the content type of the respone
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		out.println("<h1>“They say you are what you eat and I still ain’t pussy”</h1>");
		out.println("<h3>By Jcole </h3>");
		out.println("<h3>Today\'s date & time "+new Date().toString()+"</h3>");
	}

	public void destroy() {
		System.out.println("Going to destrop servlet object");
	}

	// Non-Life Cycle Methods

	public ServletConfig getServletConfig() {
		return this.config;
	}

	public String getServletInfo() {
		return "This Servlet is created Ajay Rawat";
	}
}
```

**web.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="https://jakarta.ee/xml/ns/jakartaee"
	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
	id="WebApp_ID" version="6.0">
	<display-name>ServletLearning</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.jsp</welcome-file>
		<welcome-file>default.htm</welcome-file>
	</welcome-file-list>

	<!-- Servlet Declaration -->
	<servlet>
		<servlet-name>MyFirstServlet</servlet-name>
		<!-- You need to provide FULL QUALIFIED NAME i.e package & class name -->
		<servlet-class>com.learningservlet.servlets.MyFirstServlet</servlet-class>
	</servlet>

	<!-- Mapping -->
	<!-- This is an important tag because here we define our url pattern through which we will get our servlet -->
	<servlet-mapping>
		<servlet-name>MyFirstServlet</servlet-name>
		<url-pattern>/MyFirstServlet</url-pattern>
	</servlet-mapping>
</web-app>
```
**index.html**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>My First Servlet</h1>
</body>
</html>
```

### GenericServlet
* GenericServlet is an abstract class.
* It has implemented 4 methods of Servlet interface which are init(), destroy(), getServletConfig() and getServletInfo().
* It has not provided the body of service() method.

![GenericServlet](/java/servlet/img/GenericServlet.png)

**MyServletUsingGenericServlet**
```java
package com.learningservlet.servlets;

import java.io.IOException;
import java.io.PrintWriter;

import jakarta.servlet.GenericServlet;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;

public class MyServletUsingGenericServlet extends GenericServlet {

	@Override
	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		System.out.println("We are using GenericServlet");
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		out.println("<h1>This is MyServlet which is using GenericServlet</h1>");
	}
}
```

**web.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="https://jakarta.ee/xml/ns/jakartaee"
	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
	id="WebApp_ID" version="6.0">
	<display-name>ServletLearning</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.jsp</welcome-file>
		<welcome-file>default.htm</welcome-file>
	</welcome-file-list>

	<!--Servlet Declaration -->

	<!-- Servlet Declaration of MyFirstServlet -->
	<servlet>
		<servlet-name>MyFirstServlet</servlet-name>
		<!-- You need to provide FULL QUALIFIED NAME i.e package & class name -->
		<servlet-class>com.learningservlet.servlets.MyFirstServlet</servlet-class>
	</servlet>

	<!-- Servlet Declaration of MyServletUsingGenericServlet -->
	<servlet>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.MyServletUsingGenericServlet</servlet-class>
	</servlet>

	<!-- ================================================================================== -->

	<!-- Mapping -->

	<!-- Mapping of MyFirstServlet -->
	<!-- This is an important tag because here we define our url pattern through 
		which we will get our servlet -->
	<servlet-mapping>
		<servlet-name>MyFirstServlet</servlet-name>
		<url-pattern>/MyFirstServlet</url-pattern>
	</servlet-mapping>

	<!-- Mapping of MyServletUsingGenericServlet -->
	<servlet-mapping>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<url-pattern>/MyServletUsingGenericServlet</url-pattern>
	</servlet-mapping>
	
</web-app>
```

**index.html**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>My First Servlet</h1>
	<h1><a href="MyFirstServlet">My First Servlet</a></h1>
	<h1><a href="MyServletUsingGenericServlet">MyServletUsingGenericServlet</a></h1>
</body>
</html>
```

### HttpServlet
* HttpServlet is an abstract class which extends GenericServlet class.
* A subclass of HttpServlet must override at least one method, usually one of these:
	* doGet, if the servlet supports HTTP GET requests
	* doPost, for HTTP POST requests
	* doPut, for HTTP PUT requests
	* doDelete, for HTTP DELETE requests
	* init and destroy, to manage resources that are held for the life of the servlet
	* getServletInfo, which the servlet uses to provide information about itself

![HttpServlet](/java/servlet/img/HttpServlet.png)

**MyServletUsingHttpServlet**
```java
package com.learningservlet.servlets;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public class MyServletUsingHttpServlet extends HttpServlet {

	public void doGet(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
			System.out.println("This is doGet() method.....");
			response.setContentType("text/html");
			PrintWriter out = response.getWriter();
			out.println("<h1>This is doGet() method of MyServletUsingHttpServlet</h1>");
			out.println("<h1>Date :- "+new Date().toString()+"</h1>");
	}
}
```

**web.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="https://jakarta.ee/xml/ns/jakartaee"
	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
	id="WebApp_ID" version="6.0">
	<display-name>ServletLearning</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.jsp</welcome-file>
		<welcome-file>default.htm</welcome-file>
	</welcome-file-list>

	<!--Servlet Declaration -->

	<!-- Servlet Declaration of MyFirstServlet -->
	<servlet>
		<servlet-name>MyFirstServlet</servlet-name>
		<!-- You need to provide FULL QUALIFIED NAME i.e package & class name -->
		<servlet-class>com.learningservlet.servlets.MyFirstServlet</servlet-class>
	</servlet>

	<!-- Servlet Declaration of MyServletUsingGenericServlet -->
	<servlet>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.MyServletUsingGenericServlet</servlet-class>
	</servlet>

	<!-- Servlet Declaration of MyServletUsingHttpServlet -->
	<servlet>
		<servlet-name>MyServletUsingHttpServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.MyServletUsingHttpServlet</servlet-class>
	</servlet>

	<!-- ================================================================================== -->

	<!-- Mapping -->

	<!-- Mapping of MyFirstServlet -->
	<!-- This is an important tag because here we define our url pattern through 
		which we will get our servlet -->
	<servlet-mapping>
		<servlet-name>MyFirstServlet</servlet-name>
		<url-pattern>/MyFirstServlet</url-pattern>
	</servlet-mapping>

	<!-- Mapping of MyServletUsingGenericServlet -->
	<servlet-mapping>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<url-pattern>/MyServletUsingGenericServlet</url-pattern>
	</servlet-mapping>

	<!-- Mapping of MyServletUsingHttpServlet -->
	<servlet-mapping>
		<servlet-name>MyServletUsingHttpServlet</servlet-name>
		<url-pattern>/MyServletUsingHttpServlet</url-pattern>
	</servlet-mapping>
</web-app>
```

**index.html**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>My First Servlet</h1>
	<h1><a href="MyFirstServlet">My First Servlet</a></h1>
	<h1><a href="MyServletUsingGenericServlet">MyServletUsingGenericServlet</a></h1>
	<h1><a href="MyServletUsingHttpServlet">MyServletUsingHttpServlet</a></h1>
</body>
</html>
```

### Life Cycle of Servlet

![LifeCycle Of Servlet](/java/servlet/img/LifeCycleOfServlet.png)

### How to fetch data of form using servlet

**RegisterServlet (Main Class)**
```java
package com.learningservlet.servlets;

import java.io.IOException;
import java.io.PrintWriter;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public class RegisterServlet extends HttpServlet {

	public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		// Set content type for response
		response.setContentType("text/html");

		// This helps to print in the browser
		PrintWriter out = response.getWriter();
		out.println("<h1>Welcome to RegisterServlet</h2>");

		// Fetching data and Printing data on the browser
		String name = request.getParameter("user_name");
		String password = request.getParameter("user_password");
		String email = request.getParameter("user_email");
		String gender = request.getParameter("user_gender");
		String course = request.getParameter("user_course");
		String termAndCondtion = request.getParameter("condition");

		if (termAndCondtion != null) {

			if (termAndCondtion.equals("checked")) {
				out.println("<h1>Name:- " + name + "</h1>");
				out.println("<h1>Password:- " + password + "</h1>");
				out.println("<h1>Gender:- " + gender + "</h1>");
				out.println("<h1>Email:- " + email + "</h1>");
				out.println("<h1>Course:- " + course + "</h1>");

			} else {
				out.println("<h1>Something went wrong...</h1>");
			}
		} else {
			out.println("<h1>You have not checked terms and condition</h1>");
		}
	}
}
```

**form.html**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Form page | Learning Servlet</title>

<style>
.container {
	width: 38%;
	border: 1px solid black;
	margin: auto;
	margin-top: 60px; padding : 40px;
	font-size: 25px;
	padding: 40px;
}

#myform table tr td input {
	font-size: 20px;
}

#myform table tr td button {
	font-size: 20px;
}

#myform table tr td select {
	font-size: 20px;
}
</style>
</head>
<body>
	<div class="container">
		<h1>My Form</h1>
		<!-- post is more secure as compare to get method.
		     We can share audio, video but in get method we have limitation
		-->
		<form id="myform" action="RegisterServlet" method="post">
			<table>
				<tr>
					<td>Enter Name :-</td>
					<td><input type="text" name="user_name"
						placeholder="Enter your name" /></td>
				</tr>

				<tr>
					<td>Enter Password :-</td>
					<td><input type="password" name="user_password"
						placeholder="Enter your password" /></td>
				</tr>

				<tr>
					<td>Enter Email :-</td>
					<td><input type="email" name="user_email"
						placeholder="Enter your email" /></td>
				</tr>

				<tr>
					<td>Select Gender</td>
					<td><input type="radio" name="user_gender" value="male" />&nbsp;
						Male &nbsp; <input type="radio" name="user_gender" value="female" />
						Female</td>
				</tr>

				<tr>
					<td>Select your course</td>
					<td><select name="user_course">
							<option value="Java">Java</option>
							<option value="Hibernate">Hibernate</option>
							<option value="Spring">Spring</option>
							<option value="J2EE">J2EE</option>
					</select></td>
				</tr>

				<tr>
					<td style="text-align: right;"><input type="checkbox"
						value="checked" name="condition" /></td>
					<td>Agree terms & conditions</td>
				</tr>

				<tr>
					<td></td>
					<td>
						<button type="submit">Submit</button>
						<button type="reset">Reset</button>
					</td>
				</tr>
			</table>
		</form>
	</div>
</body>
</html>
```

**index.html**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>My First Servlet</h1>
	<h1><a href="MyFirstServlet">My First Servlet</a></h1>
	<h1><a href="MyServletUsingGenericServlet">MyServletUsingGenericServlet</a></h1>
	<h1><a href="MyServletUsingHttpServlet">MyServletUsingHttpServlet</a></h1>
	<h1>Go to Form Section:- <a href="form.html">Form Page</a></h1>
</body>
</html>
```

**web.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="https://jakarta.ee/xml/ns/jakartaee"
	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
	id="WebApp_ID" version="6.0">
	<display-name>ServletLearning</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.jsp</welcome-file>
		<welcome-file>default.htm</welcome-file>
	</welcome-file-list>

	<!--Servlet Declaration -->

	<!-- Servlet Declaration of MyFirstServlet -->
	<servlet>
		<servlet-name>MyFirstServlet</servlet-name>
		<!-- You need to provide FULL QUALIFIED NAME i.e package & class name -->
		<servlet-class>com.learningservlet.servlets.MyFirstServlet</servlet-class>
	</servlet>

	<!-- Servlet Declaration of MyServletUsingGenericServlet -->
	<servlet>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.MyServletUsingGenericServlet</servlet-class>
	</servlet>

	<!-- Servlet Declaration of MyServletUsingHttpServlet -->
	<servlet>
		<servlet-name>MyServletUsingHttpServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.MyServletUsingHttpServlet</servlet-class>
	</servlet>
	
	<!-- Servlet Declaration of RegisterServlet -->
	<servlet>
		<servlet-name>RegisterServlet</servlet-name>
		<servlet-class>com.learningservlet.servlets.RegisterServlet</servlet-class>
	</servlet>

	<!-- ================================================================================== -->

	<!-- Mapping -->

	<!-- Mapping of MyFirstServlet -->
	<!-- This is an important tag because here we define our url pattern through 
		which we will get our servlet -->
	<servlet-mapping>
		<servlet-name>MyFirstServlet</servlet-name>
		<url-pattern>/MyFirstServlet</url-pattern>
	</servlet-mapping>

	<!-- Mapping of MyServletUsingGenericServlet -->
	<servlet-mapping>
		<servlet-name>MyServletUsingGenericServlet</servlet-name>
		<url-pattern>/MyServletUsingGenericServlet</url-pattern>
	</servlet-mapping>

	<!-- Mapping of MyServletUsingHttpServlet -->
	<servlet-mapping>
		<servlet-name>MyServletUsingHttpServlet</servlet-name>
		<url-pattern>/MyServletUsingHttpServlet</url-pattern>
	</servlet-mapping>
	
	<!-- Mapping of RegisterServlet  -->
	<servlet-mapping>
		<servlet-name>RegisterServlet</servlet-name>
		<url-pattern>/RegisterServlet</url-pattern>
	</servlet-mapping>
</web-app>
```