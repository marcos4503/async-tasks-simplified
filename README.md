# Async Tasks Simplified

Async Tasks Simplified is a small utility script that allows your application to execute code in another Background Thread easily, in addition to allowing your Background code to call code in the Main Thread easily. Currently, Async Tasks Simplified supports Java and C#!

Async Tasks Simplified allows you to run slow or time-consuming code in another background thread, such as network request code, file processing, changes to the UI based on timing or anything that would freeze your UI if executed in Main Thread. Async Tasks Simplified was based on but not copied from Android's AsyncTask class, which is now marked Obsolete by Google. Async Tasks Simplified was born with the idea of bringing a simple, clean and intuitive code to do background tasks.

# How it works?

Async Tasks Simplified works much like similar to the standard Android AsyncTask class. After a few years the AsyncTask API was marked Obsolete by Google and the Async Tasks Simplified was created to be a simple replacement for the AsyncTask class. Initially I wrote the class for Java only, but here you will also see examples of use for other languages.

Firstly, you must create a new "AsyncTaskSimplified" object and then register the callbacks that will execute your code at each step of executing your Task, in addition to passing the start parameters. The start parameters are `strings` that you can define, which will be available in the start and execution stages of your code in the background.

In Java (Android Studio) only, the Async Tasks Simplified gives you the option to run your code in normal Threads or in native Java Executors, you are able to choose for example if your background code should run in Serial with other Async Tasks in a single Thread, or if your Async Task should run in parallel with other Async Tasks in a Thread Pool.

# How to use?

First, clone this repository, and copy the `AsyncTaskSimplified` file that is in the `Async-Tasks-Simplified-Source` folder of this repository. Copy the file that refers to the language you need. Then add it to your project. Now just follow the information below!

In Java, to start an Async Task, you can use the example code below...

```java
new AsyncTaskSimplified(context, new AsyncTaskSimplified.Listener() {
        @Override
        public void onStartTask_RunMainThread(Context context, String[] startParameters) {
            //Run before background code, this will run on UI/Main Thread
        }

        @Override
        public String[] onExecuteTask_RunBackground(Context context, String[] startParameters, AsyncTaskSimplified.ThreadTools threadTools) {
            //Here is the code that should be executed in Background Thread.
            //This will return some result to the "onDoneTask_RunMainThread"

            //Make thread sleep
            threadTools.MakeThreadSleep(3000);

            //Report a new progress
            threadTools.ReportNewProgress("100%");

            return new String[0];
        }

        @Override
        public void onNewProgress_RunMainThread(Context context, String progressOfBackground) {
            //Run when background thread (onExecuteTask_RunBackground) calls
            //"threadTools.ReportNewProgress()", this will run on UI/Main Thread
        }

        @Override
        public void onDoneTask_RunMainThread(Context context, String[] resultOfBackground) {
            //Run after Background Code finishes, this will run on UI/Main Thread
        }
    }, new String[]{"Parameter 1", "Parameter 2", "Parameter 3"})
    .Execute(AsyncTaskSimplified.ExecutionMode.ExecutorServiceThreadSingle);
```

Keep in mind that an Async Task goes through a total of 4 steps! See each of the steps now!

<h3>onStartTask_RunMainThread</h3>

This step is performed BEFORE your Background code starts executing. Furthermore, the code registered here runs on the Main Thread. In this callback, you also have access to the Context that started the Task and you also have access to the Start Parameters informed when starting the Task.

<h3>onExecuteTask_RunBackground</h3>

In this step, the code registered here is executed completely in another Thread that runs in the Background. The code registered here has easy access to the Context that started the Task, the Start Parameters informed when starting the Task and also has access to the `ThreadTools` belonging to that Task.

The `ThreadTools` is an object that only exists in the "onExecuteTask_RunBackground" event and with it you are able to make the Thread sleep for as many milliseconds as you want, and it is also capable of Reporting New Progress, which will activate the next step that you will see below.

The code registered here MUST return, at some point, a array of String containing the result of the code that was executed in the Background. This can be done easily just using something like "return new String[]{}".

<h3>onNewProgress_RunMainThread</h3>



<h3>onDoneTask_RunMainThread</h3>

dsds




Remember that each method of this class has a description that can be seen in the auto complete of your IDE (like Android Studio) or in the class itself, so you can read the descriptions of the methods to better understand how each one works and its details.









# Support projects like this

If you liked this Class and found it useful for your projects, please consider making a donation (if possible). This would make it even more possible for me to create and continue to maintain projects like this, but if you cannot make a donation, it is still a pleasure for you to use it! Thanks! 😀

<br>

<p align="center">
    <a href="https://www.paypal.com/donate/?hosted_button_id=MVDJY3AXLL8T2" target="_blank">
        <img src="Async-Tasks-Simplified-Source/Resources/paypal-donate.png" alt="Donate" />
    </a>
</p>

<br>

<p align="center">
Created with ❤ by Marcos Tomaz
</p>