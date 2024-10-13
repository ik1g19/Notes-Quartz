# Animation

At the top of the sprite image editor you can create more frames

The small drop down tab beneath frames will let you change the frame speed

Duplicate your sprites and rotate them to have four different sprites for each direction a character can walk

Use *Image* > *Rotate All Frame (clockwise 90)*

Use the *Scripts* folder to create some constants

```gml
#macro RIGHT 0
#macro UP 1
#macro LEFT 2
#macro DOWN 3
```

Create an array in the *create* event to hold the direction sprites

```gml
sprite[RIGHT] = spr_player_right;
sprite[UP] = spr_player_up;
sprite[LEFT] = spr_player_left;
sprite[DOWN] = spr_player_down;

face = DOWN
```

Use a variable to keep track of the current direction

Set the sprite with **sprite_index**

```gml
sprite_index = sprite[face]
```

To determine the direction you are facing:

```gml
if yspd == 0 {
	if xspd > 0 {face = RIGHT};
	if xspd < 0 {face = LEFT};
}
if xspd > 0 && face == LEFT {face = RIGHT};
if xspd < 0 && face == RIGHT {face = LEFT};
if xspd == 0 {
	if yspd > 0 {face = DOWN};
	if yspd < 0 {face = UP};
}
if yspd > 0 && face == UP {face = DOWN};
if yspd < 0 && face == DOWN {face = UP};
sprite_index = sprite[face];
```

To stop a character from animating when they are not moving:

```gml
if xspd == 0 && yspd == 0 {
	image_index = 0;
}
```

This will set the sprite image to the first frame whenever the character stops moving

Full code:

```gml
var _right_key = keyboard_check(vk_right);
var _left_key = keyboard_check(vk_left);
var _up_key = keyboard_check(vk_up);
var _down_key = keyboard_check(vk_down);

xspd = (_right_key - _left_key) * move_spd;
yspd = (_down_key - _up_key) * move_spd;


if yspd == 0 {
	if xspd > 0 {face = RIGHT};
	if xspd < 0 {face = LEFT};
}
if xspd > 0 && face == LEFT {face = RIGHT};
if xspd < 0 && face == RIGHT {face = LEFT};
if xspd == 0 {
	if yspd > 0 {face = DOWN};
	if yspd < 0 {face = UP};
}
if yspd > 0 && face == UP {face = DOWN};
if yspd < 0 && face == DOWN {face = UP};
sprite_index = sprite[face];


if place_meeting(x + xspd, y, obj_wall) == true {
	xspd = 0;
}

if place_meeting(x, y + yspd, obj_wall) == true {
	yspd = 0;
}


x += xspd;
y += yspd;


if xspd == 0 && yspd == 0 {
	image_index = 0;
}

```

# Tiles

Tile sets pull from sprite in blocks

In the sprite editor press **G** to toggle the grid

This is currently so far only a sprite still, go to the tile set folder and create a new tile set to use the sprite

Tilesets *always* start with the first tile blank

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325015547.png]]

Go back to the Room scene and click **Create New Tile Layer** to start using the tile set

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325020619.png|400]]

Once you have selected the tile set you can then select a tile and paint the room with it

Going back to the workspace, we can turn off visibility for the walls object to hide them

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325021035.png|400]]

Now create a new instance layer called **walls**, this is where we will paint walls for collision on top of our tiles

Select the wall object from the asset browser and paint where walls are needed

You can make your tileset longer - but *never* wider
- This is because the tiles are 0 indexed from the top left
- So adding more tilesets *along* the tileset will mean that the indexes of the rest of the tiles in use will change

# Simple Camera

Increase the room size under room settings

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325021734.png|400]]

Expand **Viewport 0** and set **Object Following** to the player object

The Horizontal and Vertical Border properties determine how close the player has to be to the edge of the viewport for the viewport to start scrolling
- Set these properties to half of the viewport size to have the player remain at the centre of the screen

A horizontal and vertical speed of -1 means that the viewport will be following the player as fast as the player is moving

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325022110.png|400]]

