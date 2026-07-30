# Level 0 → 1
### Objective: Figure out the password for level 1 hidden on a webpage
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
# Level 1 → 2
### Objective: Figuring out the password for next level on a webpage but right click isn't allowed
### What I thought and executed:
1. I tried right click to see if it was actually not permitted or was written to just throw people off.
2. If right click isn't allowed, the answer to this level is either in `inspect` or `View page source`. 
3. So I needed a *shortcut key* from the keyboard, or any other way to open *dev tools*, which is `Ctrl + Shift + i`.
4. Similar to the last level, after opeing the nested `...` (ellipses), I found the password to the next level in the `<div></div>` tag.
### What was required:
1. `Ctrl + Shift + i` to open *dev tools*, since right click wasen't permitted.
2. In `Elements` menu, after opening the nested `...`, under the `<div></div>` tag, I found the password for the next level.
### What I learnt:
- `Ctrl + Shift + i` is shortcut key for opeing dev tools, instead of right click inspect.
---
# Level 2 → 3
### Objective: Figuring out password for next level, but 'There is nothing on this page'
### What I thought and executed:
1. I right clicked and chose `inspect`, then went under `Elements` menu and read the code thoroughly, but didn't find anything.
2. I clicked `vie-source` clickable option near the `Elements` menu but didn't find anything.
3. After some thinking, I went back to `Elements` menu and carefully read the code once again, and under `<script></script>`, I found a password, but it was for the current level (*noted for the future).
4. Under `<script></script>`, another tag `<style></style>` tag, and in it was written:
```output
visibility: hidden !important
```
5. I didn't know what it meant. Then i went back to the orignal website and instead of right clikcing and selecting `inspect`, I chose `View source code`.
6. In the HTML file that opens in another tab, I read the code and found an `<img>` tag for the image of a `.`... then I saw the `src` and the complete tag was `<img src="files/pixel.png">`, meaning there is another folder `files` on the server which has one file `pixel.png`, not much to say that there couldn't be aother files.
7. So I types the URL `http://natas2.natas.labs.overthewire.org/files/` to open the folder `files` on the server. It opened a mini table having 2 entries: `pixel.png` and `users.txt`.
8. I clciked `users.txt` and found bunch of names with passwords, amongst which was password for `natas3`.
### What was required:
1. Right click and select `View page source`.
2. Carefully look at the `<img src="files/pixel.png"` tag and open the `files` folder on the server and read the password.
### What I learnt:
- To carefully read the code, output etc not once but many times, there can be many things missed.
- To look at code in a way that even `<img src="files/pixel.png"` read not as 'oh, there is an img in this code' but as 'oh, there is a folder `files` on this server' as first instinct.
- In the `<script></script>` tag, the password for the current levelis written with a `pass` condition for the same.
---
# Level 3 → 4
### Objective: Figuring out the password for next level but "There is nothing on this page"
### What I thought and executed:
1. I right clicked `inspect` and `View source code` for this page and explored, no hidden comments and no `<img>` tage to tell me if there were any hidden files stored on the server.
2. I still tried the URL `http://natas3.natas.labs.overthewire.org/files/` but there was no `files` folder.
3. In one of the comments in the code of `View source code`, there was a comment stating that 'not even Google can help me here'...which prompted me to google this level and I got the hint of `robots.txt`.
4. `robots.txt` is a text file stored in the server which tells the server which pages they can and can't visit. So, there might be a few *hidden pages* for a website that the server is not allowed to show the client. So, I entered the URL `http://natas3.natas.labs.overthewire.org/robots.txt`.
5. It showed a mini table with a file *users.txt*, like the last level.
6. I opened `users.txt` file and got the password for the next level.
### What I learnt:
- `robots.txt` is a file stored on the server which contains the files that the server is and isn't allowed to visit, meaning few hidden files may be stored there.
---
