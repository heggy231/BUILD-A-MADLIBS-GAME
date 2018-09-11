http://jsbin.com/fuqovem/1/edit?html,output

Our mission for 1st lesson:
  1) New data type: arrays
  2) Count in JS
  3) Translating JS into HTML

- Mad Lib is a word substitution game that uses parts of speech
  ex) Give me a Noun! < Panda Bear!
  Give me a Verb! < Poop!

  * Josh asked Debbie on a "panda bear" to go "poop" with him.

  * Josh asked Debbie on a "chair" to go "bounce" with him.

  * Our JS Mad Lib will ask the user one question, and then after they answer it, a brand new question will appear on screen as if by magic!

- Mad Lib, we can either have many individual variables, OR try hold a bunch of different pieces of information in one fancy value.  Such as data type arrays.
  var array = [ thing1, thing2, thing3 ];

// List of prompts for the user
var prompts = [
  'Type your name',
  'Type an adjective',
  'Type a noun'
];

prompts variable contains an array; array

http://jsbin.com/fuqovem/2/edit?html,output
- to check if JS works, write an alert!
alert(prompts.length); // how many items are in this array.

- alert one of item in the prompt array
alert(2);
alert(name);

- To alert number or var, you put inside parentheses
alert(prompts[0]);

When built Cotter's robot, used JQuery function .css to shove the info out of JS into CSS stylesheet
 ex) $("body").css("background", randomRGBA);

- JQuery function .html move info out of JS into HTML markup.
  1) make an empty HTML container to hold the content that JS will spit out.
  <body>
  // empty HTML container to hold the content that JS
  <div class="prompt"></div> 

http://jsbin.com/fuqovem/4/edit?html,output

  * JQuery .html function:
  // find a class named .prompt; put prompt[0] content inside HTML markup.
  $('.prompt').html(prompts[0]);

  - Make it show 3rd prompts!
  $('.prompt').html(prompts[2]);
http://jsbin.com/fuqovem/5/edit?html,output

- Mission: 
1) Change which prompt shows up on screen with the click of a button
2) Figure out how to move around inside an array (so the button works!)

In the last lesson, we manually wrote .html function 
based on which prompt number we want prompts[i]
  $('.prompt').html(prompts[0]);

  - now JS will write dynamically (change) itself i of prompts[i]
    1) start with variable 
    // currentPrompt Keep track of current prompt we're on. starting at first prompt!
      var currentPrompt = 0;

    - var currentPrompt is a magic box holding a number value that's set to start off at 0.  The number can change with JS, but the name of the var will always stay the same.  
    * like the num in randomRGBA did!

    2) go back to .html function: instead of (prompts[0]), you can say (prompts[currentPrompt]).
      $('.prompt').html(prompts[currentPrompt]);

    3) Next, Add button
    <button>Next</button>
      http://jsbin.com/fuqovem/6/edit?html,output

    4) Add function to button
    // run nextPrompt function when button is clicked
    $('button').click(function() {
      nextPrompt();
    });

    Summary; when any button is clicked, run a function called nextPrompt.

    - variable nextPrompt.  It will make a 'click'ing on your button grab and display the-wait for it-next prompt!

    You've made variables that have numbers in them and variables that have arrays in them.  nextPrompt() contains a function.

    * nextPrompt() will do 2 things:
    1) Get the array number of the next prompt out of the prompts array, and into your variable currentPrompt

    2) Stick the text that corresponds to the array number of the new currentPrompt into the HTML
    
    Frame of the variable called, nextPrompt, that will change currentPrompt's value.  Wrap it around your html function.  

    // A function that will call the next prompt
    var nextPrompt = function() {
      // put first prompt in all html elements with class prompt
      $('.prompt').html(prompts[currentPrompt]);
    }

  - There's one unintended thing that 'nextPrompt' does.  Putting your 'html' function inside the 'nextPrompt' function creates dependency: The 'html' function won't push any prompt into the HTML until the 'click' calls 'nextPrompt'!

Currently button only works only once.  Next, figure out how to advance to next prompt (address the html function)

Remember how what's inside a variable changes but the variable name stay the same?  From part3 of the CSS robot, randomRGBA whose value changed every time you clicked a button.  However, name remained the same randomRGBA.

- That's what is happening to currentPrompt variable.  Click the button changes the number value inside the currentPrompt variable.

That value will change from the first item in the array(0) to the second(1), then third(2). To change the value we add +1.
// move the next prompt into variable currentPrompt
currentPrompt = currentPrompt + 1;

http://jsbin.com/fuqovem/7/edit?html,output
  - currentPrompt isn't static value; it's a box.
  Increment currentPrompt by 1! which moves the position of i to next in the array.

- Next lesson goal:
1) Make the first prompt show up before the first click
2) Give JS something useful to say when it runs out of prompts in the array.
3) Fancify your MadLibs app with CSS

We are writing JS that moves thru an array of prompts, asking the user or info.

Lesson 3 Mission: 
1) Make the first prompt visible on the page load.
2) Write 'if' statement
3) Create an alternate ending with an 'else' statement.

- Recall, after wrapping HTML function inside 'nextPrompt' the first prompt waited for a click before showing up the screen.

  // A function that will call the next prompt
  var nextPrompt = function() {
    // put first prompt in all html elements with class prompt
    $('.prompt').html(prompts[currentPrompt]);
  }

  Just defining the function isn't always enough to make it run.  Trick to make sure that the first prompt shows up right away.
  * you can tell nextPrompt to run, independently of the button, just by calling it in your script.

  All you need to do call the function is say its name.  It goes at the end of your script.
  
  // Show the 1st prompt as soon as js loads
  nextPrompt(); // calling the function 

  - The reason nextPrompt() was called at the bottom, so it read top to bottom, it doesn't know until the end what nextPrompt is (like CSS). After you tell it then JS knows.  

  