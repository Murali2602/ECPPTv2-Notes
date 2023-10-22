
##### Skeletal Code

```C++
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello World!" << endl;
    return 0;
}
```

### Variables 

```C++
#include <iostream>
using namespace std;

int main()
{
	// String Datatype
    string name="Murali";
    // Int Datatype
    int age=20;
    cout << "Hello World!" << endl;
    // Calling multiple variables
    cout << name << " is " << age << " years old" << endl;
    return 0;
}
```

##### Data Types

```C++
#include <iostream>
using namespace std;

int main()
{
    // char - can hold only one character and always denoted using single quotes
    char grade = 'A';

    // strings are a bunch of characters
    string phrase = "Murali";

    // integer (eg: 50 or -50)
    int age = 50;

    // float 
    float pi = 3.14;

    // double 
    double gpa = 3.7;

    // bool
    bool isMale = true;
    
    return 0;

}
```


### Working with Strings

Find a particular part of a string using index - `index[3]`

##### phrase.find()
Find if a particular thing is inside a string
**Usage**: `cout << phrase.find("Murali", 0);`
Here 0 is an index position from which it starts finding "Murali".

##### phrase.substr()
Grab string from particular index
**Usage:** `cout << phrase.substr(4, 2)`
Here it will start grabbing characters from index 4 and grab 2 characters.


### Working with Numbers

`sum++` adds 1 to the sum
`sum--` subtracts 1 from the sub
`sum += 80` adds 80 to the sum (Works for all other operators too)

Math - 
```C++
#include <iostream>
#include <cmath>

using namespace std;

int main()
{
    
    cout << pow(2, 8);

    return 0;

}
```


### User Input

One word - 
```C++ 
    #include <iostream>
    #include <cmath>

    using namespace std;

    int main()
    {
        
        int age;

        cout << "Enter your age: ";

        cin >> age;

        cout << "You are " << age << " years old.";

        return 0;

    }
```
Multi Word -
```C++
    #include <iostream>

    using namespace std;

    int main()
    {
        
        string name;

        cout << "Enter your name: ";

        getline(cin, name);

        cout << "You are " << name << "." << endl;

        return 0;

    }
```

### Arrays 
```C++
#include <iostream>

using namespace std;

int main()
{
    // luckyNums[20] allows us to store upto 20 integers in the array; Initialize empty array - int luckyNums[20];
    int luckyNums[20] = {4, 8, 2, 5, 1, 8};
    // Print Index 2 of the luckyNums array
    cout << luckyNums[2] << endl;
    return 0;

}
```
