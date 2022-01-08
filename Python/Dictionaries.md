# Dictionary

----
## Common Dictionary Syntax -
```python
Dictionary_Name = {
	"Test":"This is a dictionary",
	"Test1":"This is just another entry",
}
```

---
## Retreiving items from the Dictionary - 
```python
Dictionary_Name = {
	"Test":"This is a dictionary",
	"Test1":"This is just another entry",
}
print(Dictionary_Name["Test"])
```
> ***Output - ***
> ##### ***This is a  Dictionary***

---
## Adding new items to Dictionary -
```python
Dictionary_Name = {
	"Test":"This is a dictionary",
	"Test1":"This is just another entry",
}
Dictionary_Name["Test2"] = "This is Test2 entry"
print(Dictionary_Name)
```
> ***Output - ***
> ##### ***{'Test': 'This is a dictionary', 'Test1': 'This is just another entry', 'Test2': 'This is Test2 entry'}***
---
## Create an Empty Dictionary - 
```python
Dictionary_Name = {}
```
---
## Wipe an existing Dictionary - 
```python
Dictionary_Name = {}
print(Dictionary_Name)
```
---
## Edit an item in Dictionary - 
```python
Dictionary_Name = {
	"Test":"This is a dictionary",
	"Test1":"This is just another entry",
}
Dictionary_Name["Test1"] = "This is gonna replace the existing stuff"
```
---
## Loop through a Dictionary - 

> ### Looping only ***"Keys"***
> ```python
> for key in Dictionary_Name:
> print(key)
> ```
  
> ### Looping Both ***Keys and Value***
>```python
>for key in Dictionary_Name:
>	print(key)
>	print(Dictionary_Name[key])
>```

---

## Nesting In Dictionary - 

We can nest ***Lists and Dictionaries*** inside ***Dictionaries.***
- #### Nesting a List inside Dictionary -
>```python
>travel_log = {
>	 "France" : ["Paris", "Lille", "Dijon"],
>	 "Germany" : ["Berlin", "Hamburg", "Stuttgart"],
 >}
>print(travel_log)
>```
	
- #### Nesting a Dictionary inside a Dictionary - 
> ```python
>travel_log = {  
 >"France" : {"cities_visited": ["Paris", "Lille", "Dijon"],
 >"visits": 12, "People": ["Murali","Kajal"]},  
>"Germany" : ["Berlin", "Hamburg", "Stuttgart"],  
>}  
>print(travel_log)
>``` 
   
- #### Nesting a Dictionary inside a List - 
>  ```python
>travel_log = [  
>  {
>	   "country":"France",
>	   "cities_visited" : ["Paris", "Lille", "Dijon"],
>	   "visits": 12,
>	   "People": ["Murali","Mohan","Kajal"]
>   },  
>{
>"country":"Germany",
>  "cities_visited":["Berlin", "Hamburg", "Stuttgart"]
> },  
>]  
>for list in travel_log:  
>      print(list)
   