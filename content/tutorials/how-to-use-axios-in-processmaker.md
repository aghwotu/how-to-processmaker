---
title: "How to Use Axios in Processmaker"
date: 2020-08-24T20:19:03+01:00
draft: false
---

{{% notice note %}}
This tutorial is for ProcessMaker version 3
{{% /notice %}}


For making ajax calls in ProcessMaker, a very helpful library is [axios](https://github.com/axios/axios) which is a promise based HTTP client for the browser and node.js. 

{{% notice tip %}}
For a quick runthrough of Axios, you can check out this YouTube video by Traversy Media on [Axios Crash Course | HTTP Library](https://youtu.be/6LyagkoRWYA)
{{% /notice %}}

For this tutorial, we shall be looking at these 3 use cases:
1. Making an API request to a Trigger
2. Chaining multiple API requests to a Trigger
3. Passing a parameter to an API 

For this project we shall be using the [axios cdn](https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js) and the [JSONPlaceholder api](https://jsonplaceholder.typicode.com/) which is a fake online REST API for testing and prototyping.

### Use case 1 - Making an API request to a Trigger

#### Creating our variables
Create a variable with Variable Name: ```userId``` and Variable Type of ```String``` and save it. We shall use this variable in our third use case

#### Writing our Triggers
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

```

2. Next we will create another Trigger and give it a title of ```Get All Todos``` then we will make a GET request to the ```/todos``` routes of our API, then save our trigger

![image](https://user-images.githubusercontent.com/22425217/91176535-50bc5400-e6da-11ea-8591-b35e21bf269f.png)


```php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://jsonplaceholder.typicode.com/todos",
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

```

3. Finally, we will create our third Trigger and give it a title of ```Get User```. This will contain a GET request to the ```/users``` route of our API. For this call, we shall be fetching a single user by specifying the id of the user that we want to get. This is the code for our trigger:

```php

$curl = curl_init();

//get 'id' from form
$formData = json_decode(file_get_contents("php://input"), true);
$id = trim($formData['id']);

$url = "https://jsonplaceholder.typicode.com/users/" . $id;

curl_setopt_array($curl, array(
  CURLOPT_URL => $url,
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

```


#### Designing our Dynaform

1. To begin, we will create a Dynaform and name it ```Axios``` .
Save and Open it.

2. Inside the ```external libs``` section, include the Axios cdn ```https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js``` like so:
![image](https://user-images.githubusercontent.com/22425217/91169702-b0613200-e6cf-11ea-94c8-f44626dfad90.png)


3. To begin designing the Dynaform, we will drag a form control of panel onto it and give it an id of ```panelTitle```, a border of zero, an html content of:

```html

<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>Axios API in ProcessMaker</h4>

</div>

```

4. Next we will create a new row of equal ```col-span``` of size ```6 6```. This will place them side by side and we now drag onto the form two button form controls side by side. The first button will have an id and name of ```btnGetPosts``` and a label of ```Get Posts``` while the second button will have an id and name of ```btnGetTodos``` and a label of ```Get Posts and Todos```.

5. Below the two buttons we will drag onto the form two panels that will be placed side by side with ```col-span``` of size ```6 6``` and will serve as headers for our result. 
The panel on the left will have an id of ```panelPostsTitle``` and will be styled thus:

```css

<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>Posts Result</h4>

</div>

```

The second panel on the will have an id of ```panelTodosTitle``` and will be styled thus:

```css

<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>Todos Result</h4>

</div>

```



6. Below the two header panels, we will drag onto the form two panels side by side with with ```col-span``` of size ```6 6``` and they will hold the results of our Posts and Todos request. 
The panel on the left will hold the result of our Posts request and will have an id of ```panelPostsResult``` and have this content:

```html

<div class="panel panel-default" id="resultPanel" style="height: 100px">
	
</div>

```

The panel on the right will hold the result of our Todos request with an id of ```panelTodosResult``` and will also have the same content as the ```panelPostsResult``` like so:

```html

<div class="panel panel-default" id="resultPanel" style="height: 100px">
	
</div>

```

7. For the next steps, we shall add the form controls for the third use case. First, below the panels with ids ```panelPostsResult``` and ```panelTodosResult``` , we will add another panel and give it an id of ```panelUserTitle``` . This will serve as the title for our next section and it will have a border of zero - 0 and the content for it is:
```html

<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>Get Single User</h4>

</div>

```

8. Right below the panel above, we will have a new column of col-span ```6 6``` . On the left column, we will drag onto the form a form control of type textbox and assign to it the variable ```userId```. The id field will automatically take the name of the variable. There is no need to change it. Give it a label of ```Enter User ID:```. 
We will enter the id of the user we want to fetch into this texbox.

9. On the right column, drag a form control of type button and give it an ```id``` and ```name``` of ```btnGetUser```. This button will be used to get the user information based on the id entered into the textbox above.

10. The last form control we shall drag onto the form is a panel which will display the user information that we fetch from the API.
This panel will have an ```id``` of ```panelUserResult``` and a border of zero - 0. The content for this panel is:
```html

<div class="panel panel-default" id="resultPanel" style="height: 100px">
	
</div>

```


Our Dynaform Designer should look like this and we should go on to edit the javascript of our Dynaform:

![image](https://user-images.githubusercontent.com/22425217/109059229-4fe59880-76e4-11eb-9e9a-130bf5dd13f4.png)



#### Writing our JavaScript
1. First off we need our constants for making ajax requests from our Dynaform to the Trigger

```javascript
const host = PMDynaform.getHostName(); /* get the hostname */
const ws = PMDynaform.getWorkspaceName(); /* get the current workspace */
const token = PMDynaform.getAccessToken(); /* get the access Token */
const app_uid = frames.app_uid ? frames.app_uid : ''; /* get the case ID */
const postsTrigUid = "5981547606035f2a5306d74085295262"; /* Trigger ID of 'Get All Posts' */
const todosTrigUid = "2269777596035f2b352c5b0067833332"; /* Trigger ID of 'Get All Todos' */

//AXIOS GLOBALS - set default global config
axios.defaults.headers.common['Authorization'] = 'Bearer ' + token;

```

2. Next we need to write a function that takes in an object and formats our result and passes it to our panel:

```javascript

function showOutput(output) {

  document.getElementById(output.id).innerHTML = `
		<pre>${JSON.stringify(output.data, null, 2)}</pre>
  `;

}

```

3. Now we write a function to make an ajax call to the ```Get All Posts``` trigger using axios

```javascript

function getPosts() {
  const url = host + "/api/1.0/" + ws + "/cases/" + app_uid + "/execute-trigger/" + postsTrigUid;
  const config = {
    headers: {
      'Content-Type': 'application/json'
    }
  };
	
  return axios({

    method: 'put',
    url: url,
    config

  })
  
}

```

4. We now call the ```getPosts()``` function when we click the button with id ```btnGetPosts```

```javascript

document.getElementById('btnGetPosts').addEventListener('click', function() {

  getPosts()
  .then(postsResponse => {
 
    showOutput({id: 'panelPostsResult', data: postsResponse.data});
    
  })

});

```

5. Next, we create the ```getTodos()``` function 

```javascript

function getTodos() {
  const url = host + "/api/1.0/" + ws + "/cases/" + app_uid + "/execute-trigger/" + todosTrigUid;
  const config = {
    headers: {
      'Content-Type': 'application/json'
    }
  };
	
  return axios({

    method: 'put',
    url: url,
    config

  })
  
}

```

### Use case 2 - Chaining multiple API requests to a Trigger

6. Here, we call the ```getPosts()``` and the ```getTodos()``` function together when we click the button with the id of ```btnGetTodos```

```javascript

/* get todos and posts */
document.getElementById('btnGetTodos').addEventListener('click', function() {
  
  Promise.all([getPosts(), getTodos()])
  .then(function (results) {
    const posts = results[0];
    const todos = results[1];
    
    showOutput({id: 'panelPostsResult', data: posts.data});
    showOutput({id: 'panelTodosResult', data: todos.data});
    
  });

});

```

When we preview the form it should look like this:
![image](https://user-images.githubusercontent.com/22425217/108971353-85599a00-7682-11eb-8787-f2454fe832dd.png)


### Use case 3 - Passing a parameter to an API 

7. For this, we shall create a javascript function called ```getUser()``` that takes in the ```id``` of the user we want to fetch:

```javascript

function getUser($id) {
  
  const url = host + "/api/1.0/" + ws + "/cases/" + app_uid + "/execute-trigger/" + userTrigUid;
  const data = JSON.stringify({ id: $id });
  const config = {
    headers: {
      'Content-Type': 'application/json'
    }
  };
	
  return axios({

    method: 'put',
    url: url,
    data,
    config

  })
  
}

```

8. Next, we call the ```getUser()``` function on click of the button with ```id``` of ```btnGetUser```

```javascript

/* get user */
document.getElementById('btnGetUser').addEventListener('click', function() {
  
  let id;
  id = $('#userId').getValue(); /* get the number inputted into the textbox */
  
  let getUserResponse = getUser(id); /* this returns a Promise */

  getUserResponse
  .then(userResponse => {
 
    showOutput({id: 'panelUserResult', data: userResponse.data});
    console.log(userResponse);
    
  })

});

```