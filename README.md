# Animating-Emojis-in-URLs
You can use emoji (and other graphical unicode characters) in URLs. And wow is it great. But no one seems to do it. Why? Perhaps emoji are too exotic for normie web platforms to handle? Or maybe they are avoided for fear of angering the SEO gods?

Whatever the reason, the overlapping portion on the Venn diagram of "It's Possible v.s. No One Is Doing It" is where my excitement usually lies. So I decided to put a little time into the possibilities of graphical characters in URLs. Specifically, with the possibility for animating these characters by way of some Javascript.

## 1. Animating Moon
![moon.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/moon.gif)


```javascript
var f = ['🌑', '🌒', '🌓', '🌔', '🌝', '🌖', '🌗', '🌘'];

    function loop() {
        location.hash = f[Math.floor((Date.now()/100)%f.length)];

        setTimeout(loop, 50);
    }

    loop();
```

## 2. Rolling Clock
If you don't like the spinning moons you can swap out that array with whatever emojis you want. Like a clock:

![clock.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/clock.gif)

```javascript
var f = ['🕐','🕑','🕒','🕓','🕔','🕕','🕖','🕗','🕘','🕙','🕚','🕛'];


    function loop() {
        location.hash = f[Math.floor((Date.now()/100)%f.length)];

        setTimeout(loop, 50);
    }

    loop();
```

## 3. Color-changing Babies    
This is a real simple example. Too simple really. So let's upgrade our loop so that it generates a string of multiple emoji! This time we're utilizing the emoji "skin tone modifiers" characters to make some color-changing babies:


![babies.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/babies2.gif)

```javascript
var e = ['🏻', '🏼', '🏽', '🏾', '🏿'];

    function loop() {
        var s = '',
            i, m;

        for (i = 0; i < 10; i ++) {
            m = Math.floor(e.length * ((Math.sin((Date.now()/100) + i)+1)/2));
            s += '👶' + e[m];
        }

        location.hash = s;

        setTimeout(loop, 50);
    }

    loop();
```

## 4. Rising Sun
We use a sine wave controlled by time and position to select which color we want. This gives us a nice loopy color changing effect!
Or how about we revisit our moon spinner, spread it out, and make something resembling a loading indicator? Sure, let's do it:

![sun.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/moons.gif)

```javascript
var f = ['🌑', '🌘', '🌗', '🌖', '🌕', '🌔', '🌓', '🌒'],
        d = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        m = 0;

    function loop() {
        var s = '', x = 0;

        if (!m) {
            while (d[x] == 4) {
                x ++;
            }

            if (x >= d.length) m = 1;
            else {
                d[x] ++;
            }
        }
        else {
            while (d[x] == 0) {
                x ++;
            }

            if (x >= d.length) m = 0;
            else {
                d[x] ++;

                if (d[x] == 8) d[x] = 0;
            }
        }

        d.forEach(function (n) {
            s += f[n];
        });

        location.hash = s;

        setTimeout(loop, 50);
    }

    loop();
```

## 5. 2D Wave

Many of these lend themselves better to a two dimensional output. But they're still pretty good on the single line we have to play with. For instance we can make a string of multiple height varied block characters and construct a nice little wave:

![wave.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/wavy.gif)

```javascript
function loop() {
        var i, n, s = '';

        for (i = 0; i < 10; i++) {
            n = Math.floor(Math.sin((Date.now()/200) + (i/2)) * 4) + 4;

            s += String.fromCharCode(0x2581 + n);
        }

        window.location.hash = s;

        setTimeout(loop, 50);
    }

    loop();
```

## 5. Progress bar

Using the variable width characters we can even wiggle on the horizontal, creating something like a progress bar:
Check it out Live Demo here: http://wavyurl.com/

![progress.gif](http://matthewrayfield.com/articles/animating-urls-with-javascript-and-emojis/progress.gif)

```javascript
function loop() {
        var s = '',
            p;

        p = Math.floor(((Math.sin(Date.now()/300)+1)/2) * 100);

        while (p >= 8) {
            s += '█';
            p -= 8;
        }
        s += ['⠀','▏','▎','▍','▌','▋','▊','▉'][p];

        location.hash = s;
        setTimeout(loop, 50);
    }
```


## Credits - by Matthew Rayfield
