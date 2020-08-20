---
title: "How to Use Fetch Api in Processmaker"
date: 2020-08-15T23:09:18+01:00
draft: 
---

When trying to use the fetch api to make an ajax call in ProcessMaker, we need to consider if we are making the call to a trigger or not. We shall be looking at both instances where: 
1. We make an ajax call to a trigger and 
2. We call an api directly.

For this tutorial, we shall be using the [JSONPlaceholder](https://jsonplaceholder.typicode.com/) which is a fake online REST API for testing and prototyping. 
Let us begin.

#### API Call From Trigger

1. First we will create a Trigger and give it a title of ```Get All Posts``` then we will make a GET request to the ```/posts``` routes of our API, then save our trigger

![image](https://user-images.githubusercontent.com/22425217/90324000-33141f80-df61-11ea-8ec4-9f98da2345eb.png)




```php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://jsonplaceholder.typicode.com/posts",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET"
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

````

2. Next we create a Dynaform and give it a title of ```Fetch API``` then ```Save & Open``` it.
![image](https://user-images.githubusercontent.com/22425217/90323294-5c2fb280-df57-11ea-9d67-abdf48c57796.png)


3. To begin designing the Dynaform, we will drag a panel onto it and give it an id of ```panelHeading```, a border of zero, then style it like so:

```html

<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>Fetch API in ProcessMaker</h4>

</div>

```

4. Next, we will drag a button under the ```panelHeading``` and give it and id and name of ```btnGetRequest``` and a label of ```GET POSTS```. We will attach a click event to it later to be used to fetch our posts from the API.

5. Under the button, drag another panel onto the Dynaform and give it an id of ```panelResult```, a border of zero and style it like so:

```html

<div id="resultPanel" style="height: 200px">

</div>

```

6. Now, our Dynaform should look like the image below and  we can now write our JavaScript in the Dynaform code editor which we will open by clicking the button highlighted in red:

![image](https://user-images.githubusercontent.com/22425217/90822421-50176c80-e32c-11ea-954c-6d96481709d3.png)


7. In our editor, we will first of all declare all our constants:


```javascript

const host 		= PMDynaform.getHostName(); // get the hostname
const ws 		= PMDynaform.getWorkspaceName(); // get the current workspace
const token 	= PMDynaform.getAccessToken(); // get the access Token
const app_uid 	= frames.app_uid ? frames.app_uid : ''; // get the case ID
let trig_uid; 	// set to the ID of the trigger

```

8. We will write a function that will format our json result from the ajax call into our panel with id ```panelResult```

```javascript

function showOutput(res) {

  document.getElementById('resultPanel').innerHTML = `
		<pre>${JSON.stringify(res)}</pre>
  `;

}

```


9. Next, we write our function to make the ajax call to our ```Get All Posts``` trigger

```javascript

function getAllPosts(){
  
  trig_uid = "7602398855f3874765e8fa2087940747"; // Trigger ID of 'Get All Posts'
  const url = host + "/api/1.0/" + ws + "/cases/" + app_uid + "/execute-trigger/" + trig_uid;
  const testing =  fetch(url, {
    method: 'PUT',
    headers: {
      Authorization: 'Bearer ' + token
    }

  })
  .then(response => response.json())
  .then(json => showOutput(json))

 
}

```


10. Finally we attach a ```click``` event to our button to call our function

```javascript

$(document).ready(function() {
  
    document.getElementById("btnGetRequest").addEventListener("click", getAllPosts);

  
});

```