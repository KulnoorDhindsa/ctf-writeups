# Level 0 → 1
### Objective: Figure out the password for level 1 hidden on a webpage
### What I thought and executed:
1. I searched around for hidden texts in plain sight by randomly selecting the screen using the mouse, which obviously failed.
2. Then I clicked on `Submit Token`, it led me to another webpage `WeChall[WeChall]`, which I explored and did not find the password.
3. Then, after going back to the [Natas0](https://natas0.natas.labs.overthewire.org) web page, right-clicked and selected `inspect` to open `Dev Tools` (Developer Tools).
4. I explored all the menus: `Elements`, `Console` and the lot. 
5. Then I googled the suggested tools at [OverTheWire Natas](https://overthewire.org/wargames/natas/), i.e. `curl` and `ZAP proxy`.
6. I ran the default syntax of `curl` in the `console` by running `curl -I https://natas0.natas.labs.overthewire.org` and got error after error.
7. Then I went back to the elements, and decided to look at the HTML code in front of me carefully, without over-complicating things at the beginning level.
8. Then I saw there are clickable `...` in between tags in the code. I clicked on multiple `...` nested in the HTML code until I found the password for the next level inside a comment using the `<!---    --->` tag.
### What was required:
1. Right-click on the website for Natas0 and click `inspect`.
2. In the `Elements` menu, click on the clickable `...` in between the `<body></body>` tags.
3. Click on the `...` in between the `<div id="content"></div>`, which revealed the password in the comments written in the `<!---  --->`. 
### What I learnt:
- Dev Tools, *automatically* collapses the content of `<body></body>` to save screen space, by using `<body>...</body>` (`...` are *ellipses*).
- After reading the content of the `<body></body>` or any other collapsed content of any tag, to get the *ellipses* `...` back, a small **triangle/arrow icon** appears beside the text; when clicked, restores code to the collapsed form.
- Go through the code **carefully**, read terminal outputs carefully; hints are usually right in front.
- Certain details can be easily *compromised* in the code, or even the terminal outputs, which are mostly logged and stored somewhere.
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
### What was required: 
1. Entering the URL `http://natas3.natas.labs.overthewire.org/robots.txt`, clicking the `users.txt` file and obtaining the password.
### What I learnt:
- `robots.txt` is a file stored on the server which contains the files that the server is and isn't allowed to visit, meaning few hidden files may be stored there.
---
# Level 4 → 5
### Objective: Figuring out the password to the next level but access is only given to 'natas5', not natas4 user
### What I thought and executed: 
1. Since it read that only `natas5` user is allowed permission and not `natas4`, I had to either login as `natas5` or make it look like I'm `natas5` user. 
2. I tried to login natas5 website, but without the correct password, that attempt failed.
3. I googled, (rather used  CLAUDE), as to how do I make it look like I'm `natas5` and not `natas4` user, I was suggested `curl` which comes pre-installed in windows 10/11.
4. There are 2 ways to go forward from here:
5. Method 1
    1. I had already installed **Burpsuite**, so I manually turned on the **Intercept mode** in Burpsuite and in settings of my laptop, I turned proxy settings on, and connected it to port: 8080 and IP address `127.0.0.1`.
    2. Then I refreshed the page of `natas4`, and Burp caught the request, which was raw HTTP, there I scrolled down to `Referer` header and changed it to `http://natas5.natas.labs.overthewire.org`, making it look like I was `natas5` user and not user `natas4`. And the password to next level was visible.
6. Method 2
    1. Using the `curl` command in **command prompt** as `curl -u natas4:password_to_natas4 -e "http://natas5.natas.labs.overthewire.org"` where `-u` tag is for *user* and is of the format *-u user:password* and `-e` tag is for *referer* header.
    2. This command directly changes the *referer* header without requiring a *proxy*. And the password for next level was visible on the page.
### What was required:
1. `curl -u natas4:password_to_natas4 -e "http://natas5.natas.labs.overthewire.org"` to directly alter the **referer** header to natas5 without requiring a *proxy*.
### What I learnt:
>A **proxy** sits in between browser and server. Every request made by browser, is first sent to proxy, which then *forwards* it to the server.

>Any data orignating from client side (like headers, cookies and js-side validation) has no proof, and is just something asserted by the client. This allows client side checks to by *by-passed*.

- **Burp Suite** is a *proxy server*.
- The IP address `127.0.0.1` means **this localhost machine**. Its's used here so that Burp Suite can send/recieve traffic to/from my localhost machine only, and not from somewhere else on the internet.
- Port `8080` is the by-default port that burp Suite listens to and is active on.
- This can and probably has become a common method of hacking systems, by intervening active *response* and *requests* from end-systems, falsifying information or even copying data.
---
# Level 5 → 6
### Objective: Figuring the password for the next level but "Access dissalowed. You are not logged in."
### What I thought and executed
1. I tried `http://natas5.natas.labs.overthewire.org/robots.txt/` to check is the password was in there, but this page doesnt exist. (due to the `404 Error` which means 'not found').
2. I right clicked and selected `inspect` and checked `Elements` along with `View page source`, but found nothing. I viewd the same again and again incase I overlooked something, but nothing.
3. Then I thought, it says 'Access dissalowed' and 'not logged in', in websites requiring logins, `cookies` are responsible for knowing my identity as I scroll through the website. I googled how to look at 'active cookies' on a website using 'dev tools'.
4. In `inspect`, I went to `Network` menu, refreshed the page and clicked on the first link that shared the name of the URL. I scrolled through it, and found two sections `Request Headers` and `Response Headers`, and under both of them was `cookies` section. 
5. The `Request Header` has `loggedin=0` and `Response Header` had a `ga_` followed by a string, which I found out was **Google Analytics Tracking Cookies** of the website OverTheWire, which I figured was had nothing to do with this specific level.
>All client side data is not proof, and is just an **assertion**. So, this can be falsified.
6. I searched how to change the value of a cookie on a website using dev tools in Natas. Then I went on `Application` and in *Cookies*, there was a cookie named `http://natas5.natas.labs.overthewire.org`, I clicked it, then on the 'value' section where it said `loggedin=0`.
7. I first tried `natas5`, but it failed. Then I got to thinking, `natas5` didn't work, the password won't work either. After a few minutes, it hit that computer's response is either `0` or `1`. If it isn't `0`, it has got to be `1`. Then I refreshed the page, and the password was visible on the screen.
### What was required:
1. To right click, `Network`, refresh the page, select the page sharing with the URL.
2. Look throught the headers, and under headers, `Request Header`, it said `cookie  loggedin=0`.
3. In `Application` and then `storage`, selecting the cookie under `cookie` that shares the URL, double clicking the value `0`, changing it to `1` and refreshing the page.
### What I learnt:
- Cookies are responsible for knowing our identity (IP address, username (if logged in)) while we look through the website. 
- Slight *binary* changes in the code, can possibly lock people out of their accounts
- Computer communicates in binary, and it's responses will be either `0` meaning *no*/*False* and `1` meaning *yes*/*True*.
- Since client side information is just **assertion** and has no proof, it can be altered and not be questioned.
---
# Level 6 → 7
### Objective: Figuring out the password for next level but `Input Secret: `
### What I thought and executed: 
1. I right clicked and selected `inspect`, viewd the html code, which had a new `<form></form>` tag, which labeled the input as *secret*.
2. Then I went to `Network`, refreshed teh page and scrolled through the headers, it had `gzip` encoding and the accepted encoding was `gzip` in english.
3. I also found in `authorisation` in network, a *string* but it wasen't the password.
4. Then I clicked the `View Sourcecode` link given on the home page. This code had `<?></?>` tag, which included `include "includes/secret.inc"`.
5. I went to `http://natas6.natas.labs.overthewire.org/includes/secret.inc` which opened another html page with the `secret`, which was a string.
6. I entered this `secret` string in the input box on the home page, and I got the password.
### What was required:
1. Click the `View Sourcecode` link on the home page, look at the `include "includes/secret.inc"`.
2. Go to `http://natas6.natas.labs.overthewire.org/includes/secret.inc`, copy the *secret* string, paste it in the input box on the home page, and get the password.
### What I learnt:
1. To look at html code with attachements not as 'this is an attachement link', but as 'there are these folders on the server which may contain more than just the attachement (be it video, image or a file)'.
---
