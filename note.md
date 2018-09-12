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

- Right now, your nextPrompt function runs forward thru the items in your prompts array.  It doesn't know what to do when it hits the last thing in the array.  This is where we tell it!
Mission: nextPrompt needs to:
  1) Find out if it is at the end of prompt array
  2) Move the next prompt into var currentPrompt (done)
    currentPrompt = currentPrompt + 1;
  3) Stick the new currentPrompt into HTML (done)
    part from nextPrompt() = $('.prompt').html(prompts[currentPrompt]);

    $('button').click(function() {
      nextPrompt();
    });

  4) Inform the user when it runs out of new prompts

1) Find out if it is at the end of prompt array
  - Is there another prompt?  
    yes: display the next prompt in the page's HTML
    no: display a message that no more prompts are available.

  Convert this into JS language.
    IF there is another prompt, show the next prompt.  If not, do something ELSE

    if (something) {
      // do this;
    } else {
      // do this instead;
    }
  
  - Add an if statement to your function:
  if (something), {
    run code in the 
    nextPrompt
    function
  }

  - Add else statement
  var nextPrompt = function() {
    // if there is a next prompt
    if () {
      // put first prompt in all html elements with class prompt
      $('.prompt').html(prompts[currentPrompt]);
      // move the next prompt into variable currentPrompt
      currentPrompt = currentPrompt + 1;
    // or else if we're at the end of the array
    } else {

    }
  }
http://jsbin.com/fuqovem/10/edit?html,output

- If there is another prompt..
  How can JS figure out if there are more prompts coming up next?
  * use length property of array! if the number held in currentPrompt is smaller than the total number of prompts.
  var currentPrompt = 0;
  if (currentPrompt < prompts.length) {}

  - this is saying if 0 is less than 3, do something.  true 
  - This is how this dash slides work, we have 'slide.lenght' var that advances the 'nextSlide'.  When it hits end, JS makes it rain!

  - What does JS do when currentPrompt is less than length?
    It runs hmtl function inside nextPrompt then adds 1 to currentPrompt

    At the last prompt >= length, else stmt that pushes "no more prompts" into .prompt class
    else {
      $('.prompt').html("no more prompts");
    }

Summary: 
  3 things happen as you run JS:
  1) A variable defines the contents of prompts array, with a length of 3.
  2) currentPrompt gets set to 0.
  3) The nextPrompt function is run.

- NextPrompt does this:
(the first time it runs, when currentPrompt = 0)
1. Is 0 < prompt.length? yes
2. Put prompt number 0 in HTML ('Type your name')
3. Then add 1 to 0! (this changes currentPrompt to 1)

- Next lesson, you'll learn 
1. Form fields, use them to capture responses for each prompt
2. Make JS remember the answers your users type into the forms.

Interactive Mad Lib game.  Currently, it holds three questions and displays them as your player interacts with the game.  Now we want user inputs.

- Mission:
1) Code up a place for the answers to each prompt to go!
2) Tell JS to remember those answers
3) Modify your else stmt to display the user-provided answers when it runs out of prompts.

1) Code up a place for the answers to each prompt to go!
  - 2 parts to collecting user info
    1) form field with HTML <input type="email">
      User can type in info but the data evaporates as they submit
      - let's put form field in HTML-JS
      // add (+) a line break (<br>) after the prompt, and stick a form field (<input>) on the new line.
      $('.prompt').html(prompts[currentPrompt] + '<br><input type="text">');

http://jsbin.com/fuqovem/13/edit?html,output

- What happens to what you type? It disappears.  Tell JS to grab the stuff and hold on to it! store.  Like prompts array to hold prompts, catch answers in answers array!  Set up an empty array.
  // here's an array to keep answers in
  var answers =[];

 2) Tell JS to talk to input field and answer array need to exchange info.
 '<br><input type="text">' and var answers =[]; need to talk to eachother!

 - Meet .val(): The same way you alert length of an array to make sure there were things in it, we can use a JQuery method called .val() to give us the value contained in the input field.  
	  // alert the .val of the form
	  alert($('input').val());
  // note $ dollar sign is shorthand that says "this thing is a JQuery object!"
  Add this alert before an empty form gets added to your page.

When running, alert box says "undefined" why?
  When JS 1st loads up on the page, the input field is empty!  There's nothing in it, so there's nothing for JS to alert!  But the field exists, and undefined acknowledges that by helpfully telling you that there's no content in it.

  Now, dismiss the first undefined window.  Enter your name, see your name alert back to you!
  Whatever you typed shows up!

- Now that we know asking .val() stores the content of input really does work.
  $('input').val()
