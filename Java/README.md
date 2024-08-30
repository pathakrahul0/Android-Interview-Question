# Java Interview Questions and Answers

Quick Jump to Topics:
 > * [Basic](#basic)
 >> * [null safety](#null-safety)
 > * [RxJava](#rxjava)
 > * [Coroutines](#coroutines)


https://veskoiliev.com/40-rxjava-interview-questions-and-answers/

### Basic

-   **Explain OOP Concepts**<br/>
    OOP is a programming paradigm that models real-world entities as objects. Each object has properties (attributes) and behaviors (methods). These concepts form the foundation of OOP:

    1) <b>Object:</b>
    A fundamental unit in OOP that represents a real-world entity.
    It has properties (data) and methods (functions).
    Example: A Car object might have properties like color, make, model, and methods like start, stop, accelerate.
    2) <b>Class:</b>
    A blueprint or template for creating objects.
    Defines the properties and methods that objects of that class will have.
    Example: The Car class would define the common attributes and behaviors for all cars.
    3) <b>Encapsulation:</b>
    The process of bundling data (attributes) and methods (functions) within a single unit (object).
    Protects data from unauthorized access or modification.
    Achieved through access modifiers (public, private, protected).
    4) <b>Inheritance:</b>
    A mechanism where one class (child class) acquires properties and methods of another class (parent class).
    Promotes code reusability and creates hierarchical relationships.
    Example: A Truck class might inherit from the Vehicle class, gaining its properties and methods.
    5) <b>Polymorphism:</b>
    The ability of objects of different classes to be treated as if they were objects of the same class.
    Allows for flexible and dynamic code.
    Achieved through method overriding and method overloading.
    Example: A Dog and Cat class can both have a speak method, but they will implement it differently.
    6) <b>Abstraction:</b>
    Simplifying complex reality by focusing on essential features and ignoring irrelevant details.
    Achieved through abstract classes and interfaces.
    Example: An Animal class might have an abstract makeSound method, forcing its child classes to implement it.
    Benefits of OOP:
    Modularity: Breaks down complex problems into smaller, manageable units.
    Reusability: Code can be reused in different contexts.
    Maintainability: Easier to understand, modify, and extend code.
    Flexibility: Adaptable to changing requirements.

-   **What is Polymorphism? What about Inheritance?**<br/>

-   **Can an Interface implement another Interface?**<br/>

-   **Difference between method overloading and overriding.**<br/>

-   **Differences between abstract classes and interfaces?**<br/>

-   **What are the access modifiers you know? What does each one do?**<br/>

-   **How is String class implemented? Why was it made immutable?**<br/>

-   **What does it means to say that a String is immutable?**<br/>

-   **Difference between StringBuffer and StringBuilder**<br/>

-   **Can you create an object for Abstract Class directly?**<br/>
    No, we cannot create an object of an abstract class, but we can create a reference variable of an abstract class pointing to the object of its implementation.

-   **Can you create an object for an Interface directly?**<br/>
    No, similar to abstract class, we cannot create an object of an Interface. But we can create a reference variable of an Interface pointing to the object of its implementation.

-   **Can you create an object for Abstract Class directly?**<br/>
-   **Can you create an object for Abstract Class directly?**<br/>
-   **Can you create an object for Abstract Class directly?**<br/>



### RxJava
-   **Basic Building Blocks for Rx Programming?**<br/>
    There are 2 main building blocks for Reactive / Rx Programming

    1) <b>Observable:</b>
    Observables simply emits the data to those which subscribed to them. All the emission is done asynchronously to the subscribers.

    Example code:

    ```java
    // RxAndroid Tutorial - Adding Observable
    Observable<String> stringObservable = Observable.just("Hello Reactive Programming!");
    ```
   
    2) <b>Observer:</b>
    Observer consumes the data emitted by the Observable. To do this, Observer needs to subscribe to the Observable.

    ```java
    // RxAndroid Tutorial - Adding observer
    Observer<String> stringObserver = new Observer<String>() {
            @Override
            public void onSubscribe(Disposable d) {
            }

            @Override
            public void onNext(String s) {
                Toast.makeText(MainActivity.this, s, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onError(Throwable e) {
            }

            @Override
            public void onComplete() {
            }
        };
    ```
    3) <b>Subscribers:</b>
    Subscriber helps an Observer subscribe /unsubscribe from Observable.

    ```java
    // RxAndroid tutorial - observer subscribing to observable
    stringObservable.subscribe(stringObserver);
    ```
    
    Note:An Observable emits data if there is at least one Observer subscribed to it.

