# Java Interview Questions and Answers

Quick Jump to Topics:
 > * [Basic](#basic)
 >> * [null safety](#null-safety)
 > * [RxJava](#rxjava)
 > * [Coroutines](#coroutines)


### Basic

-   **How does Kotlin work on Android?**<br/>
    Just like Java, the Kotlin code is also compiled into the Java bytecode and is executed at runtime by the Java Virtual Machine i.e. JVM. When a Kotlin file named ```Main.kt``` is compiled then it will eventually turn into a class and then the bytecode of the class will be generated. The name of the bytecode file will be ```MainKt.class``` and this file will be executed by the JVM.

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

-   **What are Operators in the World of RxJava?**<br/>
    Operators perform certain tasks on Observables. There are few operators that can Create Observables, and there are other operators that can perform various actions on Observables.

    Types of Operators Available in RxJava
    [adinserter block=”7″]

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
