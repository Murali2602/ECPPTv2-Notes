# Functions
## Basic Syntax - 
```python
def greet():
	print('Hello')
	print('Good Morning')
	
	
greet() #Calling the function
```

## Parameters and Arguments - 
```python
def add(x,y):   #x and y are called parameters
	z = x + y 
	print(z)

	
add(4, 6)  #4 and 6 are called arguments
```

- ### Keyword Arguments 
```python
def person(name,age):
	print(name)
	print(age)
	
	
person(name='Murali', age=18)  # Here name= and age= are called as keyword parameters. 
```

- ### Default Parameters
```python
def person(name,age=18): # Here age= is known as default parameter.
	print(name)
	print(age)
	

person('Murali') # If you do not specify the age= value it will still work since u have given a default parameter in the function already(18).
```

- ### Variable Length Parameters 

```python
def sum(a,*b):  #'*b' here is known as variable length parameter meaning you can give as many arguments as you want to parameter b and it will store everything in a tuple so this would look something like (25,123,123414,12313), i didn't include 26 since it is assigned to 'a'.
	
	c = a
	print(a,b)
	for i in b:
		c = c + i
		
	print(c)

	
sum(26,25,123,123414,12313)
```

**Output**:  
> ![Nothing](https://i.imgur.com/3z9LxY9.png)

- ### Keyword Variable Length Arguments(**kwargs)
```python
def person(name, **data): #We use ** to specify Keyword Variable Length Arguments.
	print(name)
	for i,j in data.items(): # Printing Key:Value pair since kwargs are stored in a dictionary.
		print(i,j)
		

person('Murali',age=18,city='Bangalore',mob=123456789) #These are known as Keyword arguments.
```
**Output**: 
> ![example](https://i.imgur.com/VGWFAaP.png)
## Global vs Local Scope
```python
a = 10  #Here 'a' is a global variable.

def something():
	a = 2  #Here 'a' is a local variable since it's inside a function.
	print(a)

something()
print(a)
#Note: You can't print/access a 'local' variable outside the function but you can access 'global' variable inside a function.
```
**Output:**
> ![example](https://i.imgur.com/qcP1v65.png)


To use a global variable inside a function explicitly: 
```python
a = 10

def something():
	global a #This will modify a value globally too.(basically calling global variable.)
	a=8
	print(a)
	
something()
print(a) #Here  of 'a' will be 8 since we changed the value to 8 inside the function which was called globally.
```
**Output:**
>  ![example](https://i.imgur.com/1afysmR.png)

To access a global variable inside a function but have a local variable too(even if it has the same name):
```python
a = 10 
print(id(a)) #Printing id of 'a'

def something():
	a = 2 # Local variable
	x = globals()['a'] #To access the global variable of 'a' inside a function.
	print(id(x)) #Printing id of 'a'
	print('In function ',a) #Printing value of 'a' inside the function.
	
	#To change the value of global value too
	globals()['a'] = 15
	
something()
print(a)
#Note: This way we can use 'a' as both local variable and a global variable.
```
**Output:**
> ![example](https://i.imgur.com/69AndBv.png)

## Return vs Print
#### Print - 
Print is used to print out the things inside the function. 
**For example**: 
```python
def test():
	print('Hello World')
  	
test() #This will  'Hello World'
```

#### Return - 
Return is used to store the value inside the function. 
**For example**: 
```python
def format():
	fname = input("Enter your First Name: \n")    
	lname = input("Enter your Last Name: \n")   
	return fname+" "+lname  #Return will store the output as a value inside format() function. 

name = format()
print(name)
#If the input was 'Jake Peralta', the value of format() would be 'Jake Peralta'.
```
	



	



