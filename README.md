[oop1(object oriented programming)](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop01%20(classes%20and%20objects).py)

In programming, there are three styles.

1. Imperative : doing programming with different loops, if/else statement and general basics.

2. Functional : doing programming with pure, higher order, recursive and all types of functions.

3. Object oriented: doing programming with classes and objects.

OUTSIDE OF THE TOPIC:

pure function is the type of function which does not affect any out code of the function. exp: adding calculator

impure function is the type of function which affects any out code of the function. exp:appending to a list

higher order function is the type of function which either take a function as an argument or return

a function as their return value is called a higher order function. exp:map,filter

classes and objects

What is an object?

an object is basically a collection of properties which can be expressed as variables and some functions.

we need to put the object in a variable.

that variable will contain a whole set of properties of the object.

object contains data which are unique to each other.

What are attributes?

The variables within the object are called either "Instance variables" or "attributes".

What is a method?

The functions within the object are called methods.

What is a class?

A class is basically like a blueprint from which we can make objects.

a class doesn't refer to any particular object.

We need to give a suitable name to a class.

The first letter of the name must be "capitalize".

creating a class.

```Python
class Employee:

    pass

```
Here we write the pass method because we are not going to work with it right now.

creating an object.

```Python
emp1 = Employee() # this simply says create a new object with the class "Employee".

```
here we are using the default python constructor for this class "Employee".

setting attributes or instances(variables) to an object.

```Python
emp1.first="ahammad"

emp1.last="shawki"          

emp1.pay=1000

```
here each attributes are unique to other.

we can now create a new object in this class too

```Python
emp2=Employee()

emp2.first="christiano"

emp2.last="ronaldo"

emp2.pay=2000

```
printing from class

```Python
print(emp1.pay) 

print(emp2.pay)

```
but in this code, we are writing the same line in the object again and again.

That's OK but not great!!

It is too messy.

it can give us an attribute error if we mis-spell any attribute incorrectly in the object.

So, the best way to deal with it is using a constructor.

let's create the same class using constructor.

```Python
class Employee1:

    def __init__(self,first,last,pay):# this is called a constructer.in python to make constructor we must use the keyword "__init__"

        self.first=first

        self.last=last      # in our constructor we are setting the instance variables or attributes.

        self.pay=pay

        self.email=first +"."+last+"@company.com"

```
when we create methods within a class,they receive the attributes as the first argument automatically.

and by convention we should call the attribute "self".

We can call it whatever we want. But it is a good idea to stick with the conventions.

so, we need to write "self" as the first argument of the constructor.

Once we have a constructor in our class the default constructor will stop working.

now we can pass value in our constructor(outside the class)

```Python
emp3=Employee1("zinedin","zidan",3000)

emp4=Employee1("sergio","ramos",4000)

```
in our object, attributes pass automatically.

so we don't have to write any self argument.

```Python
print(emp3.pay)

print(emp4.pay)

"""What is happening behind the scenes?

   self is a keyword.

   when we built constructors and an object like this one-

   python thinks that,

   self=emp1

   so "self.first" refers to"emp1.first"

   """

```
if we want to print the full name of an employee.

We can do it manually outside our class.

```Python
print(f"{emp3.first},{emp3.last}")

```
but let's ignore this bunch of code and go to our class and make a method which will handle this task easily.

```Python
class Employee2:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last      

        self.pay=pay

        self.email=first +"."+last+"@company.com"

    def fullname(self):                           # here note that, we need to add "self" argument to every method we want to add in the class.

        return f"{self.first} {self.last}"

emp5=Employee2("zinedin","zidan",3000)

emp6=Employee2("sergio","ramos",4000)

print(emp5.fullname()) # remember we have to use brackets after fullname. Because it is a method not an attribute.

```
or-

```Python
print(Employee2.fullname(emp6))
```

*******************************************************
*******************************************************
[oop2](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop02%20(class%20variables).py)

**class variables**

What are class variables?

class variables are variables that are shared among the attributes of a class.

While instance variables are unique to each other, class variables should be the same for each attribute.

```Python
class Employee:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*1.04)

emp1=Employee("ahammad","shawki",200)

emp2=Employee("cristiano","ronaldo",400)

print(emp1.pay)

emp1.apply_raise()

print(emp1.pay) 

```
In this code, we are calculating the raise of employees pay.

it is good but not great

If we want to change the amount, we have to change it manually several times in several places.

we can rather use a class variable. 

```Python
class Employee2:

    raise_amount=1.04  # here we are setting our class variable.

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*self.raise_amount)# in order to access our class variable, we need to write self before the variable name.

    #or self.pay=int(self.pay*Employee.raise_amount)# we can also write the class name before the variable name.

    # but do these two cases have a difference? 

emp1=Employee2("ahammad","shawki",200)

emp2=Employee2("cristiano","ronaldo",400)

print(emp2.pay)

emp2.apply_raise()#applying the function on emp2 

print(emp2.pay)

```
here to know actually what is going on, we are writing some additional code

```Python
print(Employee2.raise_amount)

print(emp1.raise_amount)

print(emp2.raise_amount)

```
we can access the class variable from both the class and the attributes

how to print the emp1 info in a dictionary

```Python
print(emp1.__dict__)

```
there is no raise_amount in the list.

now we print out the Employee2 class.

```Python
print(Employee2.__dict__)

```
this class contains the raise_amount attribute.

When we run this code, python first searches to access the raise_amount from the object.

if it doesn't find any attribute,

it will access the raise_amount from the Employee2 class.

When we update the raise_amount outside/of our class, the raise_amount will automatically update in all attributes.

```Python
Employee2.raise_amount=1.05

print(Employee2.raise_amount)

print(emp1.raise_amount)

print(emp2.raise_amount)

print("\n\n")

```
but when we change the raise_amount of any attribute, it only changes the raise amount of that specific attribute.

```Python
emp2.raise_amount=1.09

print(Employee2.raise_amount)

print(emp1.raise_amount)

print(emp2.raise_amount)

```
Why did it do that?

when we made that assigning it actually created the raise_amount attribute within the emp2.

so now we have a raise amount attribute in emp2.

it is no longer a class variable for emp2, it is an attribute.

```Python
print(emp2.__dict__)

```
so if python finds the attribute in the object,

it won't access it from the class.

```Python
Employee2.raise_amount=1.08

print(Employee2.raise_amount)

print(emp1.raise_amount)

print(emp2.raise_amount)

```
here we have again change the class variable from the class,

but emp2 has raise_amount still 1.09 as it has made its own property(attribute)

so we should write "self.raise_amount" rather than "Employee.raise_amount"

because it gives us flexibility to update our raise_amount in any object later.

it also allowed any subclass to overwrite that constant if we wanted to.

Now lets look at another example of a class variable where it wouldn't really make sense to use self.

Let's say we wanted to keep track of how many employees we have.

so the number of employee should be the same for all our class and object

```Python
class Employee3:

    numemp=0 # each time we created a new employee it will increase

    raise_amount=1.04  

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        Employee3.numemp +=1  # we are going to do that in our constructor. because it runs every time we create a new employee.

    # here we must use "Employee3" instead of "self"

    # because in the previous case we may think that we may need to override the class variable.

    # but in this case there's no use case where we can think of where we want our total number of employees to be different for any one attribute.

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*self.raise_amount)

print(Employee3.numemp)# it will give us zero because we have not made any object yet.

emp1=Employee3("ahammad","shawki",200)

emp2=Employee3("cristiano","ronaldo",400)

```
now, we print out the number of employee

```Python
print(Employee3.numemp)# it will give us two because it has been raised two times.

```
DIFFERENCE BETWEEN ATTRIBUTE AND CLASS VARIABLE 

In the attribute we need to write self.

and we can call them by object.

In the class variable we can write both class and self.

we can call by both class and object.


*******************************************************
*******************************************************
[oop3](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop03%20(class%20methods).py)

**class methods**

regular methods in a class automatically pass attributes as an argument as the first argument. By convention, we call it "self". 

class methods in a class automatically pass class as an argument as the first argument. By convention, we call it "cls". 

```Python
class Employee:

    raise_amount=1.04  

    numemp=0

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        Employee.numemp +=1

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*self.raise_amount)

    # To turn a regular method into a class method, we need to add a decorator to the top called @classmethod.

    # this decorator alters the functionality of our method to where now we receive the class to our first argument.

    # by convention, we called the first argument of our class method "cls"

    # we can't use the class as our first argument here, because the word has a different meaning in this language.

    @classmethod 

    def set_raise_amt(cls,amount): 

       cls.raise_amount=amount

    # now within this method we are going to work with class instead of object   

emp1=Employee("ahammad","shawki",200)

emp2=Employee("cristiano","ronaldo",400)

Employee.set_raise_amt(1.05)# changing the raise_amount

```
This will change all raise_amount both class and object.

