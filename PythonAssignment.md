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
A:   Sets are used to store multiple items in a single variable. A set is a collection which is unordered, unchangeable(but items can be removed and new items can be added), unindexed ad always contains unique items.

Q46. How can you create a set?
A:   Sets can be created with items seperated by commas, surrounded by curly braces {}.

Q47. Create a set and add "iNeuron" in your set.
A:   
     s = {'iNeuron'}
     print(s)

Q48. Try to add multiple values using add() function.
A:   
     s.add('Python')
     s.add('Bigdata')
     print(s)
        

Q49. How is update() different from add()?
A:   Using add() we can only add a single item but update() can be used to add multiple items at a time and also for adding items from another set (or any other iterable).

Q50. What is clear() in sets?
A:   The clear() method removes all elements in a set

Q51. What is frozen set?
A:   Frozen set is an immutable version of a Python set object. While elements of a set can be modified at any time, elements of the frozen set remains the same after creation.

Q52. How is frozen set different from set?
A:   Sets are mutable but frozen sets are immutable, which implies no items can be added or removed from frozen set.

Q53. What is union() in sets? Explain via code.
A:   union() method returns a new set which contains all the elements from the original sets without any duplicates.
        
     set1 = {2,4,6,8,1}
     set2 = {1,3,5,7,2}
     print("Union of set1 and set2:",set1 | set2)
     
     Union of set1 and set2 returns all the elements from set1 and set2 without any duplicates.
     
Q54. What is intersection() in sets? Explain via code.
A:   intersection() method returns a new set which contains only common items between the sets.

     set1 = {2,4,6,8,1}
     set2 = {1,3,5,7,2}
     set3 = {1,2,3,4,5}
     print("Intersection of set1,set2 and set3:",set1 & set2 & set3)

     Intersection of set1, set2 and set3 returns common elements present in all 3 sets, that is {1, 2}.

Q55. What is dictionary ibn Python?
A:   A dictionary consists of a collection of key-value pairs. Each key-value pair maps the key to its associated value.

Q56. How is dictionary different from all other data structures.
A:   Dictionary stores elements as a key-value pairs while other data structures stores elements as a single value.

Q57. How can we delare a dictionary in Python?
A:   Dictionary are declared using curly braces {}.key value pairs are seperates using colon : and each pairs are seperated by commas.

Q58. What will the output of the following?
```
var = {}
print(type(var))
```
A:   <class 'dict'>

Q59. How can we add an element in a dictionary?
A:   
     val ={}
     val['name'] ="xyz"
     val['age'] = 29
     print(val)

Q60. Create a dictionary and access all the values in that dictionary.
A:
     val ={"Name":"xyz","Age":29,"Country":"India"}
     for k,v in val.items():
         print("Key is", k ,"and Value is",v)

Q61. Create a nested dictionary and access all the element in the inner dictionary.
A:   
     Employees ={"Employee1":{"Name":"chris","Age":28},"Employee2":{"Name":"Sam","Age":32}}
     for k,v in Employees["Employee1"].items():
         print("Key is", k ,"and Value is",v)

Q62. What is the use of get() function?
A:   get() function is used to access the values in a dictionary using a key.
     
     val ={"Name":"xyz","Age":29,"Country":"India"}
     print(val.get("Name"))
     
Q63. What is the use of items() function?
A:   items() function is used to get list of all the key values of dictionary.

     val ={"Name":"xyz","Age":29,"Country":"India"}
     print(val.items())

Q64. What is the use of pop() function?
A:   pop() is used to remove the element from the dictionary by dict key and return the value related to the removed key.
     
     val ={"Name":"xyz","Age":29,"Country":"India"}
     popped_value = val.pop("Name")

Q65. What is the use of popitems() function?
A:   popitem() removes and returns the item that was last inserted into the dictionary.

     val ={"Name":"xyz","Age":29,"Country":"India"}
     popped_value = val.popitem()

Q66. What is the use of keys() function?
A:   keys() function returns a view object that displays a list of all the keys present in a dictionary.

     val ={"Name":"xyz","Age":29,"Country":"India"}
     print(val.keys())

Q67. What is the use of values() function?
A:   values() function returns a view object that displays a list of all the values present in a dictionary.

     val ={"Name":"xyz","Age":29,"Country":"India"}
     print(val.values())

Q68. What are loops in Python?
A:   loops are used to iterate over a block of code over and over until a particular condition is satisfied.

