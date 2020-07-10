## How to ProcessMaker

These are resources, links and code snippets that can be used for [ProcessMaker](https://www.processmaker.com/)

The website is [hosted on Netlify](https://how-to-processmaker.netlify.app/)

## Motivation

This project was created as a guide to help me document code snippets that have been useful to me when writing code in ProcessMaker

## Screenshots


## Tech/framework used
<b>Built with</b>
- [Hugo](https://gohugo.io/)

## Features
- It includes code snippets for working with ProcessMaker Dynaform controls

## Code Example
For example if you want to hide multiple form controls, you can do this
```javascript
//this accepts an array of textbox ids
function hideMultipleElements(arrInput) {
    arrInput.forEach(hideElementId); 
    function hideElementId(item, index) {
      return $("#" + item ).hide();
    }
}

let formControls = ["textboxId", "textareaId", "gridId"]; //ids of the form controsls

hideMultipleElements(formControls); //pass the formControls[] array into the hideMultipleElements() function
```
<!-- Show what the library does as concisely as possible, developers should be able to figure out **how** your project solves their problem by looking at the code example. Make sure the API you are showing off is obvious, and that your code is short and concise. -->

## Installation
Provide step by step series of examples and explanations about how to get a development env running.

## API Reference

Depending on the size of the project, if it is small and simple enough the reference docs can be added to the README. For medium size to larger projects it is important to at least provide a link to where the API reference docs live.

## How to use?
If people like your project they’ll want to learn how they can use it. To do so include step by step guide to use your project.

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## Support
Link to the processmaker forum

## Credits
Give proper credits. This could be a link to any repo which inspired you to build this project, any blogposts or links to people who contrbuted in this project. 

#### Anything else that seems useful

## License
A short snippet describing the license (MIT, Apache etc)

MIT © [Yourname]()