This happens because we ran this set_raise_amt method which is a class method which means now we are working with class instead of the object.

and we are setting that class variable raise amount equal to the amount that we passed in here which is 1.05.

what we have done here is the same thing of saying-

```Python
Employee.raise_amount=1.05

print(Employee.raise_amount)

print(emp1.raise_amount)

print(emp2.raise_amount)

```
we can also use class methods as alternative constructors

It means we can use these class methods in order to provide multiple ways to create our object.

Let's say someone is using our class.

```Python
emp_str_1 ="john-doe-700"

emp_str_2 ="steve-smith-800"

emp_str_3 ="sergio-ramos-900"

```
we have three strings here that are employees separated by hyphens.

if we want to create new objects with this string we have to first split on the hyphen-

```Python
first, last, pay =emp_str_1.split("-")

new_emp1=Employee(first,last,pay)

print(new_emp1.pay)

```
but this takes a lot of code and time.

so lets create an alternative constructor that allows us to pass in the string and we can create the employee.

So let's create a new class method and we are going to use that method as an alternative constructor.

```Python
class Employee2:

    raise_amount=1.04  

    numemp=0

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        Employee.numemp +=1

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*self.raise_amount)

    @classmethod

    def form_string(cls,emp_str):# here form is a convention.

        first, last, pay =emp_str.split("-")

        return cls(first,last,pay)# here we are using cls instead of Employee2 because cls and Employee2 are basically the same thing.

emp_str_1 ="john-doe-700"

emp_str_2 ="steve-smith-800"

emp_str_3 ="sergio-ramos-900"

new_emp1=Employee2.form_string(emp_str_1)

print(new_emp1.pay)

```
characteristics of class methods:

. We need to add decorator @classmethod on the top of the class method.

. We need to add cls as the first argument of the class method.

. We should use cls inside the class method.

. Outside the class, we should call the class method with the class name.

. We can use the class method as an alternative constructor.


*******************************************************
*******************************************************
[oop4](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop04%20(static%20methods).py)

**static method**

Regular methods in a class automatically pass attributes as an argument as the first argument. By convention, we call it "self" 

class methods in a class automatically pass class as an argument as the first argument. By convention, we call it cls.

static methods in a class don't pass any argument automatically. They pass neither the attribute nor the class.

Static functions behave just like regular functions except we include them in our class because they have some logical connections with the class.

```Python
class Employee:

    num_emp=0

    raise_amount=1.04

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        self.email=first+last+"@gmail.com"

        Employee.num_emp +=1

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply(self):

        self.pay=int(self.pay*self.raise_amount)

    @classmethod

    def set_raise(cls,amount):

        cls.raise_amount=amount

    @classmethod

    def str_name(cls,emp_str):

        first, last, pay = emp_str.split("-")

        return cls(first, last ,pay)

    # suppose, we want to know if the day is weekday or not in our class.

    # it is logically connected to the Employee class.

    # but it does not depend on class or attributes.

    # so we need to create a static method which tells us if it is a weekday or not.

    @staticmethod # to create a static method we need to use this decorator

    def workday(day):

        if day.weekday()==5 or day.weekday()==6: # in python monday is numbered 0, sunday is numbered 6 and so on.

            return False                         # here day.weekday() function is used to refer to days of the week in the function.

        else:

            return True

emp1=Employee("ahammad","shawki",1000)

emp2=Employee("shakil","abrar",2000)

import datetime

my_date=datetime.date(2016,7,10)# this function makes our date read-able for python.

```
r my_date=datetime.datetime.strptime("2016,7,10","%Y,%m,%d").date()

```Python
print(Employee.workday(my_date))# we need to write Employee before calling the static method.

```
How to be sure that it is a class method or a static method?

If anywhere in the method we need to use the cls variable that is definitely a class method.

If anywhere in the method we need to use a self variable that is definitely a regular method.

otherwise, it is a static method.

In the regular method we need to write self.

and we can call them by object. 

In the class method we need to write cls.

and we can call them by class.

In the static method we need to write nothing.

and we should call them by class.


*******************************************************
*******************************************************
[oop5](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop05%20(inheritance%20and%20subclasses).py)

**inheritance and subclasses**

inheritance allows us to inherit attributes and methods from a parent class. 

this is useful because we can create subclasses and get all the functionalities of our parent class,

and then we can overwrite or add completely new functionality without affecting the parent class.

Now let's create different types of employees.

Let's say we wanted to create developers and managers.

here we need to use subclasses.

```Python
class Employee:

    raise_amount=1.04

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        self.email=first+last+"@gmail.com"

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay=int(self.pay*self.raise_amount)

```
making a subclass

```Python
class Developer(Employee):# here we are using the parent class name in the brackets,

    pass                  # to specify which parent class' functionality we want to inherit.

```
here our subclass don't have any code of its own.

but this subclass will have all the attributes methods of our Employee class.

```Python
dev_1=Employee("ahammad","shawki",200)

dev_2=Employee("cristiano","ronaldo",400)

print(dev_1.email)

print(dev_2.email)

```
it will also work if we create our object in Developer subclass

```Python
dev_1=Developer("ahammad","shawki",200)

dev_2=Developer("cristiano","ronaldo",400)

print(dev_1.email)

print(dev_2.email)

```
What happened here?

when we instantiated our Developers it first looked in our Developers subclass for constructor.

And it's not going to find it in our developer class because it's currently empty.

so what python is going to do then is walk up a chain of inheritance until it finds what it is looking for.

This chain is called "method resolution order".

We can visualize that by a help function.

print(help(Developer))

here we can see that-

```Python
"""Method resolution order:

    Developer

    Employee      

    builtins.object"""

```
So when we create a new developer object it first looks in our developer subclass for constructor.

If it didn't find it there then search in the Employee parent class.

If it didn't find it there also the last place that it would have looked is this bulitins.object class.

Every class in python inherits from this base builtins.object class.

We can also know by the help method that our subclass has inherited all the variables and methods from the parent class for free.

Now we want to customize our subclass.

And we are going to change the raise_amount for our developers.

but first lets see what happens when we apply the raise_amount function to our current developers.

```Python
print(dev_1.pay)

dev_1.apply_raise()

print(dev_1.pay)

```
lets say we want our developers to raise amount of 1.10

we can do this by-

```Python
class Developer2(Employee):

    raise_amount=1.10

dev_3=Developer2("sergio","ramos",500)

print(dev_3.pay)

dev_3.apply_raise()

print(dev_3.pay)

```
Now python using our developer subclass raise amount instead of the parent class raise amount.

Actually by changing the raise_amount and our subclass does not affect any of our employee parent classes.

So we can make these kinds of changes to our subclasses without worrying about breaking anything in the parent class. 

```Python
dev_4=Employee("gerath","bale",800)  

print(dev_4.pay)

dev_4.apply_raise()

print(dev_4.pay)

```
sometimes we need to initiate our subclasses with more information than our parent class can handle.

Let's say we want to add an extra attribute for our developers which is their main programming language.

but currently our parent class doesn't contain that attribute.

so to pass an additional attribute for our developers subclass, we need to give the subclass its own constructor.

so we can do this-

```Python
class Developer3(Employee):

    def __init__(self,first,last,pay,prog_lang):

        super().__init__(first,last,pay)# here we don't need to write all the code like self.pay=pay etc.

        self.prog_lang=prog_lang

```
Instead of doing that we will let our parent class handle first, last and pay attributes.

We will let the developer set the prog_lang attribute.

So in order to let our parent class to handle previous attribute, we can write-

super().__init__(first,last,pay)

Here super is a function which allows us to do this.

In the brackets after init we don't have to write "self" as our first argument.

now we have handled the prog_lang just like old tecnic.

```Python
dev_5=Developer3("luca","modrich",300,"ruby")

dev_6=Developer3("neymar","jr.",900,"java")

print(dev_5.email)

print(dev_5.prog_lang)

```
let's make a new subclass called manager.

```Python
class Manager(Employee):

    def __init__(self,first,last,pay,employees=None):# here we don't use an empty list for our default employees value.

        super().__init__(first,last,pay)             # because we should not pass any mutable data type like empty list or dictionary.

        if employees is None:                        # instead of that we use None and do some extra coding to make sure that our code is error free.

            self.employees=[]

        else:

            self.employees=employees

```
add a employee           

```Python
    def add_emp(self, emp):    

        if emp not in self.employees:

            self.employees.append(emp)

```
remove a employee

