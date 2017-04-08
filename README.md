# About
Kahoot.js is a library to interact with the Kahoot API. Currently, kahoot.js supports joining and interacting with quizes.
**Installation requires Node.js 6.0.0 or higher.**<br>
![NPM](https://nodei.co/npm/kahoot.js.png)

# Basic Example
```js
var Kahoot = require('kahoot.js');
var client = new Kahoot;
console.log("Joining kahoot...");
client.join(9802345 /* Or any other kahoot token */, "kahoot.js");
client.on("joined", () => {
    console.log("I joined the Kahoot!");
});
client.on("quizStart", quiz => {
    console.log("The quiz has started! The quiz's name is:", quiz.name);
});
client.on("questionStart", question => {
    console.log("A new question has started, answering the first answer.");
    question.answer(0);
});
client.on("quizEnd", () => {
    console.log("The quiz has ended.");
});
```

## Documentation / How to use can be found in Documentation.md<br>
## Examples can be found in examples/<br>
## More examples can be found in tests/<br>
