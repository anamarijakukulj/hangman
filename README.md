# hangman

Intro
Your assignment will be to create a clone of the classic hangman game. If by any chance you haven’t
played hangman before, here is the description on Wikipedia:
https://en.wikipedia.org/wiki/Hangman_(game)
And here is an example:
https://www.hangmanwords.com/play/custom?g=VGhpcyUyMGlzJTIwYW4lMjBleGFtcGxlJTIwaG
FuZ21hbiUyMGdhbWUu
[the solution to this particular example is “This is an example hangman game”]
Basic flow/specification
1. The first screen should prompt the user for the name (this is required for continuing). After
the name is submitted, the game proceeds to the next screen
2. Fetch the text of the puzzle by sending a GET request to api.quotable.io/random
This will fetch a random quote from a famous person.
3. The game screen itself should contain a button for restarting - this fetches a new quote, and
restarts the game.
You don’t have to bother with drawing the hangman (you can if you like) - what is important
is to keep count of the number of errors (and have it presented to the user the whole time).
Note that only letters should be masked at the beginning (commas, apostrophes, and other
special characters should be shown as-is, and the user should not need to input them). Also,
the game should be case-insensitive - if the user enters the letter “b” (uppercase or
lowercase), all of the “B” and “b” should be uncovered.
Feel free to choose your own mechanism for entering the letters (with keyboard, or selecting
them with the mouse from screen or both... )
4. When the user successfully finishes the game, you should send the scoring data by making a
POST request to:
https://my-json-server.typicode.com/stanko-ingemark/hang_the_wise_man_frontend_tas
k/highscores
The Content-Type should be ‘application/json’. The body should have the following data:
{
“quoteId”: <string, the id of the quote you fetched in phase 2 from api.quotable.com>,
“length”: <integer, length of the quote>,
“uniqueCharacters”: <integer, number of unique letters in the quote, disregarding the case>,
“userName”: <string, name the user entered in step 1>,
“errors”: <integer, number of errors user did before finishing the game>,

“duration”: <integer, number of milliseconds it took for the game to finish>`
}
Note that although you’ll get a status of 201 on successful request, don’t be confused if your score is
not persisted (this isn’t implemented for this test).
5. After sending the scoring data, you should get the current high scores by sending the GET
request to
https://my-json-server.typicode.com/stanko-ingemark/hang_the_wise_man_frontend_tas
k/highscores
On the last screen of the game, you should display the high score table. Every entry consists of a user
name and score.
Score is calculated as (100/1+<number of errors>). Highscore table should be ordered by score.
Submission and technical requirements
Share your solution on Github, Bitbucket, or Gitlab. In the root of the solution there should be a
README file with clear instructions for installation and running.
The solution should be implemented in React, using axios for HTTP requests and redux for state
management. Feel free to use other libraries if you need them.
Visual design and style are entirely up to you.
Bonus
Design and implement the “smarter” function for calculating the score. It should accept the following
parameters:
● quote length (integer, L)
● number of unique letters in the quote (integer, U)
● number of errors (integer, E)
● solving time (integer, T)
And return a positive number. Higher numbers mean better scores.
The function should have the following characteristics:
● it’s pure (no side-effects), the output should depend entirely on the above-mentioned input
parameters
● score of the solution with fewer errors should always be higher than for the solution with
more errors
● given the same number of errors, solutions with larger numbers of unique letters should be
scored higher
● given the same number of errors and unique letters, longer solutions should be scored higher

● given the same number of errors, unique letters, and quote length, faster solutions should be
scored higher
Illustrate each of the characteristics (except the function being pure) with one or more unit tests. You
can use the test runner/framework of your choice. Include the instructions for running the tests in
the README file.
