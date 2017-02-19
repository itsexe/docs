# UI
## NUI
NUI files define the ingame windows. Each nui file contains one window with its elements like buttons, textedits etc.
The file format is pretty simple. A element is defined between the "begin" and "end" tag.
```
begin <element type>
<attribute> = <value>
<attribute> = <value>
end
```

A NUI containing just a window with a button would look like this:
```
begin genwnd
id = channel;
rect = 0,0,434,434;
drag_rect = 0,26,430,420;
style = KSTYLE_ALPHA_SHOW | KSTYLE_MOVE_BY_CUSTOM ;
end

begin button
id = channel03;
spr = SG.spr;
ani = button_common_button00;
caption = "key_channel_chan_03";
rect = 151,142,420,165;
end
```

### Element types
There are following elements.
* genwnd (The window itself)
* static (Mostly images or texts without any functions)
* SimpleCheck
* Check
* SimpleButton (Usually a single image like the "x" to close the window)
* Button (Usually a real button with animations and stuff)
* Edit (Textedit)

### Element attributes
* id (name)
* rect (Size)
* drag_rect (Region where you can drag the window)
* style (?)
* spr (SPR file)
* ani (Refers to a resource in the spr file)
* flag (?)
* caption (Text, can be formatted using HTML)

## SPR
SPR files are a bit more complicated compared to NUI files. They contain (mostly multiple) images for buttons etc.

The format looks like this:
```
<resource name>
<number of images in resource>
<image name>
<image dimensions>
<unknown (always 0 or 1)>
<resource name>
<number of images in resource>
...
```
Snippet of SG.spr file
```
button_characterbox_minus
4
button_characterbox_minus_00.tga
59,18
0
button_characterbox_minus_01.tga
0,0
0
button_characterbox_minus_02.tga
0,0
0
button_characterbox_minus_03.tga
0,0
0
button_characterbox_plus
4
button_characterbox_plus_00.tga
59,18
0
button_characterbox_plus_01.tga
0,0
0
button_characterbox_plus_02.tga
0,0
0
button_characterbox_plus_03.tga
0,0
0
```


The background images are ususally split into 9 seperate images (Corners, sides and center).
This way the background is not fixed to a specific resolution and can be resized or even used for multiple forms.
![split window](https://raw.githubusercontent.com/itsexe/docs/master/img/1.png)

The images are usually saved as tga or sometimes as dds.
