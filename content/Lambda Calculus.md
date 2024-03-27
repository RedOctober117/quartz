# Fundamentals

$$
\lambda 
$$
$\lambda$ calculus "can be called the smallest universal programming language of the world" ([source](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf)). It consists of a single transformation rule and a single function definition scheme. Expressions and names comprise the foundation of $\lambda$ calculus.

$$
\begin{aligned}
expression := name | function | application \\
function := \lambda \space name.expression \\
application := (expression)(expression) \\
\end{aligned}
$$

Expressions can be enclosed in parenthesis for clarity, such that:
$$
E = (E)
$$
The convention is to evaluate expressions left to right:
$$
E_1E_2E_3...E_n
$$
is evaluated as:
$$
(...((E_1E_2)E_3)...E_n)
$$
This is the same principle that the post script notation uses.
## Functions

$\lambda$ expressions have a single identifier, $\lambda$, and look as follows:
$$
\lambda x.x
$$
The name after $\lambda$ is the parameter $x$ for the body $x$. This is the identity function, as we will soon see.

An $application$ is one expression applied to another, like so:
$$
(\lambda x.x)y
$$
Here, we applied the expression $y$ to the expression $(\lambda x.x)$. When doing so, we substitute the free variable $y$ for each occurrence of the bound variable $x$:
$$
(\lambda x.x)y = [y/x]x = y
$$

Left of the first equals, we have the application. Next, we have $[y/x]$, meaning substitute $y$ for all occurrences of $x$ in the body of $\lambda x.x$. Because the body is comprised entirely of $x$, only one substitution takes place. Thus, $y$ is returned as the result of $(\lambda x.x)y$.

Names do not have any functional purpose other than to distinguish one variable from another. For example:
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
(\lambda x.xy)(\lambda y.y)
$$
This application first computes the identity of $y$, and passes that value into $(\lambda x.xy)$, where it is substituted for $x$, thus resulting in the function $(\lambda y.y)$. 

??????????????????? ^^
## Substitutions

In $\lambda$ calculus, functions _do not_ have names. The whole function is written when it is required, but this process can be simplified with capital letters, numbers, and symbols as synonyms. 

As an example, the identity function can be represented as $I \equiv (\lambda x.x)$, and so
$$
II \equiv (\lambda x.x)(\lambda x.x)
$$
is the identity function applied to itself.