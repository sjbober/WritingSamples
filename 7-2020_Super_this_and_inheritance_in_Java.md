# Super, this, and inheritance in Java

Before learning about ***super*** and ***this***, we might have defined a class that represents a user account like this:

```java
public class Account {
	// Instance variables
	private String username;
	private String password;
	private String email;
	
	// Constructor
	public Account(String name, String pw, String em) {
		username = name;
		password = pw;
		email = em;
	}
}
```

In the constructor, the names of the parameters are different from the names of the instance variables, which is fine, but conceptually it can be a bit confusing because they represent the same characteristics for the new object. But, we can't give them the same exact names due to scope rules, because an instance variable will be hidden in a method or constructor if we give a parameter or local variable the same name (Eck, 2019, ch. 4.8.4). For example, if we changed our parameter names to match our instance variables, we would have the following constructor: 

```java
public Account(String username, String password, String email) {
	username = username;
	password = password;
	email = email;
}
```

But, this constructor is useless. It just assigns each parameter to itself and does not change a single instance variable. 

However, the keyword ***this*** can be used like a variable in a class to represent the object that is being created or has had its method called. We can use the dot operator "." to access the properties for that object (Eck, 2019, ch 5.6.1). For example, we can rewrite our constructor like this:

```java
public Account(String username, String password, String email) {
	this.username = username;
	this.password = password;
	this.email = email;
}
```

When this constructor is called, it assigns the instance variables for *this new object* to the arguments passed in the constructor call. And because we used ***this*** to access the object's variables, the compiler can easily tell the difference between the parameters and the global instance variables.

In a similar way, ***this*** can also represent the class that directly contains (as in, not a superclass or subclass) the object and be used as a constructor (Eck, 2019, ch. 5.6.3). For example, let's say we want to write another constructor that only takes two parameters because the email field is optional. We could write a constructor like this:

```java
public Account(String username, String password, String email) {
	this.username = username;
	this.password = password;
}
```

This constructor works fine, but you'll notice that we duplicated the same two lines from the first constructor. This might not seem like an issue now, but what happens if we decide to add additional code to make sure the username doesn't already exist in the system, or that the password meets strict security requirements? We would have to make code changes for both constructors, which means duplicate work and more room for error. 

Instead, we can use ***this*** to act as a constructor for the class, like so:

```java
public Account(String username, String password) {
	this(username,password, null);
}
```

This constructor calls the constructor in *this class* that has three parameters, and whose parameters are Strings (there should only be one constructor that meets these criteria, based on method overloading rules). So this constructor actually calls the constructor we defined earlier and just passes its parameters and one null value to that constructor call.

***Super*** is a keyword that behaves similarly to ***this*** but is used when we want to access properties of an object's superclass (Eck, 2019, ch. 5.6.2). For example, let's say we want to create a subclass of Account that has extra privileges for Admin users. We want to use the same constructors as the superclass to save time, but we know that constructor methods are not passed down to subclasses (Eck, 2019, ch. 5.6.3). 

For the constructor with three parameters, we could write the following: 

```java
public class Admin extends Account {
	// Constructor
	public Admin(String username, String password, String email) {
		super(username, password, email);
	}
}
```

This subclass constructor just calls the constructor of the superclass that has three String parameters and passes its parameters as arguments. 

For the subclass constructor with two parameters, we actually have two options. We could use ***super*** again to call the constructor of the superclass with three parameters, like this:

```java
public Admin(String username, String password) {
		super(username,password, null);
	}
```

Or, we can call the constructor of the subclass that has three parameters using ***this***:

```java
public Admin(String username, String password) {
		this(username,password, null);
	}
```

In our case, it is probably better to use ***this***, so if we ever have to make special code changes for our admin constructor accounts we only have to make it in one place. 

Finally, ***super*** can be used to access instance variables of a class' superclass if those same variables are hidden because the subclass has variables of the same name (Eck, 2019, ch. 5.6.2). 

As an example, let's say our Admin account needs an instance variable *securityCodes* which is an array of integer values representing different security access levels. Our modified Admin account class could look like this:

```java
public class Admin extends Account {
	int[] securityCodes = {1, 2};
	
	// Constructors
	public Admin(String username, String password, String email) {
		super(username, password, email);
	}

	public Admin(String username, String password) {
		this(username,password, null);
	}
}
```

Now, let's say we want to create a subclass of Admin called SuperAdmin for special admin accounts that have even more privileges. SuperAdmin will also have an instance variable called securityCodes, which will consist of the same security codes as Admin plus a few more. We *could* assume that the Admin security codes will never change and write a subclass that looks like this:

```java
public class SuperAdmin extends Admin {	
	int[] securityCodes = {1, 2, 9, 10};
	
	public SuperAdmin(String username, String password, String email) {
		super(username, password, email);
	}
}
```

However, although we know *now* that Admin has two security codes (1 and 2), it is not clear if that will be the case forever. There may be a time in the future when someone changes the code in Admin so they have a few more codes or maybe even fewer codes. If that were to happen, someone would have to remember to make the changes in both classes, which is another scenario that could lead to human error. To avoid that, it would be better to write SuperAdmin in a flexible way to account for as many codes that there might be at the time that the account is created. So, we could write SuperAdmin like this instead:

```java
public class SuperAdmin extends Admin {	
	int[] securityCodes;
	
	public SuperAdmin(String username, String password, String email) {
		super(username, password, email);
		
		
		int numCodes = super.securityCodes.length + 2;
		this.securityCodes = new int[numCodes];
		
		for (int i = 0; i < super.securityCodes.length; i++) {
			this.securityCodes[i] = super.securityCodes[i];
		}
		
		this.securityCodes[numCodes - 2] = 9;
		this.securityCodes[numCodes - 1] = 10;
	}
}
```

In this new version, ***this*** and ***super*** are both used to distinguish between the subclass and superclass's instance variable securityCodes. The SuperAdmin constructor first calls the Admin's contructor using ***super***. Then, it declares a variable *numCodes* to store how long the array should be. It uses ***super*** to get the length of the Admin's securityCodes, and adds 2 to it because the SuperAdmin account will have 2 extra security codes. The constructor then initializes its own instance variable of securityCodes using ***this***. Then, it uses a *for* loop to initialize the first set of values in the SuperAdmin securityCodes array to the values in the Admin securityCodes array. Finally, it adds the special SuperAdmin codes to the last two indexes in the array.


## Reference

Eck, D. J. (2019). Introduction to programming using Java, version 8.1. [http://math.hws.edu/javanotes](http://math.hws.edu/javanotes)