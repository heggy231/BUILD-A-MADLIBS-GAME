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


