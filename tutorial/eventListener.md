
# Add Event Listeners
If you plan to create an application based on Keikai or integrate Keikai with your existing system, you definitely need to implement your application logic according to user actions. When a user interacts with Keikai spreadsheet, Keikai will send events to the server and invoke the corresponding event listeners you added.

For instance, if you need to perform some batch check when a user clicks a cell, you can add a listener like:

```java
RangeEventListener rangeEventListener = new RangeEventListener() {
    @Override
    public void onEvent(RangeEvent rangeEvent) throws Exception {
        // implement your application logic
    }
};
spreadsheet.addEventListener(Events.ON_CELL_CLICK, rangeEventListener);
```

For complete event list, please check [Events Javadoc]({{page.javadoc}}io/keikai/client/api/event/Events.html).