Q69. How many type of loop are there in Python?
A:   Two types of loops are there is python: for and while.

Q70. What is the difference between for and while loops?
A:   for loop is used when the number of iterations is known, whereas execution is done in the while loop until the statement in the program is proved wrong.

Q71. What is the use of continue statement?
A:   continue statement passes the flow of exrcution to next iteration.

Q72. What is the use of break statement?
A:   break statement forces the flow to execution to come out of the loop.

Q73. What is the use of pass statement?
A:   pass statement passes the flow of execution to next line.Empty code is not allowed in loops, function definitions, class definitions, or in if statements hence pass can be used there to avoid error.

Q74. What is the use of range() function?
A:   The range() function returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and stops before a specified number.
     range(start,stop,step)
     we can give start, stop and step values to get a sequence.

Q75. How can you loop over a dictionary?
A:   
     val ={"Name":"xyz","Age":29,"Country":"India"}
     for k,v in val.items():
         print("Key is", k ,"and Value is",v)


### Coding problems
Q76. Write a Python program to find the factorial of a given number.
A:
    def factorial(n):
        if n<0:
            return(0)
        elif n==0:
            return(1)
        else:
            fact=1
            for val in range(1,n+1):
                fact=fact*val

        return(fact)

Q77. Write a Python program to calculate the simple interest. Formula to calculate simple interest is SI = (P*R*T)/100
A:   
     def SI(P,R,T):
         si = P*R*T/100
         return(si)

     print("Simple Interest is",SI(1000,5.5,2))

Q78. Write a Python program to calculate the compound interest. Formula of compound interest is A = P(1+ R/100)^t.
A:   
     def CI(P,R,T):
         A = P*(1+R/100)**T
         ci = A-P
         return(ci)

     print("Compound Interest is",CI(1000, 5.5, 2))

Q79. Write a Python program to check if a number is prime or not.
A:   
     from math import sqrt

     def is_prime(n):
         prime_flag=0
         if n>1:
             for i in range(2,int(sqrt(n))+1):
                 if n % i==0:
                     prime_flag=1
                     break
             if prime_flag==0:
                 print(n," is a prime number")
             else:
                 print(n," is not a prime number")
         else:
             print(n," is not a prime number")

     m=7
     is_prime(m)


Q80. Write a Python program to check Armstrong Number.
A:   
     def is_armstrong(n):
         l = len(str(n))
         s = 0 
         for i in str(n):
         s = s+(int(i)**int(l))
         if n==s:
             print(n," is armstrong number")
         else:
             print(n," is not armstrong number")

     is_armstrong(371)

Q81. Write a Python program to find the n-th Fibonacci Number.
A:
     def fibonacci(n):
         if n<=0:
             print("Invalid")
         if n==1:
             return 0
         if n==2:
             return 1
         else:
             return fibonacci(n-1)+fibonacci(n-2)

     n=8    
     print(f"{n}th fibonacci number is {fibonacci(8)}")

Q82. Write a Python program to interchange the first and last element in a list.
A:
     def swap_list(l):
         temp=l[0]
         l[0]=l[-1]
         l[-1]=temp
         return(l)

     l=[23,5,67,8,98]
     print(swap_list(l))

Q83. Write a Python program to swap two elements in a list.
A:
     def swap_list(l,pos_1,pos_2):
         temp=l[pos_1]
         l[pos_1]=l[pos_2]
         l[pos_2]=temp
         return(l)

     l=[23,5,67,8,98]
     print(swap_list(l,2,4))

Q84. Write a Python program to find N largest element from a list.
A:
     def n_largest(L,N):
         max_list=[]
         for j in range(0,N):
             max=L[0]
             for i in range(1,len(L)):
                 if L[i]>max:
                     max=L[i]
    
             max_list.append(max)
             L.remove(max)
         print(f"{N} largest elements of list are:{max_list}")

     n_largest([1,3,5,7,2,4,6],3)

Q85. Write a Python program to find cumulative sum of a list.
A:
     def cum_sum(L):
         sum=0
         sum_list=[]
         for i in L:
             sum=sum+i
             sum_list.append(sum)

         print(f"Cumulative Sum list:{sum_list}")

     cum_sum([1,3,5,7,2,4,6])

Q86. Write a Python program to check if a string is palindrome or not.
A:
     def is_palindrome(s):
         if s==s[::-1]:
             print(f"{s} is palindrome")
         else:
             print(f"{s} is not palindrome")

     is_palindrome("abccba")

