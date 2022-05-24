# Pong inspired game in p5js

```JavaScript

var myRect;
var mycirc;
var speedx;
var speedy;
var gameState;
var score;
var colour;

function setup() {
  createCanvas(500,500);

  //ball speed
  speedx=3
  speedy=3;

  gameState=1;
  score = 0;
  colour=0;
  
  //player paddle
  myRect = {
    x:100,
    y:400,
    length: 125,
    height: 20
  };

  mycirc = {
    x:50,
    y:120,
    size:50
  }
}

function draw() {
  background(colour*-1,colour,colour);

  if (gameState==1){
    fill(255);
    textSize(25);
    text("Press s to start,q to quit\nd to lengthen,a to shorten",50,100);

  } else if (gameState==3){
    text("Game Over",50,100);
  } else {
  // start game

  myRect.x=mouseX;
  rect(myRect.x,
    myRect.y,
    myRect.length,
    myRect.height
  );

  //draw circle
  circle(mycirc.x,mycirc.y,mycirc.size);

  //circle speeds
  mycirc.x=mycirc.x+1*speedx;
  mycirc.y=mycirc.y+1*speedy;

  //bounce of screen
  if (mycirc.y<=mycirc.size/2){
    speedy=speedy*-1;
  } else if (mycirc.x>=width-mycirc.size/2){
    speedx=speedx*-1;
  } else if (mycirc.x<=mycirc.size/2){
    speedx=speedx*-1;
  } 
  
  //debugging
  //line(mycirc.x,mycirc.y,myRect.x,myRect.y);
  //line(mycirc.x,mycirc.y,myRect.x+125,myRect.y);

  //text(dist(mycirc.x,mycirc.y,myRect.x,myRect.y),50,50)
  //text(dist(mycirc.x,mycirc.y,myRect.x+125,myRect.y),50,100)

  //bounding box
  if(mycirc.x>mouseX && 
    mycirc.x<mouseX+myRect.length && 
    mycirc.y+mycirc.size/2<=400&&mycirc.y+mycirc.size/2>=400)
    {speedy=speedy*-1;
    score=score+1;
    colour=random(255);
  }

  text("score: "+score,50,50);
    
  if (mycirc.y>=height+25){
      gameState=3;
    } 

}

}

function keyPressed () {
  if (key=='s'){
    gameState=2;
  } else if (key=='q'){
    gameState=1;
  } else if (key=='d'){
    myRect.length=myRect.length-10;
  } else if (key=='a'){
    myRect.length=myRect.length+10;
  } 
}
```
