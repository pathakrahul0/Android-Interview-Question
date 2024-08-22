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
 > * [Scoped Functions](#scoped-functions)
 > * [Infix Functions](#infix-functions)
 > * [Inline Functions](#Inline-Functions)
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
    const val companyName = "ExampleVariable" // this will work
    val comapanyname = "ExampleVariable" // this will work
    
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
    var name: String = "ExampleVariable"
    name = null //error
    ```
    
    So, to assign null values to a variable, you need to declare the name variable as a nullable string and then during the access of this variable, you need to use a safe call operator i.e. ?.
   
    ```kotlin
    var name: String? = "ExampleVariable"
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
    var name = "ExampleVariable"
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

-   **Is there any difference between == operator and === operator?**<br/>
    Yes. The == operator is used to compare the values stored in variables and the === operator is used to check if the reference of the variables are equal or not. But in the case of primitive types, the === operator also checks for the value and not reference.

    ```kotlin
    // primitive example
    val int1 = 10 
    val int2 = 10
    println(int1 == int2) // true
    println(int1 === int2) // true
    // wrapper example
    val num1 = Integer(10)
    val num2 = Integer(10)
    println(num1 == num2) // true
    println(num1 === num2) //false
    ```

-   **Is there any difference between == operator and === operator?**<br/>
    In Kotlin, to use the functionality of a for-each loop just like in Java, we use a forEach function. The following is an example of the same:
   
    ```kotlin
    var listOfExampleVariable = listOf("ExampleVariable.com", "blog.ExampleVariable.com", "afteracademy.com")
    listOfExampleVariable.forEach {
        Log.d(TAG,it)
    }
    ```

### null safety

-   **How to ensure null safety in Kotlin?**<br/>
    One of the major advantages of using Kotlin is null safety. In Java, if you access some null variable then you will get a NullPointerException . So, the following code in Kotlin will produce a compile-time error:

    ```kotlin
    var name: String = "ExampleVariable"
    name = null //error
    ```

    So, to assign null values to a variable, you need to declare the name variable as a nullable string and then during the access of this variable, you need to use a safe call operator i.e. ?.
    
    ```kotlin
    var name: String? = "ExampleVariable"
    print(name?.length) // ok
    name = null // ok
    ```

-   **What is the difference between safe calls(?.) and null check(!!)?**<br/>
    Safe call operator i.e. ```?.``` is used to check if the value of the variable is null or not. If it is null then null will be returned otherwise it will return the desired value.

    ```kotlin
    var name: String? = "ExampleVariable"
    println(name?.length) // 8
    name = null
    println(name?.length) // null
    ```

    If you want to throw NullPointerException when the value of the variable is null, then you can use the null check or ```!!```operator.

    ```kotlin
    var name: String? = "ExampleVariable"
    println(name?.length) // 8
    name = null
    println(name!!.length) // KotlinNullPointerException
    ```

-   **What is Elvis operator in Kotlin?**<br/>
    In Kotlin, you can assign null values to a variable by using the null safety property. To check if a value is having null value then you can use if-else or can use the Elvis operator i.e. ```?:``` For example:

    ```kotlin
    var name:String? = "ExampleVariable"
    val nameLength = name?.length ?: -1
    println(nameLength)
    ```

    The Elvis operator(```?:```) used above will return the length of name if the value is not null otherwise if the value is null, then it will return -1 .

### lateinit

-   **When to use the lateinit keyword in Kotlin?**<br/>
    ```lateinit``` is late initialization. Normally, properties declared as having a non-null type must be initialized in the constructor. However, fairly often this is not convenient.
    
    ```lateinit``` in Kotlin is useful in a scenario when we do not want to initialize a variable at the time of the declaration and want to initialize it at some later point in time, but we make sure that we initialize it before use.
    
    One way(that is not a good way) to achieve this is by creating a ```nullable``` variable as below:
    
    ```koltin
    private var mentor: Mentor? = null
    ```
    
    And as we all know that there is always a better way in Kotlin to achieve what we need.
    
    What if we do not want to make the variable ```nullable```?
    The answer is ```lateinit```.
    Let's update our code:
    
    ```kotlin
    private lateinit var mentor: Mentor
    ```
    Here, we can notice that the ```lateinit``` keyword and also the variable is ```non-nullable```.
    
    Things to consider when we use the ```lateinit``` property:
    
    1) Can be only used with the var keyword.
    2) Can be only used with a non-nullable variable.
    3) Should be used if the variable is mutable and can be initialized later.
    4) Should be used if you are sure about the initialization before use.
    
    For example, properties can be initialized through dependency injection, or in the setup method of a unit test. In this case, you cannot supply a non-null initializer in the constructor, but you still want to avoid null checks when referencing the property inside the body of a class. To handle this case, you can mark the property with the lateinit modifier.

