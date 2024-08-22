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
    1) Kotlin is concise
    2) Kotlin is null-safe
    3) Kotlin is interoperable

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
    
    In the above example, we are declaring the ```const``` variable named ```FILE_EXTENSION``` in the companion object and the ```FILENAME``` variable as ```val``` and initialise it with custom getter.
    As the extension of the file will always be same, so it is declared as a const variable. But, the name of the file will be changed based on the logic that we use for the file name. Here, in our example, we are naming the file based on the current time. You can't give some value to it initially because the value is fetched at the runtime. So, we are using ```val``` here.
    What happens after the code compilation is that wherever the ```const``` variables are used in the code, those variables are replaced by the value of that ```const``` variable but in case of ```val``` , the variables are kept as it is because we don't know the value of ```val``` at compile-time. So, if you decompile the above code, then you will see
    
    ```kotlin
    public final String getFILENAME() {
        return "Img_" + System.currentTimeMillis() + ".png";
    }
    ```
    Here, you can find that the variable ```FILE_EXTENSION``` has been replaced by its value i.e. "```.png```" i.e. the value has been inlined and hence there is no overhead to access that variable at the runtime. This is the advantage of using ```const``` over ```val``` .

-   **How to choose between a switch and when in Kotlin?**<br/>
    One of the major advantages of using Kotlin is null safety. In Java, if you access some null variable then you will get a NullPointerException . So, the following code in Kotlin will produce a compile-time error:
    ```kotlin
    var name: String = "MindOrks"
    name = null //error
    ```
    
    So, to assign null values to a variable, you need to declare the name variable as a nullable string and then during the access of this variable, you need to use a safe call operator i.e. ?.
    ```kotlin
    var name: String? = "MindOrks"
    print(name?.length) // ok
    name = null // ok
    ```

-   **What is the open keyword in Kotlin used for?**<br/>
    By default, the classes and functions are final in Kotlin. So, you can't inherit the class or override the functions. To do so, you need to use the open keyword before the class and function. For example:

-   **Do we have a ternary operator in Kotlin just like java?**<br/>
    No, we don't have a ternary operator in Kotlin but you can use the functionality of ternary operator by using if-else or Elvis operator.

-   **How to convert a Kotlin source file to a Java source file?**<br/>
    Steps to convert your Kotlin source file to Java source file:
    
    1) Open your Kotlin project in the IntelliJ IDEA / Android Studio.
    2) Then navigate to Tools > Kotlin > Show Kotlin Bytecode.
    3) Now click on the Decompile button to get your Java code from the bytecode.

-   **What is the use of @JvmStatic, @JvmOverloads, and @JvmFiled in Kotlin?**<br/>
    1) <b>@JvmStatic:</b> This annotation is used to tell the compiler that the method is a static method and can be used in Java code.
    2) <b>@JvmOverloads:</b> To use the default values passed as an argument in Kotlin code from the Java code, we need to use the @JvmOverloads annotation.
    3) <b>@JvmField:</b> To access the fields of a Kotlin class from Java code without using any getters and setters, we need to use the @JvmField in the Kotlin code.

-   **Can we use primitive types such as int, double, float in Kotlin?**<br/>
    In Kotlin, we can't use primitive types directly. We can use classes like Int, Double, etc. as an object wrapper for primitives. But the compiled bytecode has these primitive types.

-   **What is String Interpolation in Kotlin?**<br/>
    If you want to use some variable or perform some operation inside a string then String Interpolation can be used. You can use the $ sign to use some variable in the string or can perform some operation in between ```{}``` sign.
    
    ```kotlin
    var name = "MindOrks"
    print("Hello! I am learning from $name")
    ```

-   **What is the equivalent of Java static methods in Kotlin?**<br/>
    To achieve the functionality similar to Java static methods in Kotlin, we can use:
    1)companion object
    2)package-level function
    3)object

-   **Can we use the new keyword to instantiate a class object in Kotlin?**<br/>
    No, in Kotlin we don't have to use the new keyword to instantiate a class object. To instantiate a class object, simply we use:
    ```kotlin
    var varName = ClassName()
    ```

-   **What are visibility modifiers in Kotlin?**<br/>
    A visibility modifier or access specifier or access modifier is a concept that is used to define the scope of something in a programming language. In Kotlin, we have four visibility modifiers:

    1)private: visible inside that particular class or file containing the declaration.
    2)protected: visible inside that particular class or file and also in the subclass of that particular class where it is declared.
    3)internal: visible everywhere in that particular module.
    4)public: visible to everyone.

    Note: By default, the visibility modifier in Kotlin is public .

### null safety

-   **How to ensure null safety in Kotlin?**<br/>
    One of the major advantages of using Kotlin is null safety. In Java, if you access some null variable then you will get a NullPointerException . So, the following code in Kotlin will produce a compile-time error:

    ```kotlin
        var name: String = "MindOrks"
        name = null //error

        So, to assign null values to a variable, you need to declare the name variable as a nullable string and then during the access of this variable, you need to use a safe call operator i.e. ?.
        var name: String? = "MindOrks"
        print(name?.length) // ok
        name = null // ok
    ```

-   **What is the difference between safe calls(?.) and null check(!!)?**<br/>
    Safe call operator i.e. ```?.``` is used to check if the value of the variable is null or not. If it is null then null will be returned otherwise it will return the desired value.

    ```kotlin
    var name: String? = "MindOrks"
    println(name?.length) // 8
    name = null
    println(name?.length) // null
    ```

    If you want to throw NullPointerException when the value of the variable is null, then you can use the null check or ```!!```operator.

    ```kotlin
    var name: String? = "MindOrks"
    println(name?.length) // 8
    name = null
    println(name!!.length) // KotlinNullPointerException
    ```

-   **What is Elvis operator in Kotlin?**<br/>
    In Kotlin, you can assign null values to a variable by using the null safety property. To check if a value is having null value then you can use if-else or can use the Elvis operator i.e. ```?:``` For example:

    ```kotlin
    var name:String? = "Mindorks"
    val nameLength = name?.length ?: -1
    println(nameLength)
    ```

    The Elvis operator( ```?:``` ) used above will return the length of name if the value is not null otherwise if the value is null, then it will return -1 .


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


