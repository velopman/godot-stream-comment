# Godot Stream Comment

A small Godot plugin to make automated code comments easy. 

## Behaviour

Once called, `StreamComment.comment` will insert a comment into the currently active script, the line above where the cursor is located. If there is enough interested, other methods will be added to do things like randomly insert to the current script, or insert into any open script. 

To avoid annoyances while programming, `StreamComment.comment` will restore the current cursors position as well as any active selection.

## Usage

**Note**: This plugin has been created as an editor plugin, and as such should only be activated through the editor. 

To add a comment to the currently acivey script, call the `.comment` method on the `StreamComment` singleton. A comment will be added to the line above the cursor. 
``` gdscript
StreamComment.comment("Hello world")

output: 
# Hello world
```

`.comment` has a second, optional parameter that is a boolean to control if new line characters are escaped. By default, this parameter is true.
``` gdscript
StreamComment.comment("Hello world\nIt is I!", true)

output: 
# Hello world\nIt is I!

StreamComment.comment("Hello world\nIt is I!", false)

output: 
# Hello world
# It is I!
```

In the event that there is no active script, `.comment` will return `false` to signal that the comment could not be placed. If you want to have the comment written to the next active script, it is possible to do so by calling `.enqueue_comment` as you would `.comment`. 
``` gdscript

var comment: String = "Hello world"

if !StreamComment.comment(comment):
  StreamComment.enqueue_comment(comment)
```

## Connecting to Twitch events

This plugin was created with Twitch channel point redemptions in mind; making it simpler to automate the act of commenting on redemption. It doesn't however do the connection to Twitch's event sub API. I am however actively working with [Yagich](https://github.com/Yagich) to develop [velopteam/YATL](https://github.com/velopteam/YATL), another Godot plugin that will greatly simplify connecting to Twitch. 

I've created a sample project to illustrate a basic usecase: [velopman/godot-plugin-examples](https://github.com/velopman/godot-plugin-examples/tree/main/stream-comment).
