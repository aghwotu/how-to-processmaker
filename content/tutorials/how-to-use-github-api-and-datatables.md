---
title: "How to Use Github Api and Datatables"
date: 2020-07-11T14:56:51+01:00
weight: 1
draft: 
---


 One of the requirements you may have for a grid in ProcessMaker is the ability to search through records and arrange columns in ascending or descending order. This is where [DataTables](https://datatables.net/) comes in. It is a library that will allow you to do this easily. 

#### Variable

Our first step is to create a string variable and name it ```hiddenUserList```. 

#### Trigger
Next, we create a [trigger](https://wiki.processmaker.com/3.0/Triggers) and name it ```Get List of Users```

Inside the trigger, we will write the code to call the [GitHub API to list users](https://developer.github.com/v3/users/#list-users).


{{% notice note %}}
To learn more about GitHub APIs you can visit the [GitHub Developer](https://developer.github.com/) page
{{% /notice %}}


```php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.github.com/users?since=135",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
));

$response = curl_exec($curl);

curl_close($curl);

/*
assign the json_encode() $response to the hiddenUserList variable
*/

@@hiddenUserList = json_encode($response);

``` 


#### Dynaform
We will now create a Dynaform and name it ```GitHub Users``` and open it.

1. In the Dynaform, drag a hidden form control and assign the ```hiddenUserList``` to it. It will contain the list of users.


2. Inside the Dynaform, we will add a [panel](https://wiki.processmaker.com/3.0/Panel_Control). 
Give the panel an id name of ```panelTitle``` 
and then, insert this html code to style the panel:

```html
<div>
    <!-- panelTitle content -->
</div>
``` 


3. We then drag another panel onto the form and give it an id of ```panelTable```. This panel will hold our DataTable. Add this html code in the panel.

```html
<div>
    <!-- panelTable content -->
</div>
``` 


4. In the Dynaform javascript editor, we  we will add the following code snippets


```javascript

const tableInfo = {tableId: "", tableListId: "", hasButtons: true};

$(document).ready(function() {

    getTableList();

});
``` 

 Then we add this function outside the ```$(document).ready(function(){});``` block. The function accepts an object

```javascript
function getTableList(tableObject) {

}
```