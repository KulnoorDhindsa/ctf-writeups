# Level 0 → 1
### Objective: Figure out the password for level 1 hidden on this level
### What I thought and executed:
1. I searched around for hidden texts in plain site by randomly selecting the screen using the mouse, which obviously failed.
2. Then I clicked on `Submit Tocken`, it lead me to another webpage `WeChall[WeChall]`, which I explored and did not find the password.
3. Then, after going back to the [Natas0](https://natas0.natas.labs.overthewire.org) web pade, right clicked and selected `inspect` to open `Dev Tools` (Developer Tools).
4. I explored all the menus `Elements`, `Console` and the lot. 
5. Then I googled the suggested tools at [OverTheWire Natas](https://overthewire.org/wargames/natas/), i.e. `curl` and `ZAP proxy`.
6. I ran the default syntax of `curl` in the `console` bu running `curl -I https://natas0.natas.labs.overthewire.org` and got error upon error.
7. Then I went back to the elements, and decided to look at the html code infront of me carefully, without over-complicating things in the beginning level.
8. Then I saw there are click-able `...` in between tags in the code. I clicked on multiple `...` nested in the html code, untill I found the password for the next level inside a comment using the `<!---    --->` tag.
### What was required:
1. Right click on the website for Natas0 and click `inspect`.
2. In the `Elements` menu, click on the clickable `...` in between the `<body></body>` tags.
3. Click on the `...` in between the `<div id="content"></div>` which revealed the password in the comments written in the `<!---  --->`. 
### What I learnt:
- Dev Tools, *automatically* collapses the content of `<body></body>` to save screen space, by using `<body>...</body>` (`...` are *ellipses*).
- After reading the content of the `<body></body>` or any other collapsed content of any tag, to get the *ellipses* `...` back, small **triangle/arrow icon** appears beside the text, when clicked, restores code to the collapsed form.
- Go through the code **carefully**, read terminal outputs carefully, hints are usually right infront.
---