-   **How to check if a lateinit variable has been initialized or not?**<br/>
    You can check if the lateinit variable has been initialized or not before using it with the help of isInitialized method. This method will return true if the lateinit property has been initialized otherwise it will return false. For example:

    ```kotlin
    class Person {
        lateinit var name: String
        fun initializeName() {
            println(this::name.isInitialized)
            name = "ExampleVariable" // initializing name
            println(this::name.isInitialized)
        }
    }
    fun main(args: Array<String>) {
        Person().initializeName()
    }
    ```

    The above function will return the following:

    ```false```</br>
    ```true```


### lazy

-   **What is the difference between lateinit and lazy in Kotlin?**<br/>
    Things to consider when we use the ```lateinit``` property:
   
    1) Can be only used with the var keyword.
    2) Can be only used with a non-nullable variable.
    3) Should be used if the variable is mutable and can be initialized later.
    4) Should be used if you are sure about the initialization before use.
    
    Things to consider when we use the lazy property:
    1) Can be only used with the val keyword, hence read-only property.
    2) We want the variable to be initialized only if we need it for the first time.
    3) Must understand that it only creates the object when we access it for the very first time and
    then in the subsequent access, it returns the same object.

    ```kotlin
    class Session {
        private val mentor: Mentor by lazy { Mentor() }
    }
    ```

    Suppose Mentor is an expensive object. And Session is the object that is dependent on the Mentor object. If Mentor object creation takes time, it will delay the creation of Session object. So, this is where the lazy keyword in Kotlin will help us.


### companion objects

-   **What are companion objects in Kotlin?**<br/>
    In Kotlin, if you want to write a function or any member of the class that can be called without having the instance of the class then you can write the same as a member of a companion object inside the class.

    To create a companion object, you need to add the companion keyword in front of the object declaration.
    
    The following is an example of a companion object in Kotlin:

    ```koltin
    class ToBeCalled {
        companion object Test {
            fun callMe() = println("You are calling me :)")
        }
    }
    fun main(args: Array<String>) {
        ToBeCalled.callMe()
    }
    ```

### object

-   **How to create a Singleton class in Kotlin?**<br/>
    A singleton class is a class that is defined in such a way that only one instance of the class can be created and is used where we need only one instance of the class like in logging, database connections, etc.
    
    To create a Singleton class in Kotlin, you need to use the object keyword.
    
    ```kotlin
    object AnySingletonClassName
    ```

    Note: You can't use constructor in object, but you can use init.

-   **Companion object vs Object in Kotlin?**<br/>
    <b>Declaration:</b></br>
        1) <b>companion object:</b> It is declared inside a class and is used to define properties and methods that belong to the class itself, rather than to instances of the class. The companion object is defined using the companion keyword.</br>

        <b>object:</b> It is declared outside of any class and is used to define a standalone singleton object. The object keyword is used to declare and define the object.</br>
    <b>Accessibility:</b></br>
        2) <b>companion object:</b> The properties and methods defined inside a companion object can be accessed using the class name, similar to accessing static members in Java. They are visible and accessible within the class.</br>

        <b>object:</b> The properties and methods defined inside an object can be accessed directly using the object's name. They are globally accessible, similar to a top-level function or property.</br>
    <b>Inheritance and Interfaces:</b></br>
        3) <b>companion object:</b> A companion object can implement interfaces and inherit from other classes. It can also be accessed through the class it is defined in.</br>

        <b>object:</b> An object cannot inherit from a class or implement interfaces. It is a standalone singleton and cannot be accessed through any class.</br>
    <b>Naming:</b></br>
        4) <b>companion object:</b> A class can have only one companion object, and it does not have a separate name. It is always called a companion.</br>
        
        <b>object:</b> Each object has a unique name and can be referred to using that name.</br>

### constructors

