## Assignment Part-1
Q1. Why do we call Python as a general purpose and high-level programming language?
A:  Python is called general purpose as it can be used for wide variety of applications and its is not specialized for any specific problem. 
    Python is a high-level programming language because it is very easy to code and understand. 

Q2. Why is Python called a dynamically typed language?
A:  There is no need to declare the type of variable explicitly while writing the program, the type is determined during runtime.

Q3. List some pros and cons of Python programming language?
A:  Pros:
* Python is User friendly language. It is very easy to code and understand.
* Python has a vast collection of libraries.
* Python has free & open source license.

  Cons:
* Python is slower compared to compiled languages.
* High memory consumption.

Q4. In what all domains can we use Python?
A:  * Data Science
    * Machine Learning
    * Deep Learning
    * Artificial Intelligence
    * Scientific Computing Scripting
    * Networking
    * Game Development to Web Development.

Q5. What are variable and how can we declare them?
A: Name given to an object is called variable. In python, a variable is created the moment a value is assigned to it.
   
   Ex: a = 15

Q6. How can we take an input from the user in Python?
A:  User input can be taken using the function : input().

Q7. What is the default datatype of the value that has been taken as an input using input() function?
A:  default datatype is string.

Q8. What is type casting?
A:  type casting is changing the datatypes of the variables.

Q9. Can we take more than one input from the user using single input() function? If yes, how? If no, why?
A:  Yes, we can take more than one input from input() function by using split() method.

Ex: a,b = input("Enter 2 nums:").split()
    print("Value of a:",a)
    print("Value of b:",b)

Q10. What are keywords?
A:  keywords are special reserved words that have specific meanings and purposes and can't be used for anything but those specific purposes.

Q11. Can we use keywords as a variable? Support your answer with reason.
A: No, we cannot use keywords as a variable because keywords are specially reserved words that are used for specific purposes.

Q12. What is indentation? What's the use of indentaion in Python?
A:  Indentation is spaces at beginning of code line. Indentation in python indicates that the codelines belongs to specific block of code. 

Q13. How can we throw some output in Python?
A:  using print() function.

Q14. What are operators in Python?
A:  Operators are those symbols that perform specific computation or operations on variables in python. 

Q15. What is difference between / and // operators?
A:  / is a division operator which gives float result.
    // is also a division operator but gives integer result.

Q16. Write a code that gives following as an output.
```
iNeuroniNeuroniNeuroniNeuron
```
A:  print("iNeuron"* 4)

Q17. Write a code to take a number as an input from the user and check if the number is odd or even.
A:  
    num = float(input("Enter a number:"))
    if num % 2 ==0:
      print("Even number")
    else:
      print("Odd number")

Q18. What are boolean operator?
A:  Boolean Operators are those that result in the Boolean values of True and False.
    and, or and not are used as boolean operators which may evaluate to true or false.

Q19. What will the output of the following?
```
1 or 0

0 and 0

True and False and True

1 or 0 or 0
```
A: 1
   0
   False
   1

Q20. What are conditional statements in Python?
A:  Conditional statements are used to make decision based on certain condition. these statements control the flow of exectution.

Q21. What is use of 'if', 'elif' and 'else' keywords?
A:  'if' condition is checked first.
    'elif' condition is checked when if condition is unsatisfied.
    'else' condition is checked when all the above conditions are unsatisfied.

Q22. Write a code to take the age of person as an input and if age >= 18 display "I can vote". If age is < 18 display "I can't vote".
A:  
      age = int(input("My age:"))
      if age>=18:
          print("I can vote")
      else:
          print("I can't vote")

Q23. Write a code that displays the sum of all the even numbers from the given list.
```
numbers = [12, 75, 150, 180, 145, 525, 50]
```
A:  print(sum([x for x in numbers if x%2==0]))

Q24. Write a code to take 3 numbers as an input from the user and display the greatest no as output.
A:  
      x,y,z = input("Enter 3 numbers:").split()
      
      if int(x)>int(y) and int(x)>int(z):
          print(x,"is greatest")
      elif int(y)>int(z):
          print(y,"is greatest")
      else:
          print(z,"is greatest")

Q25. Write a program to display only those numbers from a list that satisfy the following conditions

- The number must be divisible by five

- If the number is greater than 150, then skip it and move to the next number

- If the number is greater than 500, then stop the loop
```
numbers = [12, 75, 150, 180, 145, 525, 50]
```
A:  
    result = []
    for n in numbers:
      if n > 150:
        if n > 500:
          break
      elif n%5==0:
        result.append(n) 

    print(result)

Q26. What is a string? How can we declare string in Python?
A:  String is an array of bytes representing unicode characters. strings are declared in single or double quotation marks.

Q27. How can we access the string using its index?
A:  square brackets are used to access the string elements.

