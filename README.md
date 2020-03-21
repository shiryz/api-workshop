**Author**: [@lucymonie](https://github.com/lucymonie)  

**Maintainer**: [@lucymonie](https://github.com/lucymonie)

# Introducing APIs

There are a few core concepts you need to understand in making API requests. By the end of this morning's workshop you should have a mental model of
- The request-response pattern
- HTTP methods and status codes
- The fetch API

### The workshop
We will be working in pairs this morning, so figure out who you will be working with. The plan is that each pair should actively read and discuss each topic and try to make sure they both understand the material. How you do this is up to you - you may like to take some time to read separately and then discuss the material between you. Remember: Google is your friend.

For each topic we will give you 10-15 minutes of reading and discussion time in your pairs, and then we will spend 10-15 minutes asking you questions about the material, and we will pick on pairs at random to answer the questions or explain aspects of the material. We will also attempt to answer any questions you may have for us.

After that we will work on some examples in which we will make API requests.

#### What to do
Start by adding [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) a Chrome extension that makes JSON data much more readable in Chrome

Read each section and be ready to answer questions  

1. [Request and response pattern](https://github.com/shiryz/api-workshop/blob/master/01-request-response.md)  

2. [HTTP](https://github.com/shiryz/api-workshop/blob/master/02-http.md)  

3. [Fetch API](https://github.com/shiryz/api-workshop/blob/master/03-fetch.md)  


5. [Fix a broken API request](https://github.com/shiryz/api-workshop/blob/master/api-example)  
    - You will need to clone the repository and work on the code locally
    - If you have ssh keys for github: `git clone git@github.com:shiryz/api-workshop.git`
    - Otherwise, use:`git clone https://github.com/shiryz/api-workshop.git`
    - Open index.html in the browser and you will see that the API request is not working
    - Open main.js and look for what's broken or missing in the code. If you're confused, check it line-by-line against the description of fetch in [this file](https://github.com/shiryz/api-workshop/blob/master/03-fetch.md)


### Follow up and further learning
- If you're at all hazy about how the Internet works, watch [this excellent explanation]( https://www.youtube.com/watch?v=7_LPdttKXPc)
- If you're interested in how domains are translated into ip addresses, watch [this amusing discussion of DNS](https://www.youtube.com/watch?v=72snZctFFtA)
- REST (Representational State Transfer) is a best practice standard for web interactions. [This video](https://www.youtube.com/watch?v=YCcAE2SCQ6k) gives some background about REST.
- If you need a more comprehensive tutorial on fetch, follow [this post](https://scotch.io/tutorials/how-to-use-the-javascript-fetch-api-to-get-data#toc-how-do-we-use-the-fetch-api-)
