# Notes

* Programs store data and apply functionlaity to it. But there are 2 parts to applying functions to collections of data
    1. The process of accessing each element
    2. What we want to do to each element
* `Iterators` automate the accessing of each element - so we can focus on what to do to each element - and make it available to us in a smooth way.
    - This changes the thought of instead of dealing with a static collection of data as an array/list we view it as a stream/flow of data.
    - The iterator will handle grabbing the next element in the collection
    - This concept relies on the `Closure` concept in JavaScript
        * The biggest thing to take away is that the inner function declaration will utlize a C.O.V.E (Closed Over Variable Environment) from the data that was declared in its parent createFunction. This allows inner to persist things in memory
        ```javascript
        function createFunction(array) 
        {
            let i = 0;
            function inner() 
            {
                const element = array[i];
                i++;
                return element
            }
            return inner
        }

        // Here returnNextElement is considered an iterator function as it
        // allows the function to be able to return the next element in a collection
        const returnNextElement = createFunction([4,5,6]);
        const element1 = returnNextElement();
        const element2 = returnNextElement();
        ```