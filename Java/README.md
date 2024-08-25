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

    ```kotlin
    // RxAndroid Tutorial - Adding Observable
    Observable<String> stringObservable = Observable.just("Hello Reactive Programming!");
    ```
   
    2) <b>Observer:</b>
    Observer consumes the data emitted by the Observable. To do this, Observer needs to subscribe to the Observable.

    ```kotlin
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

    ```kotlin
    // RxAndroid tutorial - observer subscribing to observable
    stringObservable.subscribe(stringObserver);
    ```
    
    Note:An Observable emits data if there is at least one Observer subscribed to it.
