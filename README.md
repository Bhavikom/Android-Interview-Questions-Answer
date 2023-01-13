# Android-Interview-Questions-Answer 

I have try to make collection of interview questions-answer related to Android with java and kotlin.

## **Kotlin** :-

1. Why should we use Kotlin (benefits over java	)?
	
	-> 1. Shorter program for the same task - It's (way) More Concise Than Java    
	-> 2. Easy Code    
	-> 3. Java Compatibility - It's Completely Interoperable With Java    
	-> 4. Eliminating Null References: - Safer Code    
	-> 5. Solution To Some Of Java’s Flaws   
	
2. How to declare a variable in Kotlin?

	To declare a variable in Kotlin, either var or val keyword is used. Here is an example:    

	var language = "Hindi"    
	val score = 95    
	
	However, you can explicitly specify the type if you want to:    

	var language: String = "English"    
	val score: Int = 95    
	
4. Difference Between var and val    

	val (Immutable reference) - The variable declared using val keyword cannot be changed once the value is assigned. It is similar to final variable in Java.    
	
	var (Mutable reference) - The variable declared using var keyword can be changed later in the program. It corresponds to regular Java variable.    
	
	Here are few examples:    

	var language = "Hindi"    
	language = "English"         
	Here, language variable is reassigned to German. Since, the variable is declared using var, this code work perfectly.    

	val language = "Hindi"    
	language = "English"      // Error 
	
5. Kotlin Basic Data Types

	Kotlin is a statically typed language like Java. That is, the type of a variable is known during the compile time. For example,    

	val language: Int    
	val marks = 12.3    
	Here, the compiler knows that language is of type Int, and marks is of type Double before the compile time.    

	The built-in types in Kotlin can be categorized as:    

	*Numbers    
	*Characters    
	*Booleans    
	*Arrays    
	
6. what is varang keyword in kotlin    

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