http://jsbin.com/fuqovem/14/edit?html,output

  Let's delete
  > alert($('input').val());

- JS you wrote can grab any value that's typed into the input field, but how can you tell it to push that content into the array called answers?

  answers.push($('input').val());

  Translation: "push the value from the HTML <input> tag into the answers array."

  But we don't want it every time! (the very first time, input's val is undefined!)
    if (currentPrompt != 0) {
      answers.push($('input').val());
    }
    // if statement that will only push an answer if you have an answer to push.

  if the currentPrompt is not zero, grab the contents of the input field, and stash it in the answers array:
    if (currentPrompt != 0) {
      answers.push($('input').val());
    }
  JS uses an ! exclamation point (bang) to mean the opposite of: Not, No, IS Not, Do Not

Add an alert to your else statement.  It should pop up everything in the answers array at the end of the prompts array.
  } else {
    $('.prompt').html("no more prompts here");
    alert(answers);

What happens at the end?? the last answer doesn't show up!

- Final step: Concatenation: smashing things together
  var randomRGBA = 'rgba('+red+','+green+','+blue+', 1)';
  // from background color changing in CSS robot lesson: ex concatenation

  - put together new concatenated variable that goes inside of HTML body!
When function showFinal is run, display answer 0 and a space and answer 1 and a space and answer 2 in the .prompt of your html.

// puts the user's input into the html
var showFinal = function() {
  $('.prompt').html(answers[0]+' '+answers[1]+' '+answers[2]);
}

- currently, we have not made showFinal run. "When a function called showFinal is run.."  When and where should showFinal appear on the screen?
- You run a function just by saying its name. showFinal();

  We want the answers to show up when there are no more prompts left.

  else {
    // runs showFinal to put the answers in HTML body
    showFinal();
  }

http://jsbin.com/fuqovem/15/edit?html,output

Mission: 
1) Learn a sneaky new JS function that makes HTML elements vanish!
2) Connect player answers into a real Mad Libs story
3) Add some CSS to make the app styling!

- The next button should vanish once prompts have been answered!
JQuery has function
var showFinal = function () {
  $('.prompt').html(answers[0]+' '+answers[1]+' '+answers[2]);
  $('button').hide();
}

* hide() function in JQuery is similar to the toggle() function you used in Esha's and Cotter's projects.  There is also show() function in JQuery!

- Connect the dots: 
  Last lesson, we concatenated 3 things inside an answers array.

  var showFinal = function () {
    // answers[0]:name, answers[1]:adjective, answers[2]:noun
    $('.prompt').html(answers[0]+' '+answers[1]+' '+answers[2]);
  }

  - For this lesson: This is the story of [name] and the [adjective] [noun].
  var showFinal = function () {
    $('.prompt').html('This is the story of '+answers[0]+' and the '+answers[1]+' '+answers[2]);
    $('button').hide();
  }

- Now, HTML and JS are settled, we will work on CSS to fancy it up!
google fonts follow the style rule here: https://developers.google.com/fonts/docs/getting_started
google.com/fonts > + > copy the link!
1) Fjalla One is nice big readable type
<link href="https://fonts.googleapis.com/css?family=Fjalla+One" rel="stylesheet">

2) Shadows Into Light handwritten (hand writing) font Shadows+Into+Light
<link href="https://fonts.googleapis.com/css?family=Shadows+Into+Light" rel="stylesheet">

Put it top of <head> tags.
<head>
  <link href="https://fonts.googleapis.com/css?family=Fjalla+One" rel="stylesheet">
  <link href="https://fonts.googleapis.com/css?family=Shadows+Into+Light" rel="stylesheet">
  <script src="/assets/jquery.js"></script>

- Apply CSS with new font, text 20px, centered
body {
  text-align: center;
  font-family: 'Fjalla One';
  font-size: 20px;
}
http://jsbin.com/fuqovem/17/edit?html,output

- Give background color to body, Give button some breathing room, Make input box bigger!
body {
  //background color
  background: #e6eaf0
}
button {
  // button some breathing room
  margin: 40px
}
input {
  font-size: 24px;
}

- We want mad lib to have underline and red color with different hand writing font (Shadows Into Light).
  To accomplish this, wrap span with a class called "fill" around the fill-in-the blank parts, so they can have style!

  $('.prompt').html('This is the story of <span class="fill">'+answers[0]+'</span> and the <span class="fill">'+answers[1]+'</span> <span class="fill">'+answers[2]+'</span>.');

  - Next, tell CSS to style .fill answer part
  // assign background color: white, font color: red, solid black border: just on the bottom
  .fill {
    background: white;
    color: red;
    border-bottom: 2px black solid;
  }