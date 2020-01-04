## Request and response: Learning Outcomes

* Understand what a request and a response is
* Be familiar with what a request object and response object looks like
* Know what JSON is used for and what it looks like

## Request and response

### The pattern

Request/response is a pattern that's central to making API requests. 

![client-server-image](https://developer.mozilla.org/files/4291/client-server.png)

A familiar example of request and response is when you open your browser, type in
a url and hit enter. What you're doing is opening a connection between your
browser (the client) and some domain (the server). The server at that address
processes your request and replies with any data (files, images etc) associated
with the address you specified in your request. You will learn how to construct
requests shortly.

An API request also opens a connection between a client (your code running in
the browser) and a server, and makes a request. It even uses an HTTP url, just
like you use in your browser address bar. The server responds with data, which
might be information about the weather, pictures of cats or links to news
articles.

### A code example

Open up this repl: https://repl.it/@jc66/xhr-example

It contains a working code example of making a request to the Giphy API, and logging the response. In case you don't know, [Giphy](https://giphy.com/) is a website for getting animated GIFs based on your search terms.

Read on to understand how the code works.

### The request object

An API request is an object, and you create one by calling the XMLHttpRequest
constructor like this:

```js
var xhr = new XMLHttpRequest()
```

`xhr` is going to be our object for making requests and receiving responses.

Next, we need to initialise our request:

```js
xhr.open('GET', 'https://api.giphy.com/v1/gifs/search?q=funny+cat&api_key=dc6zaTOxFJmzC')
```

The first argument, `'GET'`, states that we want to do an HTTP GET request (you will learn more about this in the HTTP section).

The second argument, `'https://.api.giphy...'`, is the url for the Giphy API. This is the location where we want to make the request.

Finally, before we talk about the response object, look at this line at the bottom:

```js
// This is what actually sends the request!
xhr.send()
```

### The response object

We need to tell our `xhr` object what to do when it receives a response. We can do that by setting the `onreadystatechange` function:

```js
// We define a function and assign it to xhr.onreadystatechange
xhr.onreadystatechange = function() {
  // This function will be called automatically whenever the state of the `xhr` object changes
  // eg: when our xhr object receives a response
}  
```

Inside this function, we need to do a few checks before accessing the response:

```js
xhr.onreadystatechange = function() {
    // If xhr.readyState is 4, we received a response
    // If xhr.status is 200, the response was successful 
    if (xhr.readyState == 4 && xhr.status == 200) {
      // In here, we're ready to deal with the response  
      // We can access our response with xhr.responseText         
    }
}  
```

So now we are ready to access the response using `xhr.responseText` (at this point, the response has been automatically assigned to `xhr.responseText`). But what actually is this response, and what does it look like? Try opening https://api.giphy.com/v1/gifs/search?q=funny+cat&api_key=dc6zaTOxFJmzC in a seperate browser tab. You should see a big object with lots of data. It should look similar to a JS object.

You are officially looking at 🌟🌟JSON 🌟🌟. But what is it?

> JavaScript Object Notation (JSON) is a standard text-based format for representing structured data based on JavaScript object syntax. It is commonly used for transmitting data in web applications (e.g., sending some data from the server to the client, so it can be displayed on a web page, or vice versa)

> https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON

So JSON a data format that looks a lot like a JS object (but it can be used by lots of different programming languages, not just JS).

It's also a text-based format, ie: a string. This means that we can't treat it like an object straight away:

```js
// this would throw an error
xhr.responseText.data
```

First, we need to covert it from JSON to a regular JS data type. Luckily, the browser has a handy tool for converting data to/from JSON format, using the [standard built-in `JSON` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON). 


The built-in `JSON` object has two methods to convert JSON strings to regular JS and back again: 

* `var JSONString = JSON.stringify(object)`
* `var object = JSON.parse(JSONString)`

In our case, we will parse the `xhr.responseText` we receive back from our API call from a string into a JSON object like so:

`var data = JSON.parse(xhr.responseText);`

Once the responseText has been parsed, you can access it like you would any other
JavaScript object. I've called my parsed object 'data'. I could then `console.log(data);` to get a look at my parsed object.  

It follows that before *sending* JSON data anywhere, we should also use the `JSON.stringify()` method in JS to transform our data to a JSON string:

`var jsonDataToSend = JSON.stringify(dataToSend);`

In the mean time we will only use the `.parse()` method, once you start to build your
own server in the next weeks you will start using the `JSON.stringify()` method.

### But what if the response object is not a JSON object? 

In this case using `JSON.parse(responseText)` will throw an error.   This might be because the address we have requested data from is responding with a file, webpage, or other media that isn't structured in a JSON format. This could also happen if there was an error with the connection and the JSON response is returned with missing chunks. 

To protect against this you could wrap your `JSON.parse(responseText)` in a `try... catch` block like so:

```js
try {
  var data = JSON.parse(xhr.responseText)
} catch (e) {
  console.log('error =', e)
}
```
You can learn more about the `try... catch` statement at [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) but don't worry too much about implementing it now.

Many REST APIs send the response as a JSON object. JSON object is a very
popular form of data which is why we are focusing on this response type in this workshop.

### Let's take a look at an example of a response object:

- Try running the code in the repl, what does the data look like? Try opening some of the URLs returned inside the data
- Try `console.log()`ing the `xhr.responseText` before using `JSON.parse()`. This is what it looks like in it's JSON stringified form 
- Take a look at the api url. You don't need to understand it all right away
   but it's worth having a look at it to see the relationship between the url
   and what's in the response object.

### Summary

When you make an api request you write code that sends a request object to a
server. The response you get back is a mash of text and you use the
`JSON.parse()` method to transform your response into an object you can use.
