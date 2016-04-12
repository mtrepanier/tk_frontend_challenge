### Password Importer Challenge

Many password managers offer a way of exporting your data to import it into another password manager. Your task is to build a password importer. You will be given data exports from three different password managers (Dashlane, 1Password & LastPass), will convert these into a standard format, and present the formatted data in a UI.

### Importer Object Specification

Write the importer as a function that accepts 2 arguments:

* The first argument is the raw data as a string (the password manager export file)
* The second argument is a string that designates the type of importer to use (e.g. 'dashlane', '1password', 'lastpass')

Your function will then return a Promise that when resolved, returns the data in a curated format.

```
importer(data, 'dashlane')
  .then(function(data) {
    console.log(data); // Formatted output
  });
```

Internally, the importer should implement a strategy pattern where each parser is implemented as a seperate
constructor function conforming to a shared interface. The interface consists of only 2 functions, validate() and parse().
Ex:

```
function Parser() {}
Parser.prototype.parse = function(rawInput) {
  throw new Error('not implemented')
};
Parser.prototype.validate = function(row) {
  throw new Error('not implemented')
};
```
parse() is the main function that will be called by the Importer object and provided the raw input as an argument.
While processing the input rows, the parser will use validate() on each row to make sure it conforms to all the rules
specified in the `Data processing requirements` section below. Make sure that your concrete implementations inherit from
the Parser interface and not modify it directly. Finally, make sure rows that fail validation are output as well
and shown in the UI as explained below.


### Output Format

```
[{
  name: 'Facebook',
  url: 'https://facebook.com',
  username: 'Jon Snow',
  password: 'iknownothing'
}, {
  name: 'Twitter',
  url: 'http://twitter.com/login',
  username: 'eddardstark@gmail.com',
  password: 'iamseanbean'
}]
```

### Data processing requirements
* Some fields will have bad data, you must handle this elegantly through the UI.
* Reject records that do not have a URL.
* Missing data in input fields should have empty strings in the output, except for the name field, which should be created by using the URL field.
* The URL field should conform to _very basic_ url validation like having a protocol and a TLD.

### UI

You must present the formatted data by integrating the UI provided in the Photoshop file. A user should be able to filter, select/deselect specific passwords. Clicking "Migrate" should log the user's selected passwords to the console.

## Requirements

* Commit every hour you are working on this, to allow us to see your approach and progress.
* You are allowed to use open source code.
* You are not allowed to use yeoman generators.
* Obviously, you need to solve the problem using javascript.
* You *must* use a module bundler like Browserify or Webpack, and make sure it accepts CommonJS modules.
* Your code must run entirely in the browser.
* Your test suite must run in the browser.
* If you have any knowledge of technologies we use (Marionette, Backbone, Handlebars, etc.), it definitely can be a good thing to use them to showcase your skill.
* You *must* use a CSS pre-precessor of your choice (Sass, Less, etc.)

### What we're going to look at

* Code quality
* Tests (Core logic + Views)
* How you choose to approach the problem
* If your code actually works

### Included files

* `exports/dashlane.csv` - Dashlane export
* `exports/1password.txt` - 1Password export
* `exports/lastpass.html` - Lastpass export
* `ui/import-passwords.psb` - If you have Photoshop
* `ui/import-passwords.png` - If you don't have Photoshop