```Python
    def remove_emp(self, emp):

        if emp in self.employees:

            self.employees.remove(emp)

```
print out the fullnames of employees

```Python
    def print_emp(self):

        for emp in self.employees:

            print("-->",emp.fullname())

man_1=Manager("zinedin","zidane",100,[dev_1])

print(man_1.email)

man_1.add_emp(dev_2)

man_1.add_emp(dev_3)

man_1.remove_emp(dev_1)

man_1.print_emp()

```
so now we know the importance of subclass?

=> here the code for all of our developers and managers is specific.

=> and they dont create problem with each other.

=> and we can inherit all the properties of parent class to our subclass by a single line of code.

=> so we are really getting reuse our code nicely here if we use subclasses.

python has two buit_in function called isinstance and issubclass.

is instance will tell us if an object is an instance/object of a class.

```Python
print(isinstance(man_1,Manager))

print(isinstance(man_1,Employee))

print(isinstance(man_1,Developer))

```
here we need to enter two arguement.

first one is the instance and the second is the class.

is subclass will tell us if it is a subclass of a class.

```Python
print(issubclass(Developer,Employee))

print(issubclass(Manager,Employee))

print(issubclass(Manager,Developer))

```
here we need to enter two arguement.

first one is the subclass and the second is the parent class.

there is also an important function called hasatter().

it is used to see if a class or a object has certain properties or not.

for example, if we want to see if Manager class has the add_emp() method or not, we can-

```Python
print(hasattr(Manager,"add_emp")) # NOTE: we have to pass the name of the property in string.

```
we can also use this method with object instead of class,

```Python
print(hasattr(man_1,"remove_emp"))

```
Extra tip:

types of inheritance:

single:

```Python
    # when a inheritance involves one child class and one parent class only.

```
multiple:

```Python
    # when a inheritance involves more than one parent class.

```
multilevel:

```Python
    # the child class acts as a parant class for another parent class.

```
hierarchical:

```Python
    # it involvs multiple hybrid inheritance form the same parent class. it spreads like a tree.

```
hybrid:

```Python
    # it involves more than one type of inheritance. 

```
code:

single:

```Python
class Parent:

    def func1(self):

        print("A function from the parent class")

class Child(Parent):

    def func2(self):

        print("A function from the child class")

```
multiple:

```Python
class Parent1:

    def func3(self):

        print("A function from the parent1 class")

class Parent2:

    def func4(self):

        print("A function from the parent2 class")

class Child1(Parent1, Parent2):

    def func5(self):

        print("A function from the child1 class")

```
multilevel:

```Python
class Parent3:

    def func6(self):

        print("A function from the parent3 class")

class Child2(Parent3):

    def func7(self):

        print("A function from the child2 class")

class Child3(Child2):

    def func8(self):

        print("A function from the child3 class which is a of child2 class")

```
hierarchical(basic):

```Python
class Parent4:

    def func6(self):

        print("A function from the parent4 class")

class Child4(Parent4):

    def func7(self):

        print("A function from the child4 class")

class Child5(Parent4):

    def func8(self):

        print("A function from the child5 class")

```
hierarchical(hybrid):

```Python
class Parent5:

    def func9(self):

        pass

class Child6(Parent5):

    def func10(self):

        pass

class Child7(Parent5):

    def func11(self):

        pass

class Child8(Child6,Child7):

    def func12(self):

        pass

```

*******************************************************
*******************************************************
[oop6](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop06%20(special_magic_dunder%20methods).py)

**special/magic/dunder methods**

There are some methods in python we can use within our classes.

These methods are called special methods or magic methods or dunder methods.

These special methods allow us to emulate some built_in behaviour within python and it's also how we implement operator overloading.

```Python
class Employee:

    raise_amount=1.05

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        self.email=first+last+"@gmail.com"

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay =self.pay*self.raise_amount

emp_1=Employee("ahammad","shawki",10000)

emp_2=Employee("cristiano","ronaldo",20000)

```
if we print emp_1 , we find some message.

```Python
print(emp_1) 

```
it is nice if we change its behaviour and print out something user-friendly .

These special methods are going to allow us to do that.

special method are always surrounded by double underscore(_)

So for that reason, it is also called dunder.

so dunder init means `__init__`

Let's look at some other common special methods.

```Python
class Employee2:

    raise_amount=1.05

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        self.email=first+last+"@gmail.com"

    def fullname(self):

        return f"{self.first} {self.last}"

    def apply_raise(self):

        self.pay =self.pay*self.raise_amount

    def __repr__(self):# repr is meant to be an ambiguous representation of the object and should be used for debugging ang logging and things like that.

        return "Employee('{}','{}','{}')".format(self.first,self.last,self.pay)

    def __str__(self):# str is meant to be more of a readable representation of an object and is used as a display to the end_user.

        return f"{self.fullname()} - {self.email}"

    def __add__(self, other):

        return self.pay + other.pay

    def __len__(self):

        return len(self.fullname())

emp_3=Employee2("ahammad","shawki",10000)

emp_4=Employee2("cristiano","ronaldo",20000)

print(emp_3)

```
Now it returns a string that we specified in the `__repr__` method.

so if we wanted to recreate this we can just copy our output.

And it's the exact same thing that we used to make our object.

but when we make our `__str__` method then it will access our str special method.

it is a readable display for end_users.

even we can also print dunder repr and str

```Python
print(repr(emp_3))

print(str(emp_3))

```
So what's going on in the background is that it's directly calling  those special methods.

```Python
print(emp_3.__repr__())

print(emp_3.__str__())

```
It is actually the same thing.

So these special methods allow us to know how our object will be printed and displayed.

so print(emp_3) first executed dunder str.

If there is no dunder str it will run dunder repr.

If there is no dunder repr it will then run that ugly message.

So it's a good habit that if we create dunder str, we should create dunder repr in our class too.

There are also many magic methods in arithmetic.

```Python
print(1+2)

```
when we run this code, it will run a dunder add in the background.

```Python
print(int.__add__(1,2))# here int is a default object.

```
string uses their own dunder add method.

```Python
print("a"+"b")

print(str.__add__("a","b"))

```
we can also add the salaries of our employees by dunder add.

remember that though these methods are available for our code, but that's not available for our class by default.

so in order to make them available for our class and objects we need to do some additional coding.

if we do not do so our code will give us errors.

```Python
print(emp_3+emp_4)# to add this we need to use + instead of "," 

```
There are also many dunder methods.

You can find them in this description "https://docs.python.org/3/references/datamodel.html#special-method-names"

infact, "len" is a dunder method too.

```Python
print(len("shawki"))

print("shawki".__len__())

```
we can apply this to our class.

```Python
print(len(emp_3))

```
It is useful when someone is writing a document and needs to know how many characters the employee's name will take up.

so we see that in python all operations have a top level function like len or add.

and the top level functions are surrounded by __ which allows us to implement those top level functions.

Let's see some other magic methods.

`__len__ `        len()

`__add__ `        +

`__sub__ `        -

`__mul__ `        -

`__truediv__`     /

`__floordiv__`    //

`__mod__  `       %

`__pow__ `        **

`__and__ `        &

`__xor__ `        ^

`__import__`      |

`__lt__ `         <

`__le__ `         <=

`__eq__  `        ==

`__ne__ `         !=

`__gt__ `         >

`__ge__`          >=

`__getitem__`

`__setitem__`

`__delitem__`

`__iter__`

`__next__`

`__name__`

`__main__`

`__contains__`

`__call__ `       x()

`__doc__`

`__iadd__   `     +=

`__isub__  `      -=

`__imul__ `       *=

`__idiv__ `       /=

`__imod__ `       %=

we have lots and lots more dunder methods in python. we have said earliar and saying again go to that link.

"https://docs.python.org/3/references/datamodel.html#special-method-names"

or we can google it.


*******************************************************
*******************************************************
[oop7](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop07%20(%40property%20decorator).py)

**property decorator**

property decorator allows us to give our class attributes getter,setter and a deleter functionality.

```Python
class Employee:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

        self.email=first+last+"@gmail.com"

    def fullname(self):

        return f"{self.first} {self.last}"

emp_1=Employee("ahammad","shawki",10000)

print(emp_1.first)

print(emp_1.email)

print(emp_1.fullname())

```
Here we have printed what we have expected.

Now we are going to update our first name and again do the same actions.

```Python
emp_1.first="jim"

print(emp_1.first)

print(emp_1.email)

print(emp_1.fullname())

```
but it prints the previous email which we hadn't expected.

Now what should we do in this situation?

This property decorator is useful.

It allows us to define a method that we can access like an attribute.

