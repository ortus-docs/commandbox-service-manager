# Task Services

CommandBox Task Runners are a powerful way to accomplish CLI scripting.  You may have a task you'd like to run as a daemon so it's always executing.  This could be a message queue consumer, a scheduled task, or a file system watcher.  It is important that your tasks never exits, but always stays running forever.  Make sure you use an uninterruptible method of blocking the task such as `sleep()` so that when the service is shutdown, the interrupt signal will stop the task cleanly. &#x20;

Here is example of a task that uses sleep to stay running, but any command that stops when you press Ctrl-C from the command line will work (such as a file system watcher).

Create an empty task runner like so:

```bash
task create --open
```

And now put some code into it.  The `while( true )` loop makes it run forever (daemon) and the sleep will throw an exception when the thread is interrupted so it can be stopped.

{% code title="task.cfc" %}
```javascript
component {
    
  function run() {
    try{
      while( true ) {
        print.line( "still running!" ).toConsole()
        sleep( 5000 );
      }
    // Catching this will give us a clean shutdown so the service doesn't show as failed
    } catch( java.lang.InterruptedException e ) {
      print.line( 'Task interrupted ...' ).toConsole();
    } finally {
      // Any logic needed to clean up here
    }

}
```
{% endcode %}

You can test your task like so:

```bash
task run
```

Hit Ctrl-C to stop it.  Now, create a service out of.

```bash
task service create --start
```

