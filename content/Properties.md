_Properties_ in [[CSharp|c#]] bundle instance variables and methods together in a single call. They include a private `backing field` by default, and can also provide an `accessor` and `mutator`. Consider the following:
```csharp
namespace proj {
	class PropertiesEx {
		private string name;
		
		public PropertiesEx(){}
		
		public PropertiesEx(string name){
			this.name = name;
		}
			
		public void setName(string name){
			this.name = name;
		}
			
		public string getName(){
			return this.name;
		}
	}
}
```
In the above code we have:
- an **instance variable**, `name`
- two **constructors**, `PropertiesEx()` and `PropertiesEx(string name)`
- a **setter**, `setName(string name)`
- and a **getter**, `getName()`

These components are the barebones of a class in [[CSharp|c#]]. Properties allow us to simplify this code significantly. The following example achieves the same functionality as the above example, but with far less code:
```csharp
namespace proj {
	class PropertiesEx2{
		public string Name { get; set; }
			
		public PropertiesEx2(){}
		
		public PropertiesEx2(string name){
			Name = name;
		}
	}
}
```

Properties make use of the same terminology that we're already using, but now with far more power. Notice what our **instance variable** `name` has become: 
```csharp
public string Name { get; set; }
```

You may first notice that the 'N' is capital in our **property**. This is the standard naming convention of **properties** in c#, but it does not affect functionality. 

Next, you will notice that instead of terminating with a `;` after `Name`, we have placed two key words in `{}`. These are our methods. C# does the heavy lifting here and does a couple of things in the background. First, when we declare a **property** without explicitly declaring the **backing field**, the compiler declares it for us. Automatically, a variable `name` is created, of type `string`, with an **access modifier** of `private`. To explicitly declare the **backing field**, declare your **instance variable** _(in camel case)_, and write the corresponding explicit logic in the **property**:
```csharp
namespace proj {
	class PropertiesEx3{
		private string name;
		
		public string Name { 
			get { return name;}
			set { name = value; }
		}
			
		public PropertiesEx3(){}
		
		public PropertiesEx3(string name){
			Name = name;
		}
	}
}
```
It is important to understand that the explicit and implicit declarations are equivalent, _until_ other logic is introduced. 

Now that we know how to write **properties**, let's take a look at how to use them. With traditional **setters** and **getters**, the syntax is:
```csharp
SomeObject.someMethod(maybeSomeParamiter);
```
In our previous examples, if we wanted to get and set the `name`, it would look like this:
```csharp
PropertiesEx p1 = new PropertiesEx("Jack");
Console.WriteLine(p1.getName());
p1.setName("Jack 2, the Electric Boogaloo");
Console.WriteLine(p1.getName());
```
And we would receive the following:
```txt
Jack
Jack 2, the Electric Boogaloo
```
When we use **properties**, they look like **fields** _(instance variables)_, but act like **methods**. Here is how we recreate the previous example _(using implicit declaration of our instance variable)_:
```csharp
PropertiesEx2 p2 = new PropertiesEx2("Jack");
Console.WriteLine(p2.Name);
p2.Name = "Jack 2, the Electric Boogaloo";
Console.WriteLine(p2.Name);
```
And our output:
```txt
Jack
Jack 2, the Electric Boogaloo
```
Allow me to highlight the differences:
```csharp 
// The method way:
p1.getName()
p1.setName("Jack 2, the Electric Boogaloo");

// The property way:
p2.Name
p2.Name = "Jack 2, the Electric Boogaloo";
```
As you can see, they _look_ like variables because they don't have the `()` suffix, but they _act_ like methods. **Properties** use the context of their environment to determine whether or not a **set** or **get**. We have achieved equal functionality, but with fewer _(and arguably more readable)_ lines code.