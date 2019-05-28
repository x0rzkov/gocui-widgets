# gocui-widgets

[![](https://img.shields.io/badge/godoc-reference-5272B4.svg)](http://godoc.org/github.com/shilangyu/gocui-widgets)
[![](https://goreportcard.com/badge/github.com/shilangyu/gocui-widgets)](https://goreportcard.com/report/github.com/shilangyu/gocui-widgets)

Set of thin gocui widgets with higher-level abstractions such as event listeners and changers to help you build TUI apps. It is meant to use **with** [gocui](https://github.com/jroimartin/gocui) not instead.

```sh
go get github.com/shilangyu/gocui-widgets
```

- [usage](#usage)
- [widgets](#widgets)
  - [Text](#Text)
  - [Collection](#Collection)
  - [Menu](#Menu)
  - [Input](#Input)
- [examples](#examples)

## Usage

All widgets implement `gocui.Manager` therefore can be added as managers or rendered directly with `Widget.Layout(g)`.

All widgets expose their `*gocui.View` as well in the `Widget.View` property.

Some widgets accept callback functions called `OnSomething` that are called when `Something` happens.

Some widgets have changers methods called `ChangeSomething` that you call with `gocui.Update` whenever you need to change `Something`.

Check the [\_examples](https://github.com/shilangyu/gocui-widgets/tree/master/_examples) to find out more and [godoc](http://godoc.org/github.com/shilangyu/gocui-widgets) for a more thorough documentation

## Widgets

### Text

Plain text

```go
NewText(name, text string, frame, center bool, x, y int)
```

Parameters:

| name   | description                                     |
| ------ | ----------------------------------------------- |
| name   | ID of your widget (passed to the gocui.View)    |
| text   | value to the printed in your widget             |
| frame  | if true a frame is rendered                     |
| center | if true x and y become the center of the widget |
| x, y   | coordinates of the widget                       |

Changers:

| name       | description                          |
| ---------- | ------------------------------------ |
| ChangeText | changes the inner text of the widget |

### Collection

Renders a grouping frame with title

```go
NewCollection(name, title string, center bool, x, y int, w, h int)
```

### Input

Renders an input

```go
NewInput(name string, frame, center bool, x, y int, w, h int, onChange gocui.EditorFunc)
```

- `onChange` is being called with the `gocui.EditorFunc` parameters when text is inputted (you dont have to call `gocui.DefaultEditor.Edit`, it calls it for you)
- `ChangeText`: changes the inner text of the widget

### Menu

Renders a menu

```go
NewMenu(name string, items []string, x, y int, center, arrows bool, onChange, onSubmit func(i int))
```

Menu is controlled by mouse clicks (therefore make sure to set `g.Mouse` to true), if an item is already highlighted and clicked it is counted as a submit action. If arrows is true, the menu will also be controlled by keyboard arrows where <kbd>Enter</kbd> is submit action.

- `onChange` is being called with the index when user changes his highlighted item
- `onSubmit` is being called with the index when user submits a choice

## Examples

To run a widget example clone this repo and go to the `_examples` directory. Then:

```sh
go run <widget-name>.go
```
