#Programming Notes
### Initial Comments
I'm an experienced JS developer so I got a little bored doing the challenge task. That being said, I found fun in obfuscating and hiding my code as well as changing up the design a bit. See if you can figure out how the code works! If you can't, or if you have but can't understand it, as it's minified and compiled check the link at the bottom for a fully commented version.

Additionally, it was a bit unclear as to what browser this is to run on, and whether or not external libraries and frameworks are allowed. As such, I assumed this was to be run on the most recent browser and external libraries would not be allowed.

If you look at my code you will notice that I tried to make use of as many new array prototype functions as possible. Generally in JS interviews they'd like to see the use of .bind .call and .apply. I did use .apply in my bootstraping code on the index page, and I used .bind in the onclick handler in the Simon game :).


### Problems and Hardships
Obviously animations in VanillaJS are a pain, so that was probably the most difficult part of the whole thing.

### Plans for the Future
I got busy so there were a couple things that I was planning on doing but didn't bother with in the end.  Here they are:

- Multiplayer Simon using WebRTC. (Obviously this requires a server for signaling but luckily the nice people who created the PeerJS library provide a free one).
- Simon using some sort of [randomness test](https://en.wikipedia.org/wiki/Randomness_tests) to add to scoring. Right now it just adds the product of the number of notes and some constant.


## SPOILERS AHEAD!!!


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
Alright, since you're reading this I'm assuming you either found out how my code works, got lazy, didn't try, or simply don't understand what's going on.


Here's how it works:
The script at the bottom of the page executes the following code; you can test this by replacing `eval` with `console.log`:

```js
// Load a canvas and grab the context
a = document.createElement("canvas"), b = a.getContext("2d");
a.width = 700;

// Draw an image to said canvas
b.drawImage(II, 0, 0);

// Iterate through the RGBA values of each pixel of the first two pixel rows in the image.
// Filter out every 4th value as the alpha channel is always 255 to prevent compression based data loss
// use String.fromCharCode to convert it to a string.
eval(String.fromCharCode.apply(null, b.getImageData(0, 0, 638, 2).data.filter(function(c, d) {
    return 0 < c && 3 != d % 4
})) + ")")

```
Essentially, that code looks at the top two lines in the image and extracts the data from it. After I minified my JS I converted the each letter to its ASCII value, converted that to an array and stuck it at the top of the logo. Each pixel can hold 3 letters as R G and B have a range: [0,255]. As such if you look carefully at the top of the logo image, you'll see:

![weird colours](http://i.imgur.com/D1U871h.png)


As you can see from the image there's a bunch of different colours. This is hidden in the HTML as the container that holds this image cuts that small part out and the image is scaled.

If you still don't understand it, here's what's going on. Suppose you had the JS: 
```js
    function(){}
```
If we convert this to a string and split it we get the following array:
```js
  ["f","u","n","c","t","i","o","n","(",")","{","}"]
```
If we map out the ascii values we get:
```js
    [102,117,110,99,116,105,111,110,40,41,123,125]
```
Let's take a look at the first three pixels
```js
    [102,117,110]
```
We can take these three bytes and convert them to RGB values, which can be stored as a pixel, which would look like: ![cool pixel](http://i.imgur.com/cCwXgHM.png) <- This is one pixel scaled up
Ta-da!