```Python
class Employee2:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    def fullname(self):

        return f"{self.first} {self.last}"

    def email(self):# so right now this method is similar to fullname method.so each time we run it it will access the current first and last name.

        return f"{self.first}{self.last}.@gmail.com"

emp_2=Employee2("ahammad","shawki",10000)

emp_2.first="jim"

print(emp_2.first)

print(emp_2.email())# but now as email is a method so we need to use brackets.

print(emp_2.fullname())

```
So if anyone is using our class they have to change their code also.

But we don't want to do that.

```Python
class Employee3:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    @property    

    def fullname(self):

        return f"{self.first} {self.last}"

    @property   # it is a property decorator.it is defining the email method of our class like an attribute. 

    def email(self):

        return f"{self.first}{self.last}.@gmail.com"

emp_3=Employee3("ahammad","shawki",10000)

emp_3.first="jim"

print(emp_3.first)

print(emp_3.email)

print(emp_3.fullname)

```
so in order to access email like an attribute.

we can just add a property decorator above that method.

We can do this fullname as well.

```Python
class Employee4:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    @property    

    def fullname(self):

        return f"{self.first} {self.last}"

    @property    

    def email(self):

        return f"{self.first}{self.last}.@gmail.com"

    @fullname.setter# it is a setter

    def fullname(self,name):# here we need to create another method with the same name.

        first,last=name.split(" ")

        self.first=first

        self.last=last

emp_4=Employee4("ahammad","shawki",10000)

emp_4.fullname="jim headings"

print(emp_4.first)

print(emp_4.email)

print(emp_4.fullname)

```
Here we change our fullname.

Let's say we wanted to change our first, last, email by changing our fullname.

if we just change this property decorator without doing any additional code it will give us an error 

In order to do that error-free, we are going to use a setter.

It is another decorator.

The name we are going to use for our setter is going to be the name of the property. 

we can also make a deleter in the same way.

if we want to delete the fullname of our employee we have to run some clean up code. so to do this,

We are going to do the same action as setter but instead of setter it will be deleter.

```Python
class Employee5:

    def __init__(self,first,last,pay):

        self.first=first

        self.last=last

        self.pay=pay

    @property    

    def fullname(self):

        return f"{self.first} {self.last}"

    @property    

    def email(self):

        return f"{self.first}{self.last}.@gmail.com"

    @fullname.setter

    def fullname(self,name):

        first,last=name.split(" ")

        self.first=first

        self.last=last

    @fullname.deleter# it is a deleter

    def fullname(self):

        print("name deleted!")

        self.first =None

        self.last =None

emp_5=Employee5("ahammad","shawki",10000)

emp_5.fullname="jim headings"

print(emp_5.first)

print(emp_5.email)

print(emp_5.fullname)

```
deleter code is useful if we want to delete an attribute.

```Python
del emp_5.fullname

```
When we run this code it sets our first and last attribute to none value.

property decorator is also used to make an attribute read-only.

If we there is a method in the class with the same name of an attribute,

Then if we use the property decorator and run that, the function will be executed not the attribute.
So the attribute becomes an read_only attribute. 

*******************************************************
*******************************************************
[oop8](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop08%20(combining%20multiple%20classes).py)

**combining multiple classes and objects**

```Python
class Robot :

    def __init__(self,name,color,weight):

        self.name=name

        self.color=color

        self.weight=weight

    def introduce_self(self):

        return "My name is "+ self.name

r1=Robot("Tom","red",30)

r2=Robot("Jerry","blue",40)

print(r1.introduce_self())

print(r2.introduce_self())

class Person :

    def __init__(self,name,personality,isSitting):

        self.name=name

        self.personality=personality

        self.isSitting=isSitting

    def sit_down(self):# when we run this method to any object the isSitting value will be true.

        self.isSitting=True

    def stand_up(self):# when we run this method to any object the isSitting value will be false.

        self.isSitting=False

p1=Person("Shawki","Intelligent",False)

p2=Person("Sowad","talkative",True)

```
if p1 owns r2 and p2 owns r1

```Python
p1.robotOwened=r2

p2.robotOwened=r1

```
Now we can access this robotOwned attribute in the p1/p2 object.

```Python
print(p1.robotOwened.introduce_self())

print(p2.robotOwened.introduce_self())
```

*******************************************************
*******************************************************
[oop9](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop09%20(5%20important%20tips%20and%20tricks%20for%20oop).py)


**Tip 1**

multiple inheritance

```Python
class A:

    def intro(self):

        print(" I am from class A")

class B:

    def intro(self):

        print(" I am from class B")

```
we can create a subclass and inherit from multiple parent class too.

```Python
class C(A,B):

    pass

```
now if we create an object of C class and apply the intro function to it.

```Python
object_C=C()

object_C.intro()

```
We can see that it is executing the class A intro() function.

Python always follows an order for execution of different functions.

we can see the order by mro() function.

```Python
print(C.mro())

```
we can see that the order is 

<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>]

So it first searches C, then A, then B and after that object.

What is MRO?

Method Resolution Order (MRO) is the order in which Python looks for a method in a hierarchy of classes.

It plays a vital role in the context of multiple inheritance as a single method may be found in multiple super classes.

**Tip 2**

**super() method**

We have already seen a use case of super() method. We have used this to inherit the constructor from the parent class.

actually, super() is used in the subclass for calling a function which is situated in the parent class.

```Python
class G:

    def num(self):

        print(1)

class H(G):

    def num(self):

        print(0) 

        super().num()# this num() is situated in the parent class.

object_H=H()

object_H.num()

```
NOTE: In the previous example of super() method we have changed the functionality of a method of parent class in the child class.

In programming, this is called "Method Overriding" similar to the operator overloading.

**Tip 3**


**operator overloading**

We see how different operators work in python. They are nothing but dunder methods.

We can actually change the characteristics in python.

It is called operator overloading.

```Python
class Myoperats:

    def __init__(self,value):

        self.value=value

    def __add__(self,other):

        return (self.value **2) + (other.value**2)

num1=Myoperats(5)

num2=Myoperats(12)

print(num1+num2)

```
here we have changed what our + operator actually does.

**Tip 4**

**object life cycle**

objects have three periods in their life in the memory.

They are Creation, Manipulation and Destruction.

when we create an object by a class, __new__ and __init__ method start working.

and other parts of the code can use the object and manipulate it.

we can destroy the object after we use it. This is called "garbage collection".

When "garbage collection" is  done the memory that the object used becomes free and we can use it for another reason.

Python automatically does the "garbage collection" after we use the object.

so we can now make an ideal definition of "garbage collection"

The process by which Python periodically frees and reclaims blocks of memory 

that no longer are in use is called Garbage Collection.

python's garbage collector runs during program execution and is triggered 

when an object's reference count reaches zero.

What is reference count?

When we code, an object can be linked with multiple objects.

The number of objects that an object is linked to is called its reference count.

let's see an example.

```Python
a=42 # a is linked to 42. so its reference count is 1

b=a  # a is linked to b. so its reference count is 2

c=[1,2,3]

c[0]=a # a is linked to c. so its reference count is 3

```
Now we can manually decrease the reference count by the `del` method.

```Python
del a # a is not linked to 42. so its reference count is 2

b=98 # a is not linked to b. so its reference count is 1

c[0]=54 # a is not linked to c. so its reference count is 0

```
When a reference count becomes 0. It is no longer of any use for us. So, python deletes the object a from the memory. 

that is what "garbage collection is"

**Tip 5**


**data hiding**

oop has 4 important concepts

They are encapsulation, inheritance, polymorphism, and abstraction.

Encapsulation means a technique where we combine some variables and functions and express them as a single unit.

This concept makes a barrier between the variables of different classes.

We can only grab the variables by executing some functions of the same class.

This is called "data hiding".

In other words, data hiding means hiding the implementation details of a class.

In other programming languages, we can use keywords(access modifiers) to make class attributes and methods private or protected.

But in python, things are a little different. they said, we are all consenting adults here.

It means it is not advisable to keep any class's element protected from outside's access.

So python doesn't have any real method for data hiding.

Instead of that, python advises not to access important implementation details from outside.

**weakly private (protected)**

When we use underscore(_) before an attribute or method name, we are saying that they are weakly private.

We can use them outside of our class but we should not access them outside of our class.

```Python
class Mlist:

    def __init__(self,*contents):

        self._hidden=[*contents]

    def add(self,*contentsr):

        self._hidden.extend([*contentsr])

    def _show(self):

        print(self._hidden)

l1=Mlist(1,2,3,4,5,6)

l1.add(7,8,9)

l1._show()

```
Note that: If we import a module having weakly private attributes and methods, then they are not imported.

even if we use from module_name import * 

so they remain private.

strongly private

