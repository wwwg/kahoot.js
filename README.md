# About
Kahoot.js is a library to interact with the Kahoot API. Currently, kahoot.js supports joining and interacting with quizes.
***Installation requires Node.js 6.0.0 or higher.***

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

# Documentation

## Classes

### Kahoot 
Kahoot client that can interact with quizes.

**Events**<br>
`on('ready')`, `on('join')` - Emitted when the client joins the game.<br>
`on('quizStart', Quiz)`, `on('quiz', Quiz)` - Emitted when the quiz starts for the client. Passes a `Quiz` class.<br>
`on('question', Question)` - Emitted when the client recieves new question. This is NOT the same as the `questionStart`<br> event, which is emitted after the question has started. Passes a `Question` class.<br>
`on('questionStart', Question)` - Emitted when a question starts. Passes a `Question` class.<br>
`on('questionSubmit', QuestionSubmitEvent)` - Emitted when your answer has been submitted. Passes a `QuestionSubmitEvent` class.<br>
`on('questionEnd', QuestionEndEvent)` - Emitted when a question ends. Passes a `QuestionEndEvent` class.<br>
`on('finish', QuizFinishEvent)` - Emitted when the quiz ends. Passes a `QuizFinishEvent` class.<br>
`on('finishText', FinishTextEvent)` - Emitted when the quiz finish text is sent. Passes a `FinishTextEvent` class.<br>
`on('quizEnd')`, `on('disconnect')` - Emitted when the quiz closes, and the client is disconnected.<br>
<br>
**Methods**<br>
`join(sessionID, playerName)`<br>
Parameters:<br>
*sessionID (number)* - The Kahoot session ID to join.<br>
*playerName (string)* - The name of the user.<br>
Returns: Promise<br>
`answerQuestion(id)`<br>
Parameters:<br>
*id (number)* - The ID of the question to answer. (0 is the first answer, 1 is the second answer, etc.)<br>
Returns: Promise<br>
`leave()`<br>
Returns: Promise<br>
<br>
**Properties**<br>
`sendingAnswer (boolean)` - Whether or not the client is currently sending an answer.<br>
`token (String)` - The client token of the user.<br>
`sessionID (Number)` - The the session ID of the quiz.<br>
`name (String)` - The user's name.<br>
`quiz (Quiz)` - The current quiz of the client.<br>
`nemesis (Nemesis)` - The client's nemesis. (Will be `null` if the client does not have a nemesis.)<br>
`nemeses (Nemesis Array)` - An array of all the client's past nemeses.<br>

### Quiz

**Properties**<br>
`client (Kahoot)` - The client the quiz is attached.<br>
`name (String)` - The name of the quiz.<br>
`type (String)` - The quiz type.<br>
`currentQuestion (Question)` - The current question the quiz is on.<br>
`questions (Question Array)` - An array of every single question in the quiz. New questions get added as they come in.<br>

### Question

**Methods**<br>
`answer(number)`<br>
Parameters:<br>
*number (Number)* - The question number to answer. (0 is the first answer, 1 is the second answer, etc.)<br>

**Properties**<br>
`client (Kahoot)` - The client attached to the question.<br>
`quiz (Quiz)` - The quiz that the question for.<br>
`index (Number)` - The index of the question.<br>
`timeLeft (Number)` - The time left in the question.<br>
`type (String)` - The question type.<br>
`usesStoryBlocks (Boolean)` - Whether or not the question uses 'Story Blocks'.<br>
`ended (Boolean)` - Whether or not the question has ended.<br>
`number (Number)` - The number of the question.<br>

### QuestionEndEvent

**Properties**<br>
`client (Kahoot)` - The client attached to the event.<br>
`quiz (Quiz)` - The quiz that the event is attached to.<br>
`question (Question)` - The question that the event is attached to.<br>
`correctAnswers (String Array)` - A list of the correct answers.<br>
`correctAnswer (String)` - The correct answer. (if there are multiple correct answers, this will be the first in the array.)<br>
`text (String)` - The text sent by Kahoot after a question has finished.<br>
`correct (Boolean)` - Whether or not the client got the question right.<br>
`nemesis (Nemesis)` - The client's nemesis. (Will be `null` if the client does not have a nemesis.)<br>

### QuestionSubmitEvent

**Properties**<br>
`message (String)` - The message sent by Kahoot after you sent in an answer.<br><br>
`client (Kahoot)` - The client attached to the event.<br>
`quiz (Quiz)` - The quiz attached to the event.<br>
`question (Question)` - The question attached to the event.<br>

### Nemesis

**Properties**<br>
`name (String)` - The name of the nemesis user.<br>
`id (Number / String)` - The client ID of the user<br>
`score (Number)` - The score of the nemesis user.<br>
`isKicked (Boolean)` - Whether or not the nemesis user is kicked or not.<br>
`exists (Boolean)` - Whether or not the nemesis exists (All other values will be `undefined` if this is `false`)<br>

### FinishTextEvent

**Properties**<br>
`firstMessage (String)` - The first finishing message sent by Kahoot.<br>
`secondMessage (String)` - The second message sent by Kahoot. (this property will be `undefined` if a second message was not sent.)<br>
`messages (String Array)` - An array of the messages sent.<br>
`metal (String)` - The medal recieved after the quiz.<br>

### QuizFinishEvent

**Properties**<br>
`client (Kahoot)` - The client attached to the event.<br>
`quiz (Quiz)` - The quiz attached to the event.<br>
`players (Number)` - The number of players on the quiz.<br>
`quizID (String)` - The ID of the quiz.<br>
`rank (Number)` - The client's ranking on the quiz.<br>
`correct (Number)` - The number of questions that were scored correct.<br>
`incorrect (Number)` - The number of questions that were scored incorrect.<br>
