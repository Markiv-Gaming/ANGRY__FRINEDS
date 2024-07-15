# AngryBirdsReplica

A simple replica of the famous mobile game Angry Birds made using javascript.

Some interesting concepts used:

Asynchronous Background Image Loading: The use of asynchronous functions to fetch data from an API and change the game background based on real-world time. This background loading adds a layer of interactivity and realism to the game.

                async function getbackgroundimg(){
    var response = await fetch("http://worldtimeapi.org/api/timezone/Asia/Kolkata");
    var responseJSON = await response.json();
    var datetime = responseJSON.datetime;
    var hour = datetime.slice(11, 13);
    if (hour >= 06 && hour <= 18) {
        bg = "sprites/bg.png";
    } else {
        bg = "sprites/bg2.jpg";
    }
    backgroundImg = loadImage(bg);
    }


Scoring System: The code includes a scoring system where points are updated and displayed in real-time. Each Pig object has a method score() which updates the score based on the game events.

    var score = 0;
    function draw(){
    if (backgroundImg) {
        background(backgroundImg);
    }
    noStroke();
    textSize(35);
    fill("white");
    text("score: " + score, width - 300, 50);
    Engine.update(engine);
    }


Interactive SlingShot Mechanism: The code includes an interactive slingshot mechanism that allows the user to drag and release the bird. This is a key feature that adds an engaging gameplay element, demonstrating how constraints can be used in Matter.js to create interactive elements.

     slingshot = new SlingShot(bird.body, {x: 200, y: 50});


Game State Management: The game uses a gameState variable to manage the state transitions, specifically to control the bird's behavior when it is being dragged and launched. This helps in maintaining the game flow and ensuring that user interactions are handled appropriately.

     var gameState = "onSling";
     function mouseDragged(){
     if (gameState !== "launched") {
     Matter.Body.setPosition(bird.body, {x: mouseX , y: mouseY});
     }
     }
     function mouseReleased(){
     slingshot.fly();
     gameState = "launched";
     }


Modular Object-Oriented Design: The code uses a modular, object-oriented approach to define various game objects like Box, Pig, Log, Bird, and Ground. This makes the code more organized, reusable, and easier to manage.

     box1 = new Box(700,320,70,70);
     pig1 = new Pig(810, 350);
     log1 = new Log(810,260,300, PI/2);
     bird = new Bird(200,50);




