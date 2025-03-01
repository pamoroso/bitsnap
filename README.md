# Bitsnap

Bitsnap is a screenshot capture tool written in Interlisp for the Medley environment. It can capture screenshots of the full screen, a window or its interior, or an arbitrary area. Screenshots can optionally be saved to a file in [PBM](https://en.wikipedia.org/wiki/Netpbm#PBM_example) (Portable BitMap) format which some operating systems display natively and is easy to convert to other formats with [Netpbm](https://en.wikipedia.org/wiki/Netpbm) and other utilities.

![The bitmap of a window captured with Bitsnap and its menu on Medley Interlisp.](https://raw.githubusercontent.com/pamoroso/bitsnap/main/bitsnap.png)


## Installation

To install Bitsnap download the source file BITSNAP from the project repo, copy it to a file system location your Medley Interlisp installation has access to, change to that location, and compile the source by evaluating the following expression at an Interlisp Exec:

```
(TCOMPL 'BITSNAP)
```

Provide these answers to the questions the compiler asks:

* listing? no
* redefine? yes
* save exprs? no

Finally, from the same directory load the compiled file by evaluating:

```lisp
(FILESLOAD BITSNAP)
```

or:

```
(LOAD 'BITSNAP.LCOM)
```

## Usage

You can use Bitsnap interactively or call it from Lisp.


### Interactive use

Bitsnap adds the item `Screenshot` to the background menu of Medley. Select this item to capture the full screen. The item has a submenu with items that let you capture the following areas of the screen:

* `Screen`: the full screen
* `Window`: a window
* `Selected`: an arbitrary area

In turn `Window` has a submenu with items for capturing the following portions of a window:

* `Full`: the whole window including the title bar and border
* `Interior`: the interior of the window with no title bar or borders

`Selected` will let you swipe out with the mouse an area of the screen.

When selecting `Window`, `Full`, or `Interior` follow the instructions in the prompt window (the black one) to designate the window to capture.

After the capture Bitsnap will ask in the prompt window to enter a file name to save the image to. It will then save the file and display the image for feedback in a window, which may be closed with the usual `Close` item of the right-click menu. The displayed image has the original size of the captured area, except for the full screen which Bitsnap displays at half size.


### Calling from Lisp

To capture screenshots from Lisp call the following function in the `IL` package:

```
(SNAP what where)
```

The function captures the area of the screen indicated by `what`, optionally saves it to the destination indicated by `where`, and returns a bitmap of the area.

`SNAP` captures the full screen if `what` is `NIL`. Otherwise the function captures the area specified by the symbol passed as the value of `what`:

* `WINDOW`: a window including the title bar and border
* `INTERIOR`: the interior of a window with no title bar or borders
* `SELECTION`: an arbitrary area

`SNAP` prompts the user to indicate the required window or area.

If `where` is `NIL` the function doesn't save the captured area but still returns a bitmap of it. If `where` is `T` the function prompts for a file name to save the area to. Otherwise `where` must be a file name to save the area.


## Learn more

* [Medley Interlisp](https://interlisp.org)


## Author

Bitsnap is developed by [Paolo Amoroso](https://github.com/pamoroso).


## License

This code is distributed under the MIT license, see the `LICENSE` file.
