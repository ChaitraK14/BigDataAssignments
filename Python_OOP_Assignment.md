## Python OOP Assignment
Q1. What is the purpose of Python's OOP?

A: An object-oriented paradigm is to design the program using classes and objects. The object is related to real-word entities such as book, house, pencil, etc. The oops concept focuses    on writing the reusable code. It is a widespread technique to solve the problem by creating objects.

Q2. Where does an inheritance search look for an attribute?

A: An inheritance search looks for an attribute first in the instance object, then in the class the instance was created from, then in all higher superclasses, progressing from left to    right (by default). 

Q3. How do you distinguish between a class object and an instance object?

A: 1.Class objects represent the class itself, while instance objects represent individual instances of the class.
   2.Class objects can have class-level attributes and methods that are shared among all instances of the class, while instance objects have their own set of attributes and methods that    are independent of other.

Q4. What makes the first argument in a class’s method function special?

A: First argument in the class's method function is SELF. It always points to the current object. By using the “self”  we can access the attributes and methods of the class in python.      It binds the attributes with the given arguments.

Q5. What is the purpose of the init method?

A: The __init__ method lets the class initialize the object's attributes.

Q6. What is the process for creating a class instance?

A: To create class instances, we have to call the class using class name and pass in whatever arguments its __init__ method accepts.

Q7. What is the process for creating a class?

A: class is like a blueprint for objects. By creating a class, we can create any number of objects from class.

Q8. How would you define the superclasses of a class?

A: The class from which a class inherits is called the parent or superclass.

Q9. What is the relationship between classes and modules?

A: The difference between a class and a module in python is that a class is used to define a blueprint for a given object, whereas a module is used to reuse a given piece of code inside another program.

Q10. How do you make instances and classes?

A: Classes can be created using class keyword.

   Ex: 
   
        class student:
            def __init__(self,name,age):
                  self.name=name
                  self.age=age     
    
    Instances can be created using class and passing the attributes in paranthesis.
    
    Ex: s1 = student("xyz",29)
    
    student is a class and s1 is an object/ instance of the class student.

Q11. Where and how should be class attributes created?

A: Class attributes are created inside class and outside the constructor(__init__ method).

Ex: 

         class Student:
            school = "abc"
            def __init__(self,name,age):
               self.name=name
               self.age=age

    here school is a class attribute.

Q12. Where and how are instance attributes created?

A: Instance attributes are created inside the constructor of a class. In the above example name and age are instance attributes.

Q13. What does the term "self" in a Python class mean?

A: "self" in a python class is a reference to the current instance of the class, and is used to access variables that belongs to the class. 

Q14. How does a Python class handle operator overloading?

A: The operator overloading in Python means provide extended meaning beyond their predefined operational meaning. Such as, we use the "+" operator for adding two integers as well as        joining two strings or merging two lists. We can achieve this as the "+" operator is overloaded by the "int" class and "str" class.

Q15. When do you consider allowing operator overloading of your classes?

A: When one or both operands are of a user-defined class or structure type, operator overloading makes it easier to specify user-defined implementation for such operations. This makes      user-defined types more similar to the basic primitive data types in terms of behaviour.

Q16. What is the most popular form of operator overloading?

A: The most popular instance is the adding up operator '+', where it can be used for the usual addition and also for combining two different strings.

Q17. What are the two most important concepts to grasp in order to comprehend Python OOP code?

A: The most important concepts are:
   1. Inheritance : OOP allows us to create a class(child class) based on another class(parent class).The child class copies the attributes (both data and procedural) from the parent         class. This concept is called inheritance.
   2. Polymorphism : The function with same name behaves differently for different type of objects.

Q18. Describe three applications for exception processing.

A: 1. To handle divide by zero
   2. To handle index out of range error
   3. To handle wrong key name for dictionaries

Q19. What happens if you don't do something extra to treat an exception?

A: If we don't do anything to treat an exception, we will get an error and the execution stops there itself.

Q20. What are your options for recovering from an exception in your script?