when we use double underscore`__` before an attribute or method name, we are saying that they are strongly private.

Python changed their name a little bit. so we cant access them from the outside.

Mainly, it isn't done for resisting the access.

it is done for if we have any other attribute in the subclass with the same name, so that it won't conflict with that.

```Python
class Make:

    __cake=10

    def print_num(self):

        print(self.__cake)

a=Make()

a.print_num()

```
print(a.__cake)

We can't run this line. it would say that Make has no attribute __cake.

But we can still access the attribute like this. _classname__attributename

```Python
print(a._Make__cake)

```
Actually, python made the change to its name.

Why is encapsulation and data hiding important?

it is important because it gives one programmer freedom to implement the details of the component,

Without concern that other programmers will be writing code that intricately depends on those internal decisions.

It means programmers won't have to worried about that someone will change the private properties of that class in future

So that it becomes unusable.



*******************************************************
*******************************************************

[oop10](https://github.com/MINIMALaq/Object-Oriented-Programming-in-Python/blob/master/oop10%20(polymorphism%20in%20python).py)
**polymorphism**

It is one of the main principles of oop programming.

Sometimes an object comes in many types and forms.

So we can create a method that will access all types of that object and do the same thing regardless what type of the object it is.

The idea is called polymorphism.

It means there will be one function but it can behave various ways depending on the type of the input.

polymorphism can be achieved by overriding and overloading in python.

**method overriding:**

It means having two methods with the same name but doing different tasks.

it means one of the methods overrides the other.

if there is any method in the parent class and a method with the same name in the child class,

then if we execute the method, the method of the corresponding class will be executed.

```Python
class Parent:

    name="Father"

    def num(self):

        print(1)

class Child(Parent):

    # overriding variable

    name="Son"

    # overriding num() method in the child class

    def num(self):

        print(0) 

object_P=Parent()

print(object_P.name)

object_P.num()

object_H=Child()

print(object_H.name)

object_H.num()

```
Here we are using the same method and variable for 2 different class 

and they are handling each class separately which is polymorphism

**overloading**

In python we can define a method in such a way that there are multiple ways to call it.

if we are given a single method or function, we can specify the number of parameters ourselves.

```Python
class Human:

    def hello(self,country=None):

        if country is None:

            print("Hello")

        elif country=="ENGLAND":

            print("Hello!")

        elif country=="GERMANY":

            print("Gutan Tag!")

        elif country=="FRANCE":

            print("Bonjour!")

        elif country=="MEXICO":

            print("Ola Amigo!")

        elif country=="INDIA":

            print("Namaste!")

        else:

            print("Hey!")

obj=Human()

obj.hello("MEXICO")

obj_2=Human()

obj_2.hello("FRANCE")

```
Here hello is the same method but it will work differently depending on the arguments.

We can do polymorphism with this overloading too.

There is another type of overloading which is operator overloading.

add(+) operator is the same operator but works differently for different types of input.

it sum the value of int and float objects,

It concat string objects,

It extends list objects.

we can also create our own class and change the functionality of the add(+) operator.

```Python
class Special():

    def __init__(self,value):

        self.value=value

    def __add__(self,other):

        return self.value * other.value

        # changing the behaviour of + method (making it *)

num_1=Special(100)

num_2=Special(20)

print(num_1+num_2)

print(67+89)

print("Good "+"Boy")

```
here + is the same operator but it returns different values for different types of objects.

so it is an example of operator overloading.

*******************************************************
*******************************************************
abstraction in python

it is one of the main principles in oop

DEFINITION:

abstraction is the act of removing elements of specificity to emphasize commonality.

it is the process of describing things using only the important details for the task at hand.

in computer context, this involvs only providing attributes and methods to an object

that are useful for that perticular task only.

Abstract Class

abstract classes are the classes that contains abstract methods.

an abstract method is a method that is declared, but contains no implementation.

abstract classes cannot be instantiated it means we cannot create objects of the abstract class. 

and requires subclasses to provide implementations for the abstract methods (we can create objects of subclass)

Subclasses of an abstract class in python are not required to implement abstract methods of the parent class.

we want to make an abstract class.

in python there is a pre-defined abstract class called ABC(abstract base class).

we have to import ABC class from abc module.

```Python
from abc import ABC, abstractmethod

```
here A is an abstract class

```Python
class Configure(ABC):

    # lets create an abstract method. we have to use the @abstractmethod decorator.

    # we have to import it from abc module

    @abstractmethod

    def display(self):

        pass

    # so abstract method has declaration but no implementation.

```
if we want to implement this abstract method we need to create a subclass.

```Python
class Mechanic(Configure):

    # implementing the abstract method by overriding

    def display(self):

        print("this is display method for mechnic")

        # we can call the abstract method from parent class by super() method.

        super().display()

        # generally we dont have any implementation in abstract methods. but if we have any then we can use that.

```
we have to create object of the child class.

```Python
m=Mechanic()

m.display()

```
what if we have two different abstract methods in the parent calss and only one overridden abstract method in the child class?

```Python
class Configure2(ABC):

    @abstractmethod

    def engine(self):

        pass

    @abstractmethod

    def color(self):

        pass 

class Mechanic2(Configure2):

    def engine(self):

        print("this is engine method for mechnic")

    # def color(self):

    #     pass

```
here we have two abstract methods in parent class

and we only have implemented one of the methods in the subclass.

now can we create an object for the subclass?

m2=Mechanic2()

m2.engine()

we can see that we cant do it because there is another abstract method remaining 

which our subclass inherit from the parent class and we havent implement that.

so our Mechanic2() class is also a abstract class

how to solve this problem?

there is several ways we can do this.

method 1: we can implement the remaining function in the subclass.

method 2: create another subclass of the subclass Mechanic2() and implement the remaining function there.

```Python
class Sub_Mechanic2(Mechanic2):

    def color(self):

        print("this is abstract color method form a subclass of mechanic2")

        super().color()

```
create the object of the Sub_Mechanic2() class.

```Python
m3=Sub_Mechanic2()

m3.engine()

m3.color()

```
we can also create a constructor in the abstract class.

```Python
class Cal(ABC):

    def __init__(self,value):

        self.value=value

        # NOTE: here value is a local variable for the __init__ constructure.

        # when we use self.value it becomes class variable for the entire class.

    @abstractmethod

    def add(self):

        pass

    @abstractmethod

    def sub(self):

        pass

class C(Cal):

    def __init__(self,value):

        super().__init__(value)

    def add(self):

        return self.value+100

    def sub(self):

        return self.value-10

obj=C(100)

print(obj.add())

print(obj.sub())

```
Why should we use abstract class?

we should use abstraction when we are designing an application in a oop way.

if we create an abstract class, the subclasses will have some restrictions to which method they musst have to defined.

for example, in the previous example our Mechanic2 class must have 2 methods which are color() and engine()


*******************************************************
*******************************************************
inner class

we have seen that a class can contain variables and methods.

but can a class contain another class?

Interestingly, yes.

lets see an example:

```Python
class Student:

    def __init__(self,name,roll):

        self._name=name

        self._roll=roll

        # creating Laptop object inside the outer class

        #self.lap=self.Laptop(brand,cpu,ram)

        # we have to use self here as it in the class.

        # we can do this if we pass the attributes when creating a student class.

    def show(self):

        print(f"STUDENT INFORMATION \n\t name : {self._name} \n\t roll : {self._roll}")

    # students also have a laptop, so we want a laptop attribute in this class.

    # but the problem is when we talk about laptop,

    # it has different properties and configaration.

    # we can add those properties one by one as an attribute but that isn't great.

    # we can instead create a class and use that.

    class Laptop:

        def __init__(self,brand,cpu,ram):

            self.brand=brand

            self.cpu=cpu

            self.ram=ram

        def show(self):

            print(f"LAPTOP CONFIGURATION \n\t brand : {self.brand} \n\t cpu : {self.cpu} \n\t ram : {self.ram}")

    # to create the object of the inner laptop class in the outer class, we can do that in the __init__ method.

    # or we can directly create an object of Laptop class outside of the outer class.

s1=Student("Shawki",5130)

s2=Student("Arko",5162)

s1.show()

```
creating Laptop object for students. 

```Python
s1.lap=s1.Laptop("Lenovo","i5",4)

s2.lap=s2.Laptop("HP","i3",2)

```
this object will be an attribute of the student object.

we can print the attributes of Laptop using,

```Python
print(s1.lap.brand)

```
we have two different classes with the same name. but we can access both of them.

```Python
print()

s1.show()

print()

s1.lap.show()

```
NOTE: it is not simmilar to inheritance.

it can reduce potential name conflicts because it allows for a simmilarly named class to exists in another context.

another advantage is that it allows for a more advanced form of inheritance

in which a subclass of the outerclass can override the defination of its inner class.


*******************************************************
*******************************************************
Libray and User code

suppose we are working in the user code class and we are inheritting form library code.

we want a specific method that must include in the parant class of the library module.

in that case we can use assert statements before creation of the User codes class.

Library Code

```Python
class Parent:

    def first(self):

        return "hi"

```
User Code

from module_name import Parent  # actually, library and user code situated in two different module.

```Python
assert(hasattr(Parent, "first")),"Must need to have first() function"

class Child(Parent):

    def second(self):

        return self.first()

```
now lets say, we are working with the library code and dont change the user code.

but we want some functions defined in the user code's class so that our library code doesn't crash.

we can do that in 3 technics.

```Python
    # 1. __build_class__ method

    # 2. meta class

    # 3. __init_subclass__ method

```
__build_class__ method

this method allows us to hook into and do cool things in the process of building classes.

this method is from builtins module

```Python
import builtins

```
first grab the old __build_class__ within our interpreter.

```Python
old_method = __build_class__

```
now lets create our own method.

```Python
def new_method(*args,**kwargs): 

    # NOTE :

        # here **kwargs are those arguements that we pass in the perenthesis after the class name.

        # it is not the attributes and methods in the class body.

    print(f"Building class with arguements:{args} and key-word arguements: {kwargs}")

    return old_method(*args,**kwargs)

```
now replace the old method with our new one.

```Python
builtins.__build_class__=new_method

```
Now if we create a class we can see the magic is happening.

```Python
class Boss():

    pass

```
we can see that the class is building.

Building class with arguements:(<function Boss at 0x000001C4057B1AF0>, 'Boss') and key-word arguements: {}

now we can do some cool stuffs with this.

first create a class.

```Python
class InfrastructureLibary:

    def primary(self):

        return self.secondary()

class User(InfrastructureLibary):

    def secondary(self):

        return "secondary"

```
suppose we are working with the low-level programming team when we are developing the first class.

we have no right to change the User class.

we can see the the User class must need to have the secondary() method unless our code will fail.

so how to remind the developer of the User class that they must need to include secondary() in there code.

well we can use the __build_class__ method here.

```Python
import builtins

old_method2 = __build_class__

```
here we have changed the *args little bit. 

it is actually separated into the name of the functions, name of the class and its base class.

```Python
def new_method2(function,name,base=None,**kwargs):

    if base is InfrastructureLibary:

        print("WARNING: You must need to create a secondary() function.")

    if base is not None:

        return old_method2(function,name,base,**kwargs)

    return old_method2(function,name,**kwargs)

builtins.__build_class__=new_method2

```
now if we create a child class of the InfrastructureLibary class, then we can see that gives us the warning.

```Python
class NewUser(InfrastructureLibary):

    def secondary(self):

        return "secondary"

```
but in the Real world example, developers wont solve the problem like this.

rather than they use MetaClass. see metaclass.py module for better understanding.

```Python
class Meta(type):

    def __new__(self,class_name,base,attrs):

        if not "secondary" in attrs:

            print("WARNING: You must need to create a secondary() function.")

        return super().__new__(self,class_name,base,attrs)

class InfrastructureLibrary2():

    def primary(self):

        return self.secondary()

class User2(InfrastructureLibrary2,metaclass=Meta):

    def secondary(self):

        pass

```
But MetaClass is pretty complex topic in python.

so the developers of python have created a new method called __init_subclass__

it allows us to hook into the subclass of any parent class.

__init_subclass__ runs after the creation of the subclass.

```Python
class Infra:

    def __init_subclass__(cls,*args,**kwargs): 

        super().__init_subclass__(*args,**kwargs)

        print("Must Have to include last() method")

        print("Creating subclass, name :", cls.__name__)

    def first(self):

        return self.last()

class UserCode(Infra):

    def last(self):

        return "last"

```
__init_subclass__ has more things to learn. i will learn them when I need them.


*******************************************************
*******************************************************
meta classes in python

part 1

in this module we will cover meta classes.

meta classes is a fairly complicated but interesting topic in python.

we are going to start from how classes are created, instantiated, the way they work in the lower level of python.

and then we will learn what metaclasses are, how they actually work and how would we want to use them.

here we will learn the basics of metaclass.

if we really want to use these we need to look to the python documentation for beyond the basics.

why metaclass?

there are several things we cannot do with classes.

meta class allow us to do those things.

lets get started.

lets we create a class inside a function.

```Python
def hello():

    class Hi:

        pass

    return Hi

```
here we wont getting any error.

it is legal in python to create a class inside a function and return it.

the reason we can do that in python is that in python classes are objects.

infact, "EVERYTHING IN PYTHON IS AN OBJECT" NOTE that

what it mean to be an object?

it means they are kind of living things.

we can interact them within runtime, we can pass in parameters, we can store it, save it, modify it etc.

we might say how can be classes are objects?

we thought that classses create object for us.

its true. but it doesn't mean that class doesn't an object.

so if class is a object, then we might have any higher level class which created that class for us.

that is a meta class

What does meta class actually do?

a class defines the basic rules for the objects. it defines the attributes, parameters, methods etc.

whereas a meta class defines the rules for a class.

so if we create a class we need the metaclass to create it.

this happens automatically in python.

now lets create another class.

```Python
class Test:

    pass

```
lets print an object of that class

```Python
a = Test()

print(a)

```
we can see that it is saying <__main__.Test object at 0x000001FA3B071C70>

now lets print the class.

```Python
print(Test)

```
we can see that it is saying <class '__main__.Test'>

we can see that it doesn't tells us that it is an object. but it is an object.

```Python
def func():

    pass

```
we can use the type method to see the type of any object.

```Python
print(type(func))

print(type(3))

print(type("h"))

print(type(a)) # here we are getting the type <class '__main__.Test'>

```
lets see the type of the class as it is a object too.

```Python
print(type(Test)) 

```
we can see that it is printing <class 'type'>

it is pretty awkward. we can see that the type of the class is "type"

here type is the metaclass. it defines the rules and create the class for us.

we can use type to create a class manually. 

```Python
MyTest=type("MyTest",(),{})

```
this is completely equivalent to the first time when we created the Test class.

we can create a object of that class also.

```Python
b=MyTest()

print(b) # we can see that it is giving <__main__.MyTest object at 0x000001F599A71DC0>

```
we can also print the class

```Python
print(MyTest)

```
we can see that this is giving us <class '__main__.MyTest'>

it is probably the less used technic for creating a class in python.

so we can create a class using metaclass "type" 

and we need to pass the name of the class, 

the name of the base class in () 

and the name of the methods and attributes in {}

so lets see an example of a class using methods and attributes.

doing some pre work-

```Python
class Parent:

    def show(self):

        print("hi")

def func2(self): # since we will add this function to the class, we need to use self

    return "Hello"

```
defining the class with all options using type class.

```Python
NewTest=type("NewTest",(Parent,),{"x":5,"new_func":func2})

```
note that here we have use comma(,) after the parent class as we want to ensure that as tuple.

creating a object of that class.

```Python
t=NewTest()

```
using the attributes and methods of t object.

```Python
print(t.x)

print(t.new_func())

print(t.show())

```
we can also create attributes outside of the class just like the regular class.

```Python
t.y=4

print(t.y)

```
So this is how we use type and use metaclass, create class with the metaclass. 

so we have seen that, metaclass is any callable that takes parameters for:

```Python
    # 1. the class's name

    # 2. the class's bases (parent class)

    # 3. the class's attributes (variables and methods)

```
the type is the default metaclass in python.

so this is the basics now we will actually dive into the real usecase of meta classes.

we will see how to create custom metaclass with the help of default type metaclass.

```Python
"""go to oop15(metaclasses2).py"""
```

*******************************************************
*******************************************************
meta classes in python

part 2

here we will create our own metaclass which will inherit from the type class.

this is pretty simmilar thing as the default type metaclass.

but we will change how the object is constructed so that we understand what can we actually do with metaclass.

so lets get started

creating meta class

```Python
class Meta(type): 

    # we not necessarily have to inherit form type. but in our purpose that will work.

    # the reason for that is type does some other operations when creating a class.

    # if we dont inherit from type, our class wont be a metaclass, 

    # it will be general class which use type metaclass to create a class.

    # besides, this inheritances will give us the ability of overriding methods of type class

    # now we will define a __new__ method. it executes before the __init__ method.

    # so this is always called first when a object is created.

    def __new__(cls, class_name, bases, attrs): 

        # remember that, in type arguement we pass name, class_name, bases and the attributes.

        # NOTE: it is not a class method but by convention we pass cls instead of self as we are creating class object.

        # do some more stuffs to override this __name__function:

        print(f"Creating Class with {attrs}")

        # creating class in return 

        return type(class_name, bases, attrs) 

        # here we can use super().__new__ method instead of type as type is the parent class.

        # return super().__new__(cls,class_name,bases,attrs)

    # __init__ method changes the values and takes the parameters in.

```
now we will create another class

```Python
class Dog(metaclass=Meta): # defining the new Metaclass in parenthesis.

    # creating some attribute

    x=5

    y=8

    def func(self):

        return "hello"

```
now we can see that it prints our message which we defined in the __new__ method.

now we know the information, metaclass can be extreamly powerful.

we can hook into the construction of a class and we can modify the construction.

lets change all of the attributes we have here into upper case.

```Python
class NewMeta(type): 

    def __new__(cls, class_name, bases, attrs): 

        new_attrs={}

        for key,value in attrs.items():

            if not key.startswith("__"):

                new_attrs[key.upper()]=value

            else:

                new_attrs[key]=value

        print(f"Creating Class with {new_attrs}")

        return type(class_name, bases, new_attrs)

class Cat(metaclass=NewMeta):

    x=5

    y=8

    def func(self):

        return "hello"

```
now lets create an attribute of Cat

```Python
c=Cat()

```
now lets print out the x attribute of c object.

rint(c.x)

this will give us an error. but we have defined x attribute in the Cat class.

well we are getting error because we changed the x attribute to X in the metaclass.

```Python
print(c.X)

```
same goes for the func() method.

```Python
print(c.FUNC())

```
now we have undertand metaclass, now we can do whatever we want when working with class.

we can change the bases, class name, attributes, do certain operations based on the parametes.

metaclasses are great for doing complicated things """ inside of the frameworks """. NOTE

metaclass is nice when we are writting library code and we want user code to be very specific.

when user codes classes are inheritting form a specific class situated in the library code,

we can force them or tell them to initialize certain methods in that class so that our code doesn't crash.

actually, in every example of metaclass we will see that,

there is a parent class and some subclasses 

and we want to control the behaviours of subclasses without explicitely writing code in them. 

again there are more complex topics in metaclass. we can see them in the python documentaion.

we dont need to use them much. we should use them when we are 101% sure about what we are doing.

they will make our code really hard to understand.

but understanding these types of expert topics in python will really help us to code better,

because then we can become sure what is going on the background.


*******************************************************
*******************************************************
meta classes in python

part 3

problem solving with metaclass.

Problem: inherited docstrings aren't perticularly informative in python.

here we have two simple class (A and B) and B is the subclass of A

```Python
class A:

    def func(self):

        """Doc_String of class A"""

        pass

class B(A):

    pass

```
printing the doc string

```Python
print(A().func.__doc__)

print(B().func.__doc__) # this is doc string of class B.

```
but we are getting doc string of A twice. that is not what we expected.

so we cant knowthat we are getting the function through class A or B

More Specificaly,

```Python
    # the "nose testing" framework prints out the doc strings of test methods as it runs them.

    # unfortunately, if we have a test suite class that inherits from another class,

    # we wont be able to tell when its running method from parent class vs subclass.

```
Solution1:

the simple solution is that just manually include information in the docstrings.

```Python
class A2:

    def func(self):

        """Doc_String of class A2"""

        pass

class B2(A2):

    def func(self):

        """Doc_String of class B2"""

print(A2().func.__doc__)

print(B2().func.__doc__) 

```
but there will be lot of work if we have lots of subclasses or methods.

so there might be a better solution.

Solution2:

we can manually change the docstring in the __init__ method.

```Python
class A3:

    def __init__(self):

        old_doc=self.func.__doc__

        cls_name=type(self).__name__

        # changing the docstring

        #self.func.__doc__= str(old_doc) + str(cls_name)

        # but we are getting an error because doc string of method object is not writable.

        # NOTE: function docstrings in general are writable but methods docstring aren't.

    def func(self):

        """Doc_String of class """

        pass

class B3(A3):

    pass

print(A3().func.__doc__)

print(B3().func.__doc__) 

```
so if there is any way that we can change the doc string before function becomes a method?

yes. but before that we have to step back.

what are classes? --> a class is a special kind of object which create other objects called instances.

type() method tells us the class of an instance. so if we look for the type of a class.

```Python
print(type(A3)) # we can see that the type of a class is "type" it means class is a object of type class.

```
the type object actually do 3 different things in python.

```Python
    # 1. It denotes the type of an object (the types of classes, specifically).

    # 2. It tells us what type an object is.

    # 3. It can create new classes.

```
creating class with type

```Python
def hello(self):

    return "hello"

class_name="MyClass"

bases=(A3,)

attrs={"hello":hello}

MyClass=type(class_name,bases,attrs)

```
Now, lets try to solve our problem again.

Solution 3:

```Python
def make_class(name, bases, attrs):

    for f in attrs:

        attrs[f].__doc__=f"{attrs[f].__doc__} {name}"

    cls = type(name,bases,attrs)

    return cls 

def func(self):

    """Doc_String of class"""

    pass

```
creating class with make_class

```Python
A4=make_class("A4",(object,),{"func":func})

print(A4().func.__doc__) # it prints Doc_String of class A4

B4=make_class("B4",(A4,),{"func":func})

print(B4().func.__doc__) # it prints Doc_String of class A4 B4

```
but thats not we wanted. why this happend?

the answer is that both of these classes A4 and B4 are using same method in the memory.

so python modified the doctrings of the same object(function) in the memory.

rather than having two separate function in A4 and B4, they point to the same function.

```Python
print(A().func.__doc__ is B().func.__doc__) # it will return True.

```
so how can we solve this problem. well we can also create a function on fly using the func_type() class.

so lets create a function that copy a function.

```Python
def copy_function(f):

    func_type=type(f)

    new_func=func_type(

        f.__code__,    # bytecode

        f.__globals__, # global namespace

        f.__name__,    # function name

        f.__defaults__,# default keyword arguements values

        f.__closure__) # closure variables

    new_func.__doc__=f.__doc__

    return new_func

```
now lets try again to solve our problem

Solution 4:

```Python
def make_class2(name, bases, attrs):

    for f in attrs:

        new_f = copy_function(attrs[f])

        new_f.__doc__=f"{attrs[f].__doc__} {name}"

        attrs[f] = new_f

    cls = type(name,bases,attrs)

    return cls 

def func2(self):

    """Doc_String of class"""

    pass

A5=make_class2("A5",(object,),{"func":func2})

print(A5().func.__doc__) 

B5=make_class2("B5",(A5,),{"func":func2})

print(B5().func.__doc__)

```
hey we solved our problem using metaclass!

here the make_class function we are using is a meta class.

python use different complex way to create metaclass.

```Python
def make_class3(name, bases, attrs):

    for f in attrs:

        # skipping special methods and non-callable functions since we dont want to mess up with those.

        if f.startswith("__") or not hasattr(attrs[f],"__call__"):

            continue

        # copy the function, replace the docstring and return the old method.

        new_f = copy_function(attrs[f])

        new_f.__doc__=f"{attrs[f].__doc__} {name}"

        attrs[f] = new_f

    cls = type(name,bases,attrs)

    return cls 

```
and then we are going to create a class with class keyword.

then we can do this by adding metaclass arguement in the parenthesis.

```Python
class A6(metaclass=make_class3):

    def func3(self):

        """doc string of class"""

        pass

class B6(A6, metaclass=make_class3):

    pass

print(A6().func3.__doc__)

print(B6().func3.__doc__)

```
note that, here we are not having our expected results for subclass B6.

it means subclasses not actually rewrite the doc strings correctly.

this is happening because func3() is not passed as an attribute of B6 (it is already an attribute of A6)

to make this really work we have to go through all the attributes of all the parent classes and copy them, too.

so now we know that meta classes are powerful tool. we can use it for many purposes.

What exactly can we do with meta classes?

we see that meta classes intervene on class (not instances) creation.

this gives us the oppurtunity to modify the class's method before the class is created.

we can,

```Python
    # 1. copy each of the functions that will become methods later

    # 2. change doc strings or any other properties of this new functions

    # 3. create the class using these new functions instead of those which are originally given.

```
we can find more useful real world example where metaclasses are used.

for example, django use metaclasses to simplify its interface.

it gives us opportunity to work with complex classes as user 

where all the fancy complex parts are handled by the metaclass.


*******************************************************
*******************************************************
__slots__ dunder method in python

here we will demonstrate in code why using __slots__ results faster instant attributes access.

and space in memory become more and more relevent as the number of instant creation grows.

first lets create two classes identical in may ways.

```Python
class Planet:

    def __init__(self,cities):

        self.cities = cities

```
creating object

```Python
earth = Planet(["Dhaka","DC"])

class SlottedPlanet:

    # the only difference between this two class it that it has a __slot__ apecial attribute at the top.

    __slots__ = ["cities"] # it takes strings and this strings are the name of all attributes

    def __init__(self,cities):

        self.cities=cities

```
creating object    

```Python
slotted_earth = SlottedPlanet(["Madrid","Paris"])

```
lets print those objects.

```Python
print(earth)

print(slotted_earth)

```
printing the attributes of those objects.

```Python
print(earth.cities)

print(slotted_earth.cities)

```
we can see that there is no difference.

now lets add a new attribute in the earth object called country.

```Python
earth.country=["Bangladesh","United States"]

```
if we try to do the same with the slotted_earth we get an attribute error.

lotted_earth.country=["Spain","France"]

the only attributes that this object can have are those which we have provided to the __slots__.

so we can even left the __slots__ attribute empty.

```Python
class EmptyBin:

    __slots__=[]

```
creating object

```Python
empty_object=EmptyBin()

```
we cant create any attribute of that object.

mpty_object.att="new attribute"

why cant we add attributes in a slotted object in the general way?

we can also store attributes in a general earth object by storing them in the instant dictionary.

we can access the dictionary by __dict__ method.

```Python
print(earth.__dict__)

```
but in the slotted_earth we do not have any __dict__ method.

rint(slotted_earth.__dict__)

this will give us an attribute error.

so SlottedPlanet class dont even created a dictionary.

we know that dictionary even though empty one take up space.

so since slotted object dont create dictionary we can have a much space in the memory. so it is a lightweight object.

we can see the space of any object by the getsizeof() method from the sys module.

```Python
import sys

```
we can see that this object take 48 bytes space.

```Python
print(sys.getsizeof(earth))

```
and its dictionay take 104 bytes space.

```Python
print(sys.getsizeof(earth.__dict__))

```
so in total 152 bytes of memory usage.

again the slotted_earth also takes only 48 bytes space.

```Python
print(sys.getsizeof(slotted_earth))

```
so we can see that the memory space is decrreased though a little portion of it.

but if we have big data, then it will be a great benefit by releasing much GBs of memory

and it also can give us a performance boost.

lets see the time it needed to perform operations in a regualar object vs slotted object.

we have to import timeit module for that.

```Python
import timeit

```
creating two classes

```Python
class UnSlotted:

    pass

class Slotted:

    __slots__=["values"]

```
creating a get_set_delete_func function

```Python
def get_set_delete_func(obj):

    # creating another function which will

    def get_set_del():

        obj.values=[0,1]   # set values

        obj.values         # get values

        del [obj.values]   # delete values

    return get_set_del     # returnning the inner function

```
creating object

```Python
non_slotted_obj = UnSlotted()

slotted_obj=Slotted()

```
repeating operations multiple time using repeat() function of timeit module 

and printing the minimum process time (in seconds) using min function(). 

```Python
print(min(timeit.repeat(get_set_delete_func(non_slotted_obj),repeat=5)))

```
doing the same operation with slotted_obj.

we can see 15% to 20% improvement in time.

```Python
print(min(timeit.repeat(get_set_delete_func(slotted_obj),repeat=5)))

```
we can not only use classes having __slots__ attributes for memory and time boost,

we can also use them in the library code 

and ensure that the user cant define new attributes and methodsin our class

which can make our class unstable.

library code

```Python
class Library:

    __slots__=["attr1","attr2"]

    def __init__(self,attr1,attr2):

        self.attr1=attr1

        self.attr2=attr2

```
user code

```Python
user1=Library(0,1)

```
we cant create more attribute here.

now lets see inheritance of slotted class.

```Python
class Computer:

    __slots__=["ram"]

slotted_comp=Computer()

slotted_comp.ram="4 GB"

```
create a subclass of the slotted class

```Python
class Laptop(Computer):

    pass

inherited_laptop=Laptop()

```
if our subclass dont initiatize __slots__ attribute,

then every object of our subclass will still have instant dictionary.

```Python
print(inherited_laptop.__dict__)

```
printing the size of inherited object

```Python
print(sys.getsizeof(inherited_laptop))

print(sys.getsizeof(inherited_laptop.__dict__))

```
adding attributes to inheritted object.

```Python
inherited_laptop.ram="8 GB"

inherited_laptop.rom="2 TB"

```
printing the instant dictionary again.

```Python
print(inherited_laptop.__dict__)

```
we can see there is newly created rom attribute but no previous ram attribute.

actually the parant class will continue to be sloted if we created object of a subclass.

the attribute thst was presious defined in the __slots__ of parent class will store there.

whereas the newly defined attributes will store in the instant dictionary of that object. 

lets do that again. but in this time we will use __slots__ attribute in the subclass and set that equal to empty.

```Python
class Desktop(Computer):

    __slots__=[]

inherited_desktop=Desktop()

inherited_desktop.ram="16 GB"

```
though the __slots__ is empty, we can store the ram attribute which was previously mentioned in the __slots__ attribute of parent class.

but we cant add another attribute here it will give us an attribute error.

nherited_desktop.cpu="i7"

again, we cant see the __dict__ attribute too as it doesn't have one.

rint(inherited_desktop.__dict__)

what if we want to add attributes to class dynamicaly?

then we can add "__dict__" attribute in the __slots__ attribute.

```Python
class Dynamic:

    __slots__=("x","__dict__") # we can use both list or tuple to our __slots__ method. but we should use tuple if we want to make it immutable.

dynamic_slotted=Dynamic()

dynamic_slotted.x=1

dynamic_slotted.y=2

dynamic_slotted.z=3

dynamic_slotted.p=4

```
it has a __dict__ method as we mention it earliar in the __slots__

```Python
print(dynamic_slotted.__dict__)

```
we can see that the first attribute x not in the __dict__ as we add that separately in the __slots__

but "y", "z", "p" attribute are in the __dict__

NOTE: one thing we have to be very careful about that we should not add same attribute in the parent and subclass's __slots__ attribute.

```Python
class Parent:

    __slots__=("x")

class Child:

    __slots__=("x","y") # x is in the both __slots__ method.

class NewChild:

    __slots__=("y",)

```
creating object

```Python
child_slotted=Child()

new_child_slotted=NewChild()

```
printing the size of the object.

```Python
print(sys.getsizeof(child_slotted))

print(sys.getsizeof(new_child_slotted))

```
this wont give us any error. 

but doing this will force our object to take op more space than they need to.

we can see that it takes more bytes than necessary.

NOTE: in a very large codebase, it is important not to use __slots__ unless very much necessary.

because there can be problem in multiple inheritance.

```Python
class ParentA:

    __slots__=("x",)

class ParentB:

    __slots__=("y",)

```
our Subclass inherits both from ParentA and ParentB

```Python
class Subclass(ParentA,ParentB):

    pass

```
when both parents have a non-empty __slots__, 

then we will have an TypeError saying "TypeError: multiple bases have instance lay-out conflict"

to overcome the problem one of the parent has to have a __slots__ defined with an empty list or tuple.


*******************************************************
*******************************************************
OOP quick tips

Tip 1

printing the children classes of Parent class.

Parent classes

```Python
class Father:

    def __init__(self):

        value=0

    def update(self):

        value+=1

    def renew(self):

        value=0

    def show(self):

        print(value)

class Mother:

    def __init__(self):

        value=1

    def update(self):

        value-=1

    def renew(self):

        value=0

    def show(self):

        print(value)

```
Children classes

```Python
class Child_1(Father):

    def update(self):

        value+=2

class Child_2(Mother):

    def update(self):

        value-=2

```
the main function.

```Python
def interiors(*classx):

    subclasses=set()

    work=[*classx]

    while work:

        parent=work.pop()

        for child in parent.__subclasses__():

            if child not in subclasses:

                subclasses.add(child)

                work.append(child)

    return subclasses

print(interiors(Father,Mother))

```

On Sat, Mar 26, 2022 at 9:36 PM Mahdi Rasoulinezhad <mahdi.rasoulinezhad@gmail.com> wrote:
During the past few days, I was developing an idea for a self-organized logistics system. To compare my results, I used the Google or-tools package. The total distance of the or-tools routes is 6208 meters.The total distance of my code is 6260 meters. That sounds promising.More details about this example can be found at: https://developers.google.com/optimization/routing/vrp
The advantage of this self-organized method is its ease of use and ease of making agents more realistic. It is more condition/constraint friendly, and it does not require lots of OR experience to develop a solution.
