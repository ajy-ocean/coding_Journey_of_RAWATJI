# Hibernate Framework

#### INDEX
* [What is Hibernate FrameWork](#what-is-hibernate-framework)
* [Hibernate Configuration For Eclipse](#hibernate-configuration-for-eclipse)
* [Hibernate Configuration Code](#hibernate-configuration-code)
* [First Hibernate Program](#first-hibernate-program)
* [Commonly Used Hibernate Annotations](#commonly-used-hibernate-annotations)

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

* Student.class
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

* hibernate.cfg.xml
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

* App.java (Main Class)
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

hibernate.cfg.xml
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

Student.java
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

Address.java
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

	@Transient // This column(field) will not created in our table
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
App.java
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







