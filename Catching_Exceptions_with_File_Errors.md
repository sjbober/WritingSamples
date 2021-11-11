# Catching Exceptions with File Errors

Since there are many different errors that can occur while working with files, it is important to catch any exceptions that might occur with try/except blocks (Downey, pp. 140) so we can give the user meaningful error messages instead of allowing our program to blow up. 

**Error example #1:**
Let's say we want to write a program which asks the user to provide a name and then creates a new folder with that name. We can use the function *mkdir()* in the *os* module, which takes a string argument and creates a new folder with the argument as its name (Ndlovu, n.d.). 

```python
import os

new_folder = input("Please enter the name of the folder you want to create: \n")
os.mkdir(new_folder)
```

This program seems innocent enough, but let's say we run it and give 'homework' as our folder name, which we forgot already exists in our current folder:

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Please enter the name of the folder you want to create:
homework
Traceback (most recent call last):
  File "C:\Users\sjbober\Documents\UoPeople\CS1101\unit8\code.py", line 9, in <module>
    os.mkdir(new_folder)
FileExistsError: [WinError 183] Cannot create a file when that file already exists: 'homework'
```

Our program blew up and the result is very ugly. So let's put our attempt to create a new folder in a try block. If any exceptions occur, we can print an error.

```python
import os

new_folder = input("Please enter the name of the folder you want to create: \n")

try:
    os.mkdir(new_folder)
    print("{} folder successfully created.".format(new_folder))
except:
    print("Some error occurred. Please try again.")
```

We can enter the same folder name this time, and our program will end beautifully.

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Please enter the name of the folder you want to create:
homework
Some error occurred. Please try again.
```


**Error example #2:**
Now let's say we want to display the contents of a particular folder to a user. We ask them for a folder name and we assume that the folder they want to see is in the same folder where our code is. We can use various functions from the *os* module to help us: *getcwd()* to get the path for the current working directory, *path.join()* to combine the current working directory and the requested folder name to get the path for the requested folder, and *listdir()* to list the contents of the requested folder (Downey, pp. 139-140).

```python
import os

folder_name = input("Which folder contents would you like to see?\n")
current_directory = os.getcwd()
folder_path = os.path.join(current_directory,folder_name)

folder_contents = os.listdir(folder_path)
print(folder_contents)
```

This program works fine until a user enters a folder name that does not exist, and then the entire program blows up:

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Which folder contents would you like to see?
homeworkk
Traceback (most recent call last):
  File "C:\Users\sjbober\Documents\UoPeople\CS1101\unit8\code.py", line 18, in <module>
    folder_contents = os.listdir(folder_path)
FileNotFoundError: [WinError 3] The system cannot find the path specified: 'C:\\Users\\sjbober\\Documents\\UoPeople\\CS1101\\unit8\\homeworkk'
```

We can prevent this exception by putting our function *listdir()* in a try block. If an exception occurs, we print out an error message.

```python
import os

folder_name = input("Which folder contents would you like to see?\n")
current_directory = os.getcwd()
folder_path = os.path.join(current_directory,folder_name)

try:
    folder_contents = os.listdir(folder_path)
    print(folder_contents)
except:
    print("Some error occurred. Please try again.")
```

When we try again with the same folder name, the program ends with an error message.

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Which folder contents would you like to see?
homeworkk
Some error occurred. Please try again.
```


**Error example #3:**
In our final example, we want to ask the user for a file name and some content, and modify the file with the content. We can use the "*with open(...) as..."* pattern to create a file object and open it in writing mode to modify its contents (Ndlovu, n.d.).

```python
import os

new_file = input("Please enter the name of the file you want to rewrite or create:\n")
file_content = input("Now enter the content to be added to the file:\n")
with open(new_file, 'w') as f:
    f.write(file_content)
```

However, if the user forgets the file extension (such as .txt, .py, etc) while entering the file name, then an error occurs.

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Please enter the name of the file you want to rewrite or create:
hello
Now enter the content to be added to the file:
hi
Traceback (most recent call last):
  File "C:\Users\sjbober\Documents\UoPeople\CS1101\unit8\code.py", line 28, in <module>
    with open(new_file, 'w') as f:
PermissionError: [Errno 13] Permission denied: 'hello'
```

We can put our statements to open the file and write to it in a try block. That way, if there are any errors opening the file, the program will print an error instead of blowing up. 

```python
import os

new_file = input("Please enter the name of the file you want to rewrite or create:\n")
file_content = input("Now enter the content to be added to the file:\n")

try:
    with open(new_file, 'w') as f:
        f.write(file_content)
except:
    print("Some error occurred. Please try again.")
```

Now, with the same input, the program gives an error message.

```python
C:\Users\sjbober\Documents\UoPeople\CS1101\unit8>code.py
Please enter the name of the file you want to rewrite or create:
hello
Now enter the content to be added to the file:
hi
Some error occurred. Please try again.
```

If these programs were part of a large production program, it would be helpful to print more specific error messages to the user. For example, in each except block, I could write code that checks what type of error occurred and print out different messages for each error. In example #1, I could print out a message saying that a folder with that name already exists. In code for error #2, I could print a message that says the given folder doesn't exist, and in #3 I could print an error message that the file extension is missing.

Instead of exiting the program when an error occurs, I could also create a loop that continuously asks the user for the required input until (a) valid input is given, or (b) a certain number of tries has been reached (so as to not overwhelm the user, or as a security precaution) or (c) give the user another way to exit the loop, such as being able to type 'exit.' 

Additionally, I could remind the user about valid inputs. In examples 1 and 2, I could print a list of existing folders in the current directory. And in example #3, in the input statement I could remind them to include their file extensions.


## References

Downey, A. (2015). Think Python, How to think like a computer scientist. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0)

Ndlovu, V. (n.d.). Working with files in Python – Real Python. Retrieved from [https://realpython.com/working-with-files-in-python/#making-directories](https://realpython.com/working-with-files-in-python/#making-directories)