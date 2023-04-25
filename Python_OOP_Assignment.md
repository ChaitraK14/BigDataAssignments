## Python OOP Assignment
Q1. What is the purpose of Python's OOP?

A: An object-oriented paradigm is to design the program using classes and objects. The object is related to real-word entities such as book, house, pencil, etc. The oops concept focuses on writing the reusable code. It is a widespread technique to solve the problem by creating objects.

Q2. Where does an inheritance search look for an attribute?

A:An inheritance search looks for an attribute first in the instance object, then in the class the instance was created from, then in all higher superclasses, progressing from left to right (by default). 

Q3. How do you distinguish between a class object and an instance object?

A: 

Q4. What makes the first argument in a class’s method function special?

A: First argument in the class's method function is SELF. It always points to the current object. By using the “self”  we can access the attributes and methods of the class in python. It binds the attributes with the given arguments.

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

A: 

Q11. Where and how should be class attributes created?

A: Class attributes are created inside class and outside the constructor(__init__ method).

Ex: class Student:
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

A: The operator overloading in Python means provide extended meaning beyond their predefined operational meaning. Such as, we use the "+" operator for adding two integers as well as joining two strings or merging two lists. We can achieve this as the "+" operator is overloaded by the "int" class and "str" class.

Q15. When do you consider allowing operator overloading of your classes?

A: When one or both operands are of a user-defined class or structure type, operator overloading makes it easier to specify user-defined implementation for such operations. This makes user-defined types more similar to the basic primitive data types in terms of behaviour.

Q16. What is the most popular form of operator overloading?

A: The most popular instance is the adding up operator '+', where it can be used for the usual addition and also for combining two different strings.

Q17. What are the two most important concepts to grasp in order to comprehend Python OOP code?

A: The most important concepts are:
   1. Inheritance : OOP allows us to create a class(child class) based on another class(parent class).The child class copies the attributes (both data and procedural) from the parent class. This concept is called inheritance.
   2. Polymorphism : The function with same name behaves differently for different type of objects.

Q18. Describe three applications for exception processing.

A: 

Q19. What happens if you don't do something extra to treat an exception?

A: If we don't do anything to treat an exception, we will get an error and the execution stops there itself.

Q20. What are your options for recovering from an exception in your script?

A: 

Q21. Describe two methods for triggering exceptions in your script.

Q22. Identify two methods for specifying actions to be executed at termination time, regardless of  
whether or not an exception exists.

Q23. What is the purpose of the try statement?

Q24. What are the two most popular try statement variations?

Q25. What is the purpose of the raise statement?

Q26. What does the assert statement do, and what other statement is it like?

Q27. What is the purpose of the with/as argument, and what other statement is it like?

Q28. What are *args, **kwargs?

Q29. How can I pass optional or keyword parameters from one function to another?

Q30. What are Lambda Functions?

Q31. Explain Inheritance in Python with an example?

Q32. Suppose class C inherits from classes A and B as class C(A,B).Classes A and B both have their own versions of method func(). If we call func() from an object of 
class C, which version gets invoked?

Q33. Which methods/functions do we use to determine the type of instance and inheritance?

Q34.Explain the use of the 'nonlocal' keyword in Python.

Q35. What is the global keyword?
