# AsyncJavascript
Course notes on Async javascript

## Promises
* JavaScript has 2 queues in order to handle asynchronus tasks
    - `Callback Queue` can be referred to as `Task Queue`: Background Work (Web Browser APIs) do not return anything back into JavaScript. They just take in a pointer to a function and add it to a Queue that will perseve the order in which the event loop will add it to the Call stack. The callbacks in these typs of background tasks will end up in this Queue of the Event loop. This would be an example of the Old School method of a facade function.

    - `Microtask Queue` can be referred to as `Job Queue`: Background Work (Web Browser APIs) that return an Object (Promise) back into Javascript. The Web Browser will update a property on the Object to the value it was able to get/calculate. The Object that exists in JavaScript will notice the value has been updated and will execute an array of functions that are held in a property of that same Object (Promise). The callbacks that are in the array will end up in this Queue of the Event loop. This would be an example of the New School method of a facade function. 
        - The event loop wil stay in the `Microtask Queue` until there are no more tasks to handle

    - The `Event Loop` prioritizes functions in the `Microtask Queue` over the ones on the `Callback Queue` in regards to adding it to the `Call Stack`. A really good example of this is when we fetch data from and endpoint that is JSON. it would be something like...:
    ```javascript
    const promise = fetch(url);
    promise
    .then((httpRes) => httpRes.json())
    .then((json) => console.log(json))

    ```

    ```javascript
    // Promise Object (theorectically)
    const Promise = 
    {
        value: undefined, // will eventually get set
        onSuccess: [() =>,/* more functions */],
        onFailure: [() =>,/* more functions */],
    }
    ```
* `Promises` have 3 statuses: Resolved, Rejected, and Pending.
    - They use these statuses in order to trigger the array of functions that are held in one of its own properties
    - They have a property for the Resolved status that can house an array of functions to execute if the process was successful
    - They have a property for the Rejected status that can house an array of functions to execute if the process was un-successful  

* Some web Browser APIs work with promieses
    - in this case some just give a function/s to the browser apio in order to execute whenever the browser is done dont some sort of work.
    - This second case JavaScript will create a special object and then work with the Browser API

* 2 Schools of Facade functions when interacting with Browser APIs in JavaScript
    - `Old School`: This is achieved by using callbacks in order let the Browser API execute Javascript functionality whenever the API as completed (reference the setTimeout function)

    - `New School`: This is achieved by creating an Object in JavaScript with a value property (the future value the Browser API calculates) and a onFullfilment property (an array that holds functions). The Browser API called interacts with this Object by updating the value property once the Browser API call has completed its work. Once the value property of the Object has been updated the onFullfilment gets triggered and executes the functions in the array passing in the value properties value from the Object