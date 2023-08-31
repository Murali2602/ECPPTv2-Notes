
### Insecure Direct Object Reference

This is a type of access control vulnerability.
This occurs when the input data is not validated on the server-side.

For example - 
![](https://i.imgur.com/EGkOKbG.png)

In this image when we change the order number to something else it displays the output of it without any checking. This proves that this is vulnerable to IDOR. We can fuzz through it to find valid orders and get more information.


> Note: Try to look at the network tab for get requests for some interesting request calls such as ?user_id=15 as this can used to check for idor
> ***Example*** - 
> ![](https://i.imgur.com/PhEqp0l.png)


