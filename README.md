# Android-Interview-Questions-Answer 

I have try to make collection of interview questions-answer related to Android with java and kotlin.

## **Kotlin** :-

**1. Why should we use Kotlin (benefits over java)?**
	
	-> 1. Shorter program for the same task - It's (way) More Concise Than Java    
	-> 2. Easy Code    
	-> 3. Java Compatibility - It's Completely Interoperable With Java    
	-> 4. Eliminating Null References: - Safer Code    
	-> 5. Solution To Some Of Java’s Flaws   
	
	Features of kotlin:

	Extension function
	High order function
	Inter-operable with java
	Null safety
	Smart cast
	Default and named arguments
	Multi-value return from function
	Data class	
	
**2. How to declare a variable in Kotlin?**

	To declare a variable in Kotlin, either var or val keyword is used. Here is an example:    

	var language = "Hindi"    
	val score = 95    
	
	However, you can explicitly specify the type if you want to:    

	var language: String = "English"    
	val score: Int = 95    
	
**4. Difference Between var and val** 

	val (Immutable reference) - The variable declared using val keyword cannot be changed once the value is assigned. It is similar to final variable in Java.    
	
	var (Mutable reference) - The variable declared using var keyword can be changed later in the program. It corresponds to regular Java variable.    
	
	Here are few examples:    

	var language = "Hindi"    
	language = "English"         
	Here, language variable is reassigned to German. Since, the variable is declared using var, this code work perfectly.    

	val language = "Hindi"    
	language = "English"      // Error 
	
**5. Kotlin Basic Data Types**

	Kotlin is a statically typed language like Java. That is, the type of a variable is known during the compile time. For example,    

	val language: Int    
	val marks = 12.3    
	Here, the compiler knows that language is of type Int, and marks is of type Double before the compile time.    

	The built-in types in Kotlin can be categorized as:    

	*Numbers    
	*Characters    
	*Booleans    
	*Arrays    
	
**6. what is varang keyword in kotlin**   

	Sometimes we need a function where we can pass n number of parameters, and the value of n can be decided at runtime. 
	Kotlin provides us to achieve the same by defining a parameter of a function as vararg. We can pass n number of parameters 
	to a vararg variable of the defined datatype or even of a generic type. 	
	Example :    
	
	fun getAverage(vararg input: Int): Float {    
   		var sum = 0.0f    
    		for (item in input) {    
        		sum += item    
    		}
    		return (sum / input.size)    
	}    
	val result1 = getAverage(1, 2, 3)    
	val result2 = getAverage(1, 2, 3, 4, 5)    
	
**7. what is JvmStatic Annotation in Kotlin**

	JvmStatic Annotation is used to call kotlin method from java in kotlin style    
	Ex :- object AppUtils {    
		 @JvmStatic    
    		fun install() {    
    	}    
	Now, we can call install() method from Java as below:    
	AppUtils.install();    
}

**8. what is JvmOverloads Annotation in Kotlin**

	Kotlin support default parameters and Java support method overloading.
	
	Assume that we have a data class Session in Kotlin as below:
	data class Session(val name: String, val date: Date = Date())
	We can create the objects in Kotlin as below:
	
        val sessionOne = Session("Session One", Date())
	val sessionTwo = Session("Session Two")
	
	Both the lines of the code will compile as expected as for the 2nd object, it -will take the default value of the Date.
	
	But, when we create the objects from Java as below:

	Session sessionOne = new Session("Session One", new Date());
	Session sessionTwo = new Session("Session Two"); // compilation error
	The first line will compile, but the second line will not as we have not passed Data as a parameter. It will give us the error:
	
	As we know that Java does not support default parameters. It supports overloading.
	So, we will have to use @JvmOverloads. It instructs the Kotlin compiler to generate overloads for the function that substitute default parameter values
	
	Let's update our data class Session as below:

	data class Session @JvmOverloads constructor(val name: String, val date: Date = Date())
	Notice that we have used @JvmOverloads to instruct the Kotlin compiler to generate overloads for the function.

	Now, if we create the objects from Java as below:

	Session sessionOne = new Session("Session One", new Date());
	Session sessionTwo = new Session("Session Two");
	
	And, it works perfectly. Both the lines of the code will compile as expected as the Kotlin compiler has generated the overloads for the function.

	This is how we can use the JvmOverloads annotation in Kotlin.
	
