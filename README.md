# Python Optimization

Recently, I was teaching one of my friends at work about the basics of python. He was doing the CS50 course from Harvard and would solve the problem set in his free time at work. Most often the solutions he wrote were not optimal but it did the job done and instead of guiding him towards the optimal way, I assisted him in achieving the same thing with his own train of thoughts. This got me thinking how in the early days of programming everyone (me) just wants to complete the task at hand, we never really care about efficiency when it comes to coding, it is just about getting results. Over the years we learn better techniques but more often then not, it is a result of years of doing the same thing rather than a conscious decision to write better code. Hence, I did a little profiling of different types of codes that I did for myself and also so that I could show my colleague and friend how a single decision can matter in coding.

The codes below will require jupyter-notebook installed which can be done using:

```sh
pip install jupyter-notebook
```

Alternatively, you can use the IPYTHON kernel. I prefer notebook. To anyone reading this I would like to encourage to run the query and see for themselves. Also, I would appreciate if someone with more knowledge could reach out and provide more details and/or correct me if I am wrong.

# Table of Contents

- [List in Python](#list-in-python)
- [Note](#note)

## List in Python

### Time

```py
%timeit -n 50 -r 50 l = list()
%timeit -n 50 -r 50  l = []
```

The first way is slower as it requires function call while the second one does not.

Now, let take it up a notch and try to populate the list

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

The first way is slowest as it requires method call `append` while the second one does not (not sure about the detail of its implementation tho). The way method is fastest as it does not even require for loop.

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

## Note

This can only be used as a starting point to understand and observe efficient code writing techniques in Python. Similar to all my other projects, I do plan on continuing this and adding more content; however, there is high probability that I might never get around to it.
