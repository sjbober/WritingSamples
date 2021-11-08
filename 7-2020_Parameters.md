# Introduction to Parameters

When we want to generalize a method to work for various scenarios, we can give it parameters that allow it to take custom input values from whoever calls it. Formal parameters are variables that act as placeholders in our method. When someone calls the method, the formal parameters are assigned the values of the actual parameters that are passed to the method (Eck, 2019, ch. 4).

Consider the following method with no parameters, which prompts a user to enter a password, and compares their attempt to the real password. 

```java
import javax.swing.JOptionPane;

public class CheckPWNoParam {

    public static void main(String[] args) {
    	checkPassword();
    }
    
    private static void checkPassword() {
        String realPassword = "mysecretpassword";
	
        do {
            String attempt = JOptionPane.showInputDialog("What is your password?");
			
            if (realPassword.equals(attempt)) {
                System.out.println("Password is correct! Logging you in now.");
                break;
        }

            System.out.println("Password is incorrect. Please try again.");
			
        } while (true);
    } 
    
} 
```

This program works, but it has hard-coded the actual password directly into the method, meaning that the value of the real password is the same every time the method is called. This means that in a real system, we would need one method per user/password combination that exists in the system, which could be not only unrealistic depending on how many users we have but also makes our program difficult to maintain. If we ever need to make changes to our code, we would need to make changes to every method, which requires a lot of work and is susceptible to human error. Instead, we can use parameters to generalize our function to work for every user/password combination. 

Now consider the same program which has been modified to include one *String* parameter. The formal parameter is *realPassword*, and when the main method calls the *checkPassword* method, the formal parameter is assigned the value of the actual parameter, which is the literal "mysecretpassword".

```java
import javax.swing.JOptionPane;

public class CheckPassword {
	
	public static void main(String[] args) {
	    checkPassword("mysecretpassword");
	}
	
	private static void checkPassword(String realPassword) {
    	
        do {
            String attempt = JOptionPane.showInputDialog("What is your password?");
			
            if (realPassword.equals(attempt)) {
                System.out.println("Password is correct! Logging you in now.");
                break;
        }

            System.out.println("Password is incorrect. Please try again.");
			
        } while (true);
		
	}

}
```

Of course, in a real-world situation, the actual parameter should not be hard-coded directly into the method call, but instead returned from some other method call that asks the system for the password for a specific user. But at the very least, we have a simple method to check passwords that can work for many different users. 


 ## Reference

Eck, D. J. (2019). Introduction to programming using Java, version 8.1. [http://math.hws.edu/javanotes](http://math.hws.edu/javanotes)