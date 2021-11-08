# Classes and Objects

Object-oriented programming was created to allow programmers to model code in a similar way to how things are categorized in real-life. A class is essentially a blueprint for a category of things, and it specifies the characteristics and behaviors that the things in that category have in common (Eck, 2019, ch. 5.1.1). We can use a class to create objects to represent the individual things in that category.

For example, user accounts on a website all share the same template for data and behavior. Each user account has a username and a password. Account passwords can be changed and usernames can be modified. And the system will be able to view passwords and usernames to verify if the person attempting to log in should be allowed to. So even though no two user accounts will look exactly the same, they can all be modeled using the template. 

Consider the following class *Account* which represents a user account. This class has two String variables to represent the username and the password for the account. When someone tries to create a new account, the constructor Account will be called and will initialize the username and password variables to the values passed to the constructor. There are also getter and setter methods to view and change the password and username for the account.

```java
public class Account {
	String username;
	String password;
	
	public Account(String name, String pw) { // constructor
		username = name;
		password = pw;
	}
	
	public void setPassword(String pw) {
		password = pw;
	}
	
	public String getPassword() {
		return password;
	}
	
	public void setUsername(String usern) {
		username = usern;
	}
	
	public String getUsername() {
		return username;
	}

}
```

Now that we have an *Account* class, we can use it to actually create accounts. In the below program, we declare two *Account* variables called *sarah* and *ben*. Then, we create two new *Account* objects and assign the **references** to these objects to our variables. Using some print statements, we test that these objects were created by getting the values for their usernames and passwords.  

```java
Account sarah;
Account ben;

sarah = new Account("sbober","mypw");
ben = new Account("benny","thispw");

System.out.println("Sarah's username and password:");
System.out.println(sarah.getUsername());
System.out.println(sarah.getPassword());

System.out.println("Ben's username and password:");
System.out.println(ben.getUsername());
System.out.println(ben.getPassword());
```

Output:

```java
Sarah's username and password:
sbober
mypw
Ben's username and password:
benny
thispw
```

It is important to note that object variables do not actually contain objects. They contain references to objects, which is essentially their address in the computer's memory (Eck, 2019, ch. 5.1.2). If we reassign an object variable's value, we are just making it refer to a different object. 

In this program, the *ben* variable is reassigned to the same reference as the *sarah* variable. Now, both variables are pointing to the same object. When we use one of the variables to make changes to the object, the other variable "sees" the changes because they are both referring to the same object in memory. 

```java
ben = sarah;
ben.setPassword("ilikeben");

System.out.println();
System.out.println("Values after reassignment:");
System.out.println("Sarah's username and password:");
System.out.println(sarah.getUsername());
System.out.println(sarah.getPassword());

System.out.println("Ben's username and password:");
System.out.println(ben.getUsername());
System.out.println(ben.getPassword());
```

Output:

```java
Values after reassignment:
Sarah's username and password:
sbober
ilikeben
Ben's username and password:
sbober
ilikeben
```


## Reference

Eck, D. J. (2019). Introduction to programming using Java, version 8.1. [http://math.hws.edu/javanotes](http://math.hws.edu/javanotes)