We create a script to save time in the future for adding text to the `text[]` array

```
/// @param text
function scr_text(_text){
	text[page_number] = _text;
	
	page_number++;
}
```

We can then use this code in the instance creation code of the room instead

```
scr_text("Test text");
scr_text("Test text but even longer");
scr_text("Short");
scr_text("Long long long long long long");
```

We will now create an object that will allow us to dynamically create a textbox

We create `obj_speakblock` and `spr_speakblock`

`obj_speakblock` has the following code

```
if position_meeting(mouse_x, mouse_y, id) && mouse_check_button_pressed(mb_left) {
	with ( instance_create_depth(0, 0, -999, obj_textbox) ) {
		scr_text("Test text");
		scr_text("Test text but even  longer");
		scr_text("Short");
		scr_text("Long long long long long long");
	}
}
```

`position_meeting` is checking whether the mouse is colliding the object and then `mouse_check_button_pressed` checks if the user has clicked it

Any `instance_create` method returns the id of the object created

`with` blocks can be used to execute code as an instance of another object, so here the `with` block captures the textbox created and then adds some text

# Storing Game Text

We create a script `scr_game_text`

```
function scr_game_text(_text_id){
	switch(_text_id) {
		case "npc 1":
			scr_text("I am npc 1");
			break;
			
		case "npc 2":
			scr_text("I am npc 2");
			break;
			
		case "npc 3":
			scr_text("I am npc 3");
			break;
	}
}
```

We can hold all our game text in this file so that we can use ids for each game object to tie them to a group of text

We then change the `obj_speakbox` `Step` event to

```
var _s = id;

if position_meeting(mouse_x, mouse_y, id) && mouse_check_button_pressed(mb_left) {
	with ( instance_create_depth(0, 0, -999, obj_textbox) ) {
		scr_game_text(_s.text_id);
	}
}
```

Now, a speakbox will create a textbox, store a reference to itself as `_s`, and then pass this identifier to `scr_game_text` to add the right lines of dialogue

We can then set the `text_id` in the instance creation code of each speakbox

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240328003039.png|600]]