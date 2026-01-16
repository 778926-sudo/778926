What I implemented today week 2 day 1:

The main concept I implemented today was variables and data tracking. I used variable to track the game state and store important information such as which screen the game is on currently and the buttons that are used for navigating my UI

This is a code snippet:
 int STATE_MENU = 0;
int STATE_HELP = 1;
int STATE_PLAY = 2;
int STATE_GAMEOVER = 3;

int gameState = STATE_MENU; //this variable keeps track of the current screen

//thse buttons are used across diffrent screens
Button playBtn;
Button helpBtn;
Button backBtn;
Button rematchBtn;
Button menuBtn;

Where I used it, and why I did it that way:

I used variables to control the flow of the game and manage different screens such as the menu, help screen, gameplay, and game over screen. The gameState variable is also checked inside the draw()  loop to decide which screen should be displayed.
Using constants like STATE_MENU instead of raw numbers makes the code way easier to read and understand. Instead of guessing what gameState == 0 means, it is clear that STATE_MENU represents the menu screen. Doing it in this way  makes the code way more organized and easier to debug later.
Buttons were stored as variables so they could be reused across different screens instead of being recreated repeatedly.
Some challenges, and how I fixed them:

One challenge I faced was understanding how to switch between different screens without restarting the program. At first, I tried drawing everything in one place, which made the code confusing. I solved this by using a gameState variable and separating each screen into its own method (such as drawMenu() and drawHelp()).
Another challenge was handling button clicks properly. I fixed this by checking the mouse position using a method that detects whether the mouse is inside a button’s area before changing the game state.
// This class represents a player character in the game and controls its movement and behavior





Learning Log – Day 2

Topic: Selection Structure (if / else statements)

What I implemented today

The concept I implemented today is the selection structure, by using if, else if, and else statements. The selection structure allows my program to make decisions and run different code depending on the conditions

//chekcs which screen should be shown
  if (gameState == STATE_MENU) {
    drawMenu();
  } else if (gameState == STATE_HELP) {
    drawHelp();
  } else if (gameState == STATE_PLAY) {
    updateGame();  // update movement & physics
    drawGame();    // draw players and ground

  } else if (gameState == STATE_GAMEOVER) {
    drawGameOver();
  }
}


Where I used it and why I did it that way

I used selection structures to control which screen is currently on/ shown in my game.
The variable gameState stores which screen the game  is currently on for example:MENU, HELP, PLAy, or GAMEOVER.

Each if or else if checks the value of gameState and only runs the code for that screen. This prevents all screens from drawing at the same time and keeps the game nice and  organized.

I did it this way since it makes it easier to control using one variable, each screen has its own method which keeps the code clean, and it allows a nice smooth transition when switching between screens while using the buttons.

c)  The challenges I encountered and how I fixed them 

One challenge I encountered was that the players were not appearing on the play screen.
The issue was that I was only calling a method that did not draw the players.

So originally my code only called 
drawPlayScreen();

That method did not include player drawing or updates

To fix that I changed the selection structure so when gameState == STATE_PLAY the programs calls
updateGame();
drawGame();

This fixed the issue since updateGame() updates the players movement and physics, and drawGame(); draws the player and the ground.
	
	













Day 3 log: Repetition Structure



The concept I implemented

The concept I have implemented is repetition structure. In my game repetition is used to continuously update the players physics, movement, collisions and the game state while the game is running

if (hitCooldown > 0) {
  hitCooldown--;
}


Where I used it and why I did it that way

This repetition structure is used inside the updateGame() method, which is called every frame while the game is in the PLAY state

Since the draw() method in Processing runs automatically about 60 times per second, this line of code is repeatedly done. Each frame, the cooldown value decreases by 1 until it reaches 0.

I did it this way so that the damage cannot happen every single frame when players collide. Instead, the cooldown counts down over multiple frames, creating a short delay between hits. This makes the game fairer and more playable.

The challenges I encountered and how I fixed them 

One challenge I faced was that players were losing health wayyy too quickly when they touched each other. Since collision detection happens every frame, damage was being applied repeatedly without a delay.
To fix this, I added the hitCooldown variable and used repetition to reduce it over time. By checking if hitCooldown > 0 before allowing damage, I prevented repeated hits from happening too fast. This solved the issue and made the gameplay feel more balanced.








Learning log day 4:


Topic: arrays and data structures

The concept I implemented

The concept I implemented is Arrays & Data Structures. I used an array to store and manage multiple falling items (hearts and blocks) that appear during gameplay.

// Array to store falling items
FallingItem[] items;
int itemCount = 0;
int MAX_ITEMS = 25;

And 

items = new FallingItem[MAX_ITEMS];// Initializing the falling items array 

WHere I used it and why I used it that way
I used the array in my game to store multiple falling items at the same time. Each element in the array represents one FallingItem object, which can be either a heart (heals the player) or a block (damages the player).

An array was the best choice since the number of items needed to be limited, the items need to be added, updated, drawn, and removed, and lastly arrays allow me to use loops to manage all the items efficiently.

For example I loop through the array to update items movement and check for player collisions:

void updateItems() {//this method updates all falling items and checks for collions
  for (int i = 0; i < items.length; i++) {
    if (items[i] != null) {//only update items that exisis
      items[i].update();//moves the item downwards

I also use null values to represent the empty slots in the array. So when an item is collected or falls off the screen I set the position back to null which frees up space for new items

c)The challenges I encountered

One challenge I faced was making sure the array did not overflow when spawning items. At first, items were spawning too often and could exceed the intended limit.

So to fix that I added a MAX_ITEMS constant, tracked the current number of items using itemCount and used a check to stop spawning when the array was full: if (itemCount >= MAX_ITEMS) return;
