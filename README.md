prototype
=========

Simply prototype 2D games using an easy, minimal interface that lets you draw simple primitives and images on the screen, easily handle mouse and keyboard events and play sounds.

Installation
------------

First you need to install the Go programming language from [this link](https://golang.org/dl/). After clicking the download link you will be referred to the installation instructions for your specific operating system. Follow these instructions so you have the GOROOT and GOPATH environment variables set in your system.

You of course also need git (for Windows, get it from [here](https://git-scm.com/downloads)).

Because this library uses C libraries you also need a working C compiler. If you are on Linux you probably already have GCC installed. For Windows you can use [MinGW](http://sourceforge.net/projects/mingw/files/latest/download?source=files). After downloading, run the installer and follow the instructions until you get to the "MinGW Installation Manager". Put a check mark on the following components: *mingw-developer-toolkit*, *mingw32-base*, *mingw-gcc-g++* and *msys-base*. In the "Installation" menu click "Apply Changes" and wait for it to finish. Then add the tools directories (they default to *C:\MinGW\bin* and *C:\MinGW\msys\1.0\bin*) to your PATH environment. See the instructions from the Go installation page for how to edit your environment variables.

After installing all the tools you are ready to install this library and finally start prototyping. From the command line run:

	go get github.com/gonutz/prototype/draw

This will install and build the library.

Documentation
-------------

For a description of all library functions, see [the godoc page](http://godoc.org/github.com/gonutz/prototype/draw) for this project. Note that most of the functionality is in the Window interface and hence the descriptions are listed as code comments in the source for that type.

Example
-------

```Go
package main

import "github.com/gonutz/prototype/draw"

func main() {
	draw.RunWindow("Title", 640, 480, draw.Resizable, update)
}

func update(window draw.Window) {
	// find the screen center
	w, h := window.Size()
	centerX, centerY := w/2, h/2

	// draw a button in the center of the screen
	window.FillEllipse(centerX-20, centerY-20, 40, 40, draw.DarkRed)
	window.DrawEllipse(centerX-20, centerY-20, 40, 40, draw.White)
	window.DrawScaledText("Close!", centerX-40, centerY+25, 1.6, draw.Green)

	// check all mouse clicks that happened during this frams
	for _, click := range window.Clicks() {
		dx, dy := click.X-centerX, click.Y-centerY
		squareDist := dx*dx + dy*dy
		if squareDist <= 20*20 {
			// close the window and end the application
			window.Close()
		}
	}
}
```
	
This displays a resizable window with a round button in the middle to close it. It demonstrates some basic drawing and event handling code.