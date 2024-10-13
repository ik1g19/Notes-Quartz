# Sprites

Create the sprite `spr_main_font`

This sprite will contain the font to be used in the game

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240326190631.png]]

Create the sprite `spr_menu`

This sprite is going to hold the texture to be used by menu screens

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240326190753.png]]

Create the animation that you want to play in the centre

Gamemaker supports Nine Sliceing, which means that you can adjust the borders so that as this sprite is scaled, the borders on the outside will be scaled but the inside graphics are going to be tiled across the screen

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240326190943.png]]

# Menu Logic

Create the object `obj_title_menu` and set its sprite to `spr_menu`

This is going to provide the functionality for a title menu screen

## Create Event

The `Create` event of `obj_title_menu` looks like this:

```
width = 64;
height = 104;

op_border = 8;
op_space = 16;

pos = 0;

option[0, 0] = "Start Game";
option[0, 1] = "Settings";
option[0, 2] = "Quit Game";

option[1,0] = "Window Size";
option[1,1] = "Brightness";
option[1,2] = "Controls";
option[1,3] = "Back";

op_length = 0;
menu_level = 0;
```

We initialize the variables `width` and `height` to represent the width and height of the menu

`op_border` is variable we are creating that represents the option border, which is the space between an option and the side of the menu

`op_space` is another variable we are creating that will represent the space between menu objects

`pos` is a variable we are initializing that represents which option the user has selected

`option` is a 2d array that will contain the contents of the menu and its sub-menus
- So Start Game, Settings and Quit Game will be at the top level, and Window Size, Brightness etc. are a sub menu of Settings

`op_length` and `menu_level` are both being initialized to 0
- `op_length` represents the number of options to render, which will be used later to tell gamemaker how much height each menu should be rendered with
## Step Event

This is the logic for the `Step` event of `obj_title_menu`:

```
up_key = keyboard_check_pressed(vk_up);
down_key = keyboard_check_pressed(vk_down);
accept_key = keyboard_check_pressed(vk_space);

op_length = array_length(option[menu_level]);

pos += down_key - up_key;
if pos >= op_length {pos = 0};
if pos < 0 {pos = op_length-1};

if accept_key {
	
	var _sml = menu_level;
	
	switch(menu_level) {
		case 0:
			switch(pos) {
				case 0: room_goto_next(); break;
				case 1: menu_level=1; break;
				case 2: game_end(); break;
			}
		break;
		
		case 1:
			switch(pos) {
				case 0: break;
				case 1: break;
				case 2: break;
				case 3: menu_level = 0; pos=0; break;
			}
		break;
	}
	
	if _sml != menu_level {pos=0};
	
	op_length = array_length(option[menu_level]);
}
```

The first 3 lines are listening for the keys that will be used to move up, down and select in the menu respectively

```
up_key = keyboard_check_pressed(vk_up);
down_key = keyboard_check_pressed(vk_down);
accept_key = keyboard_check_pressed(vk_space);
```

Next, a check is made to find out how many options need to be rendered at the current menu level

```
op_length = array_length(option[menu_level]);
```

Next, the logic is ran to check whether an input has been made that means the selected option in the menu needs to change:

```
pos += down_key - up_key;
if pos >= op_length {pos = 0};
if pos < 0 {pos = op_length-1};
```

Then, the rest of the logic checks if the select key was pressed, and if so, which option was highlighted when it was:

```
if accept_key {
	
	var _sml = menu_level;
	
	switch(menu_level) {
		case 0:
			switch(pos) {
				case 0: room_goto_next(); break;
				case 1: menu_level=1; break;
				case 2: game_end(); break;
			}
		break;
		
		case 1:
			switch(pos) {
				case 0: break;
				case 1: break;
				case 2: break;
				case 3: menu_level = 0; pos=0; break;
			}
		break;
	}
	
	if _sml != menu_level {pos=0};
	
	op_length = array_length(option[menu_level]);
}
```