Q87. Write a Python program to remove i'th element from a string.
A:
     def rm_ith_element(s,i):
         new_str=s[:i]+s[i+1:]
         print(f"string after removing {i}th element: {new_str}")

     rm_ith_element("abcdefg",3)

Q88. Write a Python program to check if a substring is present in a given string.
A:
     def check_substring(str,sub_str):
         if sub_str in str:
             print(f'"{sub_str}" is a substring of "{str}"')
         else:
             print(f'"{sub_str}" is not a substring of "{str}"')

     check_substring("Happy new year!!!","new")

Q89. Write a Python program to find words which are greater than given length k.
A:
     def str_greater_than_k(s,k):
         new_list=[]
         words_list = s.split(" ")
         for i in words_list:
             if len(i)>k:
                 new_list.append(i)
         print(f"words greater that length of {k}: {new_list}")

     str_greater_than_k("Welcome to my home",3)

Q90. Write a Python program to extract unquire dictionary values.
A:



     def unique_dict_values(d):
         unique_list=[]
         for v in d.values():
             unique_list.extend(v)

         print(f"Unique dictionary values:{list(set(unique_list))}")

     d={"a":[1,3,4],"b":[9,8],"c":[5,7,8],"d":[5,4]}
     unique_dict_values(d)

Q91. Write a Python program to merge two dictionary.
A:


     def merge_dictionary(dict_1,dict_2):
         dict_1.update(dict_2)
         print("dictionary after merging:",dict_1)

     d1={"a":[1,2],"b":[4,5]}
     d2={"c":[7,8],"d":[3,6]}
     merge_dictionary(d1,d2)


Q92. Write a Python program to convert a list of tuples into dictionary.
```
Input : [('Sachin', 10), ('MSD', 7), ('Kohli', 18), ('Rohit', 45)]
Output : {'Sachin': 10, 'MSD': 7, 'Kohli': 18, 'Rohit': 45}
```
A:


print(dict([('Sachin', 10), ('MSD', 7), ('Kohli', 18), ('Rohit', 45)]))

Q93. Write a Python program to create a list of tuples from given list having number and its cube in each tuple.
```
Input: list = [9, 5, 6]
Output: [(9, 729), (5, 125), (6, 216)]
```
A:

     l = [9, 5, 6]
     list_of_tuple=[]
     for i in l:
         list_of_tuple.append((i,i**3))
     print(list_of_tuple)


Q94. Write a Python program to get all combinations of 2 tuples.
```
Input : test_tuple1 = (7, 2), test_tuple2 = (7, 8)
Output : [(7, 7), (7, 8), (2, 7), (2, 8), (7, 7), (7, 2), (8, 7), (8, 2)]
```
A:


     output=[(i,j) for i in test_tuple1 for j in test_tuple2]+[(j,1) for i in test_tuple2 for j in test_tuple1]
     print(output)

Q95. Write a Python program to sort a list of tuples by second item.
```
Input : [('for', 24), ('Geeks', 8), ('Geeks', 30)] 
Output : [('Geeks', 8), ('for', 24), ('Geeks', 30)]
```
A:


t=[('for', 24), ('Geeks', 8), ('Geeks', 30)] 
for j in range(0,len(t)):
    for i in range(0,len(t)-1):
        if t[i][1]>t[i+1][1]:
            t[i],t[i+1]=t[i+1],t[i]

print(t)

Q96. Write a python program to print below pattern.
```
* 
* * 
* * * 
* * * * 
* * * * * 
```
A:

n=5
for i in range(1,n+1):
    print('* '*i)
    
Q97. Write a python program to print below pattern.
```
    *
   **
  ***
 ****
*****
```
A:


n=5
for i in range(1,n+1):
    print(' '*(n+1-i)+'*'*i)
Q98. Write a python program to print below pattern.
```
    * 
   * * 
  * * * 
 * * * * 
* * * * * 
```
A:


n=5
for i in range(1,n+1):
    print(' '*(n+1-i)+'* '*i)

Q99. Write a python program to print below pattern.
```
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
```
A:


n=5
for j in range(1,n+1):
    for i in range(1,j+1):
        print(i,end=" ")
    print("\r")

Q100. Write a python program to print below pattern.
```
A 
B B 
C C C 
D D D D 
E E E E E 
```
A:


n=5
for i in range(1,n+1):
    print((chr(64+i)+" ")*i)