**9. what is JvmField Annotation in Kotlin**

	Assume that we have a data class Session in Kotlin as below:
	data class Session(val name: String, val date: Date = Date())
	We can create the object and get the name in Kotlin as below:

	val session = Session("Session", Date())
	val name = session.name
	It works as expected.
	But, when we create the object and get the name from Java as below:

	Session session = new Session("Session", new Date());
	String name = session.name; // compilation error
	It will not compile. From Java, we will have to use the getter method as below:

	Session session = new Session("Session", new Date());
	String name = session.getName();
	Now, it will compile and work as expected.

	So, the question is: Can we use it without the getter method as we use in Kotlin?

	The answer is yes. By using the JvmField annotation. So, if we want a field to be used as a normal field and not as a getter or setter then we will have to tell the compiler not to generate any getter and setter for the same and expose it as a field by using the @JvmField annotation.

	Let's update our data class Session as below:

	data class Session(@JvmField val name: String, val date: Date = Date())
	Notice that we have used @JvmField over the field name to instruct the Kotlin compiler not to generate any getter and setter for the same and expose it as a field.

	Now, if we create the object and get the name from Java as below:

	Session session = new Session("Session", new Date());
	String name = session.name;
	Now, it works perfectly. It will compile as expected as the Kotlin compiler will not generate any getter and setter for the same and expose it as a field.

	This is how we can use the JvmField annotation in Kotlin.
	
**10. lateinit vs lazy in Kotlin**	
	
   #lateinit
	
	lateinit in Kotlin is useful in a scenario when we do not want to initialize a variable at the time of the declaration and want to 
	initialize it at some later point in time, but we make sure that we initialize it before use.
	
	private var mentor: Mentor? = null // this is not proper way to declare variable with null
	
	What if we do not want to make the variable nullable?
	The answer is lateinit. Like this 
	private lateinit var mentor: Mentor
	
	And later we can initialize the variable when we need it as below:
	fun bookASlot() {
		mentor = Mentor()
	}
	
	But we must take care that we initialize the variable before accessing it, or else it will throw the following exception.
	kotlin.UninitializedPropertyAccessException: lateinit property mentor has not been initialized

	In Kotlin, we also have a way to check if the lateinit variable is initialized or not.

	By using isInitialized:

	if(this::mentor.isInitialized) {
		// access mentor
	} else {
		// do something else
	}
	
	Things to consider when we use the lateinit property:
	 -Can be only used with the var keyword.
	-Can be only used with a non-nullable variable.
	-Should be used if the variable is mutable and can be initialized later.
	-Should be used if you are sure about the initialization before use.
	-This was about the lateinit property in Kotlin.
	
  #lazy

	For efficient memory management, Kotlin has introduced a new feature called as Lazy initialization. When the lazy keyword is used, 
	the object will be created only when it is called, otherwise there will be no object creation. lazy() is a function that takes a 
	lambda and returns an instance of lazy which can serve as a delegate of lazy properties upon which it has been applied. 
	It has been designed to prevent unnecessary initialization of objects.

	-Lazy can be used only with non-NULLable variables.
	-Variable can only be val. "var" is not allowed .
	-Object will be initialized only once. Thereafter, you receive the value from the cache memory.
	-The object will not be initialized until it has been used in the application.

        Example
        In this example, we will declare a lazy variable "myName" and we could see that the call to this parts of the code will happen only 
	once and when the value is initialized, it will remember the value throughout the application. Once the value is assigned using lazy 
	initialization, it cannot be reassigned .

           class Demo {
            val myName: String by lazy {
            println("Welcome to Lazy declaration");
            "www.tutorialspoint.com"
          }
       }
      
