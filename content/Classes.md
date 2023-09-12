A _class_ in [[Object Oriented Programming (OOP)|object-oriented programming]] is a collection of data and methods to act on said data.

Let's consider a basic [[Classes|class]] called `Mechanical Pencil`:
```java
public class MechanicalPencil{
	private String color;
	private double leadSize;
	private double springWeight;

	public MechanicalPencil(){
	}

	public MechanicalPencil(String color, double leadSize, double springWeight){
		this.color = color;
		this.leadSize = leadSize;
		this.springWeight = springWeight;
	}

	public void setColor(String color){
		this.color = color;	
	}

	public void setLeadSize(double leadSize){
		this.leadSize = leadSize;
	}

	public void setSpringWeight(double springWeight){
		this.springWeight = springWeight;
	}

	public String getColor(){
		return this.color;
	}

	public double getLeadSize(){
		return this.leadSize;
	}

	public double getSpringWeight(){
		return this.springWeight;
	}
}
```

Classes, like above, allow us to represent entities with code in a cohesive manner. To come up with the `MechanicalPencil` class, I asked myself, "What properties make up a mechanical pencil?" Those properties are the `instance variables`. `Instance variables` describe the state of an object; they tell you what makes up a given object. In this case, we have:
- `private String color;`
- `private double leadSize;`
- `private double springWeight;`

Each variable declaration consists of an `access modifier`, a `data type`, and a `variable name`. For now, let's just look at the `variable names`. These names can be anything, and thus we use them to identify the most important parts of the object/entity we are trying to represent. It is important to remember, variables _you_ define mean nothing to the compiler until _you_ assign a value to them. 

I chose `color`, `leadSize`, and `springWeight` because they are the basic components of a mechanical pencil, as far as I'm concerned. You can choose to model an object in any way that fits your requirements. Java doesn't consider `MechanicalPencil` a physical mechanical pencil, it considers it as a collection of data (`instance variables`) and the ways to manipulate that data. Because of this abstractness, it's possible to represent just about anything in [[Object Oriented Programming (OOP)|OOP]].

The compiler can't just be handed a bunch of text or numbers and be left to figure out what to do with it. We need to let Java know what to expect when we tell it the pencil is blue. This is accomplished through the use of `data types`, written immediately to the left of the variable name. In the case of `MechanicalPencil`, we told the compiler that `color` is a `String`, `leadSize` is a `double`, and `springWeight` is also a `double`. 

Now that Java knows what to call our variables and how to store them, it needs to know who gets access to them. Three `access modifiers` exist:
- `private`
- `public`
- `protected`

Because multiple objects of the same class can exist at once, we want to make sure that the color of one `MechanicalPencil` doesn't get mixed up with another `MechanicalPencil`. In fact, we don't want anything to interact with the color of a given pencil unless we specifically call for it. This is accomplished in two parts. The first is using the `private` `access modifier`. This "hides" the `instance variable` from every piece of code _except_ for its own classes `methods`. The second part is accomplished by writing `methods` to interact with `instance variables` in predefined ways. We don't want someone to change the `color` of the `MechanicalPencil` in a way that breaks something else about the object. 

Speaking of methods, it's about time we look at the rest of the code. Let's focus on these first few lines first:
```java
// trim
	public MechanicalPencil(){
	}

	public MechanicalPencil(String color, double leadSize, double springWeight){
		this.color = color;
		this.leadSize = leadSize;
		this.springWeight = springWeight;
	}
// trim
```
These are our `constructors`. `Constructors` allow us to create object instances of our `MechanicalPencil` class. The first `constructor`, `public MechanicalPencil(){}`, doesn't accept any parameters; if it did, they would go in the parentheses. When default constructors like this are called, you can think of it as a blank object. Until we actually define the `color`, `leadSize`, and `springWeight`, they will sit as empty values. They are also `public`, meaning they can be access outside of our class. This makes sense, we want to make `MechanicalPencils` in more than one place.

The second constructor allows us to create a `MechanicalPencil` _and_ define it's `instance variables` all at once. Let's say we want a pencil that's purple, uses 0.5 lead, and has a spring weight of 6:
```java
MechanicalPencil myPencil = new MechanicalPencil("purple", 0.5, 6);
```
On the right hand side of the `=`, we see our `constructor`. We don't need to type out what each variable is called, we just need be make sure that our parameters are passed in the same order the `constructor` is expecting. On the left hand side, we have `MechanicalPencil myPencil`. At first glance, you may not realize that this is a simple variable declaration. We have our `data type`, `MechanicalPencil`, and our variable name, `myPencil`. Remember, we need to tell Java what to expect when we assign `myPencil` to a value. In this case, we are setting `myPencil` to a new `MechanicalPencil` object. Thus, we define it's `data type` as `MechanicalPencil`. Now, Java knows how to handle our new variable.

Let's move along to our methods. Consider:
```java
// trim
	public void setColor(String color){
		this.color = color;	
	}

	public void setLeadSize(double leadSize){
		this.leadSize = leadSize;
	}

	public void setSpringWeight(double springWeight){
		this.springWeight = springWeight;
	}

	public String getColor(){
		return this.color;
	}

	public double getLeadSize(){
		return this.leadSize;
	}

	public double getSpringWeight(){
		return this.springWeight;
	}
// trim
```
`Methods` are similar to `constructors`. They're `public`, so that we can use them outside of this file, and sometimes they accept parameters. There are two major differences:
- Each `method` has a `data type`
- `Methods` are written in camel case

The `data type` of a given method depends entirely on the purpose of said function. There are two major purpose categories: `accessors` and `mutators` (or `getters` and `setters`, if you'd like). `Accessors` allow us to get the current value of an `instance variable`, its state. Because they `return` a value, we need to tell Java, yet again, what to expect. If we want to know the `color` of a given `MechanicalPencil`, the compiler should expect a `String` in return, a `double` for `leadSize`, and a `double` for `springWeight`. Again, they are `public` so that we can use them outside of this class file. 

An important note: you may notice that the `accessors` use `this.` in their `return` statement. `this.` points to the `instance variable` of that name. Imagine that you're holding a mechanical pencil and someone asks you "what color is your mechanical pencil?" You reply "this is purple." `this.color` is purple. Using this shorthand also lets you be _lazy_, if you will, with your parameter variables. Instead of having to say:
```java
public void setColor(String newColor){
	this.color = newColor;
```
I can just say:
```java
public void setColor(String color){
	this.color = color;
}
```
So the assignment statement can be read as follows, "_this_ color is the passed color." And because we don't need a value to be returned from our `mutators`, we set their `return type` to `void`, telling Java to expect nothing.