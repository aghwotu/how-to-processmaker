---
title: "How to Use Github Api and Datatables"
date: 2020-07-11T14:56:51+01:00
weight: 1
draft: 
---


 One of the requirements you may have for a grid in ProcessMaker is the ability to search through records and arrange columns in ascending or descending order. This is where [DataTables](https://datatables.net/) comes in. It is a library that will allow you to do this easily. We will get the data from GitHub api and display in the DataTable.

#### Variable

Our first step is to create a variable of type string and name it ```hiddenUserList```. 

#### Trigger
Next, we create a [trigger](https://wiki.processmaker.com/3.0/Triggers) and name it ```Get List of Users```

Inside the trigger, we will write the code to call the [GitHub API to list users](https://developer.github.com/v3/users/#list-users). For the ```User-Agent``` ```CURLOPT_HTTPHEADER```, use your GitHub username. This will allow GitHub to contact you if there are problems, as stated here in their [documentation](https://developer.github.com/v3/#user-agent-required). This is the code to make the API call:   



```php

$curl = curl_init();

curl_setopt_array($curl, array(
    CURLOPT_URL => "https://api.github.com/users",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => "",
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => "GET",
    CURLOPT_HTTPHEADER => array(
        "Accept: application/vnd.github.v3+json",
        "User-Agent: your-github-username"
    ),
));

$response = curl_exec($curl);

curl_close($curl);

/*
assign the $response to the hiddenUserList variable
*/

@@hiddenUserList = $response;

``` 

{{% notice note %}}
To learn more about GitHub APIs you can visit the [GitHub Developer](https://developer.github.com/) page
{{% /notice %}}


#### Dynaform
Next we will create a Dynaform and name it ```GitHub Users``` and open it.

1. In the external libs of the Dynaform, we need the DataTable CDN

```javascript
https://cdn.datatables.net/1.10.9/js/jquery.dataTables.min.js,

https://cdn.datatables.net/1.10.9/css/jquery.dataTables.min.css

```


2. Next we drag a hidden form control and assign the ```hiddenUserList``` variable to it. It will hold the list of users.


3. Inside the Dynaform, we will add a [panel](https://wiki.processmaker.com/3.0/Panel_Control). 
Give the panel an id name of ```panelTitle``` 
and then, insert this html code to style the panel:

```html
<div style="background:#286090; 
            color:#fff; 
            text-align:center; 
            padding-top: 12px; 
            padding-bottom: 15px; 
            margin-top: 37px;" 
     
     class='container-fluid jumbotron'>

  <h4>List of Users</h4>

</div>
``` 


4. We then drag another panel below the first panel and give it an id of ```panelTable```. This panel will hold our GitHub users and this is the html code for the table:

```html
<table id="tableUserList" class="display table table-striped table-bordered" width="100%" >

</table>
``` 

![image](https://user-images.githubusercontent.com/22425217/90296523-a9daeb00-de83-11ea-9f68-ed2c6af1b74c.png)



5. In the Dynaform javascript editor, we  we will add the following code snippets as shown in the image below 
![image](https://user-images.githubusercontent.com/22425217/90296701-253c9c80-de84-11ea-82cd-b2eac05f9676.png)



```javascript

const usersInfo = {hiddenListId: "hiddenUserList", dataTableId: "tableUserList"};

$(document).ready(function() {

    getList(usersInfo);

});
``` 

 Then we write the ```getList()``` function under the ```$(document).ready(function(){});``` block. 

```javascript
function getList(tableObject) {  
  
  //here we get the list of users from the hidden variable
  let userList = $('#'+ tableObject.hiddenListId +'').getValue();
  
  userList = JSON.parse(userList);
    
  //here we insert the list of users to to the table
  const table = $('#'+ tableObject.dataTableId +'').DataTable( {
    data: userList,
    columns: [
      
      { data: "id" , title: "ID"},
      { data: "login" , title: "LOGIN"},
      { data: "node_id" , title: "NODE_ID" },
      { data: "avatar_url" , title: "AVATAR_URL"},
      { data: "gravatar_id" , title: "GRAVATAR_ID" },
      { data: "url" , title: "URL" },
      { data: "html_url" , title: "HTML_URL" },
      { data: "followers_url" , title: "FOLLOWERS_URL" },
      { data: "gists_url" , title: "GISTS_URL" },
      { data: "starred_url" , title: "STARRED_URL" },
      { data: "subscriptions_url" , title: "SUBSCRIPTIONS_URL" },
      { data: "organizations_url" , title: "ORGANIZATIONS_URL" },
      { data: "repos_url" , title: "REPOS_URL" },
      { data: "events_url" , title: "EVENTS_URL" },
      { data: "received_events_url" , title: "RECEIVED_EVENTS_URL" },
      { data: "type" , title: "TYPE" },
      { data: "site_admin" , title: "SITE_ADMIN" }
    ]

  } );
    
    

}
```


#### Putting it all Together
Place the ```Get List of Users``` trigger before the ```GitHub Users``` dynaform

![image](https://user-images.githubusercontent.com/22425217/90297242-c2e49b80-de85-11ea-9779-c988659be610.png)


When you run the case, this is what you will get:

![image](https://user-images.githubusercontent.com/22425217/90297429-53bb7700-de86-11ea-93eb-0870f13a2316.png)