## Draw Event

This is the logic for the `Draw` event of `obj_title_menu`:

```
var _new_w = 0;

for (var _i = 0; _i < op_length; _i++) {
	var _op_w = string_width(option[menu_level,_i]);
	_new_w = max(_new_w, _op_w);
}
width = _new_w + op_border*2;
height = op_border*2 + string_height(option[0,0]) + (op_length-1)*op_space;


x = camera_get_view_x(view_camera[0]) + camera_get_view_width(view_camera[0])/2 - width/2;
y = camera_get_view_y(view_camera[0]) + camera_get_view_height(view_camera[0])/2 - width/2;

draw_sprite_ext(sprite_index, image_index, x, y, width/sprite_width, height/sprite_height,0 ,c_white, 1);

draw_set_font(global.font_main);
draw_set_valign(fa_top);
draw_set_halign(fa_left);

for (var _i = 0; _i < op_length; _i++) {
	var _c = c_white;
	if pos == _i {_c = c_black};
	draw_text_color(x+op_border, y+op_border + op_space*_i, option[menu_level, _i], _c, _c, _c, _c, 1);
}
```

`_new_w` is the new width of the menu, this is going to scale according to the string with the largest width in the menu

```
for (var _i = 0; _i < op_length; _i++) {
	var _op_w = string_width(option[menu_level,_i]);
	_new_w = max(_new_w, _op_w);
}
width = _new_w + op_border*2;
```

The height scales similarly

```
height = op_border*2 + string_height(option[0,0]) + (op_length-1)*op_space;
```

The following logic is used to center the menu on the screen

```
x = camera_get_view_x(view_camera[0]) + camera_get_view_width(view_camera[0])/2 - width/2;
y = camera_get_view_y(view_camera[0]) + camera_get_view_height(view_camera[0])/2 - width/2;
```

`draw_sprite_ext` is used to draw the background of the menu, the `ext` part means that it takes additional options for scaling, rotation, blending and transparency

```
draw_sprite_ext(sprite_index, image_index, x, y, width/sprite_width, height/sprite_height,0 ,c_white, 1);
```

>[!help]
> By dividing `width` by `sprite_width` and `height` by `sprite_height`, you're essentially specifying how much you want to scale the sprite in both dimensions

The font to be used for drawing is then specified, as well as alignment

```
draw_set_font(global.font_main);
draw_set_valign(fa_top);
draw_set_halign(fa_left);
```

>[!help]
>`draw_set_valign(fa_top);`
>This line sets the vertical alignment for text rendering. `fa_top` represents "top" alignment. This means that when you draw text, the top edge of the text will be aligned with the vertical position specified when drawing. For example, if you draw text at position `(x, y)`, the top of the text will be at `y`
>
>`draw_set_halign(fa_left);`
>This line sets the horizontal alignment for text rendering. `fa_left` represents "left" alignment. This means that when you draw text, the left edge of the text will be aligned with the horizontal position specified when drawing. For example, if you draw text at position `(x, y)`, the left side of the text will be at `x`

`global.font_main` is a global variable that will be specified in the settings object later
- [[#obj_settings]]

The for loop at the end then cycles through each option at the current menu level and draws the text using the sprite sheet, and draws it a different colour if it is currently selected

```
for (var _i = 0; _i < op_length; _i++) {
	var _c = c_white;
	if pos == _i {_c = c_black};
	draw_text_color(x+op_border, y+op_border + op_space*_i, option[menu_level, _i], _c, _c, _c, _c, 1);
}
```

## obj_settings

Create the object `obj_settings`

This will be used to hold game settings

The `Create` event should be

```
global.font_main = font_add_sprite(spr_main_font, 32, true, 1);
```

The `true` means that letters will be spaced based on how wide they are

Add a `Clean Up` event to remove the font after to prevent a memory leak

```
font_delete(global.font_main);
```