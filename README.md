# PH Developers Directory
[![CircleCI](https://circleci.com/gh/PHDevsConnect/phdevsdir/tree/master.svg?style=svg)](https://circleci.com/gh/PHDevsConnect/phdevsdir/tree/master)


A Directory app for web devs in Port Harcourt, Nigeria. Built with React, Express and MongoDB

# API DOCS

`GET` `https://phdevsdir.herokuapp.com/api/v1/developers` - display all developers
`POST` `https://phdevsdir.herokuapp.com/api/v1/developers` - create a new developer
Params

- `first_name` (String) `required`,
- `last_name` (String) `required`
- `email` (String) `required`
- `stack` (Comma Delimited String) `optional`
- `github_url` (String) `required`

# Using the API
Here are some examples to aid in using the API. This API currently make use of one endpoint (`/api/v1/developers`), with two HTTP verbs attached to it (GET & POST).

### JavaScript
```js

// using XMLHttpRequest

// GET
let request = new XMLHttpRequest();
request.open('Get', "https://phdevsdir.herokuapp.com/api/v1/developers");
request.send();

request.onreadystatechange = (e) => {
  if(request.readyState == 4 && request.status == 200) {
    // request is successful, lets party
    let response = JSON.parse(request.responseText);
    console.log(response);
  }
}

// POST
let request = new XMLHttpRequest();
request.open('POST', 'https://phdevsdir.herokuapp.com/api/v1/developers');
let params = 'params=value';

request.setRequestHeader('Content-Type', 'application/json'); // application/x-www-form-urlencoded, etc

request.onreadystatechange = (e) => {
  if(request.readyState == 4 && request.status == 200) {
    let response = JSON.parse(request.responseText);
    console.log(response);
  }
}
request.send(params);

// Using axios (its easy af!)
axios.get('https://phdevsdir.herokuapp.com/api/v1/developers')
  .then( (response) => {
    console.log(response);
    })
  .catch( (err) => {
    console.log(err);
    });

axios.post('https://phdevsdir.herokuapp.com/api/v1/developers', {
  first_name: 'John',
  last_name: 'Doe'
  })
  .then( (response) => {
    console.log(response);
    })
  .catch( (err) => {
    console.log(err);
    });

```
### PHP
```php
<?php
  // GET
  $r = new HttpRequest('https://phdevsdir.herokuapp.com/api/v1/developers', HttpRequest::METH_GET);
  try {
    $r->send();
    if ($r->getResponseCode() == 200) {
        $response = $r->getResponseBody();
    }
  } catch (HttpException $ex) {
    echo $ex;
  }

  // POST
  $r = new HttpRequest('https://phdevsdir.herokuapp.com/api/v1/developers', HttpRequest::METH_POST);
  $r->addPostFields(['first_name' => 'john', 'last_name' => 'doe']);
  try {
    echo $r->send()->getBody();
  } catch (HttpException $ex) {
    echo $ex;
  }
?>
```
### Go
```go
func main() {
  // GET
  request, err := http.Get("https://phdevsdir.herokuapp.com/api/v1/developers")
  if err != nil {
    log.Println(err)
  }

  defer request.Body.Close()

  requestBytes, err := ioutil.ReadAll(request.Body)
  if err != nil {
    log.Println(err)
  }
  response := string(bodyBytes)
  log.Print(response)

  // POST
  body := []bytes("firstname=john&lastname=doe")
  req, err := http.Post("https://phdevsdir.herokuapp.com/api/v1/developers", "body/type", bytes.NewBuffer(body))

  if err != nil {
    log.Println(err)
  }
  defer req.Body.Close()
  bodyBytes, err := ioutil.ReadAll(res.Body)
  if err != nil {
    log.Println(err)
  }
  res := string(bodyBytes)
}
```
### Python
```python
import requests
import json

// GET
r = requests.get("https://phdevsdir.herokuapp.com/api/v1/developers")
print r.content

// POST
url = "https://phdevsdir.herokuapp.com/api/v1/developers"
payload = {'first_name': 'John', 'last_name': 'Doe'}
response = requests.post(url, data=json.dumps(payload))
print(response.text)
```

# Contributing
- Fork the repo
- Make your changes
- Create a PR
- Create an Issue for feature requests

# Using Postman to test routes
- Install Postman (Google Chrome Required) https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en or Download the [Desktop Client](http://getpostman.com)
- Launch the app from chrome://apps
- Paste the app link in the url bar, set the request method (POST, GET, PUT, UPDATE, etc)
- Make sure to set a Content-Type to applicaiton/json or an encoded form
- Insert Keys matching the API's params alongside your values
- Hit "send"
# Here's an example of posting data to the api using json

- Paste the app link in the url bar, set the request method from "GET" to "POST"
- Now  go under HEADERS(just after "Authorization") and make sure content-Type is set application/json  (see image below)
- ![contenttype](https://user-images.githubusercontent.com/25697914/31719203-8be3250a-b40a-11e7-8c94-13fb431889f7.png)
- then go under BODY(just after Headers) to select ur dataType: select either "x-www-form-encoded" or "raw" [I prefer to use raw]
- After you have selected raw to your left appears a category of dataTypes, default is text, change it to "JSON(application/json)".
- enter data to be submited like so: (check code below)
```
{
	"first_name": "Jane",
	"last_name": "Joe",
	"email": "jane@email.com",
	"stack": "JS, PHP",
	"github_url": "github.com/janeDoe"
}

```
- Click the SEND button behind the url bar and it return a response down below which is either a 200 - successfull and other codes for one kind of failure or the other(the picture below returns error 500; no worries  urs will be successful. *smile*)
- ![postman](https://user-images.githubusercontent.com/25697914/31720070-726578dc-b40d-11e7-8e70-91029a48e7f7.png)