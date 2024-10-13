Using an example bed sprite and collision mask

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325201135.png]]

Create a bed object and set the parent to the wall object

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325201217.png]]

When the `step` event runs in the player object and checks for collision with `obj_wall`, it will also check for collision with any children of `obj_wall`

When the player reaches the bed, the collision mask of the bed will behave as if it were a wall

# Depth

When the player walks behind the bed they will appear on top of the bed, which looks strange

To simply implement depth, add the following line to the player's `step` method:

```
depth = -bbox_bottom;
```

`depth` and `bbox_bottom` are built-in gamemaker variables

A lower `depth` value means a sprite is rendered in front of a sprite with a higher `depth` value

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325201758.png|400]]

`bbox_bottom` references **b**ounding **b**ox **bottom**, which represents the `y` value of the bottom of the collision mask

Add the exact same line of code to the `create` event of the bed object as well

Now when the player is stood behind the bed, since the bed will have a lower `depth` value, the bed will be rendered on top

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240325202114.png|600]]