**11. Scope function in kotlin**     

	1. let function
	
	generally used to prevent a NullPointerException from occurring. The let function returns the lambda result and the context object is the it identifier
	
	fun main (){
		val name: String? = null
			name?.let{
			println(it.reversed)
			println(it.length)
		}
	}
	
	2. run function
	
	Refer to the context object by using 'this'
	The return value is 'lambda result'
	
	The special about the run function is, is a combination of with and let function
    	* If developer wants to operate on Nullable object and avoid NullPointerException then use 'run' function
	
	val person4: Person? = Person() // the Person() can be null also
    	val age: Int? = person4?.run {
	        println(name)
	        println(age)
        	age + 5
    	}	
	
	3. also function
	
	Refer to the context object by using 'it'
	The return value is 'context object'
	
	// this is helpful in which there is further code or function call
    	val numbersList: MutableList<Int> = mutableListOf(1, 2, 3)
    	val numbersList1 = numbersList.also {
        println("The numbers list is: $numbersList")

        numbersList.add(100)
        println("The numbers list is: $numbersList")

        numbersList.remove(2)
        println("The numbers list is: $numbersList")

        // instead of numbersList object we can use 'it'
    	}
    	println(numbersList1)
    	// we can use the 'also' with the custom classes too
    	val person3: Person = Person().also {
        it.name = "ADITYA SHIDLYALI"
        println(it.name)
    	}
    
   	 4. apply Function
    	
    	Refer to the context object by using 'this'
    	The return value is 'context object'
    
    	val person2: Person = Person().apply {
        this.name = "Aditya Shidlyali"
        this.age += 25
    	}
    	// we can also do it by person2.apply {}

    	5. with function
    
    	Refer to context object by using 'this'
    	The return value is 'lambda result'
    
    	val person1: Person = Person()
    	// the person1 will get the name as ADITYA and age with increment of 5
    	with(person1) {
        	// we can refer the members using "this.name" and "this.age"
        	name = "ADITYA"
        	age += 25
    	}
    	// we can also assign the value of the with function
    	val age1: Int = with(person1) {
        	age + 5
    	}
    
**12. difference between == and === in kotlin ?** 

    	Structural equality (==): It checks for equals().
    	Referential equality (===): It checks whether the two references point to the same object.
	
	In this example, we will demonstrate how these two operators ("==" and "===") work.
	
	fun main(args: Array<String>) {
   	val student1 = "Ram"
   	val student2 = "shyam"
   	val student4 = "Ram"

   	val student3=student1

   	// prints true as both pointing to the same object
   	println(student1 === student3)

   	// prints false
   	println(student1 === student2)

   	//prints true
   	println(student1 == student4)
}
    
**13. Companion object in Kotlin ?**

    	We do not have a static keyword in Kotlin.
    	In Kotlin, we can call a method of a class without creating the object of that class with the use of a companion object
    
**14. Advantage of using const in Kotlin ?**

    	For ex. we have object like this
    	object Constants {
    		const val NAME = "Amit"
    	}
	
    	As the value has been inlined, there will be no overhead to access that variable at runtime. And hence, it will lead to a better 
	performance of the application.
    
