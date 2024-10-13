Create another room

The default room to be used when the game starts is dictated by the room order

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325231450.png|400]]

Create a sprite and object called **warp_block**

In the `create` event of the warp block initialise the values:

```
target_x = 0;
target_y = 0;
target_rm = 0;
```

These will hold the position and room a player will warp to

In the `step` event of the warp block object add the following code:

```
if place_meeting(x, y, obj_player) {
	room_goto(target_rm);
	obj_player.x = target_x;
	obj_player.y = target_y;
}
```

This is checking from the warp block's perspective if it has collided with the collision mask of the player object

Add an instance of `obj_warp_block` to the instances layer

Click the warp block and select `Creation Code`

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325234817.png|600]]

**Instance Creation Code** is code that is ran immediately after the constructor/create event of an object, but it specific to each instance of the object

So in this example the warp block will be used to send the player to the living room

Example warp block `Creation Code`:

```
target_x = 176;
target_y = 112;
target_rm = rm_living_room;
```

Make the player object `Persistent`

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325235321.png|600]]

This means that the player object will not be removed once the new room is loaded

# Transition Animation

Create a sprite `spr_warp_transition`

This sprite will hold the animation that will play upon a room transition

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325235558.png]]

Create a warp object `obj_warp` and assign its sprite to `spr_warp_transition`

Create an `Animation End` event for `obj_warp`, this code will run once the objects animation finishes playing

Take the code from `obj_warp_block` and add it to the `Animation End` event for `obj_warp`

```
room_goto(target_rm);
obj_player.x = target_x;
obj_player.y = target_y;

image_speed = -1;
```

`image_speed` is a built-in gamemaker variable that represents how fast the animation for an object plays, -1 will make the animation play in reverse
- Which in this example means that the animation will play and then immediately stop and play in reverse

Create a `Draw` event for `obj_warp`
- All objects will run `Draw` by default anyway if they have a sprite, but this can be altered by adding your own `Draw` event

`Draw`:

```
draw_sprite_tiled(sprite_index, image_index, 0, 0);
```

`draw_sprite_tiled` is another built-in method that will draw a sprite multiple times across the screen
- In this example it is being used to play the animation multiple times across the entire screen
- `image_index` is another built-in variable that holds the current frame of animation of the object

Change the now empty `Step` event for the `obj_warp_block`

`Step`:

```
if place_meeting(x, y, obj_player) && !instance_exists(obj_warp) {
	var inst = instance_create_depth(0, 0, -9999, obj_warp);
	inst.target_x = target_x;
	inst.target_y = target_y;
	inst.target_rm = target_rm;
}
```

- The warp only needs to happen on the **first** frame of collision, so there is now a check to make sure the warp object hasn't already been created - which would mean the warp has already been triggered
- `instance_create_depth` is used to instantiate an object at a specified depth, the warp transition animation needs to play in front of any other sprite - hence `-9999`
- The variable `inst` is used to capture the *object id* of the newly created warp object, this is because this is an object instantiated at runtime, that will need to be referenced later
- The target positions are then passed to the warp object using the variables created in the `Instance Creation Code` earlier

Make sure to enable *persistence* for the warp object as well, so that the animation will carry over into the next room

# Pausing the Game

When a room transition plays, the player should temporarily lose control

Create an object `obj_pauser`

Add the following code to the `Step` event of `obj_player`, make sure it is ran before any changes to the player sprite or position are made

```
if instance_exists(obj_pauser) {
	xspd = 0;
	yspd = 0;
}
```

If any `obj_pauser` instances currently exist, then the players speed will be 0

To have the warp object act as a pauser, set it as a child object

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240326002957.png|600]]

Any object that needs to pause the game can inherit from `obj_pauser` to implement this