-   **What are the types of constructors in Kotlin?**<br/>
    1) <b>Primary constructor:</b> These constructors are defined in the class header and you can't perform some operation in it, unlike Java's constructor.
    2) <b>Secondary constructor:</b> These constructors are declared inside the class body by using the constructor keyword. You must call the primary constructor from the secondary constructor explicitly. Also, the property of the class can’t be declared inside the secondary constructor. There can be more than one secondary constructors in Kotlin.

-   **Is there any relationship between primary and secondary constructors?**<br/>
    Yes, when using a secondary constructor, you need to call the primary constructor explicitly.

-   **What is the default type of argument used in a constructor?**<br/>
    By default, the type of arguments of a constructor in val. But you can change it to var explicitly.

-   **Default arguments vs Named arguments**<br/>
    <b>Default arguments</b> allow you to specify a default value for a function parameter. This means that if the parameter is not explicitly passed in when the function is called, it will use the default value instead.

    Here’s an example:

    ```kotlin
    fun greet(name: String = "World") {
        println("Hello, $name!")
    }

    // Call with argument
    greet("John") // Output: Hello, John!

    // Call without argument
    greet() // Output: Hello, World!
    ```

    <b>Named arguments</b> in Kotlin to allow you to pass arguments to a function by name, rather than by position. This can be useful when calling functions that have many parameters, or when you want to make the code more readable. 

    Here’s an example:

    ```kotlin
    fun printName(firstName: String, lastName: String) {
        println("First name: $firstName, Last name: $lastName")
    }

    // Call with named arguments
    printName(lastName = "Doe", firstName = "John") // Output: First name: John, Last name: Doe
    ```
        
-   **What are init blocks in Kotlin?**<br/>
    ```init``` blocks are initializer blocks that are executed just after the execution of the primary constructor. A class file can have one or more init blocks that will be executed in series. If you want to perform some operation in the primary constructor, then it is not possible in Kotlin, for that, you need to use the init block.

### Data Class

-   **What is a data class in Kotlin?**<br/>
    Data classes are those classes which are made just to store some data. In Kotlin, it is marked as data. The following is an example of the same:
    
    ```kotlin
    data class Developer(val name: String, val age: Int)
    ```
    When we mark a class as a data class, you don’t have to implement or create the following functions like we do in Java: hashCode() , equals() , toString() , copy() . The compiler automatically creates these internally, so it also leads to clean code. Although, there are few other requirements that data classes need to fulfill.
    
    Although, there are few requirements that data classes need to fulfill:
    1) The primary constructor needs to have at least one parameter.
    2) All primary constructor parameters need to be marked as val or var
    3) Data classes cannot be abstract, open, sealed, or inner.


### Sealed Class

-   **What is a data class in Kotlin?**<br/>

### Lambdas Expressions

-   **What are lambdas expressions?**<br/>
    Lambdas expressions are anonymous functions that can be treated as values i.e. we can pass the lambdas expressions as arguments to a function return them, or do any other thing we could do with a normal object. For example:

    ```kotlin
    val add : (Int, Int) -> Int = { a, b -> a + b }
    val result = add(9, 10)
    ```

### Higher-Order Functions

-   **What are Higher-Order functions in Kotlin?**<br/>
    A higher-order function is a function that takes functions as parameters or returns a function. For example, A function can take functions as parameters.

    ```kotlin
    fun passMeFunction(abc: () -> Unit) {
        // I can take function
        // do something here
        // execute the function
        abc()
    }
    ```

    For example, A function can return another function.

    ```kotlin
    fun add(a: Int, b: Int): Int {
        return a + b
    }
    ```

    And, we have a function returnMeAddFunction which takes zero parameters and returns a function of the type ((Int, Int) -> Int) .

    ```kotlin
    fun returnMeAddFunction(): ((Int, Int) -> Int) {
        // can do something and return function as well
        // returning function
        return ::add
    }
    ```

    And to call the above function, we can do:

    ```kotlin
    val add = returnMeAddFunction()
    val result = add(2, 2)
    ```

### Extension Functions

-   **What are extension functions in Kotlin?**<br/>
    Extension functions are like extensive properties attached to any class in Kotlin. By using extension functions, you can add some methods or functionalities to an existing class even without inheriting the class. For example: Let's say, we have views where we need to play with the visibility of the views. So, we can create an extension function for views like,
    
    ```kotlin
    fun View.show() {
        this.visibility = View.VISIBLE
    }
    ```
    ```kotlin
    fun View.hide() {
        this.visibility = View.GONE
    }
    ```

    and to use it we use, like,
    ```kotlin
    toolbar.hide()
    ```


