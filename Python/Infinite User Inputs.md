```python
#Example
bidding_finished = False  
while not bidding_finished:  
    name = input('What is your Name?\n')  
    bid_price = input("How much do you want to bid?\n")  
    dict[name] = bid_price  
    more_players = input('Are there more users who want to bid?\n').lower()  
    if more_players == "no":  
        bidding_finished = True
```

```python
#Another Example
def format():  
    loop = False  
 	while not loop:  
        again = input("yes or no")  
        if not again == "yes" and not again == "no":  
            print("Wrong Input")  
        if again =="yes" or again == "no":  
            return "Done"  
			 loop = True  
  
print(format())
```