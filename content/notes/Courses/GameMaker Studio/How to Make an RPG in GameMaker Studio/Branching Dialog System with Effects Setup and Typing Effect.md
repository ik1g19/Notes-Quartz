This starts assuming we have a room set up, `obj_settings`, `spr_main_font` and `spr_textbox`

![[notes/Courses/GameMaker Studio/How to Make an RPG in GameMaker Studio/Images/Pasted image 20240327230623.png|200]]

# `obj_textbox`

Create `obj_textbox`

## `Create`

The `Create` event will contain the following code

```
depth = -9999;

textbox_width = 200;
textbox_height = 64;
border = 8;
line_sep = 12;
line_width = textbox_width - border*2;
textb_spr = spr_textbox;
textb_img = 0;
textb_img_spd = 6/60;

page = 0;
page_number = 0;
text[0] = "Test text";
text[1] = "Test text but eeeeeeee eeeeeeeevvvvvvvvvvvv vvvvvveeeeeeeen longer";
text[2] = "Short";
text[3] = "Long long long long long long long long long long long long long";
text_length[0] = string_length(text[0]);
draw_char = 0;
text_spd = 1;

setup = false;
```

The textbox has a low depth since it needs to sit on top of all other layers

The following variables are setup to control the sizing of the textbox

```
textbox_width = 200;
textbox_height = 64;
border = 8;
line_sep = 12;
line_width = textbox_width - border*2;
textb_spr = spr_textbox;
textb_img = 0;
textb_img_spd = 6/60;
```

We are setting the images dynamically within the code rather than through GameMaker as it means later on we will be able to swap out textbox images at runtime, such as for a character portrait when someone is talking

The following code will be used to control the content of the textboxes

```
page = 0;
page_number = 0;
text[0] = "Test text";
text[1] = "Test text but eeeeeeee eeeeeeeevvvvvvvvvvvv vvvvvveeeeeeeen longer";
text[2] = "Short";
text[3] = "Long long long long long long long long long long long long long";
text_length[0] = string_length(text[0]);
draw_char = 0;
text_spd = 1;
```

`page` will be used to control how far through the dialogue we are

`page_number` will hold the total number of pages, this is so that we can iterate through them later

`text[]` is an array we will use to hold the dialogue for the textbox

`text_length[]` will hold how long each string is in `text[]`

`draw_char` will increment and represents what character is next to be rendered of the text, this increments like this to give the type writer effect

`text_spd` is used to control how fast the typewriter effect is

The last `setup` variable will be used by the code in the `Draw` event to know if it needs to check the length of each of the strings etc

## `Draw`

This is the `Draw` event of `obj_textbox`

```
accept_key = keyboard_check_pressed(ord("E"));

textbox_x = camera_get_view_x(view_camera[0]);
textbox_y = camera_get_view_y(view_camera[0]) + 144;

//setup
if setup == false {
	
	setup = true;
	draw_set_font(global.font_main);
	draw_set_valign(fa_top);
	draw_set_halign(fa_left);
	
	//loop through the pages
	page_number = array_length(text);
	for (var p = 0; p < page_number; p++) {
		
		//find how many characters are on each page and store that number in the "text_length" array
		text_length[p] = string_length(text[p]);
		
		//offset when there is no characters
		text_x_offset[p] = 44;
	}
}




//typing the text

if draw_char < text_length[page] {
	draw_char += text_spd;
	draw_char = clamp(draw_char, 0 , text_length[page]);
}





//flip through the pages

if accept_key {
	
	//if the typing is done
	if draw_char == text_length[page] {
		//next page
		if page < page_number-1 {
			page++;
			draw_char = 0;
		}
		
		//destroy textbox
		else {
			instance_destroy();
		}
	}
	
	//if not done typing
	else {
		draw_char = text_length[page];
	}
}





//draw the textbox
textb_img += textb_img_spd;
textb_spr_w = sprite_get_width(textb_spr);
textb_spr_h = sprite_get_height(textb_spr);

//back of the textbox
draw_sprite_ext(textb_spr, textb_img, textbox_x+text_x_offset[page], textbox_y, textbox_width/textb_spr_w, textbox_height/textb_spr_h, 0, c_white, 1);


//draw the text
var _drawtext = string_copy(text[page], 1, draw_char);
draw_text_ext(textbox_x+text_x_offset[page]+border, textbox_y+border, _drawtext, line_sep, line_width);
```