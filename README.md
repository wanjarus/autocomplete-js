
![](https://nodei.co/npm/jquery-autocomplete-js.png?compact=true)

![](https://img.shields.io/npm/v/jquery-autocomplete-js.svg?style=flat-square)
![](https://img.shields.io/npm/l/jquery-autocomplete-js.svg?style=flat-square)
![](https://img.shields.io/npm/dm/jquery-autocomplete-js.svg?style=flat-square)

# [autocomplete-js](http://isis97.github.io/autocomplete-js/)
The simplest jQuery plugin for creating autocomplete boxes with dynamically generated suggestions.

## About
This plugin allows you to create a nice looking, working suggestion input box within seconds.
It can be easily customized and adapted to any task you want.
This plugin is based on the complete-ly.js idea by Lorenzo Puccetti.
[See autocomplete-js web page](http://isis97.github.io/autocomplete-js/)

### Motivation
This plugin was made just to create new suggestions providing library being simple and lightweight.

## Features

This plugin allows you to create suggestion box with optional description box within seconds!

## Installation

Just run `npm install jquery-autocomplete-js`.

## Usage

Just place a `<div>` element anywhere and use the javascript:

```javascript
var ac = $('#div').autocomplete({
  options: ["apple", "bannana", "strawberry", "pineapple"]
});
```

You can also directly access suggestions and input history:

```javascript
ac.options = ["nope"]; //override suggestions list
ac.historyInput = []; //clear history
```

Note that the `options` field can be a function (options provider):

```javascript
ac.options = function(autocompleteInstance, text, lastToken){ //set the options provider
  return ["nope", "lol"]; //provide the suggestions list
};
```
In this case the options provider must accept the three parameters - autocomplete object instance (`autocompleteInstance`), the input query (`text`) and the last input query token (`lastToken`).


## More advanced usage

Showing the *dropdown* list:

```javascript
var ac = $('#div').autocomplete({
  options: ["apple", "amd", "august", "amerald", "America", "amused", "a", "appendix", "application", "app"],
  showDropDown: true,
  dropDownPosition: 'bottom',
  backgroundColor: 'white'
});
```

And with fancy little description box:

```javascript
ac.options = [
  {
      name: "option name", //Option name
      description: "option description", //Description text
      html: true //Use HTML code in the description
  }
]; //advanced suggestions list
```


To display the suggestions descriptions you have to enable the suggestions dropdown list by
setting the `showDropDown` constructor field to `true`. You can also set its position (top or bottom).
And modify some of its display properties.

```javascript
var ac = $('#div').autocomplete({
  options: [
    {
      name: "apple",
      description: "a <b>fruit</b>",
      html: true
    },
    "amd", "august", "amerald", "America", "amused", "a", "appendix", "application", "app"
  ],
  showDropDown: true,
  dropDownPosition: 'bottom',
  backgroundColor: 'white'
});
```

You can also enable history and add some event handlers:

```javascript
var ac = $('#div').autocomplete({
  options: [
    {
      name: "apple",
      description: "a <b>fruit</b>",
      html: true
    },
    "amd", "august", "amerald", "America", "amused", "a", "appendix", "application", "app"
  ],
  showDropDown: true,
  dropDownPosition: 'bottom',
  backgroundColor: 'white',
  onConfirmed: function(obj, text) {
    alert(obj.pullText());
  },
  onChanged: function(obj, text) {
    $('#output').html('<span>Input has changed. ('+text+')</span><br>');
  },
  onHistoryBrowsed: function(obj, hist) {
    $('#output').html('<span>History called ('+hist.join(',')+')</span><br>');
  }
});
```

## Simple methods

Just a little amount of the useful methods:


| Method name         | Description                                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------|
| `disable()`         | Disables all autocompletion suggestions (should be probably followed by `repaint()`)                                                     |
| `enable()`          | Enables all autocompletion suggestions (see `disable()`) (should be probably followed by `repaint()`)                                                  |
| `isEnabled()`       | Tests if the autocompletion suggestions are enabled (see `disable()` or `enable()`)                                                     |
| `hideDropDown()`    | Hides a drop down suggestions list by force.                                                                |
| `getOptions()`      | Returns the options array (if the `options` field set manually or/and by the constructor is `Function` type, then the array generated by it will be returned).                                                                |
| `showDropDown()`    | Shows a drop down suggestions list by force.                                                                |
| `getText()`         | Obtains the input text.                                                                            |
| `pullText()`        | Obtains the input text and clears it.                                                                            |
| `setText(String)`   | Sets the input text.                                                                               |
| `repaint()`         | Refreshes the autocomplete box.                                                                    |
| `getInputHistory()` | Get the input history array.                                                                       |
| `onHistoryNext()`   | Simulate a history browsing event.                                                                 |
| `onHistoryPrev()`   | Simulate a history browsing event.                                                                 |

All functions except these returning strings or any other special values returns the instance of the autocomplete provider, so they can be chained easily.

## Constructor properties

The autocomplete instance is created with:
```javascript
var instance = $('div.my-autocomplete').autocomplete({
  /*Constructor properties*/
});
```

Here is a list of all available initial properties:

| property                         | type                                                  | default value   | meaning                                                                     |
|----------------------------------|-------------------------------------------------------|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `onKey`                          | Handler - `function(jQuery.Event)`       | empty function  | Key input handler. It should be the function accepting one parameter - jQuery event object. The function will be called each time the user will press any non-special key (not arrows and enter) - can be used with `isDisabled` option to disable autocompletion at startup and then call `enable()` to enable the autocompletion on the specified key combination. |
| `onConfirmed`                    | Handler - `function(autocompleteInstance, String)`    | empty function  | Input confirmation handler. It should be the function accepting two parameters - autocomplete object instance and the captured value of the field. The function will be called each time the user hits enter. |
| `onChanged`                      | Handler - `function(autocompleteInstance, String)`    | empty function  | Input change handler. It should be the function accepting two parameters - autocomplete object instance and the captured value of the field. The function will be called each time the user changes anything with the input (key press, text change etc.). |
| `onHistoryBrowsed`               | Handler - `function(autocompleteInstance, String[])`  | empty function  | History browsing handler. It should be the function accepting two parameters - autocomplete object instance and the array containing the input history. The function will be called each time the user uses the history browsing. |
| `isDisabled`                     | Bool                                                  | false           | Disables autocompletion function when at initialization (can be used with `onKey` to enable autocompletion only when specified key combination was made) |
| `showDropDown`                   | Bool                                                  | false           | Enables the dropdown suggestion list                                        |
| `dropDownPosition`               | String                                                | 'bottom'        | Sets the dropdown position (top/bottom).                                    |
| `inputWidth`                     | String                                                | 100%            | CSS width of the input box                                                  |
| `dropDownWidth`                  | String                                                | 50%             | CSS width of the dropdown list                                              |
| `dropDownDescriptionBoxWidth`    | String                                                | 50%             | CSS width of the dropdown list description box                              |
| `fontSize`                       | String                                                | null            | CSS size of the text                                                        |
| `fontFamily`                     | String                                                | null            | CSS font family                                                             |
| `formPromptHtml`                 | String                                                | ''              | HTML code for the prompt                                                    |
| `color`                          | String                                                | null            | Text color                                                                  |
| `hintColor`                      | String                                                | null            | Text color of the suggestion hint                                           |
| `backgroundColor`                | String                                                | null            | CSS background color for the dropdown                                       |
| `dropDownBorderColor`            | String                                                | null            | CSS suggestions drop down border color                                      |
| `dropDownZIndex`                 | Integer                                               | 100             | CSS z-index of the drop down list.                                          |
| `dropDownOnHoverBackgroundColor` | String                                                | null            | CSS background color of the selected drop down suggestion item              |
| `enableHistory`                  | Bool                                                  | true            | Enable browsing the input history.                                          |
| `inputHistory`                   | Array                                                 | []              | Override the input history.                                                 |
| `classes.input`                  | String                                                | null            | Set the class name for the input component.                                 |
| `classes.dropdown`               | String                                                | null            | Set the class name for the drop down component.                             |
| `classes.descriptionBox`         | String                                                | null            | Set the class name for the drop down description box component.             |
| `classes.hint`                   | String                                                | null            | Set the class name for the hint text component.                             |
| `classes.wrapper`                | String                                                | null            | Set the class name for the wrapper component.                               |
| `classes.prompt`                 | String                                                | null            | Set the class name for the prompt component.                                |
| `classes.hoverItem`              | String                                                | null            | Set the class name for the hovered suggestions list item.                   |
| `classes.row`                    | String                                                | null            | Set the class name for the suggestions list row.                            |
| `maxSuggestionsCount`            | Integer                                               | 100             | Set the maximum suggestion entries number.                                  |
| `suggestionBoxHeight`            | String                                                | 75px            | CSS height of the suggestion box.                                           |
| `options`                        | Array                                                 | {}              | All strings that will be displayed as suggestions for the input box.        |
| `blockEvents`                    | Bool                                                  | true            | Blocks the events propagation - if the enter is pressed only the `onConfirmed` handler is invoked and the key event is not further propagated. |


## The autocomplete fields

Here is the list of all useful autocomplete methods and fields:

| Field                   | Type          | Meaning                                                                        |
|-------------------------|---------------|--------------------------------------------------------------------------------|
| `startFrom`             | Integer       | The index the input string is matched from for suggestions                     |
| `options`               | Array         | All string suggestions.                                                        |
| `inputHistory`          | Array         | History of the input.                                                          |
| `dropDown`              | JQuery object | The drop down component.                                                       |
| `formPrompt`            | JQuery object | The propmpt component                                                          |
| `hint`                  | JQuery object | The hint component                                                             |
| `input`                 | JQuery object | The input box object                                                           |
| `formWrapper`           | JQuery object | The wrapper component.                                                         |
| `historyBrowsingActive` | Bool          | The bool value indicating if the user currently is browsing the input history. |
| `historyIndex`          | Integer       | The currently browsed history index.                                           |