**15. Difference Between “const” and “val” in Kotlin ?**

	*Use of const in Kotlin
    
    	The const keyword is used in Kotlin whenever the variable value remains const throughout the lifecycle of an application. 
    	It means that const is applied only on immutable properties of the class. In simple words, use const to declare a read-only property of a class.

    	There are some constraints that are applied to the const variable. They are as follows −

   	const can only be applied to the immutable property of a class.

     	It cannot be assigned to any function or any class constructor. It should be assigned with a primitive data type or String.

     	The const variable will be initialized at compile-time.
	
	In the following example, we will declare a const variable and we will use the same variable in our application.
	
	const val sName = "tutorialspoint";
	// This line will throw an error as we cannot
	// use Const with any function call.
	// const val myFun = MyFunc();
	fun main() {
   		println("Example of Const-Val--->"+sName);
	}
	
	*Val Keyword
	
	In Kotlin, val is also used for declaring a variable. Both "val" and "const val" are used for declaring read-only properties of a class. 
	The variables declared as const are initialized at the runtime.

	val deals with the immutable property of a class, that is, only read-only variables can be declared using val.

	val is initialized at the runtime.

	For val, the contents can be muted, whereas for const val, the contents cannot be muted.

	Example
	We will modify the previous example in order to pass a function using val and we won't get any errors at runtime.
	
	const val sName = "tutorialspoint";

	// We can pass function using val
	val myfun=MyFunc();
	fun main() {
   		println("Example of Const-Val--->"+sName);
   		println("Example of Val--->"+myfun);
	}
	fun MyFunc(): String {
   		return "Hello Kotlin"
	}
	
