# Kotlin Interview Questions and Answers

Quick Jump to Topics:
 > * [Basic](#basic)
 >> * [null safety](#null-safety)
 >> * [lateinit](#lateinit)
 >> * [lazy](#lazy)
 >> * [companion objects](#companion-objects)
 >> * [object](#object)
 >> * [constructors](#constructors)
 > * [Data Class](#data-class)
 > * [Sealed Class](#sealed-class)
 > * [Lambdas Expressions](#lambdas-expressions)
 > * [Higher-Order functions](#higher-order-functions)
 > * [Extension Functions](#extension-functions)
 > * [Infix Functions](#infix-functions)
 > * [Inline/No-Inline Functions](#inline/noinline-functions)
 > * [Coroutines](#coroutines)


### Basic

-   **How does Kotlin work on Android?**<br/>
    Just like Java, the Kotlin code is also compiled into the Java bytecode and is executed at runtime by the Java Virtual Machine i.e. JVM. When a Kotlin file named ```Main.kt``` is compiled then it will eventually turn into a class and then the bytecode of the class will be generated. The name of the bytecode file will be ```MainKt.class``` and this file will be executed by the JVM.

-   **Why should we use Kotlin?**<br/>
    1) <b>Kotlin is concise</b>
    2) <b>Kotlin is null-safe</b>
    3) <b>Kotlin is interoperable</b>

-   **What is the difference between the variable declaration with var and val?**<br/>
    If you want to declare some mutable(changeable) variable, then you can use var . For the immutable variable, use val i.e. val variables can't be changed once assigned.

-   **What is the difference between the variable declaration with val and const?**<br/>
    Both the variables that are declared with val and const are immutable in nature. But the value of the const variable must be known at the compile-time whereas the value of the val variable can be assigned at runtime also.
    ```kotlin
    const val companyName = "MindOrks" // this will work
    val comapanyname = "MindOrks" // this will work
    
    const val companyName = getCompanyName() // will not work
    val companyName = getCompanyName() // this will work
    
    YourClassName {
        companion object {    
        const val FILE_EXTENSION = ".png"    
        val FILENAME: String
        get() = "Img_" + System.currentTimeMillis() + FILE_EXTENSION 
        }
    }
    ```
    
    In the above example, we are declaring the const variable named FILE_EXTENSION in the companion object and the FILENAME variable as val and initialise it with custom getter.
    As the extension of the file will always be same, so it is declared as a const variable. But, the name of the file will be changed based on the logic that we use for the file name. Here, in our example, we are naming the file based on the current time. You can't give some value to it initially because the value is fetched at the runtime. So, we are using val here.
    What happens after the code compilation is that wherever the const variables are used in the code, those variables are replaced by the value of that const variable but in case of val , the variables are kept as it is because we don't know the value of val at compile-time. So, if you decompile the above code, then you will see
    
    ```kotlin
    public final String getFILENAME() {
        return "Img_" + System.currentTimeMillis() + ".png";
    }
   ```
   
   Here, you can find that the variable FILE_EXTENSION has been replaced by its value i.e. ".png" i.e. the value has been inlined and hence there is no overhead to access that variable at the runtime. This is the advantage of using const over val .

-   **How to choose between a switch and when in Kotlin?**<br/>
-   **What is the open keyword in Kotlin used for?**<br/>
-   **Do we have a ternary operator in Kotlin just like java?**<br/>
-   **How to convert a Kotlin source file to a Java source file?**<br/>
-   **What is the use of @JvmStatic, @JvmOverloads, and @JvmFiled in Kotlin?**<br/>
-   **Can we use primitive types such as int, double, float in Kotlin?**<br/>
-   **What is String Interpolation in Kotlin?**<br/>
-   **What is the equivalent of Java static methods in Kotlin?**<br/>
-   **Can we use the new keyword to instantiate a class object in Kotlin?**<br/>
-   **What are visibility modifiers in Kotlin?**<br/>

### null safety

-   **How to ensure null safety in Kotlin?**<br/>
-   **What is the difference between safe calls(?.) and null check(!!)?**<br/>
-   **What is Elvis operator in Kotlin?**<br/>


### lateinit

-   **When to use the lateinit keyword in Kotlin?**<br/>
-   **How to check if a lateinit variable has been initialized or not?**<br/>

### lazy

-   **What is the difference between lateinit and lazy in Kotlin?**<br/>


### companion objects

-   **What are companion objects in Kotlin?**<br/>

### object

-   **How to create a Singleton class in Kotlin?**<br/>

### constructors

-   **What are the types of constructors in Kotlin?**<br/>
-   **Is there any relationship between primary and secondary constructors?**<br/>
-   **What is the default type of argument used in a constructor?**<br/>
-   **What are init blocks in Kotlin?**<br/>

### Data Class

-   **What is a data class in Kotlin?**<br/>

### Sealed Class

-   **What is a data class in Kotlin?**<br/>

### Lambdas Expressions

-   **What are lambdas expressions?**<br/>

### Higher-Order Functions

-   **What are Higher-Order functions in Kotlin?**<br/>

### Extension Functions

-   **What are extension functions in Kotlin?**<br/>

### Infix Functions

-   **What is an infix function in Kotlin?**<br/>

### Inline/No-Inline Functions

-   **What is an inline function in Kotlin?**<br/>
-   **What is noinline in Kotlin?**<br/>

### Coroutines

-   **What are Coroutines in Kotlin?**<br/>
-   **What does it mean when I say "it doesn't map on the native thread"?**<br/>
-   **What is Dispatchers in Kotlin Coroutines?**<br/>
-   **What is suspend function in Kotlin Coroutines?**<br/>
-   **What is the difference between Launch and Async in Kotlin Coroutines?**<br/>
-   **What is withContext in Kotlin Coroutines?**<br/>
-   **What is runBlocking in Kotlin Coroutines?**<br/>
-   **What are scopes in Kotlin Coroutines?**<br/>
-   **How Exception Handling is done in Kotlin Coroutines?**<br/>


