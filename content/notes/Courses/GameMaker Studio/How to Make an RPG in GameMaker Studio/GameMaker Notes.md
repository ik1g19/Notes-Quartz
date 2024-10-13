Use `ord()` to listen for input from normal keyboard keys

```
accept_key = keyboard_check_pressed(ord("E"));
```

Use `clamp()`to set a value to a minimum if it falls too low, or a maximum if it goes too high

```
//typing the text

if draw_char < text_length[page] {
	draw_char += text_spd;
	draw_char = clamp(draw_char, 0 , text_length[page]);
}
```

Use this syntax to add suggestions when you hover over your function

```
/// @param text
```