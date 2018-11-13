# async

## AJAX

  * Make async requests in the background
  * No page reload/refresh
  * Fetch data
  * Very interactive

### XmlHttpRequest(XHR) object

  * API in the form of an object
  * Provided by the browsers JS environment
  * Methods transfer data between client/server
  * Can be used with other protocols than HTTP
  * Can work with data other than XML(JSON, plain text)

### Libraries & Other Methods

  * Fetch API
  * Axios
  * Superagent
  * jQuery
  * Node HTTP

### AJAX at work

```
document.getElementById('button').addEventListener('click', loadData);

function loadData(){
  // Create an XHR Object
  const xhr = new XMLHttpRequest();

  // OPEN
  xhr.open('GET', 'data.txt', true);

  // console.log('READYSTATE', xhr.readyState);

  // optional - used for spinners/loader
  xhr.onprogress = function() {
    console.log('READYSTATE', xhr.readyState);
  }

  xhr.onload = function() {
    console.log('READYSTATE', xhr.readyState);
    if(this.status === 200) {
      document.getElementById('output').innerHTML = `
        <h1>${this.responseText}</h1>
      `;
    }
  }

  // Old syntax
  // xhr.onreadystatechange = function() {
  //   console.log('READYSTATE', xhr.readyState);
  //   if(this.status === 200 && this.readyState === 4){
  //     console.log(this.responseText);
  //   }
  // }

  xhr.onerror = function() {
    console.log('Request error...');
  }

  // SEND
  xhr.send();
}
/*
  readyStatus Values --------------------
  0: request not initialized
  1: server connection established
  2: request received
  3: processing request
  4: request finished and response is ready

  HTTP Status ---------------------------
  200: "OK"
  403: "Forbidden"
  404: "Not Found"
*/
```