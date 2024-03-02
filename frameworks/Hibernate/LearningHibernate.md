# Hibernate Framework
 
#### INDEX
* [What is Hibernate FrameWork](#what-is-hibernate-framework)
* [Hibernate Configuration For Eclipse](#hibernate-configuration-for-eclipse)
* [Hibernate Configuration Code](#hibernate-configuration-code)
* [First Hibernate Program](#first-hibernate-program)
* [Commonly Used Hibernate Annotations](#commonly-used-hibernate-annotations)
* [Fetch Data using get() method & load() method](#fetch-data-using-get-method--load-method)
* [@Embeddable Annotation](#embeddable-annotation)
* [OneToOne Mapping](#onetoone-mapping)
* [OneToMany & ManyToOne Mapping](#onetomany-and-manytoone-mapping)
* [ManyToManyMapping](#manytomanymapping)
* [Fetch Type:- Lazy & Eager Loading](#fetch-type)
* [Hibernate Object State || Persistent Lifecycle](#hibernate-object-state--persistent-lifecycle)
* [HQL - Hibernate Query Language](#hql--hibernate-query-language)
	* [HQL - Delete Query](#hql--delete-query)
	* [HQL - Update Query](#hql--update-query-in-hibernate)
	* [HQL - Join Query](#hql--join-query-in-hibernate)
	* [HQL - Pagination](#pagination)
* [SQL Query In Hibernate](#sql-query-in-hibernate)
* [Cascading](#cascading)
* [Caching](#caching)
	* [Types Of Hibernate Caching](#types-of-hibernate-caching)
	* [First Level Caching](#first-level-caching)
	* [Second Level Caching](#second-level-caching)
* [Mapping Using XML file](#mapping-using-xml-file)
* [Hibernate Criteria API | Criteria Restrictions](#hibernate-criteria-api--criteria-restrictions)

### What is Hibernate Framework?
* Hibernate is a java framework that simplifies the developement of java application to interact with the database.
* Hibernate is an ***ORM (Object Relational Mapping)*** tool.
* Hibernate is an Open source and lightweight framework.
* Hibernate is a *non-invasive* framework i.e it won't force the programmer to extend/implement any class/interface.
* Since hibernate is non-invasive this helps to reduce the coupling i.e it makes the application loosely coupled.
* Hibernate was invented by **Gavin King**.
* Any type of application can be built using Hibernate Framework.

### Traditional way to save data (JDBC)
![Jdbc usage](/frameworks/Hibernate/img/JDBC_usage.png)

### Modern way to save data using Hibernate
![Hibernate usage](/frameworks/Hibernate/img/Hibernate_usage.png)

### Hibernate Configuration for Eclipse
- Add Hibernate dependency from the maven repository (if you are using maven).
- In Eclipse:- Right Click on your project -> select properties -> select java build path -> Go to   Libraries section -> remove existing JRE system library -> then click on add library -> Select JRE system library -> By default workspace default JRE radio is selected let it be selected and click finish.
- The naming convention for hibernate file is **hibernate.cfg.xml**.
- Copy paste this link in your hibernate.cfg.xml file.
```
  <!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
```
- You can download this dtd file click this link to [DOWNLOAD](https://hibernate.org/dtd/). Download the file named as hibernate-configuration-3.0.dtd.
- If you get any error like this **Downloading external resources is disabled** in your hibernate.cfg.xml in eclipse then follow the below steps to resolve the issue.
- Go to top bar : Window -> Preference -> Maven -> tick the option ('download artifact javadoc')    Thats is 'Apply & Close'.

### Hibernate Configuration Code
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using, here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using, 
			here I'm using MySql -->
		<!-- If you are using other version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->
		<!-- But if your are using latest version of hibernate then you need to add MySQL8Dialect-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>

		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>
	</session-factory>
</hibernate-configuration>
```

* Create database named as myHiber.
* To check that your hibernate configuration is proper or not use below code.
```java
package com.learningHibernate;

import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

/**
 * Hello world!
 *
 */
public class App {
	public static void main(String[] args) {
		System.out.println("Project Started");
		/*
		 * SessionFactory factory = new
		 * Configuration().configure().buildSessionFactory();
		 */
		Configuration cfg = new Configuration();

		/*
		 *  configure():- In this method you need to pass 
		 *                the path of your hibernate file in my case
		 *                it's is same directory so that's why I only 
		 *                need to add name of the hibernate file but if you file 
		 *  			  is located somewhere else then put that path
		 *                for Eg:- /com/project/hibernate.cfg.xml
		*/
		cfg.configure("hibernate.cfg.xml");
		SessionFactory factory = cfg.buildSessionFactory();
		System.out.println(factory);
		System.out.println(factory.isClosed());
	}
}
```

### First Hibernate Program

**Student.class**
```java
package com.learningHibernate;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

// Annotation
/*
 * This is a class level annotation which is used to make our class an Entity 
 */
@Entity
/*
 * @Entity("student_details"):- This is annotation can be used to change the name of our entity
*/
public class Student {
	// Instance Variable (Fields)
	
	@Id // This is annotation is used make our field as primary key
	private int id;
	
	private String name;
	private String city;

	// Constructors
	public Student() {
		super();
	}

	public Student(int id, String name, String city) {
		super();
		this.id = id;
		this.name = name;
		this.city = city;
	}

	// Getters & Setters
	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	@Override
	public String toString() {
		return this.id+ " : " + this.name +" : " + this.city;
	}
}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->

		<!-- 
			But if your are using latest version of hibernate then you need to add MySQL8Dialect
			In future, MySQL8Dialect this 8 can change so search on internet to see 
			what is tne new value.
		-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>
		
		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
	</session-factory>
</hibernate-configuration>
```

**App.java (Main Class)**
```java
package com.learningHibernate;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

/**
 * Hello world!
 *
 */
public class App {
	public static void main(String[] args) {
		System.out.println("Project Started");
		/*
		 * SessionFactory factory = new
		 * Configuration().configure().buildSessionFactory();
		 */
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory factory = cfg.buildSessionFactory();

		// Creating student object
		Student student = new Student();
		student.setId(101);
		student.setName("Jcole");
		student.setCity("Fayetteville");
		System.out.println(student);

		// To save our data into database
		Session session = factory.openSession();
		/*
		 * If we have already opened a session then we can use 
		 * factory.getCurrentSession() instead of factory.openSession()
		 */		

		/*
		 * Another you can do 
		 * ==================
		 * // Starting Transaction 
		 * session.beginTransaction(); 
		 * session.save(student);
		 * 
		 * // Committing changes 
		 * session.getTransaction().commit(); 
		 * session.close();
		 */

		// Starting Transaction
		Transaction transaction = session.beginTransaction();
		// saving our student obj
		session.save(student);
		// Committing changes
		transaction.commit();
		session.close();
	}
}
```

### COMMONLY USED HIBERNATE ANNOTATIONS
* ***@Entity:-*** This annotation is used to mark any class as Entity and it is used on the class.
* ***@Table:-*** This annotation is used to change the table details like table-name.
* ***@Id:-*** It is used to mark column as id(primary key).
* ***@GeneratedValue:-*** This annotation is used to automatically generate values, it uses an internal sequence. Therefore we don't have to set it manually.
* ***@Column:-*** This annotation can be used to specify column mappings. For eg. To change the column name in the associated table in database.
* ***@Transient:-*** This annotation works like gitignore it basically ignore the fields that we don't want in our table. For eg. City is one of the instance variable in our class Employee and we don't wont' to create the column City in our table. So we just have to put @Transient annotation on it.
* ***@Temporal:-*** With the help of @Temporal annotation we can specify in which format we want to store our date field.
* ***@Lob:-*** This annotation is used to specify our object as a large object i.e it's not a simple object.For eg. Blob, Clob, etc.
* ***Other annotations:-*** @OneToOne, @OneToMany, @ManyToOne, @JoinColumn etc.
* **Below program uses all above annotations**.

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->
		<!-- But if your are using latest version of hibernate then you need to add MySQL8Dialect-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>
		
		<!-- This property of hibernate helps to create table automatically -->
		<property name="hbm2ddl.auto">create</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />
	</session-factory>
</hibernate-configuration>
```

**Student.java**
```java
package com.learningHibernate;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

// Annotation
/*
 * This is a class level annotation which is used to make our class an Entity 
 */
@Entity
/*
 * @Entity("student_details"):- This is annotation can be used to change the name of our entity
*/
public class Student {
	// Instance Variable (Fields)
	
	@Id // This is annotation is used make our field as primary key
	private int id;
	
	private String name;
	private String city;

	// Constructors
	public Student() {
		super();
	}

	public Student(int id, String name, String city) {
		super();
		this.id = id;
		this.name = name;
		this.city = city;
	}

	// Getters & Setters
	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	@Override
	public String toString() {
		return this.id+ " : " + this.name +" : " + this.city;
	}
}
```

**Address.java**
```java
package com.learningHibernate;

import java.util.Date;

import com.mysql.cj.jdbc.Blob;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Lob;
import jakarta.persistence.Table;
import jakarta.persistence.Temporal;
import jakarta.persistence.TemporalType;
import jakarta.persistence.Transient;

@Entity
@Table(name = "student_address")
public class Address {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY) // This is used to auto increment our id
	@Column(name = "address_id") // We have changed the name of column from addressId to address_id
	private int addressId;

	@Column(length = 50, name = "STREET")
	private String street;

	@Column(length = 100, name = "CITY")
	private String city;

	@Column(name = "is_open")
	private boolean isOpen;

	@Transient // This column(field) will not be created in our table
	private double familyIncome;

	@Column(name = "date_added")
	@Temporal(TemporalType.DATE) // Format our Date Field
	private Date dateAdded;

	@Lob // Since image is an large object
	@Column(columnDefinition = "Blob")
	private byte[] image;

	public Address() {
		super();
	}

	public Address(int addressId, String street, String city, boolean isOpen, double familyIncome, Date dateAdded,
			byte[] image) {
		super();
		this.addressId = addressId;
		this.street = street;
		this.city = city;
		this.isOpen = isOpen;
		this.familyIncome = familyIncome;
		this.dateAdded = dateAdded;
		this.image = image;
	}

	public int getAddressId() {
		return addressId;
	}

	public void setAddressId(int addressId) {
		this.addressId = addressId;
	}

	public String getStreet() {
		return street;
	}

	public void setStreet(String street) {
		this.street = street;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	public boolean isOpen() {
		return isOpen;
	}

	public void setOpen(boolean isOpen) {
		this.isOpen = isOpen;
	}

	public double getFamilyIncome() {
		return familyIncome;
	}

	public void setFamilyIncome(double familyIncome) {
		this.familyIncome = familyIncome;
	}

	public Date getDateAdded() {
		return dateAdded;
	}

	public void setDateAdded(Date dateAdded) {
		this.dateAdded = dateAdded;
	}

	public byte[] getImage() {
		return image;
	}

	public void setImage(byte[] image) {
		this.image = image;
	}
}
```
**App.java (Main Class)**
```java
package com.learningHibernate;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Date;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

/**
 * Hello world!
 *
 */
public class App {
	public static void main(String[] args) throws IOException {
		System.out.println("Project Started");
		/*
		 * SessionFactory factory = new
		 * Configuration().configure().buildSessionFactory();
		 */
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory factory = cfg.buildSessionFactory();

		// Creating student object
		Student student = new Student();
		student.setId(101);
		student.setName("Jcole");
		student.setCity("Fayetteville");
		System.out.println(student);

		// Creating Address object
		Address address = new Address();
		address.setStreet("Street1");
		address.setCity("MUMBAI");
		address.setOpen(true);
		address.setDateAdded(new Date());
		address.setFamilyIncome(45468.85);

		// Reading image
		FileInputStream fis = new FileInputStream("src/main/java/sinner.png");
		byte[] imageDate = new byte[fis.available()];
		fis.read(imageDate);
		address.setImage(imageDate);

		// To save our data into database
		Session session = factory.openSession();

		/*
		 * If we have already opened a session then we can use
		 * factory.getCurrentSession() instead of factory.openSession()
		 */

		/*
		 * Another you can do 
		 * ================== 
		 * // Starting Transaction
		 * session.beginTransaction(); 
		 * session.save(student);
		 * // Committing changes 
		 * session.getTransaction().commit(); 
		 * session.close();
		 */

		// Starting Transaction
		Transaction transaction = session.beginTransaction();
		// saving our student obj
		session.save(student);
		session.save(address);

		// Committing changes
		transaction.commit();
		session.close();

		System.out.println("DONE..");

	}
}
```

### Fetch Data using get() method & load() method.

![get()Vsload()](/frameworks/Hibernate/img/get()VSload().png)

![understandlingGetandLoadMethod](/frameworks/Hibernate/img/understandingGetandLoadMethod.png)

**FetchDataUsingHibernate (Main Class)** (Use above code to run this program)
```java
package com.learningHibernate;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class FetchDataUsingHibernate {

	public static void main(String[] args) {
		// get, load and methods...
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = cfg.buildSessionFactory();
		Session session = sessionFactory.openSession();

		// First uncomment get() method then comment again afterwards uncomment load() method
		/*
		 * // get() method.. 
		 * System.out.println("---------------------------");
		 * System.out.println("Using get() method");
		 * System.out.println("---------------------------");
		 * 
		 * // Student Class 
		 * Student studentUsingGetMethod = (Student)session.get(Student.class, 101);
		 * System.out.println("Student Details using get() method :- " + studentUsingGetMethod + "\n");
		 * 
		 * // Address Class 
		 * Address address = (Address)session.get(Address.class, 1);
		 * System.out.println("Address details using get() method");
		 * System.out.println("City Name :- " + address.getCity());
		 * System.out.println("Street Name :- " + address.getStreet());
		 * 
		 * // Here, Hibernate won't write another select query because data is already
		 * // present in the cache memory
		 * Address againUsingAddress = (Address)session.get(Address.class, 1);
		 * System.out.println("City Name :- " + againUsingAddress.getCity());
		 * System.out.println("Street Name :- " + againUsingAddress.getStreet() + "\n");
		 * 
		 * // Here, get() method will return null since 3(id) is not there.
		 * Address secondAddress = (Address)session.get(Address.class, 3);
		 * System.out.println("Value :- " + secondAddress + "\n");
		 * 
		 */

		/*
		 * 
		 * // load() method.. 
		 * 
		 * System.out.println("---------------------------");
		 * System.out.println("Using load() method");
		 * System.out.println("---------------------------");
		 * 
		 * // In load() method if we do not used the object then hibernate will not create query
		 * // let the student details print statement be commented
		 * 
		 * Student studentUsingLoadMethod = (Student) session.load(Student.class, 102);
		 * // System.out.println("Student Details using load() method :- " + studentUsingLoadMethod + "\n");
		 * 
		 * // Here, same hibernate will not write any select query 
		 * 
		 * Student secondStudentUsingLoadMethod = (Student) session.load(Student.class, 101); 
		 * // uncomment below line to see the select query 
		 * // System.out.println("Student Details using load() method :- " + secondStudentUsingLoadMethod + "\n");
		 * 
		 * // Here, load() will give us an Exception saying ObjectNotFoundException
		 * // Uncomment below lines of code.
		 * 
		 * // Student studentUsingLoadMethodReturnsException = (Student)session.load(Student.class, 102); 
		 * // System.out.println(studentUsingLoadMethodReturnsException);
		 * 
		 */ 
		
		session.close();
		sessionFactory.close();
	}
}
```

### @Embeddable Annotation

![@Embeddable Annotation](/frameworks/Hibernate/img/EmbeddableAnnotation.png)

**EmbeddableAnnotation.java (Main Class)**
```java
package com.learningHibernate;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class EmbeddableAnnotation {

	public static void main(String[] args) {
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = cfg.buildSessionFactory();

		Student student = new Student();
		student.setId(69);
		student.setName("Ajay");
		student.setCity("Milf City");

		Certificate certificate = new Certificate();
		certificate.setCourse("Hibernate");
		certificate.setDuration("4 Months");
		student.setCertificate(certificate);
		
		Student yamaguchi = new Student();
		yamaguchi.setId(45);
		yamaguchi.setName("Yamaguchi");
		yamaguchi.setCity("Kyoto");
		
		Certificate yamaguchiCertificate = new Certificate();
		yamaguchiCertificate.setCourse("Linux");
		yamaguchiCertificate.setDuration("3 Months");
		yamaguchi.setCertificate(yamaguchiCertificate);
		
		Session session  = sessionFactory.openSession();
		Transaction transcation = session.beginTransaction();
		
		// Saving Objects
		session.save(student);
		session.save(yamaguchi);
		
		transcation.commit();
		session.close();
		sessionFactory.close();
	}
}
```

**Certificate.java**
```java
package com.learningHibernate;

import jakarta.persistence.Embeddable;

@Embeddable
public class Certificate {

	// Fields (Instance Variable)
	private String course;
	private String duration;

	// Contructors
	public Certificate() {
		super();
	}

	public Certificate(String course, String duration) {
		super();
		this.course = course;
		this.duration = duration;
	}

	// Setters & Getters
	public String getCourse() {
		return course;
	}

	public void setCourse(String course) {
		this.course = course;
	}

	public String getDuration() {
		return duration;
	}

	public void setDuration(String duration) {
		this.duration = duration;
	}

}
```

**Student.java**
```java
package com.learningHibernate;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

// Annotation
/*
 * This is a class level annotation which is used to make our class an Entity 
 */
@Entity
/*
 * @Entity("student_details"):- This is annotation can be used to change the
 * name of our entity
 */
public class Student {
	// Instance Variable (Fields)

	@Id // This is annotation is used make our field as primary key
	private int id;

	private String name;
	private String city;

	// Reference
	private Certificate certificate;

	// Constructors
	public Student() {
		super();
	}

	public Student(int id, String name, String city) {
		super();
		this.id = id;
		this.name = name;
		this.city = city;
	}

	// Getters & Setters
	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	public Certificate getCertificate() {
		return certificate;
	}

	public void setCertificate(Certificate certificate) {
		this.certificate = certificate;
	}

	@Override
	public String toString() {
		return this.id + " : " + this.name + " : " + this.city;
	}
}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->
		<!-- But if your are using latest version of hibernate then you need to add MySQL8Dialect-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>
		
		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">create</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />
	</session-factory>
</hibernate-configuration>
```

### OneToOne Mapping

![OneToOne Mapping](/frameworks/Hibernate/img/OneToOne.png)

**HibernateOneToOneMapping.java (main class)**
```java
package com.learninghibernatemapping;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class HibernateOneToOneMapping {

	public static void main(String[] args) {
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = cfg.buildSessionFactory();

		// Creating first question
		Question firstQuestion = new Question();
		firstQuestion.setQuestionId(1212);
		firstQuestion.setQuestion("What is Java?");

		// Creating first answer
		Answer firstAnswer = new Answer();
		firstAnswer.setAnswerId(343);
		firstAnswer.setAnswer("Java is a Programming Language");
		firstAnswer.setQuestion(firstQuestion);
		firstQuestion.setAnswer(firstAnswer);

		// Creating second question
		Question secondQuestion = new Question();
		secondQuestion.setQuestionId(242);
		secondQuestion.setQuestion("What is Collection Framework?");

		// creating second answer
		Answer secondAnswer = new Answer();
		secondAnswer.setAnswerId(344);
		secondAnswer.setAnswer("API to work with objects in Java");
		secondAnswer.setQuestion(secondQuestion);
		secondQuestion.setAnswer(secondAnswer);

		// Creating Session
		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();

		// Saving to DB
		session.save(firstQuestion);
		session.save(secondQuestion);
		session.save(firstAnswer);
		session.save(secondAnswer);

		transaction.commit();
		
		// Fetching 
		Question question = (Question) session.get(Question.class, 242);
		System.out.println(question.getQuestion());
		System.out.println(question.getAnswer().getAnswer());
		
		session.close();
		sessionFactory.close();
	}
}
```

**Question.java**
```java
package com.learninghibernatemapping;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.OneToOne;

@Entity
public class Question {

	@Id
	@Column(name = "question_id")
	private int questionId;
	
	private String question;
	
	@OneToOne
	@JoinColumn(name = "answer_id")
	private Answer answer;

	public Question() {
		super();
	}

	public Question(int questionId, String question, Answer answer) {
		super();
		this.questionId = questionId;
		this.question = question;
		this.answer = answer;
	}

	public int getQuestionId() {
		return questionId;
	}

	public void setQuestionId(int questionId) {
		this.questionId = questionId;
	}

	public String getQuestion() {
		return question;
	}

	public void setQuestion(String question) {
		this.question = question;
	}

	public Answer getAnswer() {
		return answer;
	}

	public void setAnswer(Answer answer) {
		this.answer = answer;
	}

}
```

**Answer.java**
```java
package com.learninghibernatemapping;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.OneToOne;

@Entity
public class Answer {

	@Id
	@Column(name = "answer_id")
	private int answerId;
	private String answer;
	
	@OneToOne(mappedBy = "answer")
	@JoinColumn(name = "question_id")
	private Question question;

	public Answer() {
		super();
	}

	public Answer(int answerId, String answer) {
		super();
		this.answerId = answerId;
		this.answer = answer;
	}

	public int getAnswerId() {
		return answerId;
	}

	public void setAnswerId(int answerId) {
		this.answerId = answerId;
	}

	public String getAnswer() {
		return answer;
	}

	public void setAnswer(String answer) {
		this.answer = answer;
	}

	public Question getQuestion() {
		return question;
	}

	public void setQuestion(Question question) {
		this.question = question;
	}

}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->
		<!-- But if your are using latest version of hibernate then you need to add MySQL8Dialect-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>
		
		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">create</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />
		
		<mapping class="com.learninghibernatemapping.Question" />
		<mapping class="com.learninghibernatemapping.Answer" />
		
	</session-factory>
</hibernate-configuration>
```

### OneToMany and ManyToOne Mapping

![OneToMany Mapping](/frameworks/Hibernate/img/OneToManyMapping.png)

**HibernateOnetoManyandManyToOneMapping.java**
```java
/*
 *  !Important to execute properly this code watch Durgesh Hibernate Tutorial
*/

package com.learninghibernatemapping;

import java.util.ArrayList;
import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class HibernateOnetoManyandManyToOneMapping {

	public static void main(String[] args) {
		Configuration cfg = new Configuration();
		cfg.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = cfg.buildSessionFactory();

		// Creating first question
		/*
		 * Question firstQuestion = new Question(); 
		 * firstQuestion.setQuestionId(1212);
		 * firstQuestion.setQuestion("What is Java?");
		 */
		
		// Creating first answer
		/*
		 * Answer firstAnswer = new Answer(); f
		 * irstAnswer.setAnswerId(343);
		 * firstAnswer.setAnswer("Java is a Programming Language");
		 * firstAnswer.setQuestion(firstQuestion);
		 */
		
		// Creating second answer
		/*
		 * Answer firstSecondAnswer = new Answer(); 
		 * firstSecondAnswer.setAnswerId(33);
		 * firstSecondAnswer.
		 * setAnswer("With the help of Java we can create applications");
		 * firstSecondAnswer.setQuestion(firstQuestion);
		 */

		// Creating third answer
		/*
		 * Answer firstThirdAnswer = new Answer(); 
		 * firstThirdAnswer.setAnswerId(363);
		 * firstThirdAnswer.setAnswer("Java is Statically Typed Language");
		 * firstThirdAnswer.setQuestion(firstQuestion);
		 */

		/*
		 * List<Answer> listOfAnswers = new ArrayList<Answer>();
		 * listOfAnswers.add(firstAnswer); 
		 * listOfAnswers.add(firstSecondAnswer);
		 * listOfAnswers.add(firstThirdAnswer); 
		 * firstQuestion.setAnswers(listOfAnswers);
		 */

		// Creating Session
		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();

		// Saving to DB
		/*
		 * session.save(firstQuestion); 
		 * session.save(firstAnswer);
		 * session.save(firstSecondAnswer); 
		 * session.save(firstThirdAnswer);
		 */
		
		Question question = (Question) session.get(Question.class, 1212);
		System.out.println(question.getQuestion());
		
		for(Answer answer : question.getAnswers()) {
			System.out.println(answer.getAnswer());
		}
		
		transaction.commit();
		session.close();
		sessionFactory.close();
	}
}
```

**Question.java**
```java
package com.learninghibernatemapping;

import java.util.List;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.OneToMany;

@Entity
public class Question {

	@Id
	@Column(name = "question_id")
	private int questionId;

	private String question;
	
	@OneToMany(mappedBy = "question")
	private List<Answer> answers;

	public Question() {
		super();
	}

	public Question(int questionId, String question, List<Answer> answers) {
		super();
		this.questionId = questionId;
		this.question = question;
		this.answers = answers;
	}

	public int getQuestionId() {
		return questionId;
	}

	public void setQuestionId(int questionId) {
		this.questionId = questionId;
	}

	public String getQuestion() {
		return question;
	}

	public void setQuestion(String question) {
		this.question = question;
	}

	public List<Answer> getAnswers() {
		return answers;
	}

	public void setAnswers(List<Answer> answers) {
		this.answers = answers;
	}
}
```
**Answer.java**
```java
package com.learninghibernatemapping;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.ManyToOne;

@Entity
public class Answer {

	@Id
	@Column(name = "answer_id")
	private int answerId;
	
	private String answer;
	
	@ManyToOne
	private Question question;

	public Answer() {
		super();
	}

	public Answer(int answerId, String answer) {
		super();
		this.answerId = answerId;
		this.answer = answer;
	}

	public int getAnswerId() {
		return answerId;
	}

	public void setAnswerId(int answerId) {
		this.answerId = answerId;
	}

	public String getAnswer() {
		return answer;
	}

	public void setAnswer(String answer) {
		this.answer = answer;
	}

	public Question getQuestion() {
		return question;
	}

	public void setQuestion(Question question) {
		this.question = question;
	}

}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property>-->
		<!-- But if your are using latest version of hibernate then you need to add MySQL8Dialect-->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>
		
		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />
		
		<mapping class="com.learninghibernatemapping.Question" />
		<mapping class="com.learninghibernatemapping.Answer" />
		
	</session-factory>
</hibernate-configuration>
```

### ManyToManyMapping

![ManyToManyMapping](/frameworks/Hibernate/img/ManyToManyMapping.png)

**HibernateManyToManyMapping.java (main Class)**
```java
package com.learninghibernatemapping;

import java.util.ArrayList;
import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class HibernateManyToManyMapping {

	public static void main(String[] args) {
		Configuration config = new Configuration();
		config.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = config.buildSessionFactory();

		// Creating Employees
		Emp firstEmp = new Emp();
		Emp secondEmp = new Emp();
		// Assigning names & id's
		firstEmp.setEid(34);
		firstEmp.setEname("Ram");
		secondEmp.setEid(69);
		secondEmp.setEname("Jonny Bhaiya");
		
		// Creating Projects
		Project firstProject = new Project();
		Project secondProject = new Project();
		// Assigning projects name & id
		firstProject.setPid(89);
		firstProject.setProjectName("Library Management System");
		secondProject.setPid(67);
		secondProject.setProjectName("CHATBOT");
		
		// Creating two lists:- Employee & Project list
		List<Project> listOfProjects = new ArrayList<Project>();
		List<Emp> listOfEmployees = new ArrayList<Emp>();
		
		// Adding Employees
		listOfEmployees.add(firstEmp);
		listOfEmployees.add(secondEmp);
		
		// Adding Projects
		listOfProjects.add(firstProject);
		listOfProjects.add(secondProject);
		
		// Assigning projects & employees
		firstEmp.setProjects(listOfProjects);
		secondProject.setEmp(listOfEmployees);
		
		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();
		
		// Saving to db
		session.save(firstEmp);
		session.save(secondEmp);
		session.save(firstProject);
		session.save(secondProject);
		
		// Committing
		transaction.commit();
		
		session.close();
		sessionFactory.close();
	}
}
```

**Emp.java**
```java
package com.learninghibernatemapping;

import java.util.List;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.JoinTable;
import jakarta.persistence.ManyToMany;

@Entity
public class Emp {

	@Id
	private int eid;
	private String ename;

	@ManyToMany
	@JoinTable
	(
			name = "emp_assign_to_project",
			joinColumns = {@JoinColumn(name = "eid")},
			inverseJoinColumns = {@JoinColumn(name="pid")}
	)
	private List<Project> projects;
	
	// Contructors
	public Emp() {
		super();
		// TODO Auto-generated constructor stub
	}

	public Emp(int eid, String ename, List<Project> projects) {
		super();
		this.eid = eid;
		this.ename = ename;
		this.projects = projects;
	}

	// Getters & Setters
	public int getEid() {
		return eid;
	}

	public void setEid(int eid) {
		this.eid = eid;
	}

	public String getEname() {
		return ename;
	}

	public void setEname(String ename) {
		this.ename = ename;
	}

	public List<Project> getProjects() {
		return projects;
	}

	public void setProjects(List<Project> projects) {
		this.projects = projects;
	}
	
}
```

**Project.java**
```java
package com.learninghibernatemapping;

import java.util.List;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.ManyToMany;

@Entity
public class Project {

	@Id
	private int pid;

	@Column(name = "project_name")
	private String projectName;

	@ManyToMany(mappedBy = "projects")
	private List<Emp> emps;

	// Contructors
	public Project() {
		super();
	}

	public Project(int pid, String projectName, List<Emp> emps) {
		super();
		this.pid = pid;
		this.projectName = projectName;
		this.emps = emps;
	}

	// Getters and Setters
	public int getPid() {
		return pid;
	}

	public void setPid(int pid) {
		this.pid = pid;
	}

	public String getProjectName() {
		return projectName;
	}

	public void setProjectName(String projectName) {
		this.projectName = projectName;
	}

	public List<Emp> getEmp() {
		return emps;
	}

	public void setEmp(List<Emp> emps) {
		this.emps = emps;
	}
}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property> -->
		<!-- But if your are using latest version of hibernate then you need to 
			add MySQL8Dialect -->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>

		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />

		<mapping class="com.learninghibernatemapping.Question" />
		<mapping class="com.learninghibernatemapping.Answer" />

		<mapping class="com.learninghibernatemapping.Emp" />
		<mapping class="com.learninghibernatemapping.Project" />
	</session-factory>
</hibernate-configuration>
```

### Fetch Type
 * Eager Fetch Type :- This will load the object on the spot.
 * Lazy Fetch Type :- This will load the object only when we use the get() method on it.

![Fetch type](/frameworks/Hibernate/img/FetchType.png)

**FetchUsingLazyAndEagerType.java (main class)**
```java
package com.learninghibernatemapping;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class FetchUsingLazyAndEagerType {

	public static void main(String[] args) {

		Configuration config = new Configuration();
		config.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = config.buildSessionFactory();

		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();

		Question question = (Question) session.get(Question.class, 1212);

		System.out.println(question.getQuestionId());
		System.out.println(question.getQuestion());
		
		// Lazy Loading
		/*
		 * Here, you can see the query that hibernate has execute 
		 * in that query it has only selected the question not the answer
		 * but the moment I try to get the answer it will load the answer
		 * 
		 * To see the difference just comment this print statement run the program see what query
		 * hibernate has executed 
		 * Uncomment program to again see what sql query hibernate has not executed.
		 * 
		*/
		
		System.out.println(question.getAnswers().size());
		
		transaction.commit();
		sessionFactory.close();
		session.close();
	}

}
```

**Question.java**
```java
package com.learninghibernatemapping;

import java.util.List;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.Id;
import jakarta.persistence.OneToMany;

@Entity
public class Question {

	@Id
	@Column(name = "question_id")
	private int questionId;

	private String question;
	
	// Fetch Type:- Eager loading default is lazy loading
	@OneToMany(mappedBy = "question", fetch = FetchType.EAGER)
	
	// Explicit Lazy loading
	// @OneToMany(mappedBy = "question", fetch = FetchType.LAZY)
	private List<Answer> answers;

	public Question() {
		super();
	}

	public Question(int questionId, String question, List<Answer> answers) {
		super();
		this.questionId = questionId;
		this.question = question;
		this.answers = answers;
	}

	public int getQuestionId() {
		return questionId;
	}

	public void setQuestionId(int questionId) {
		this.questionId = questionId;
	}

	public String getQuestion() {
		return question;
	}

	public void setQuestion(String question) {
		this.question = question;
	}

	public List<Answer> getAnswers() {
		return answers;
	}

	public void setAnswers(List<Answer> answers) {
		this.answers = answers;
	}
}
```

**hibernate.cfg.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property> -->
		<!-- But if your are using latest version of hibernate then you need to 
			add MySQL8Dialect -->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>

		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>
		
		<!-- This property is used to format our hibernate sql query -->
		<property name="format_sql">true</property>

		<!-- This is used to map our class so that hibernate can understand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learningHibernate.Student" />
		<mapping class="com.learningHibernate.Address" />

		<mapping class="com.learninghibernatemapping.Question" />
		<mapping class="com.learninghibernatemapping.Answer" />

		<mapping class="com.learninghibernatemapping.Emp" />
		<mapping class="com.learninghibernatemapping.Project" />
	</session-factory>
</hibernate-configuration>
```

### Hibernate Object State || Persistent Lifecycle 

![Hibernate Object State or Persistent Lifecycle ](/frameworks/Hibernate/img/HibernateObjectStateAndLifecycle.png)

#### This below code show all three states i.e Transient, Persistent and Detached except Removed try to perform Removed state on your own.
- For more clarity about Hibernate States Follow this [Link](https://nikhilsukhani.medium.com/hibernate-lifecycle-states-in-hibernate-transient-persistent-detached-removed-40ba2f689b07)

**HibernateObjectStates.java**
```java
package com.learninghibernatemapping;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.learningHibernate.Certificate;
import com.learningHibernate.Student;

public class HibernateObjectStates {
	public static void main(String[] args) {

		/*
		 * Practical Of Hibernate States:- Transient,Persistent, Detached and Removed.
		 */
		System.out.println("Hibernate States");
		SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();
		
		// Creating Student object
		Student student = new Student();
		student.setId(1414);
		student.setName("Hinata");
		student.setCity("Konoha");
		student.setCertificate(new Certificate("Java Spring Course", "6 months"));
		// Now this student object is in Transient state :- This is not associated with Session and database.
		
		Session session  = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();
		session.save(student);
		// After saving our student object to db
		// Now this our student object is associated with Session and Database
		// Hence, our student object is in Persistent state
		
		// Modified our object
		student.setName("Naruto");
		transaction.commit();
		
		/*
		 * Detached state:- Now our student object goes in detached state which means 
		 * it is not associated with our session but it still associated with our Database
		 */
		session.close();
		
		/*
		 * If we delete our object then our student object goes into Removed state 
		 * which means it is not associated with our database but it is still
		 * associated with our session
		*/	
		// session.delete(student);
		
		/* As you can see since our session is closed so whatever changes me make 
		 * won't reflect in our database since our student object is in detached state
		*/
		student.setName("Sasuke");
		System.out.println(student);
		
		sessionFactory.close();
	}
}
```

### HQL | Hibernate Query Language

![Hibernate Query Language](/frameworks/Hibernate/img/Hql.png)

**HibernateQueryLanguageLearning.java (Main Class)**
```java
package com.learninghibernate.hql;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.Query;

import com.learninghibernate.Student;

public class HibernateQueryLanguageLearning {
	
	public static void main(String[] args) {
		Configuration configuration = new Configuration();	
		configuration.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = configuration.buildSessionFactory();
		
		Session session = sessionFactory.openSession();
		
		// Firing HQL query
		// Syntax
		String hqlQuery = "from Student";
		Query query = session.createQuery(hqlQuery);
		
		/* Unique result :- If we are expecting a single result */
		//query.uniqueResult();
		
		/* List Result :- If we are expecting multiple results */
		List<Student> listOfStudents = query.list();
		
		System.out.println("Student Names");
		System.out.println("==============");
		for(Student student : listOfStudents) {
			System.out.println(student.getName());
		}
		
		// Here, city is the instance variable name in Student class not the table name
		String hqlWhereQuery = "from Student where city = 'kyoto'";
		Query whereQuery = session.createQuery(hqlWhereQuery);
		
		List<Student> listOfStudentInKyoto = whereQuery.list();
		
		System.out.println("Students who live in Kyoto");
		System.out.println("=======================");
		for(Student kyotoStudent : listOfStudentInKyoto) {
			System.out.println(kyotoStudent.getName()+" : "+kyotoStudent.getCity()+" : "+kyotoStudent.getCertificate().getCourse());
		}
		
		// Dynamic Query and alias to set parameters
		// Here, =:city is like a temporary variable that we can assign later like we have used below
		String hqlDynamicQuery = "from Student s where s.city =:city and s.name =:name";
		Query dynamicQuery = session.createQuery(hqlDynamicQuery);
		dynamicQuery.setParameter("city","milf city");
		dynamicQuery.setParameter("name", "Ajay");
		
		List<Student> listOfStudentsInOsaka = dynamicQuery.list();
		
		System.out.println("Student who live in Milf City");
		System.out.println("=======================");
		for(Student milfCityStudent : listOfStudentsInOsaka) {
			System.out.println(milfCityStudent.getName()+" : "+milfCityStudent.getCity()+" : "+milfCityStudent.getCertificate().getCourse());
		}
		
		session.close();
		sessionFactory.close();
	}
}
```

### HQL:- Delete Query

```java
package com.learninghibernate.hql;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.Query;

import com.learninghibernate.Student;

public class HibernateQueryLanguageLearning {

	public static void main(String[] args) {
		Configuration configuration = new Configuration();
		configuration.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = configuration.buildSessionFactory();

		Session session = sessionFactory.openSession();

		// Firing HQL query
		// Syntax
		String hqlQuery = "from Student";
		Query query = session.createQuery(hqlQuery);

		/* Unique result :- If we are expecting a single result */
		// query.uniqueResult();

		/* List Result :- If we are expecting multiple results */
		List<Student> listOfStudents = query.list();

		System.out.println("Student Names");
		System.out.println("==============");
		for (Student student : listOfStudents) {
			System.out.println(student.getName());
		}

		// Here, city is the instance variable name in Student class not the table name
		String hqlWhereQuery = "from Student where city = 'kyoto'";
		Query whereQuery = session.createQuery(hqlWhereQuery);

		List<Student> listOfStudentInKyoto = whereQuery.list();

		System.out.println("Students who live in Kyoto");
		System.out.println("=======================");
		for (Student kyotoStudent : listOfStudentInKyoto) {
			System.out.println(kyotoStudent.getName() + " : " + kyotoStudent.getCity() + " : "
					+ kyotoStudent.getCertificate().getCourse());
		}

		// Dynamic Query and alias to set parameters
		// Here, =:city is like a temporary variable that we can assign later like we
		// have used below
		String hqlDynamicQuery = "from Student s where s.city =:city and s.name =:name";
		Query dynamicQuery = session.createQuery(hqlDynamicQuery);
		dynamicQuery.setParameter("city", "milf city");
		dynamicQuery.setParameter("name", "Ajay");

		List<Student> listOfStudentsInOsaka = dynamicQuery.list();

		System.out.println("Student who live in Milf City");
		System.out.println("=======================");
		for (Student milfCityStudent : listOfStudentsInOsaka) {
			System.out.println(milfCityStudent.getName() + " : " + milfCityStudent.getCity() + " : "
					+ milfCityStudent.getCertificate().getCourse());
		}
		
		System.out.println("-------------------------------------------------------");
		System.out.println("-------------------------------------------------------");
		
        // Delete Query in Hibernate
		Transaction transac = session.beginTransaction();
		Query deleteQuery = session.createQuery("delete from Student s where s.city=:c");
		deleteQuery.setParameter("c", "Kyoto");
		int noOfEntritesdeleted =  deleteQuery.executeUpdate();
		System.out.println("No Of Entries Deleted " + noOfEntritesdeleted);
		transac.commit();

		session.close();
		sessionFactory.close();
	}
}
```

### HQL:- Update Query In Hibernate

```java
package com.learninghibernate.hql;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.Query;

import com.learninghibernate.Student;

public class HibernateQueryLanguageLearning {

	public static void main(String[] args) {
		Configuration configuration = new Configuration();
		configuration.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = configuration.buildSessionFactory();

		Session session = sessionFactory.openSession();

		// Firing HQL query
		// Syntax
		String hqlQuery = "from Student";
		Query query = session.createQuery(hqlQuery);

		/* Unique result :- If we are expecting a single result */
		// query.uniqueResult();

		/* List Result :- If we are expecting multiple results */
		List<Student> listOfStudents = query.list();

		System.out.println("Student Names");
		System.out.println("==============");
		for (Student student : listOfStudents) {
			System.out.println(student.getName());
		}

		// Here, city is the instance variable name in Student class not the table name
		String hqlWhereQuery = "from Student where city = 'kyoto'";
		Query whereQuery = session.createQuery(hqlWhereQuery);

		List<Student> listOfStudentInKyoto = whereQuery.list();

		System.out.println("Students who live in Kyoto");
		System.out.println("=======================");
		for (Student kyotoStudent : listOfStudentInKyoto) {
			System.out.println(kyotoStudent.getName() + " : " + kyotoStudent.getCity() + " : "
					+ kyotoStudent.getCertificate().getCourse());
		}

		// Dynamic Query and alias to set parameters
		// Here, =:city is like a temporary variable that we can assign later like we
		// have used below
		String hqlDynamicQuery = "from Student s where s.city =:city and s.name =:name";
		Query dynamicQuery = session.createQuery(hqlDynamicQuery);
		dynamicQuery.setParameter("city", "milf city");
		dynamicQuery.setParameter("name", "Ajay");

		List<Student> listOfStudentsInOsaka = dynamicQuery.list();

		System.out.println("Student who live in Milf City");
		System.out.println("=======================");
		for (Student milfCityStudent : listOfStudentsInOsaka) {
			System.out.println(milfCityStudent.getName() + " : " + milfCityStudent.getCity() + " : "
					+ milfCityStudent.getCertificate().getCourse());
		}
		
		System.out.println("-------------------------------------------------------");
		System.out.println("-------------------------------------------------------");
		
        // Delete Query in Hibernate
//		Transaction transac = session.beginTransaction();
//		Query deleteQuery = session.createQuery("delete from Student s where s.city=:c");
//		deleteQuery.setParameter("c", "Kyoto");
//		int noOfEntritesdeleted =  deleteQuery.executeUpdate();
//		System.out.println("No Of Entries Deleted " + noOfEntritesdeleted);
//		transac.commit();		
		
		// Update Query in Hibernate
		Transaction transac = session.beginTransaction();
		Query updateQuery = session.createQuery("update Student set city=:c where name=:n");
		updateQuery.setParameter("c", "Summerville");
		updateQuery.setParameter("n", "Ajay");
		int noOfEntriedUpdated = updateQuery.executeUpdate();
		System.out.println("No Of Entries Update " + noOfEntriedUpdated);
		transac.commit();

		session.close();
		sessionFactory.close();
	}
}
```

### HQL:- Join Query In Hibernate

```java
package com.learninghibernate.hql;

import java.util.Arrays;
import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.Query;

import com.learninghibernate.Student;

public class HibernateQueryLanguageLearning {

	public static void main(String[] args) {
		Configuration configuration = new Configuration();
		configuration.configure("hibernate.cfg.xml");
		SessionFactory sessionFactory = configuration.buildSessionFactory();

		Session session = sessionFactory.openSession();

		// Firing HQL query
		// Syntax
		String hqlQuery = "from Student";
		Query query = session.createQuery(hqlQuery);

		/* Unique result :- If we are expecting a single result */
		// query.uniqueResult();

		/* List Result :- If we are expecting multiple results */
		List<Student> listOfStudents = query.list();

		System.out.println("Student Names");
		System.out.println("==============");
		for (Student student : listOfStudents) {
			System.out.println(student.getName());
		}

		// Here, city is the instance variable name in Student class not the table name
		String hqlWhereQuery = "from Student where city = 'kyoto'";
		Query whereQuery = session.createQuery(hqlWhereQuery);

		List<Student> listOfStudentInKyoto = whereQuery.list();

		System.out.println("Students who live in Kyoto");
		System.out.println("=======================");
		for (Student kyotoStudent : listOfStudentInKyoto) {
			System.out.println(kyotoStudent.getName() + " : " + kyotoStudent.getCity() + " : "
					+ kyotoStudent.getCertificate().getCourse());
		}

		// Dynamic Query and alias to set parameters
		// Here, =:city is like a temporary variable that we can assign later like we
		// have used below
		String hqlDynamicQuery = "from Student s where s.city =:city and s.name =:name";
		Query dynamicQuery = session.createQuery(hqlDynamicQuery);
		dynamicQuery.setParameter("city", "milf city");
		dynamicQuery.setParameter("name", "Ajay");

		List<Student> listOfStudentsInOsaka = dynamicQuery.list();

		System.out.println("Student who live in Milf City");
		System.out.println("=======================");
		for (Student milfCityStudent : listOfStudentsInOsaka) {
			System.out.println(milfCityStudent.getName() + " : " + milfCityStudent.getCity() + " : "
					+ milfCityStudent.getCertificate().getCourse());
		}

		System.out.println("-------------------------------------------------------");
		System.out.println("-------------------------------------------------------");

		// Delete Query in Hibernate
//		Transaction transac = session.beginTransaction();
//		Query deleteQuery = session.createQuery("delete from Student s where s.city=:c");
//		deleteQuery.setParameter("c", "Kyoto");
//		int noOfEntritesdeleted =  deleteQuery.executeUpdate();
//		System.out.println("No Of Entries Deleted " + noOfEntritesdeleted);
//		transac.commit();

		// Update Query in Hibernate
//		Transaction transac = session.beginTransaction();
//		Query updateQuery = session.createQuery("update Student set city=:c where name=:n");
//		updateQuery.setParameter("c", "Summerville");
//		updateQuery.setParameter("n", "Ajay");
//		int noOfEntriedUpdated = updateQuery.executeUpdate();
//		System.out.println("No Of Entries Update " + noOfEntriedUpdated);
//		transac.commit();
		
		// Joins in Hibernate
		Transaction transact = session.beginTransaction();
		Query joinQuery = session.createQuery("select q.question, q.questionId, a.answer from Question as q INNER JOIN q.answers as a");
		
		List<Object[]> listOfJoinResult = joinQuery.getResultList();
		for(Object[] result : listOfJoinResult) {
			System.out.println(Arrays.toString(result));
		}
		
		transact.commit();

		session.close();
		sessionFactory.close();
	}
}
```

### Pagination
![HQL Pagination](/frameworks/Hibernate/img/HqlPagination.png)

**pagination.java**

```java
package com.learninghibernate.pagination;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.Query;

import com.learninghibernate.Student;

public class HQLPagination {

	public static void main(String[] args) {

		SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
		Session session = sessionFactory.openSession();

		Query queryObject  = session.createQuery("from Student");
		// Implementing Pagination
		
		// This is shows from which index which want to start
		// 0 to 4
		queryObject.setFirstResult(0);
		
		// This is shows maximum result (page size)
		queryObject.setMaxResults(10);
		
		List<Student> listOfStudents = queryObject.list();
		
		for(Student student : listOfStudents) {
			System.out.println(student.getId()+ " : " +student.getName() + " : " + student.getCity());
		}
		
		session.close();
		sessionFactory.close();
	}
}
```

### SQL Query In Hibernate

**SqlUsingHibernate.java**

```java
package com.learninghibernate.sqlquery;

import java.util.Arrays;
import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;
import org.hibernate.query.NativeQuery;

import com.learninghibernate.Student;

public class SqlUsingHibernate {

    public static void main(String[] args) {
        SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
        Session session = sessionFactory.openSession();
        
        // This is SQL query
        String query = "select * from Student";
        NativeQuery<Object[]> ng = session.createNativeQuery(query);
        List<Object[]> list = ng.list();
        
        for (Object[] student : list) {
            System.out.println(student[4]+ " : " + student[1]);
        }
        
        session.close();
        sessionFactory.close();
    }
}
```

### Cascading

**HibernateCascading.java**

```java
package com.learninghibernate.cascading;

import java.util.ArrayList;
import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.learninghibernate.mapping.Answer;
import com.learninghibernate.mapping.Question;

import jakarta.persistence.CascadeType;
import jakarta.persistence.FetchType;
import jakarta.persistence.OneToMany;

public class HibernateCascading {

	public static void main(String[] args) {
		
		SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
		Session session = sessionFactory.openSession();
		
		// Hibernate Cascading
		/* 
		 * Apply This On Your Entity In My Case I Will Apply This On Question Class
		 * @OneToMany(mappedBy = "question", fetch = FetchType.LAZY, cascade = CascadeType.ALL)
		 */
		Question firstQuestion = new Question();
		firstQuestion.setQuestionId(567);
		firstQuestion.setQuestion("What is hibernate cascading");
		
		Answer firstAnswer = new Answer(234, "In hibernate it is an important concept");
		Answer secondAnswer = new Answer(235, "Cascading can be a very useful feature");
		Answer thirdAnswer = new Answer(236, "Only cascade operations that you need");
		
		List<Answer> listOfAnswers = new ArrayList<>();
		listOfAnswers.add(firstAnswer);
		listOfAnswers.add(secondAnswer);
		listOfAnswers.add(thirdAnswer);
		
		firstQuestion.setAnswers(listOfAnswers);
		Transaction transaction = session.beginTransaction();
	
		session.save(firstQuestion);
		transaction.commit();
		session.close();
		sessionFactory.close();
	}
}
```

**Question.java**
```java
package com.learninghibernate.mapping;

import java.util.List;

import jakarta.persistence.CascadeType;
import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.Id;
import jakarta.persistence.OneToMany;

@Entity
public class Question {

	@Id
	@Column(name = "question_id")
	private int questionId;

	private String question;
	
	// Fetch Type:- Eager loading default is lazy loading
	//@OneToMany(mappedBy = "question", fetch = FetchType.EAGER)
	
	// Explicit Lazy loading
	@OneToMany(mappedBy = "question", fetch = FetchType.LAZY, cascade = CascadeType.ALL)
	private List<Answer> answers;

	public Question() {
		super();
	}

	public Question(int questionId, String question, List<Answer> answers) {
		super();
		this.questionId = questionId;
		this.question = question;
		this.answers = answers;
	}

	public int getQuestionId() {
		return questionId;
	}

	public void setQuestionId(int questionId) {
		this.questionId = questionId;
	}

	public String getQuestion() {
		return question;
	}

	public void setQuestion(String question) {
		this.question = question;
	}

	public List<Answer> getAnswers() {
		return answers;
	}

	public void setAnswers(List<Answer> answers) {
		this.answers = answers;
	}
}
```

### Caching
![Caching In Hibernate](/frameworks/Hibernate/img/HibernateCaching.png)

### Types Of Hibernate Caching
![Types Of Hibernate Caching](/frameworks/Hibernate/img/TypesOfHibernateCaching.png)

### First Level Caching

**FirstLevelHibernateCaching.java**

```java
package com.learninghibernate.caching;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

import com.learninghibernate.Student;

public class FirstLevelHibernateCaching {
	
	public static void main(String[] args) {
	
		SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
		Session session = sessionFactory.openSession();
		
		// First Level Caching BY DEFAULT ENABLE
		Student student = session.get(Student.class, 2);
		System.out.println(student);
		
		System.out.println("Working on Something.............");
		/* 
		 * Here, in the console you can see that hibernate 
		 * has first fired the query for the object
		 * but again if we try to access the same object
		 * so hibernate will the return the object from it's cache memory
		 * In console you can see that the query has been fired only once
		*/
		Student student2 = session.get(Student.class, 2);
		System.out.println(student2);
		
		// This method shows that Student object is avaible in the cache memory
		System.out.println(session.contains(student2));
		
		session.close();
		sessionFactory.close();
		
	}
}
```

### Second Level Caching
#### BELOW CODE HAVE ERRORS RESOLVE THE ERRORS TO SEE THE RESULTS OR WATCH DURGESH VIDEO OF HIBERNATE SERIES.

**SecondLevelCaching.java**

```java
package com.learninghibernate.caching;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

import com.learninghibernate.Student;

public class SecondLevelCaching {
    
    public static void main(String[] args) {
    	
        SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
        Session firstSession = sessionFactory.openSession();
        
        // First
        Student studentFirst = firstSession.get(Student.class, 2);
        System.out.println(studentFirst);
        firstSession.close();
        
        Session secondSession = sessionFactory.openSession();
        // Second
        Student studentSecond = secondSession.get(Student.class, 2);
        System.out.println(studentSecond);
        secondSession.close();
        
        sessionFactory.close();
    }
}
```

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.learningHibernate</groupId>
	<artifactId>HibernateLearning</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>HibernateLearning</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>

		<!-- Hibernate Maven Dependency -->
		<!-- https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core -->
		<dependency>
			<groupId>org.hibernate.orm</groupId>
			<artifactId>hibernate-core</artifactId>
			<version>6.3.0.Final</version>
		</dependency>

		<!-- Mysql Maven Dependency -->
		<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
		<dependency>
			<groupId>com.mysql</groupId>
			<artifactId>mysql-connector-j</artifactId>
			<version>8.0.33</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/net.sf.ehcache/ehcache -->
		<dependency>
			<groupId>net.sf.ehcache</groupId>
			<artifactId>ehcache</artifactId>
			<version>2.10.9.2</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-ehcache -->
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-ehcache</artifactId>
			<version>5.6.15.Final</version>
		</dependency>


		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>
```

**hibernate.cfg.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property> -->
		<!-- But if your are using latest version of hibernate then you need to 
			add MySQL8Dialect -->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>

		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This property is used to format our hibernate sql query -->
		<property name="format_sql">true</property>

		<!-- Enable second-level cache -->
		<property name="hibernate.cache.use_second_level_cache">true</property>
		<!-- Specify the second-level cache provider -->
		<property name="hibernate.cache.region.factory_class">org.hibernate.cache.ehcache.EhCacheRegionFactory</property>

		<!-- This is used to map our class so that hibernate can unders tand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learninghibernate.Student" />
		<mapping class="com.learninghibernate.Address" />

		<mapping class="com.learninghibernate.mapping.Question" />
		<mapping class="com.learninghibernate.mapping.Answer" />

		<mapping class="com.learninghibernate.mapping.Emp" />
		<mapping class="com.learninghibernate.mapping.Project" />
	</session-factory>
</hibernate-configuration>
```

### Mapping Using XML file
![XML Mapping](/frameworks/Hibernate/img/mappingusingxml.png)
**TestingMapping.java (Main class)**

```java
package com.learninghibernate.mappingusingxml;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class TestingMapping {
	
	public static void main(String[] args) {
		
		SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();

		Person person = new Person(12, "Ajay", "Mumbai","4628942034");
		
		Session session = sessionFactory.openSession();
		
		Transaction transaction = session.beginTransaction();
		
		session.save(person);
		
		transaction.commit();
		session.close();
		sessionFactory.close();
	}
}
```

**Person.java**

```java
package com.learninghibernate.mappingusingxml;

public class Person {

	private int id;
	private String name;
	private String address;
	private String phone;

	public Person() {
		super();
	}

	public Person(int id, String name, String address, String phone) {
		super();
		this.id = id;
		this.name = name;
		this.address = address;
		this.phone = phone;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	public String getPhone() {
		return phone;
	}

	public void setPhone(String phone) {
		this.phone = phone;
	}
}
```

**Person.hbm.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC
	"-//Hibernate/Hibernate Mapping DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">

<hibernate-mapping>
	<class name="com.learninghibernate.mappingusingxml.Person" table="person">
		<id name="id" column="person_id">
			<generator class="native"></generator>
		</id>
		<property name="name" column="person_name" type="string" />
		<property name="address" column="person_address"
			type="string" />
		<property name="phone" column="person_phone" type="string" />
	</class>
</hibernate-mapping>
```

**hibernate.cfg.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
	<session-factory>
		<!-- We have to mention which Driver are we using here we are using MySql -->
		<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>

		<!-- Mention your database url -->
		<property name="connection.url">jdbc:mysql://localhost:3306/myHiber</property>

		<!-- Provide your database username and password -->
		<property name="connection.username">ocean</property>
		<property name="connection.password">ocean@root</property>

		<!-- dialect is a property which is specific for the database you are using 
			here since I'm using MySql -->
		<!-- If you are using older version of version of hibernate -->
		<!-- <property name="dialect">org.hibernate.dialect.MySQLDialect</property> -->
		<!-- But if your are using latest version of hibernate then you need to 
			add MySQL8Dialect -->
		<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>

		<!-- This property of hibernate helps to UPDATE table automatically -->
		<property name="hbm2ddl.auto">update</property>

		<!-- This property is used to see what query hibernate has fired -->
		<property name="show_sql">true</property>

		<!-- This property is used to format our hibernate sql query -->
		<property name="format_sql">true</property>

		
		<!-- This is used to map our class so that hibernate can unders tand that 
			we have a class that should be treated as an entity -->
		<mapping class="com.learninghibernate.Student" />
		<mapping class="com.learninghibernate.Address" />

		<mapping class="com.learninghibernate.mapping.Question" />
		<mapping class="com.learninghibernate.mapping.Answer" />

		<mapping class="com.learninghibernate.mapping.Emp" />
		<mapping class="com.learninghibernate.mapping.Project" />
		
		<!-- xml mapping -->
		<mapping resource="com/learninghibernate/mappingusingxml/Person.hbm.xml"/>
	</session-factory>
</hibernate-configuration>
```

### Hibernate Criteria API | Criteria Restrictions

**CriteriaDemo.java**

```java
package com.learninghibernate.criteria;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.cfg.Configuration;

import com.learninghibernate.Certificate;
import com.learninghibernate.Student;

import jakarta.persistence.criteria.CriteriaBuilder;
import jakarta.persistence.criteria.CriteriaQuery;
import jakarta.persistence.criteria.Join;
import jakarta.persistence.criteria.Predicate;
import jakarta.persistence.criteria.Root;

public class CriteriaDemo {

	public static void main(String[] args) {

		Session session = new Configuration().configure().buildSessionFactory().openSession();

		// Using CriteriaBuilder with Restriction
		CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
		CriteriaQuery<Student> criteriaQuery = criteriaBuilder.createQuery(Student.class);
		Root<Student> root = criteriaQuery.from(Student.class);
		criteriaQuery.select(root);

		// Adding the join to navigate to the certificate attribute
		Join<Student, Certificate> certificateJoin = root.join("certificate");

		// Adding the restriction
		Predicate coursePredicate = criteriaBuilder.equal(certificateJoin.get("course"), "C++");
		criteriaQuery.where(coursePredicate);

		List<Student> listOfStudents = session.createQuery(criteriaQuery).getResultList();

		for (Student student : listOfStudents) {
			System.out.println(student);
		}

		session.close();
	}
}
```