**16. What are the visibility modifiers in Kotlin ?**

	There are four visibility modifiers in Kotlin: private, protected, internal, and public. The default visibility is public.
	
	![modi](https://user-images.githubusercontent.com/35212651/216007897-397197a0-fe03-4d2d-9348-afd7fbfb359a.jpg)
	
**17. What is the equivalent of Java static methods in Kotlin ?**

	class Foo {
  		companion object {
     		fun a() : Int = 1
  		}
	}
	You can then use it from inside Kotlin code as
	Foo.a();
	But from within Java code, you would need to call it as
	Foo.Companion.a();
	
**18. How to create a Singleton class in Kotlin ?**

	Singleton Class in Kotlin is also called as the Singleton Object in Kotlin. Singleton class is a class that is defined in such a 
	way that only one instance of the class can be created and used everywhere. Many times we create the two different objects of the
	same class, but we have to remember that creating two different objects also requires the allocation of two different memories for 
	the objects. So it is better to make a single object and use it again and again. 
	
	*Properties of Singleton Class
	
	The following are the properties of a typical singleton class:

	Only one instance: The singleton class has only one instance and this is done by providing an instance of the class, within the class.
	Globally accessible: The instance of the singleton class should be globally accessible so that each class can use it.
	Constructor not allowed: We can use the init method to initialize our member variables.
	
	Example : 
	object Singleton {
    		fun show() {
        		println("This is Singleton class!")
    		}
	}
	fun run() {
    		Singleton.show()
	}
	
**19. What is the difference between open and public in Kotlin ?**

	Similarly to classes, properties and functions are also final by default in Kotlin. So, if we need to override any of them, 
	we have to make them open in the parent class. Otherwise, the compiler will complain
	
	The open keyword allows classes, functions, and properties to be extended, while public is a visibility modifier that doesn’t have 
	any explicit usage since all classes, functions, and properties are publicly visible by default.
	
**20. Label Reference in Kotlin ?**

	List and array are two popular collections supported by Kotlin. By definition, both these collections allocate sequential memory location
	
	Any expression in Kotlin may be marked with a label. This can be used to as an identifier. A label can be defined in Kotlin using label 
	name followed by @ sign in front of any expression.
	
	Let see example :- 
  
	loopi@ for( i in 1..5){
     		print(i)
 	}
	
	These labels are really helpful when dealing with nested loops or nested functions.

	Will explain the use cases in detail of label references but before that, we need to understand what are jump and return expressions.

	break : Terminates the nearest enclosing loop.
	continue : Proceeds to the next step of the nearest enclosing loop.
	return : Return from the nearest enclosing function or anonymous function.
	
	Now let’s take an example of nested loop first to understand the use of label reference.
  
	for( i in 1..3){
        	for (j in 5..7){
            		print ((i * 100) + j)
            		print(" ")
        	}
        	println( i.toString() + " loop ends")
    	}
	println("We are done")
	
	The output of the above code is
 
	105 106 107 1 loop ends 
	205 206 207 2 loop ends 
	305 306 307 3 loop ends 
	We are done
	
	Now in the above example, what if I want to break the i loop (means the entire execution of loops) when i equals to 2 and j 
	equals to 6 but still want to execute below code of lines.

	Means I want the output as
  	105 106 107 1 loop ends 
	205 
	We are done
	I’ll use a break statement with if condition (i == 2 && j == 6) inside the j loop and another if condition (i == 2) after execution of j loop.
 
	for( i in 1..3){
        	for (j in 5..7){
            		if(i == 2 && j == 6) break
            		print ((i * 100) + j)
            		print(" ")
        	}
        	if(i == 2) break
        	println( i.toString() + " loop ends")
    	}
	println("We are done")
	We need to add two condition checks and break statements because the break statement only works for the nearest enclosing loop.

	What if I say there is a better way to do the same in Kotlin.
	Label the i loop and break the same loop using label reference by checking the condition inside the j loop.
  
	loopi@ for( i in 1..3){
        	for (j in 5..7){
            		if(i == 2 && j == 6) break@loopi
            		print ((i * 100) + j)
            		print(" ")
        	}       	 
        	println( i.toString() + " loop ends")
    	}
	println("We are done")

	In the above code, we labelled the outer loop as loopi and while checking the condition we break the loop using the same label. 
	And this will break the entire execution of the loops when the condition will be true.

	The same can be used with continue expression also. The continue expression also works for the nearest enclosing loop but if we want
	to continue the outer loop, we can use the label reference.
  
	loopi@ for( i in 1..3){
        	for (j in 5..7){
            		if(i == 2 && j == 6) continue@loopi
            		print ((i * 100) + j)
            		print(" ")
        	}        
        	println( i.toString() + " loop ends")
    	}
	println("We are done")

	And the output will be
  
	105 106 107 1 loop ends 
	205 
	305 306 307 3 loop ends 
	We are done
	
**21. What is an init block in Kotlin ?**

	Constructor is a block of code which get initialised when the object is created.
	class SumOfNumbers {
   		SumOfNumbers() {
   		}
	}
	In Java, the constructor has the same name as of the class. But in Kotlin we have something different for 
	constructors i.e Primary and Secondary constructors.
	class Person(name:String,age:Int) {   
	}
	
	This is an example of a Kotlin class having a primary constructor. But like java, if we have to perform some task in constructor 
	how can we do that in Kotlin? Because this is not possible in the primary constructor.

	Either we can use secondary constructor or we can use init block. Here, in this block, we will talk about the Init Block.

	Let us understand the init block with an example.

	In the above person class, we have to check if the person is older than me or not. We can do it using,

	class Person(name: String, age: Int) {
    		val isOlderThanMe = false
    		val myAge = 25
    		init {
        		isOlderThanMe = age > myAge
    		}
	}
	Here, we have initialized two variables isOlderThanMe and myAge with a default value is false and 25 respectively.

	Now, in the init block, we check the age from the primary constructor with myAge and assign the value to isOlderThanMe . i.e. if
	the age is greater than 25, value assigned will be true else false.

	To check this,

 	var person = Person("Himanshu", 26)
 	print(person.isOlderThanMe)
	This will print the desired result. As when we have initialized the Person class with passing data name as Himanshu and age as 26. 
	The init block will also get called as the object is created and the value of isOlderThanMe has been updated based on the condition.

	Points to Note:
	The init block is always called after the primary constructor
	A class file can have one or more init blocks executing in series i.e. one after another.
	
**22. Difference between Constructor and init block ?**

	The init block will execute immediately after the primary constructor. Initializer blocks effectively become part of the primary constructor.

	The constructor is the secondary constructor. Delegation to the primary constructor happens as the first statement of a 
	secondary constructor, so the code in all initializer blocks is executed before the secondary constructor body.
	
**23. What is Pair and Triple in Kotlin ?**

	In any programming language, we use functions to perform a particular activity. For eg. , if you want to add the details of students of a 
	college then instead of writing the same lines of code a number of times, you can use the concept of a function . And after that, 
	you can call that function as many times as you want. Also, the best part of the function is that a function can return some value i.e. 
	if you are having a function to add two numbers then the return value of that function can be a number of integer type having the sum of 
	both the entered numbers.

	But functions has some limitations also(when used normally). Think of a situation, where you want the name and age of a particular 
	student of a college, then if you want to use the function approach then you can return only one value at a time. If you want to return
	more than one value for different data type (in our example, name is of string type, while age is of type integer), then you have to make 
	use of dummy class where you can declare all the variables that you want to return from the function and after that make an object of the 
	class and collect the returned value in some List.

	But the problem here is that if you are having so many things to do i.e. so many functions to work on which returns more than one value 
	then you have to make a separate class for all those functions and finally use that class. This will be a very complex and lengthy approach.

	To deal with these type of situations, Kotlin introduced the concept of Pair and Triple . 
	With the help of Pair and Triple you can return more than one value(two in case of pair and three in case of the triple) of different data types.

	So, in this blog, we will learn how to use pairs and triples in Kotlin. So, let’s get started.

*pair
	
	Pair is a predefined class in Kotlin that is used to store and return two variables at a time. Those two variables can be of the same 
	type or of a different type. So, whenever you want to return more than one variable from a function then you can use Pair in your function. 
	But how to use Pair ? Let’s have a look at how to use Pair in Kotlin:

	Pair ("Hello", "Kotlin") // here both the variables are of type string
	Pair ("Kotlin", 1) // here 1st variable is of type string and other is type of integer
	Pair (2, 20) // here both the variables are of integer type
	You can use pair as described above. Also you can define some variable and then pass that variable in the Pair. Following example shows the same:

	val variable1 = "Declaring String variable"
	val variable2 = 1 // declaring integer value

	Pair (variable1, variable2) // using declared variable in Pair class
	Using first and second property
	In order to retrieve the values stored in the Pair, we can use the first and second property of the Pair class:

	val variable1 = "Declaring String variable"
	val variable2 = 1 // declaring integer value

	val variableName = Pair (variable1, variable2) // using declared variable in Pair class

	println(variableName.first) // will print the value of variable1
	println(variableName.second) // will print the value of variable2
	Also, you can assign the variables of the Pair to another variable and use those variables like below:

	val(firstVariable, secondVariable) = Pair("Hello", 1)
	println(firstVariable)
	println(secondVariable)

	Infix
	In kotlin, we can use easily destructure the variable declaration using to infix function.

	fun getWebsite() : Pair<String, String> {
  		return "www.mindorks.com" to "the Website is"
	}
	and declare the getWebsite() function as,
	val (url: String, website: String) = getWebsite()
	// print(url)
	//print(website)
	toString() function
	toString() is a function that is used to convert the variables of the pair into string and use that variables as string.
	

	val variableName = Pair (variable1, variable2) // using declared variable in Pair class
	print(variableName.toString())
	toList() function
	toList() function converts the Pair variable in form of List i.e. you can use the Pair variables just like List items.

	val variable1 = "Declaring String variable"
	val variable2 = 1 // declaring integer value

	val variableName = Pair (variable1, variable2) // using declared variable in Pair class
	val list = variableName.toList()

	println(list[0]) // this will print the value of variable1
	println(list[1]) // this will print the value of variable2
	
*Triple
	
	Triple is another predefined class in Kotlin. With the help of Triple class in Kotlin, you can return 3 variables of same or different 
	type from one function. Also, you can use Triple class to store 3 variables of same or different type.

	The use of Triple is the same as that of Pair in Kotlin. Following example shows the use of Triple in Kotlin:

	val variable1 = "Declaring String variable"
	val variable2 = 1 // declaring integer value
	val variable3 = "Declaring second string value"

	val variableName = Triple (variable1, variable2, variable3) // using declared variable in Triple class

	println(variableName.first) // will print the value of variable1
	println(variableName.second) // will print the value of variable2
	println(variableName.third) // will print the value of variable3
	Also, there are functions like toString() and toList(), that can be used in Triple also, in the same manner as used in the Pair.
	Following example shows the use of toString() and toList() in Triple:

	val variable1 = "Declaring String variable"
	val variable2 = 1 // declaring integer value
	val variable3 = "Declaring second string value"

	val variableName = Triple (variable1, variable2, variable3) // using declared variable in Triple class

	println(variableName.toString())

	val list = variableName.toList()
	println(list[0]) // prints the first element of the list or variable1
	println(list[1]) // prints the second element of the list or variable2
	println(list[2]) /

**23. Statically Type vs Dynamically Typed Languages. Kotlin is which type of language ?**

	Simply put it this way: in a statically typed language variables' types are static, meaning once you set a variable to a type,
	you cannot change it. That is because typing is associated with the variable rather than the value it refers to.

	For example in Java:
	String str = "Hello";   // variable str statically typed as string
	str = 5;                // would throw an error since str is
                       	        // supposed to be a string only
	Where on the other hand: in a dynamically typed language variables' types are dynamic, meaning after you set a variable to a type, 
	you CAN change it. That is because typing is associated with the value it assumes rather than the variable itself.

	For example in Python:
	some_str = "Hello"  # variable some_str is linked to a string value
	some_str = 5        # now it is linked to an integer value; perfectly OK
	
	**Kotlin is a statically typed language which means that it does most the check at compile time rather being dependent on runtime**
	
**24. Why Kotlin does not support primitive type ?**

	Kotlin doesn't have primitive type (I mean you cannot declare primitive directly). It uses classes like Int, Float as an object wrapper for primitives.
	
	When kotlin code is converted to jvm code, whenever possible, "primitive object" is converted to java primitive. In some cases this cannot be done. 
	Those cases are, for example, collection of "primitives". For example, List<Int> cannot contains primitive. So, compiler knows when it can 
	convert object to primitive. And, again, it's very similar to java:

	List<Integer> numbers = new ArrayList<>;

	numbers.add(0); // <-- you use primitive, but in fact, JVM will convert this primitive to object.
	numbers.add(new Integer(0)); // <-- We don't need do that.
	Also, when you declare "nullable primitive" it is never converted to primitive (what is kind of obvious, as primitive cannot be null).
	In java it works very similar:

	int k = null; // No way!
	Integer kN = null; // That's OK.
	
**25. Parameter vs Argument ?**
	
	Parameter is variable defined in function definition, while argument is actual value passed to the function.
	To understand the difference, let’s first see an example function and its usage:

	fun randomString(length: Int): String {
    		// ....
	}
	randomString(10)
	In this example length is a parameter, and 10 (used in function call) is an argument. Here are common definitions:

**26. Difference between function and method ?**

	'method' is the object-oriented word for 'function'. That's pretty much all there is to it (ie., no real difference).
	
	A function doesn’t need any object and is independent, while the method is a function, which is linked with any object.
	We can directly call the function with its name, while the method is called by the object’s name.
	Function is used to pass or return the data, while the method operates the data in a class.
	Function is an independent functionality, while the method lies under object-oriented programming.	
	In functions, we don’t need to declare the class, while to use methods we need to declare the class.
	Functions can only work with the provided data, while methods can access all the data provided in the given class.
	
**27. What is reified keyword ?**

	"reified" is a special type of keyword that helps Kotlin developers to access the information related to a class at runtime. 
	"reified" can only be used with inline functions. When "reified" keyword is used, the compiler copies the function’s bytecode 
	to every section of the code where the function has been called. In this way, the generic type T will be assigned to the 
	type of the value it gets as an argument.
	
	For this example, we have created an Inline function and we are passing a generic "reified" argument T and from the main() of Kotlin, 
	we are calling myExample() multiple times with different arguments.
	
	// Declaring Inline function
	inline fun <reified T> myExample(name: T) {
   		println("Name of your website -> "+name)
   		println("Type of myClass: ${T::class.java}")
	}
	fun main() {
   		// calling func() with String
   		myExample<String>("www.tutorialspoint.com")
   		// calling func() with Int value
   		myExample<Int>(100)
   		// calling func() with Long value
   		myExample<Long>(1L)
	}
	
	Output
	It will generate the following output −

	Name of your website -> www.tutorialspoint.com
	Type of myClass: class java.lang.String
	Name of your website -> 100
	Type of myClass: class java.lang.Integer
	Name of your website -> 1
	Type of myClass: class java.lang.Long
	
**28. What is a spread operator? What is the recommended place to use it ?**
	
	before understood spread(*) operator we have to dive into varang keyword
	
	Kotlin also supports declaring a function that can have a variable number of arguments. You can do that by prefixing parameter name 
	with the vararg modifier: fun format(format: String, vararg args: Any)

	vararg rules
	In Java, the vararg parameter has to be the last one in the parameters list — so you can only have one vararg parameter. 
	While in Kotlin, the vararg parameter doesn’t have to be the last one in the list, multiple vararg parameters are still prohibited.

	Now let’s see how the decompiled corresponding Java source code looks like when declaring vararg parameters.

	vararg param as the last one in list
	Declaring vararg param as the last one in list, in a Kotlin function, looks like this:

	fun format(format: String, vararg params: String)
	and will be compiled into the corresponding Java code:

	void format(@NotNull String format, @NotNull String... params)
	Declaring params after the vararg
	When vararg parameter is not the last one in list, like this:

	fun format(format: String, vararg params: String, encoding: String)
	it gets compiled into corresponding Java code:

	void format(String format, String[] params, String encoding)
	In conclusion, if vararg is not the last param it will be compiled as an array of parameter type.
	
	*spread operator 
	
	It’s Kotlin’s spread operator — the operator that unpacks an array into the list of values from the array. 
	It is needed when you want to pass an array as the vararg parameter.
	
	Example : 
	
	If you try to call format function defined above like this:

	val params = arrayOf("param1", "param2")
	format(output, params)
	it will fail with Type mismatch: inferred type is Array<String> but String was expected compilation error.

	To fix this, you need to use spread operator to unpack params array into the corresponding values: format(output, *params)

	Let’s see how the corresponding decompiled Java code looks like in this case:

	String[] params = new String[]{"param1", "param2"};
	format(output, (String[])Arrays.copyOf(params, params.length));
	
**29. Explain Safe call(?.),Elvis(?:), and not-null assertion-(double-bang operator)(!!) operator ?**

	the ?. safe call opeator avoid null pointer exception and check null value
	
	the !! operator will raising KotlinNullPointerException when operates on a null reference, for example:
	null!!;// raise NullPointerException
	
	The ?: elvis operator in Kotlin is used for null safety.
	x = a ?: b
	In the above code, x will be assigned the value of a if a is not null and b if a is null.
	The equivalent kotlin code without using the elvis operator is below:
	x = if(a == null) b else a

**30. Room vs Realm ? why not Realm ?

	Realm
	A relatively fast and convenient library, all links are simply implemented, which is related to the object orientation of the database. .
	Excellent documentation. Is, perhaps, one of the best option for storing data on a mobile device at the moment, the minus can only be an 
	increase in the size of the apk-file by 2.5 MB.

	Room
	An interesting solution presented on Google I / O 2017 as optimal for working with the database on Android OS. Despite the fact that 
	it is necessary to use explicit sql-requests, the library turned out to be quite convenient and I liked it personally. On performance is 
	in the lead, so I would advise you to choose this particular library. Big advantage of this is based on build-in SQLite database. 
	Since this solution, submitted by Google, it will quickly become popular, and, therefore, there will be no problems with finding solutions 
	to problems that occur along with it.

	Realm uses more RAM and increases the apk size, build time. So I prefer Room.
	





