## How to ProcessMaker

These are resources, links, tutorials and code snippets that can be used for [ProcessMaker](https://www.processmaker.com/)

The website is [hosted on Netlify](https://how-to-processmaker.netlify.app/)

## Motivation

This project was created as a guide to help me document code snippets written by myself and other developers that have been useful to me when writing code in ProcessMaker

## Screenshots
![image](https://user-images.githubusercontent.com/22425217/87207385-b360b880-c303-11ea-98ff-e2666fd5cebc.png)


## Tech/framework used
<b>Built with [Hugo](https://gohugo.io/)</b>


<!-- ## Features
- It includes code snippets for working with ProcessMaker  -->

## Code Example
Code snippet showing you how to hide multiple form controls:
```javascript
//this accepts an array of textbox ids
function hideMultipleElements(arrInput) {
    arrInput.forEach(hideElementId); 
    function hideElementId(item, index) {
      return $("#" + item ).hide();
    }
}

let formControls = ["textboxId", "textareaId", "gridId"]; //ids of the form controls

hideMultipleElements(formControls); //pass the formControls[] array into the hideMultipleElements() function
```


## Installation
- https://wiki.processmaker.com/3.0/Windows_Manual_Installation
<!-- Provide step by step series of examples and explanations about how to get a development env running. -->


## How to use?
You can include the functions you need in your ProcessMaker editor

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## Support
For help with ProcessMaker related issues, you can make a post on the [ProcessMaker forum](https://forum.processmaker.com/)

## Credits
Some of the javascript functions was written by [Oladipupo O. Fredrick](https://github.com/fredpen)

#### Useful Resources
- [ProcessMaker Wiki](https://wiki.processmaker.com/)
- [Business Process Automation with ProcessMaker 3.1: A Beginner’s Guide](https://www.amazon.com/dp/B077WBMRSL/ref=cm_sw_r_tw_dp_x_aYEaFbNK8ZRGS) by [Dipo Majekodunmi](https://medium.com/@dipomajek) on Amazon

## License
A short snippet describing the license (MIT, Apache etc)

MIT © [Yourname]()