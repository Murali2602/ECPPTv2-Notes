# <u>break</u> - 
If the execution reaches a break statement, it immediately exits the loop and continues with the next code.
Example - 
```python 
➊ while True:
	print('Please type your name.')
	➋ name = input()
	➌ if name == 'your name':
		➍ break
➎ print('Thank you!')
```
as soon as the execution hits the line 4 it exits the loop and executes the next command outside that loop.

---
# <u>continue</u> - 
When the program execution reaches a ***continue*** statement, the program execution ***immediately jumps back to the start of the loop and reevaluates the loop’s condition.*** (This is also what happens when the execution reaches the end of the loop.)

Example - 
```python
while True:
	print('Who are you?')
	name = input()
	➊ if name != 'Joe':
		➋ continue
	print('Hello, Joe. What is the password? (It is a fish.)')
	➌ password = input()
	if password == 'swordfish':
		➍ break
➎ print('Access granted.')
```
