---
title: Suede Dactyl Manuform
date: 2020-12-11 17:30:00 -0800
categories: [Projects, Electronics]
tags: [hardware, firmware]
---
# ![](/assets/img/posts/suede-dactyl-manuform/image2.jpg)

# BACKGROUND

For quite some time now, I wanted a custom high quality keyboard, and after purchasing an Ender 5 extrusion 3d printer, I finally had the means.

When I’m not programming for work or pleasure, I like to work on electronic projects. I use arduino a lot, simply because of the support I get with the community, not because I think it’s the most superior platform out there. My day-to-day is web-development, so it's nice to jump into lower level subjects to switch things up.

# OVERVIEW

I 3D printed the shell on my [Ender 5](#ender-5) with black Hatchbox PLA. I then sanded and filed it down to get as clean a result as possible before spraying it with [loctite](#loctite) and wrapping it in [suede](#suede-1). After painstakingly cutting out, trimming, and filing the suede for each switch hole, I socketed the [switches](#purple-zealio-v2-67g-switches) and handwired them to an arduino in a matrix pattern. Finally, I customized the QMK firmware for my specific matrix layout and flashed it onto each board’s arduino.

# MILESTONES

## Shell

This whole project would not have been possible without my 3D printer. Late last year, I bought an [Ender 5](#ender-5) that let me polish my 3D printing skills. I learned what models needed what infil, when to use a thinner or thicker wall thickness, what situations requires which scaffolding, how to post cleanup and debur my prints, how to get a consistent ambient temperature while still having constant air flow, what effect humidity had on my filament when printing, and the slurry of infamous bed leveling techniques (without an auto leveler) and more.

My first print started with a good adhesion to the [printer bed](#glass-printer-bed). About an hour into it, extrusion became inconsistent and the print failed. Next try failed right after the first layer, somehow the extruder head pulled the first layer free, which might have been due to the ambient temperature being too low. The third print started well... good adhesion, ambient temperature and consistent air flow. After 24 hours, I had the left keyboard printed, and another 24 hours later, the right.

_Initial Print_
![Initial Print](/assets/img/posts/suede-dactyl-manuform/image6.jpg)

I spent a good portion of the next day carefully removing all the support structures. Next I sanded the flat surfaces and filed the corners and edges until I was absolutely sure I couldn't feel any signs of layer lines or artifacts.

## Suede

The Dactyl Manuform, in and of itself, is as custom as you can get, but I still felt that personal touch was missing. Microsoft’s Alcantara suede (faux suede), that is used on surface keyboards, softly and comfortably surrounds what would otherwise be hard keycaps. This is why I decided to wrap the entire keyboard in a high quality suede. I did some research into the quality over time of how Alcantara ages, and was disappointed to find that it wears much faster than typical suede, and after it wears, the texture becomes gritty and nasty… So I instead bought a [premium quality suede sheet](#suede-1) and some [loctite](#loctite) to wrap the freshly sanded keyboards.

I don’t have images for this portion of the process as both my hands were occupied throughout.

I sprayed the keyboard’s top and sides with the loctite and immediately applied the suede (this is time-sensitive since the loctite dries pretty fast). The loctite wasn’t particularly necessary since the suede sheet already had an adhesive, but I wanted to be extra sure that it wasn’t going to separate from the keyboard. I started wrapping from one side to the other, which was a mistake. The suede conformed to the first side well, but as it started wrapping to the adjacent sides, there was an unavoidable fold due to the geometry. Therefore, I ended up having to cut a seam at two corners to completely make contact between the suede and keyboard. The second keyboard went more smoothly. Instead of starting my wrap from a side of the keyboard, I began from the top. This allowed me to push the creases out, avoiding the need to cut a seam.

_Suede Tear Seems_
![Suede Tear Seems](/assets/img/posts/suede-dactyl-manuform/image7.jpg)

Finally, I painstakingly cut each keyboard switch hole out with an exacto knife and filed the edges before carefully socketting each switch into its final resting place. It was a very tedious process getting the switches to snugly click into place, as the 3d printing process left the formation of the sockets a bit rough even after filing. Luckily, I was able to compensate for that with a more conservative trimming of the suede on those particular holes.

## Key Switches and Wiring

I soldered the [diodes](#diodes) to direct the current flow out from the same pin on each switch. Then, I chained the diodes together forming the rows. Lastly, I soldered the thumb cluster’s diodes together to form their own logical row.

_Diode initial Soldering_
![Diode initial Soldering](/assets/img/posts/suede-dactyl-manuform/image4.jpg)

_Diode Rows Right Side_
![Diode Rows Right Side](/assets/img/posts/suede-dactyl-manuform/image8.jpg)

For the Columns, I soldered insulated [wires](#wires) to the switches’ other pin. For a cleaner look, and to cut some time, I melted off the insulation on the wire at each pin point with my soldering iron, then wrapped the uninsulated portion of the wire around said pin, soldered, and repeated the process for each column.

_Wire Columns Right Side_
![Wire Columns Right Side](/assets/img/posts/suede-dactyl-manuform/image1.jpg)

Finally, I wired the rows (colorful wires) and columns (black wires) to the arduino on pins 15, 14, 16, 10 and pins 5, 6, 7, 8, 9 respectively. Then I soldered the TRS jacks to the arduino ground and #3 pin and soldered another two wires to ground and reset pin for the reset button.

_Final Matrix Wiring to Arduinos_
![Final Matrix Wiring to Arduinos](/assets/img/posts/suede-dactyl-manuform/image3.jpg)

I used the two TRS Jacks to connect both halves of the keyboard with an Auxiliary 3 pole cable (standard headphone cable). Then, I added a simple reset button to the right keyboard so that I could easily flash it without removing the bottom screws and exposing the wiring inside.

_Reset Button with wires pulled through_
![Reset Button with wires pulled through](/assets/img/posts/suede-dactyl-manuform/image9.jpg)

## Flashing

Flashing the firmware was relatively simple. First, I set up a [QMK](#qmk-setup) environment following the Arch / Manjaro instructions and tested the build. Then I cloned the [QMK repo](#qmk-firmware-repo), pressed the keyboard’s reset button, then immediately ran make handwired/dactyl_manuform/4x5:default:flash.

_Final Keyboard_
![Final Keyboard](/assets/img/posts/suede-dactyl-manuform/image2.jpg)

## Retrospective

While this project was a lot of fun, the sheer amount of labor required to hand wire the switch matrix was more than I expected. Some people have used flat copper tape, which they line into the rows and columns, push the switch pins through, then solder, which saves a lot of time. Others have used predesigned flexible PCBs, which still require soldering, but save time when designed to the correct dimensions. Using copper tape seems a bit flimsy to me, since I already made the mistake of using a very thin gauge wire which tends to break easily whenever I need to replace a switch or get inside of the keyboard requiring more maintenance. For this reason, I wouldn’t use copper tape and am considering the flexible PCB in future projects.

Another gripe I have is that my print has slight warping, especially in thin, flatter areas like the thumb cluster. I’ve thought of sending the 3D files to a service that specializes in high quality prints, but since this is a diy project, I preferred to do as much as I can with the tools I have at my disposal. An alternative solution to this problem would be to use a heated chamber for my 3d printer, encasing the air around the print to keep an even more consistent temperature throughout the print cycle.

All in all, I really like this keyboard. No longer do I have pain when I type, and the keys are laid out in such a way that it’s very easy for your fingers to hit each one. While the learning curve was difficult, once you get used to it, things are much faster. I had to keep the layout open on my laptop while I typed for about a week until I was confident enough on my own. The keyboard is portable and doesn’t take up much room because of its split nature and it’s simple enough to flash if I ever want to change the layout in any way (which isn’t all that trivial in an off the shelf, non programmable keyboard). I’m very happy with the work I put into this keyboard so far, and am looking forward to doing a second build when I get ambitious again.

# RESOURCES/LINKS

#### [Open Source Plans](https://github.com/abstracthat/dactyl-manuform)

#### [QMK Firmware Repo](https://github.com/tshort/qmk_firmware/tree/master/keyboards/dactyl-manuform)

#### [QMK Setup](https://beta.docs.qmk.fm/tutorial/newbs\_getting\_started)

#### [Ender 5](https://www.amazon.com/gp/product/B07X9R1TWS/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8&psc=1)

#### [Glass Printer Bed](https://www.amazon.com/gp/product/B07FSM8DK9/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8&psc=1)

#### [Suede](https://www.amazon.com/gp/product/B00CBJLNW2/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8&psc=1)

#### [Loctite](https://www.amazon.com/gp/product/B0732SQRC7/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8&psc=1)

#### [Purple Zealio V2 67g Switches](https://www.1upkeyboards.com/shop/switches/set-packs/zealio-v2-switch-packs/)

#### Diodes
**Search for:** *1N4148 Fast Switching Diode by SEMTECH choose quantity USA SELLER Replaces 1N914*

#### [Wires](https://www.amazon.com/gp/product/B07HFBRBQ3/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8&psc=1)

#### [Rubber Feet Bumper Pads](https://www.amazon.com/gp/product/B07CNQC695/ref=ppx\_yo\_dt\_b\_search\_asin\_image?ie=UTF8&psc=1&fpw=alm)