### Scoped Functions

-   **What are Scoped Functions in Kotlin?**<br/>
    Scoped functions are functions that execute a block of code within the context of an object.

    The context of the object can be referred to as “it” or “this” which we will be understanding through examples in this article.
    
    <b>let:</b>
    It refers to the context of the object by using the “it” keyword and hence, this “it” can be renamed to a readable lambda parameter.

    The second advantage is it easily helps in providing null checks. Let’s say we make the “ name ” parameter of the “ Person ” class nullable and we want to print the name of the person only if it is a not null value, then we can write a clean, simple and concise code as follows:

    ```kotlin
    var name: String? = "Abcd"
    private fun performLetOperation() {
        val name = Person().name?.let {
            "The name of the Person is: $it"
        }
        print(name)
    }
    ```

    <b>run:</b>
    The “ run ” operator is similar to the “ let ” operator in terms of accepting a return value that is different from the object on which the scope function is being applied to. Hence, a “ run ” operator can be used to initialize an object and return the result of it.
    
    ```kotlin
    private fun performRunOperation() {
        Person().run {
            name = "Asdf"
            contactNumber = "0987654321"
            return@run "The details of the Person is: ${displayInfo()}"
        }
    }
    output:
    Name: Asdf
    Contact Number: 0987654321
    Address: xyz
    ```

    <b>with:</b>
    The “ with ” operator is completely similar to the run operator that we just discussed. It also refers to the context of the object as “ this ”, similar to how the “ run ” operator uses it.

    ```kotlin
    private fun performWithOperation() {
        val person = with(Person()) {
            return@with "The name of the Person is: ${this.name}"
        }
        print(person)
    }
    Output:
    The name of the Person is: Abcd
    ```
    <b>apply:</b>
    The apply function is similar to the run functionality only in terms of referring to the context of the object as “ this ” and not “ it ” and also in providing null safety checks:

    ```kotlin
    private fun performApplyOperation() {
        val person: Person? = null
        person?.apply {
            name = "asdf"
            contactNumber = "1234"
            address = "wasd"
            displayInfo()
        }
    }


    // Normal approach
    fun createIntent(intentData: String, intentAction: String): Intent {
        val intent = Intent()
        intent.action = intentAction
        intent.data = Uri.parse(intentData)
        return intent
    }

    // Improved approach, by using apply
    fun createIntent(intentData: String, intentAction: String) =
        Intent().apply {
            action = intentAction
            data = Uri.parse(intentData)
        }
    ```

    <b>also</b>:
    The “ also” function is similar to the let functionality only in terms of referring to the context of the object as “ it ” and not “ this ” and also in providing null safety checks:

    ```kotlin
    private fun performAlsoOperation() {
        val name = Person().also { currentPerson ->
            print("Current name is: ${currentPerson.name}\n")
            currentPerson.name = "modifiedName"
        }.run {
            "Modified name is: $name\n"
        }
        print(name)
    }
    output:
    Current name is: Abcd
    Modified name is: modifiedName
    ```

### Infix Functions

-   **What is an infix function in Kotlin?**<br/>
    An infix function is used to call the function without using any bracket or parenthesis. You need to use the infix keyword to use the infix function.

    ```kotlin
    class Operations {
        var x = 10; 
        infix fun minus(num: Int) {
            this.x = this.x - num
        } 
    }
    fun main() {
        val opr = Operations()
        opr minus 8
        print(opr.x)
    }
    ```

### Inline Functions

-   **What is an inline function in Kotlin?**<br/>
    Inline function instruct compiler to insert complete body of the function wherever that function got used in the code. To use an Inline function, all you need to do is just add an inline keyword at the beginning of the function declaration.
    
    Advantage of ```inline``` function: Function call overhead doesn't occur. Less overhead and faster program execution.

-   **What is noinline in Kotlin?**<br/>
    While using an inline function and want to pass some lambda function and not all lambda function as inline, then you can explicitly tell the compiler which lambda it shouldn't inline.

    ```kotlin
    inline fun doSomethingElse(abc: () -> Unit, noinline xyz: () -> Unit) {
        abc()
        xyz()
    }
    ```

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