A: 1. We can place the code which may cause exception in try block. After a try block, include an except: statement, followed by a block of code which handles the           problem.A         single try statement can have multiple except statements.We can provide generic except statement which can handle any type of exception.
   2. After the except clause(s), we can include an else-clause. The code in the else-block executes if the code in the try: block does not raise an exception.
   3. WE can use a finally: block along with a try: block. The finally block is a place to put any code that must execute, whether the try-block raised an exception or       not.

Q21. Describe two methods for triggering exceptions in your script.

A: 1. raise keyword: We can use the “raise” keyword to throw a Python exception manually. We can also add a message to describe the exception.
   2. assert keyword: assert keyword let us test if a condition in our code returns True, if not, the program will raise an AssertionError.

Q22. Identify two methods for specifying actions to be executed at termination time, regardless of  
whether or not an exception exists.

A: 1. We can place the action to be executed outside the try except block.
   2. We can place the code in finally block.

Q23. What is the purpose of the try statement?

A: The try block is used to check some code for errors i.e the code inside the try block will execute when there is no error in the program.

Q24. What are the two most popular try statement variations?

A: There are two other optional segments to a try block: else and finally . Both of these optional blocks will come after the try and the except .

Q25. What is the purpose of the raise statement?

A: Raise statement is used to throw a Python exception manually. We can also add a message to describe the exception.

Q26. What does the assert statement do, and what other statement is it like?

A: assert statement let us test if a condition in our code returns True, if not, the program will raise an AssertionError. It is like the raise statement.

Q27. What is the purpose of the with/as argument, and what other statement is it like?

A: with statement is used in exception handling to make the code cleaner and much more readable. It simplifies the management of common resources like file streams.It is like try-except    statement.

Q28. What are *args, **kwargs?

A: *args and **kwargs are special keyword which allows function to take variable length argument.
   *args passes variable number of non-keyworded arguments and on which operation of the tuple can be performed.
   **kwargs passes variable number of keyword arguments dictionary to function on which operation of a dictionary can be performed.

Q29. How can I pass optional or keyword parameters from one function to another?

A: Collect the arguments using the * and ** specifiers in the functions parameter list, this gives us the positional arguments as a tuple and the keyword arguments as a dictionary. Then    we can pass these arguments when calling another function by using * and **.

Q30. What are Lambda Functions?

A: A lambda function is an anonymous function, that can take any number of arguments but, unlike normal functions, evaluates and returns only one expression.

Q31. Explain Inheritance in Python with an example?

A: Inheritance is a mechanism through which we create a class or object based on another class or object. In other words, the new objects will have all the features or    attributes of    the class or object on which they are based. We refer to the created class as the derived or child class, and the class from which it inherits is the    base or parent class.

   Ex:
   
         #**Parent_class**
         class Vehicle:
            def __init__(self,Brand,model_name):
                  self.Brand=Brand
                  self.model_name=model_name

            def show(self):
                  print("Brand:",self.Brand)
                  print("Model:",self.model_name)

         #**Child_class**
         class Car(Vehicle):
            pass

         car_details = Car('Tata Motors','TIAGO')
         car_details.show()

         #**Child_class using super() keyword**
         class Car2(Vehicle):
            def __init__(self,Brand,model_name,launched_year):
                  super().__init__(Brand,model_name)
                  self.launched_year=launched_year

            def show(self):
                  super().show()
                  print("Lauched_year:",self.launched_year)

          car_details_2=Car2('Tata Motors','TIGOR',2017)
          car_details_2.show()

Q32. Suppose class C inherits from classes A and B as class C(A,B).Classes A and B both have their own versions of method func(). If we call func() from an object of 
class C, which version gets invoked?

A: class A

Q33. Which methods/functions do we use to determine the type of instance and inheritance?

A: The isinstance() method checks whether an object is an instance of a class.
   issubclass() method checks whether one class is a subclass of another class (or other classes).

Q34.Explain the use of the 'nonlocal' keyword in Python.

A: The nonlocal keyword is used in nested functions to reference a variable in the parent function. The nonlocal keyword won’t work on local or global variables and therefore must be      used to reference variables in another scope except the global and local one.

Q35. What is the global keyword?

A: Global keyword is used inside a function only when we want to do assignments or when we want to change a variable. 
