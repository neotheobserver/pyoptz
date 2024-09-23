# Python Optimization

Recently, I was teaching one of my friends at work about the basics of python. He was doing the CS50 course from Harvard and would solve the problem set in his free time at work. Most often the solutions he wrote were not optimal but it did the job done and instead of guiding him towards the optimal way, I assisted him in achieving the same thing with his own train of thoughts. This got me thinking how in the early days of programming everyone (me) just wants to complete the task at hand, we never really care about efficiency when it comes to coding, it is just about getting results. Over the years we learn better techniques but more often then not, it is a result of years of doing the same thing rather than a conscious decision to write better code. Hence, I did a little profiling of different types of codes that I did for myself and also so that I could show my colleague and friend how a single decision can matter in coding.

The codes below will require jupyter-notebook installed which can be done using:

```sh
pip install jupyter-notebook
```

Alternatively, you can use the IPYTHON kernel. I prefer notebook. To anyone reading this I would like to encourage to run the query and see for themselves. Also, I would appreciate if someone with more knowledge could reach out and provide more details and/or correct me if I am wrong.

# Table of Contents

- [List in Python](#list-in-python)
- [Counter](#counter)
- [Enumerate and Zip](#enumerate-and-zip)
- [Note](#note)

## List in Python

### Time

```py
%timeit -n 50 -r 50 l = list()
%timeit -n 50 -r 50  l = []
```

The first way is slower as it requires function call while the second one does not.

Now, let's take it up a notch and try to populate the list

```py
%%timeit -n 50 -r 50
l = []
for i in range(10):
    l.append(i)
```

```py
%%timeit -n 50 -r 50
l = [i for i in range(10)]
```

```py
%%timeit -n 50 -r 50
l = [*range(10)]
```

The first way is slowest as it requires method call `append` while the second one does not (not sure about the detail of its implementation tho). The third method is fastest as it does not even require for loop.

`PS: This should be replicated for tuple and dictionary as well`

### Memory

```py
import sys
l = [i for i in range(10)]
print(sys.getsizeof(l))
l = [*range(10)]
print(sys.getsizeof(l))
```

The second way is uses less memory. This is apparently due to the way list is created. In the first way each integer is added to the list one by one which has different implementation (one that uses more memory) than the second way which creates list at a single go.

## Counter

Counter is one of the class from built in `collections` module of python. It is used to count the occurence of each elements in the list.

```py
%%timeit -n 500 -r 500
from collections import Counter
a_list = ['b' ,'a', 'c' , 'd','a', 'a', 'b']
alphabet_counts = Counter(a_list)
```

`Alternatively,`

```py
%%timeit -n 500 -r 500
a_list = ['a' ,'b', 'c' , 'd', 'a', 'b', 'a']
alphabet_counts = {}
for alphabet in a_list:
    if alphabet in alphabet_counts:
        alphabet_counts[alphabet] += 1
    else:
         alphabet_counts[alphabet] = 1
```

The above code does the same thing as counter does. But it is not succint in nature. However, suprisingly, it is faster than Counter class.

`Note: Counter does return dictionary by sorting values in descending order which might explain it taking more time.`

## Enumerate and Zip

Both the code below combine lists with each same indexed item member of a single tuple.

`Enumarate` is used to iterate over the iterables and return the index as well as the value.

```py
%%timeit -n 500 -r 500
first_list = ['Apple', 'Orange', 'Mango']
second_list = ['Okay', 'Good', 'Awesome']
combined_list = [(item,second_list[i]) for i,item in enumerate(first_list)]
```

`Zip` is used to combine multiple iterables together

```py
%%timeit -n 500 -r 500
first_list = ['Apple', 'Orange', 'Mango']
second_list = ['Okay', 'Good', 'Awesome']
combined_list = [*zip(first_list,second_list)]
```

The zip method is almost twice faster than enumerate way of doing the same thing.

## Note

This can only be used as a starting point to understand and observe efficient code writing techniques in Python. Similar to all my other projects, I do plan on continuing this and adding more content; however, there is high probability that I might never get around to it.