-   **How to Subscribe / Unsubscribe in RXJava?**<br/>
    We can make an Observer to subscribe to Observable as follows:
    ```java
    // RxAndroid tutorial - observer subscribing to observable
    stringObservable.subscribe(stringObserver);
    ```
-   **What are the different types of Observables in RxJava?**<br/>
    1) <b>Single:</b> A Single in RxJava is an Observable which emits only one item if completed or returns error.

    2) <b>Maybe:</b> A Maybe in RxJava is used when the Observable needs to emit a value or a no value or an error.

    3) <b>Completable:</b> A Completable in RxJava is an Observable which just completes the task and does not emit anything if completed. It returns an error if anything fails. It is similar to reactive concept of runnable.

    4) <b>Back Pressure:</b> Back Pressure is the state where your observable (publisher) is creating more events than your subscriber can handle.

    5) <b>Flowable:</b> A Flowable in RxJava is used when the Observable emits more data than the Observer can consume. In Other words, Flowable can handle back pressure where as an Observable cannot.

-   **Hot Observables vs Cold Observables**<br/>
    1) <b>Cold Observables:</b> A Cold Observable is an Observable that does not emit items until a Subscriber subscribes. If we have more than one Subscriber, then the Cold Observable will emit each sequence of items to all Subscribers one by one.

    2) <b>Hot Observables:</b> A Hot observable is an Observer that will emit items

    The main difference between a Hot and Cold Observable in RxJava is that a Hot Observable can begin emitting items as soon as it is created, while a Cold Observable will only begin emitting items when it is subscribed to.

    A Hot Observable is useful when you want to share a single source of data among multiple subscribers. For example, a Hot Observable could be used to share a stream of stock prices among multiple subscribers.

    A Cold Observable is useful when you want to ensure that each subscriber receives the same data. For example, a Cold Observable could be used to ensure that each subscriber receives the same stream of stock prices.

    In addition, Hot Observables can emit items even if there are no subscribers, while Cold Observables will not emit any items until they are subscribed to. This means that Hot Observables can potentially lose data if there are no subscribers to receive the data.

-   **What are Operators in the World of RxJava?**<br/>
    Operators perform certain tasks on Observables. There are few operators that can Create Observables, and there are other operators that can perform various actions on Observables.

    Types of Operators Available in RxJava
    ```[adinserter block=”7″]```

    1) <b>Operators for Creating Observables</b>
    These Operators help creating new Observables. The Operators in this category are: Create, ```Just, Defer, Start, etc.```

    2) <b>Operators for Transforming Observables</b>
    These Operators help transforming the items emitted by the Observables. The Operators in this Category are: ```Map, Flatmap, Buffer, etc.```

    3) <b>Operators for Filtering Observables</b>
    These Operators help in filtering the selective items from Observable. The Most commonly used Operators in this category are: ```Filter, Distinct, Debounce, etc.```

    4) <b>Operators for Combining Observables</b>
    These Operators help in combine multiple Observables to create a single Observable. The Most commonly used Operators in this category are: ```Zip, Join, Switch, etc.```

    5) <b>Error Handling Operators</b>
    These Operators are used to help catching errors while working with Observables. Eg: ```Catch, Retry.```

    ```[adinserter block=”7″]```

    6) <b>Observable Utility Operators</b>
    These operators are used for working with Observables. Eg. ```Subscribe, SubscribeOn, ObserveOn, etc.```

    7) <b>Conditional and Boolean Operators</b>
    These operators are helpful to evaluate one or more Observables or items emitted by Observables. Eg: ```All, Contains, DefaultIfEmpty, etc.```

    8) <b>Mathematical and Aggregate Operators</b>
    These are the basic Math Operators that will operate on entire sequence of items emitted by Observable. Eg: ```Max, Min, Average, Reduce, Sum, etc.```

