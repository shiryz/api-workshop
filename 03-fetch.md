## The fetch API: Learning Outcomes
* Understand how to use fetch to make API requests

## The anatomy of fetch

### What is fetch?
>The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.

>This kind of functionality was previously achieved using XMLHttpRequest. Fetch provides a better alternative that can be easily used by other technologies such as Service Workers. Fetch also provides a single logical place to define other HTTP-related concepts such as CORS and extensions to HTTP.  

[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

### Using fetch

In a very simple manner all you really do is call fetch with the URL you want, by default the Fetch API uses the GET method, so a very simple call would be like this:

```js
fetch(url) // Call the fetch function passing the url of the API as a parameter
.then(function(data) {
    // Your code for handling the data you get from the API
})
.catch(function(error) {
    // This is where you run code if the server returns any errors
});
```

*This is the template for any Get request using fetch*  

for example:

```js
fetch('https://api.github.com/users/chriscoyier/repos')
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    // Here's a list of repos!
    console.log(data);
  })
  .catch(function(error) {
    console.log(error);
  })
```

### Line by line
Following is an explanation of each line of code from the example above.

1. `fetch(url)` --- we are calling the Fetch API and passing it the URL we defined and since no more parameters are set this is a simple GET request.
  - *url*: The requested URL (in this case, github's api) - in many cases this will be the URL of the server you are querying.

2. `.then(function(response)` --- this is the code that runs in case the request is successful, we get a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) object back.

3. `return response.json();` --- `response` is just an HTTP response of course, not the actual JSON. To extract the JSON body content from the response, we use the .json() method, we return the result so it can be accessed by the following function.

4. `.then(function(data) {...})` --- we have now passed a JSON object to this function and can now use the data.

5. `.catch(function(error) {...}` --- this code will run in case an error was thrown  while processing the request, a common scenario is when the function `response.json()` fails while the request haven't returned a JSON like object, the catch would be called with  an error message of `TypeError: Failed to fetch`,
if no error is thrown, `.catch(..`  won't be called similar to the `try catch` functionality.

*Note* - Don't worry if you don't get how `.then` and `.catch` work yet, we'll go over them in greater detail in later weeks, also however we recommend you to check
[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).


## Extra

### Fetch vs. XHR
Let's compare the two:

__XHR - XML HTTP Request__
```js
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4 && xhr.status == 200) {
      var data = JSON.parse(xhr.responseText);
      console.log(data);
    }
};
xhr.open('GET', './api/some.json', true);
xhr.send();
```

__fetch()__
```js
fetch('./api/some.json')
.then(function(response) {
    return response.json();
})
.then(function(data) {
    console.log(data);
})
```

- Both code snippets achieve the same functionality, they're both asynchronous calls to an api (more on asynchrony in the next section) and they both parse the result and log it.
- fetch is more readable and more concise, but using XHR allows you to check for failed requests in a straightforward way by checking the `status` property, while you can do so in fetch as well, a request will not fail if the status code was of an error (to understand this more, check the optional reading).
- `response.json()` and `JSON.parse()`, the two methods are used to parse the response body. `Body.json()` is asynchronous and returns a Promise object that resolves to a JavaScript object, `JSON.parse()` is synchronous can parse a string, then returns a JSON object, hence since  `response.json()` is asynchronous it returns a callback as a promise object.  

