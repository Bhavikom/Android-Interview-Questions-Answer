# Android-Interview-Questions-Answer 

I have try to make collection of interview questions-answer related to Android with java and kotlin.

## **Kotlin** :-

**1. Why should we use Kotlin (benefits over java)?**
	
	-> 1. Shorter program for the same task - It's (way) More Concise Than Java    
	-> 2. Easy Code    
	-> 3. Java Compatibility - It's Completely Interoperable With Java    
	-> 4. Eliminating Null References: - Safer Code    
	-> 5. Solution To Some Of Java’s Flaws   
	
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

	Sometimes we need a function where we can pass n number of parameters, and the value of n can be decided at runtime. Kotlin provides us to achieve the same by 		defining a parameter of a function as vararg. We can pass n number of parameters to a vararg variable of the defined datatype or even of a generic type. 	
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
	
	lateinit in Kotlin is useful in a scenario when we do not want to initialize a variable at the time of the declaration and want to initialize it at some later point in time, but we make sure that we initialize it before use.
	
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

	For efficient memory management, Kotlin has introduced a new feature called as Lazy initialization. When the lazy keyword is used, the object will be created only when it is called, otherwise there will be no object creation. lazy() is a function that takes a lambda and returns an instance of lazy which can serve as a delegate of lazy properties upon which it has been applied. It has been designed to prevent unnecessary initialization of objects.

	-Lazy can be used only with non-NULLable variables.
	-Variable can only be val. "var" is not allowed .
	-Object will be initialized only once. Thereafter, you receive the value from the cache memory.
	-The object will not be initialized until it has been used in the application.

        Example
        In this example, we will declare a lazy variable "myName" and we could see that the call to this parts of the code will happen only once and when the value is 	       initialized, it will remember the value throughout the application. Once the value is assigned using lazy initialization, it cannot be reassigned .

           class Demo {
            val myName: String by lazy {
            println("Welcome to Lazy declaration");
            "www.tutorialspoint.com"
          }
       }
      
**9. Scope function in kotlin**     

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