-   **What is the subject in RxJava?**<br/>
    The subject is another essential concept in RxJava that helps developers create reusable codes.

-   **What is the difference between an Observable and a Flowable in RxJava?**<br/>
    
    The main difference between Observable and Flowable in RxJava is the way they handle backpressure.

    Observable is a stream of data that emits items to its subscribers. It does not support backpressure, meaning that it will emit items as fast as it can, regardless of the subscriber's ability to process them. This can lead to an OutOfMemoryError if the subscriber is not able to keep up with the rate of emission.

    Flowable is a stream of data that emits items to its subscribers. It supports backpressure, meaning that it will emit items at a rate that is determined by the subscriber's ability to process them. This helps to prevent OutOfMemoryErrors by ensuring that the subscriber is not overwhelmed with data.

    In summary, the main difference between Observable and Flowable in RxJava is that Flowable supports backpressure, while Observable does not.

-   **What is an Observable in RxJava2?**<br/>
    An Observable emits data to subscribers asynchronously.

-   **What is an Observer in RxJava2?**<br/>
    An Observer consumes the data emitted by the Observable and needs to subscribe to it to do so.

-   **What is the purpose of the Schedulers in RxJava?**<br/>
    Schedulers specify the thread on which an Observable will emit, and on which a Subscriber will be notified.

    The purpose of Schedulers in RxJava is to provide a way to control the concurrency of an Observable. Schedulers allow you to specify which thread an Observable should run on, and how many threads it should use. This is important for ensuring that your application runs efficiently and that it does not overwhelm the system with too many concurrent tasks. Schedulers also provide a way to control the order in which tasks are executed, which is important for ensuring that tasks are executed in the correct order. Finally, Schedulers provide a way to control the backpressure of an Observable, which is important for ensuring that an Observable does not emit too many items too quickly.

-   **How do you handle errors in RxJava?**<br/>
    
    When dealing with errors in RxJava, it is important to understand the different types of errors that can occur and how to handle them.

    The first type of error is an onError event. This is an event that is emitted when an exception is thrown within an Observable. When this occurs, the onError event will be emitted and the subscription will be terminated. To handle this type of error, you can use the onErrorReturn() operator to return a default value or the onErrorResumeNext() operator to return an alternate Observable.

    The second type of error is an onErrorResumeNext event. This is an event that is emitted when an exception is thrown within an Observable and the onErrorResumeNext operator is used. This operator will return an alternate Observable that will be used instead of the original Observable. To handle this type of error, you can use the onErrorResumeNext() operator to return an alternate Observable.

    The third type of error is an onExceptionResumeNext event. This is an event that is emitted when an exception is thrown within an Observable and the onExceptionResumeNext operator is used. This operator will return an alternate Observable that will be used instead of the original Observable. To handle this type of error, you can use the onExceptionResumeNext() operator to return an alternate Observable.

    Finally, you can also use the catch() operator to catch any exceptions that are thrown within an Observable. This operator will catch any exceptions that are thrown and will return an alternate Observable. To handle this type of error, you can use the catch() operator to return an alternate Observable.

    By understanding the different types of errors that can occur in RxJava and how to handle them, you can ensure that your code is robust and reliable.

-   **How do you handle backpressure in RxJava?**<br/>
   
    Backpressure is an important concept to understand when working with RxJava. It is a mechanism that allows the producer of data to control the rate at which the consumer of data can process it.

    In RxJava, backpressure is handled by using the Flowable class. This class is designed to handle backpressure by allowing the producer to control the rate at which the consumer can process the data. The Flowable class provides operators such as onBackpressureBuffer(), onBackpressureDrop(), and onBackpressureLatest() which allow the producer to control the rate at which the consumer can process the data.

    The onBackpressureBuffer() operator allows the producer to buffer the data until the consumer is ready to process it. The onBackpressureDrop() operator allows the producer to drop the data if the consumer is not ready to process it. The onBackpressureLatest() operator allows the producer to keep the latest data and discard the older data if the consumer is not ready to process it.

    By using these operators, the producer can control the rate at which the consumer can process the data and handle backpressure in RxJava.


