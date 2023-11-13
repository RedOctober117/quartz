_Recursion_ is the process of using a dynamically expanding equation to find a solution, rather than a traditional [[Loops|loop]]. Let's begin with factorials as an example:

The factorial of any non-negative integer is $n!$, where $n! = n(n - 1)(n - 2) ... (n - n)$. We can represent this with the following recursive python code:

```python
def recursive_factorial(factor):
	if factor == 1:
	    return factor
	else:
	    return factor * recursive_factorial(factor - 1)
```

The first most important line of this code is:
```python
return factor * recursive_factorial(factor - 1)
```

