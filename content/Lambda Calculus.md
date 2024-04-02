# Fundamentals

$$
\lambda 
$$
$\lambda$ calculus "can be called the smallest universal programming language of the world" ([source](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf)), because it is Turing complete. It consists of a single transformation rule and a single function definition scheme. Expressions comprise all of $\lambda$ calculus.

The following are all valid forms of grammar:

$$
\begin{aligned}
E \rightarrow name  \\ 
E \rightarrow \lambda \space name.E \\ 
E \rightarrow EE \\ 
E = (E) \\ 
\end{aligned}
$$

To avoid parsing ambiguity, $expressions$ are always left associated:
$$
E_1E_2E_3...E_n
$$
is evaluated as:
$$
(...((E_1E_2)E_3)...E_n)
$$
This is the same principle that the post script notation uses.
## Functions

### Anonymous Functions

$\lambda$ functions have a single identifier, $\lambda$, and follow this format:
$$
\lambda name . E
$$
This defines a new _anonymous_ function. All functions are anonymous in $\lambda$ calculus. Here is an example:
$$
\lambda x.x
$$
This is the identity function. The name after $\lambda$ is the parameter $x$ for the body $x$. 

### Function Applications
Functions in $\lambda$ calculus are applied like so:
$$
E \rightarrow E_1E_2
$$

This calls $E_1$ and sets its formal parameter to $E_2$.

Let's use our example from [[#Anonymous Functions]] to demonstrate:
$$
(\lambda x.x)y
$$
Here, we applied the expression $y$ to the expression $(\lambda x.x)$. When doing so, we substitute the free variable $y$ for each occurrence of the bound variable $x$:
$$
(\lambda x.x)y = \{y/x\}x = y
$$
Left of the first equals, we have the application. Next, we have $\{y/x\}$, meaning substitute $y$ for all occurrences of $x$ in the body of $\lambda x.x$. Because the body is comprised entirely of $x$, only one substitution takes place. Thus, $y$ is returned as the result of $(\lambda x.x)y$.

This format is seen in most common languages like python:
```python
def x(x):
	return x
```
Note, however, that in $\lambda$ calculus, functions do not have names; all functions are anonymous. A proper (but syntactically invalid) model of this in python is:
```python
def (x):
	return x
```
If you would like to see a true application of $\lambda$s in python, see [this documentation](https://docs.python.org/3/reference/expressions.html#lambda).

Names, like variables, do not have any functional purpose other than to distinguish one variable from another. For example:
$$
(\lambda x.x) \equiv (\lambda y.y) \equiv (\lambda z.z) \equiv (\lambda u.u)
$$

## Bound Versus Free Variables

All variables are local in $\lambda$ calculus. In the identity function, the body variable $x$ is *bound* because it is preceded by $\lambda x$. Thus, the expression $x$ is inexplicably and permanently tied to $\lambda x$, because it is directly related to its own parameters.

Here, $x$ is bound, but $y$ is free:
$$
(\lambda x.xy)
$$
Here, the first $x$ is bound, the first $y$ is bound, and the third $x$ is free:
$$
(\lambda x.x)(\lambda y.yx)
$$
Note: the second $x$ is completely independent and unrelated to $(\lambda x.x)$.

A variable of some $name$ is _free_ if one of the three following cases hold:
- $name$ is free in $name$.
- $name$ is free in $\lambda name_1.expression$ if the identifier $name \neq name_1$ and $name$ is free in $expression$.
- $name$ is free in $E_1E_2$ if $name$ is free in $E_1$ or if it is free in $E_2$

Variable $name$ is _bound_ if one of two cases hold:
- $name$ is bound in $\lambda name.expression$ if the identifier $name = name_1$ or if $name$ is bound in $expression$.
- $name$ is bound in $E_1E_2$ if $name$ is bound in $E_1$ or if it is bound in $E_2$.

An identifier can be free and bound in the same expression:
$$
\begin{aligned}
(\lambda x.xy)(\lambda y.y)\\
\lambda y.yy
\end{aligned}
$$
Initially, $y$ is free in $(\lambda x.xy)$. After the application of $(\lambda y.y)$, $y$ becomes bound.

## $\alpha$ Equivalence

### Single Renaming
$\alpha$-Equivalence occurs when two functions vary only by the names of the bound variables.
$$
E_1 =_\alpha E_2
$$
One $\alpha$ equivalent expression can be converted to another with a simple renaming procedure. 
$$
E \space \{y/x\}
$$
The renamed $name \space y$ cannot already exist in $E$, neither bound nor free. 
$$
\begin{aligned}
x \space \{y/x\} = y \\
z \space \{y/x\} = z, \text{if } x \neq z
\end{aligned}
$$
All possible single-$name$ scenarios are covered by the above two expressions. For an expression $x$, $\{y/x\}$ changes all $x$s to $y$, thus returning $y$. For an expression $z$, $\{y/x\}$ is only valid if $z$ _does not_ equal $x$. That is the case here, so nothing is renamed and we are returned the original expression $z$.

### Distributed Renaming
When working with multiple expressions, the renaming procedure is distributed to both:
$$

(E_1E_2)\{y/x\} = (E_1 \space \{y/x\})(E_2 \space \{y/x\})
$$
$$ \Downarrow $$
$$
(\lambda x.E)\{y/x\} = (\lambda y.E \{y/x\})
$$
Simply put, $\lambda x$ is renamed to $\lambda y$, and because $E$ is currently unknown, we simply note the $\{y/x\}$ change along with $E$. 

## Substitutions

In $\lambda$ calculus, functions _do not_ have names. The whole function is written when it is required, but this process can be simplified with capital letters, numbers, and symbols as synonyms. 

As an example, the identity function can be represented as $I \equiv (\lambda x.x)$, and so
$$
II \equiv (\lambda x.x)(\lambda x.x)
$$
is the identity function applied to itself.