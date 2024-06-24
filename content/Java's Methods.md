```java
<access_modifier> <return_type> <name>(<parameter_data_type> <parameter_name>, . . .) {
	<body>
}
```

A _method_ in [[Java]] describes a series of steps to be performed with data. A _method_ has two main components:
- _header_
- _body_

Let's see them in action.
```java
public int addTwoNumbers(int number1, int number2) {
	return number1 + number2;
}
```

The _header_ is the first line, beginning with `public`. This line defines the constraints of the method: its _access modifier_, _return type_, _name_, and its _parameters_, in that order. Let's first discuss access modifiers.
## Access Modifier
An _access modifier_ defines the scope in which a method may be invoked (called), or modifies its implementation in the case of `abstract`. The most commonly used modifiers are:
- `public`: allows access in all scopes
- `private`: limits access to the current class's scope
- `protected`: limits access to the current class and all subclass's scope
- `static`: allows access to the method without needing to instantiate an object of its class
- `abstract`: allows defining a method header but without providing an implementation for the body