-   **What is the difference between a Subject and an Observer in RxJava?**<br/>

    The Subject in RxJava is a special type of Observable that allows values to be multicasted to many Observers. It is typically used to bridge the gap between a cold Observable and multiple Observers.

    An Observer is an object that implements the Observer interface and is used to receive notifications from an Observable. It is typically used to subscribe to an Observable and receive notifications when the Observable emits new values.

    In summary, a Subject is an Observable that can multicast values to multiple Observers, while an Observer is an object that subscribes to an Observable and receives notifications when the Observable emits new values.
    
-   **How do you create an Observable from a list of items in RxJava?**<br/>

    Creating an Observable from a list of items in RxJava is a fairly straightforward process. First, you need to create an Observable object using the Observable.from() method. This method takes a list of items as its parameter and returns an Observable object.

    Once you have the Observable object, you can then use the subscribe() method to subscribe to the Observable. This method takes an Observer object as its parameter, which is used to receive notifications from the Observable.

    Finally, you can use the onNext() method of the Observer object to receive the items from the list one by one. This method takes an item from the list as its parameter and passes it to the Observer.

    In summary, creating an Observable from a list of items in RxJava involves creating an Observable object using the Observable.from() method, subscribing to the Observable using the subscribe() method, and receiving the items from the list one by one using the onNext() method of the Observer object.

-   **How do you create an Observable from a single item in RxJava?**<br/>
    
    To create an Observable from a single item in RxJava, you can use the just() operator. This operator takes a single item and emits it as an Observable. For example, if you wanted to create an Observable from a single String item, you could do the following:

    Observable singleItemObservable = Observable.just("My String Item");

    The just() operator is a convenient way to create an Observable from a single item. It is also possible to create an Observable from a single item using the create() operator. This operator takes an OnSubscribe object as a parameter, which is responsible for emitting the item. For example, if you wanted to create an Observable from a single String item, you could do the following:

    Observable singleItemObservable = Observable.create(subscriber -> { subscriber.onNext("My String Item"); subscriber.onCompleted(); });

    The create() operator is more verbose than the just() operator, but it gives you more control over the emission of the item.

-   **What is the purpose of the RxJava operators?**<br/>
    
    The purpose of RxJava operators is to manipulate and transform the data emitted by Observables. Operators are used to filter, combine, and transform the data emitted by Observables into the desired form. They are also used to create new Observables from existing ones.

    RxJava operators can be divided into two categories: intermediate operators and terminal operators. Intermediate operators are used to transform the data emitted by an Observable and can be chained together to create complex data transformations. Terminal operators are used to consume the data emitted by an Observable and can be used to trigger side effects or to terminate the Observable.

    RxJava operators are essential for creating reactive applications as they allow developers to manipulate and transform data in a declarative manner. They are also used to create complex data flows and to handle errors and exceptions.

-   **How do you debug an RxJava application?**<br/>
    
    Debugging an RxJava application requires a few steps.

    First, you should identify the source of the issue. This can be done by examining the stack trace and looking for any errors or exceptions that may have been thrown. You can also use logging statements to help pinpoint the source of the issue.

    Once you have identified the source of the issue, you can start to debug the application. This can be done by using the RxJava debugging tools such as RxJavaPlugins. These tools allow you to observe the flow of data through the application and identify any issues.

    You can also use the RxJava debugger to step through the code and identify any issues. This can be done by setting breakpoints and stepping through the code line by line.

    Finally, you can use the RxJava TestObserver to test the application. This allows you to observe the data that is being emitted from the application and identify any issues.

    By following these steps, you should be able to debug your RxJava application and identify any issues.
