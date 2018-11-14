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

## Ajax from JSON data

```
document.getElementById('button1').addEventListener('click', loadCustomer);

document.getElementById('button2').addEventListener('click', loadCustomers);

// Load customers
function loadCustomers(e) {
  const xhr = new XMLHttpRequest();

  xhr.open('GET', 'customers.json', true);

  xhr.onload = function() {
    if(this.status === 200){

      const customers = JSON.parse(this.responseText);

      let output ='';

      customers.forEach(function(customer){
        output += `
          <ul>
            <li>ID: ${customer.id}</li>
            <li>ID: ${customer.name}</li>
            <li>ID: ${customer.company}</li>
            <li>ID: ${customer.phone}</li>
          </ul>
        `;
      });      

      document.getElementById('customers').innerHTML = output;
    }
  }

  xhr.send();
}

// Load single customer
function loadCustomer(e) {
  const xhr = new XMLHttpRequest();

  xhr.open('GET', 'customer.json', true);

  xhr.onload = function() {
    if(this.status === 200){
      // console.log(this.responseText);

      const customer = JSON.parse(this.responseText);

      const output = `
        <ul>
          <li>ID: ${customer.id}</li>
          <li>ID: ${customer.name}</li>
          <li>ID: ${customer.company}</li>
          <li>ID: ${customer.phone}</li>
        </ul>
      `;

      document.getElementById('customer').innerHTML = output;
    }
  }

  xhr.send();
}
```

## Ajax from external API

document.querySelector('.get-jokes').addEventListener('click', getJokes);

function getJokes(e) {
  const number = document.getElementById('name').value;

  const xhr = new XMLHttpRequest();

  xhr.open('GET', `http://api.icndb.com/jokes/random/${number}`, true);

  xhr.onload = function() {
    if(this.status === 200){
      const response = JSON.parse(this.responseText);
      
      let output = '';

      if(response.type === 'success'){
        response.value.forEach(function(joke) {
          output += `<li>${joke.joke}</li>`;
        });
      } else {
        output += '<li>Something went wrong</li>';
      }
      document.querySelector('.jokes').innerHTML = output;

    }
  }

  xhr.send();

  e.preventDefault();
}