Q28. Write a code to get the desired output of the following
```
string = "Big Data iNeuron"
desired_output = "iNeuron"
```
A:  print(string[9:)

Q29. Write a code to get the desired output of the following
```
string = "Big Data iNeuron"
desired_output = "norueNi"
```
A:  print(string[:7:-1])

Q30. Resverse the string given in the above question.
A:  print(string[::-1])

Q31. How can you delete entire string at once?
A:   Entire string can be deleted using del keyword. 

Q32. What is escape sequence?
A:   backslash(\) is an escape character used, when we need to insert an illegal charater in a string. For example, double quotes cannot be inserted in a string, but this can be done by inserting a backslash followed by double quotes inside the string.

Q33. How can you print the below string?
```
'iNeuron's Big Data Course'
```
A:   print("'iNeuron's Big Data Course'")
                      or
     print('\'iNeuron\'s Big Data Course\'')

Q34. What is a list in Python?
A:   list is a sequence of elements stored in a single variable, the elements can be of diffrent types.

Q35. How can you create a list in Python?
A:   list can be created using square barckets([]) and the elements are stored seperated by commas inside the square barckets.

Q36. How can we access the elements in a list?
A:   list elements can be accesed by the indexing.

Q37. Write a code to access the word "iNeuron" from the given list.
```
lst = [1,2,3,"Hi",[45,54, "iNeuron"], "Big Data"]
``` 
A:   print(lst[4][2])

Q38. Take a list as an input from the user and find the length of the list.
A:   lst = list(input("Enter elements of a list seperated by space: ").split(" "))
     print(len(lst))

Q39. Add the word "Big" in the 3rd index of the given list.
```
lst = ["Welcome", "to", "Data", "course"]
```
A:    lst.insert(2,"Big")
      print(lst)

Q40. What is a tuple? How is it different from list?
A:   Tuple is sequence of python objects stored in a single variable. Tuples are same as lists but immutable where as lists are mutable. 

Q41. How can you create a tuple in Python?
A:   A tuple is created by placing all the items (elements) inside parentheses () , separated by commas.

Q42. Create a tuple and try to add your name in the tuple. Are you able to do it? Support your answer with reason.
A:   Name cannot be added in tuple once after created, as tuple is immutable.

Q43. Can two tuple be appended. If yes, write a code for it. If not, why?
A:   Yes, tuples can be appended.

Ex: tup_1 = (2,4,6)
    tup_2 = (1,3,5)
    print(tup_1+tup_2)

Q44. Take a tuple as an input and print the count of elements in it.
A:   tup = tuple(input("Enter elements of a tuple seperated by space: ").split(" "))
     print(len(tup))

Q45. What are sets in Python?

Q46. How can you create a set?

Q47. Create a set and add "iNeuron" in your set.

Q48. Try to add multiple values using add() function.

Q49. How is update() different from add()?

Q50. What is clear() in sets?

Q51. What is frozen set?

Q52. How is frozen set different from set?

Q53. What is union() in sets? Explain via code.

Q54. What is intersection() in sets? Explain via code.

Q55. What is dictionary ibn Python?

Q56. How is dictionary different from all other data structures.

Q57. How can we delare a dictionary in Python?

Q58. What will the output of the following?
```
var = {}
print(type(var))
```

Q59. How can we add an element in a dictionary?

Q60. Create a dictionary and access all the values in that dictionary.

Q61. Create a nested dictionary and access all the element in the inner dictionary.

Q62. What is the use of get() function?

Q63. What is the use of items() function?

Q64. What is the use of pop() function?

Q65. What is the use of popitems() function?

Q66. What is the use of keys() function?

Q67. What is the use of values() function?

Q68. What are loops in Python?

Q69. How many type of loop are there in Python?

Q70. What is the difference between for and while loops?

Q71. What is the use of continue statement?

Q72. What is the use of break statement?

Q73. What is the use of pass statement?

Q74. What is the use of range() function?

Q75. How can you loop over a dictionary?


### Coding problems
Q76. Write a Python program to find the factorial of a given number.

Q77. Write a Python program to calculate the simple interest. Formula to calculate simple interest is SI = (P*R*T)/100

Q78. Write a Python program to calculate the compound interest. Formula of compound interest is A = P(1+ R/100)^t.

Q79. Write a Python program to check if a number is prime or not.

Q80. Write a Python program to check Armstrong Number.

Q81. Write a Python program to find the n-th Fibonacci Number.

Q82. Write a Python program to interchange the first and last element in a list.

Q83. Write a Python program to swap two elements in a list.

Q84. Write a Python program to find N largest element from a list.

Q85. Write a Python program to find cumulative sum of a list.

Q86. Write a Python program to check if a string is palindrome or not.

Q87. Write a Python program to remove i'th element from a string.

Q88. Write a Python program to check if a substring is present in a given string.

Q89. Write a Python program to find words which are greater than given length k.

Q90. Write a Python program to extract unquire dictionary values.

Q91. Write a Python program to merge two dictionary.

Q92. Write a Python program to convert a list of tuples into dictionary.
```
Input : [('Sachin', 10), ('MSD', 7), ('Kohli', 18), ('Rohit', 45)]
Output : {'Sachin': 10, 'MSD': 7, 'Kohli': 18, 'Rohit': 45}
```

Q93. Write a Python program to create a list of tuples from given list having number and its cube in each tuple.
```
Input: list = [9, 5, 6]
Output: [(9, 729), (5, 125), (6, 216)]
```

Q94. Write a Python program to get all combinations of 2 tuples.
```
Input : test_tuple1 = (7, 2), test_tuple2 = (7, 8)
Output : [(7, 7), (7, 8), (2, 7), (2, 8), (7, 7), (7, 2), (8, 7), (8, 2)]
```

Q95. Write a Python program to sort a list of tuples by second item.
```
Input : [('for', 24), ('Geeks', 8), ('Geeks', 30)] 
Output : [('Geeks', 8), ('for', 24), ('Geeks', 30)]
```

Q96. Write a python program to print below pattern.
```
* 
* * 
* * * 
* * * * 
* * * * * 
```
Q97. Write a python program to print below pattern.
```
    *
   **
  ***
 ****
*****
```

Q98. Write a python program to print below pattern.
```
    * 
   * * 
  * * * 
 * * * * 
* * * * * 
```

Q99. Write a python program to print below pattern.
```
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
```

Q100. Write a python program to print below pattern.
```
A 
B B 
C C C 
D D D D 
E E E E E 
```
