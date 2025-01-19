# A Bitter Delicacy


## Description:
We're getting closer and closer to the end of Pointer Overflow 2022 and it's time for me to start tipping my hand, sharing those hidden secrets, and releasing the last few 400-level challenges that remain. This one requires access to some really high-end gear.

I know, I know... One of the contest axioms is that the challenges should be solvable with cleverness and skill and not good gear. Well, I'm going to give you access to my personal botnet for this one, so you should have all you need. Just be responsible with it!

To make sure you don't get up to any mischief I've hidden the login page to the admin console, have an error.log running in a secure location a level higher than the app, and I've hidden all other sensitive information using cutting-edge Linux methods (the OS hackers and the NSA use, look it up.) If you want to solve this one, it will require discovering a couple secrets and paying close attention to what you know so you can work out what you don't know.


## Solution:

The main page of the web app is unremarkable but there is a hidden [login page](http://34.135.223.176:10404/login).

The web application's main page was unremarkable, but a hidden login page was discovered at [http://34.135.223.176:10404/login](http://34.135.223.176:10404/login). Attempting to log in resulted in an error message:

``view-file log/error.log: Err7 - Bad username or password. Please check your credentials and try again``

This error message revealed the `view-file` parameter, suggesting a potential Local File Inclusion.

Testing the `view-file` parameter with `http://34.135.223.176:10404/view-file?file=log` returned an error indicating `/log` is a directory:

``Error: [Errno 21] Is a directory: '/log'``

Accessing `http://34.135.223.176:10404/view-file?file=log/error.log` successfully displayed the original error message, confirming local file inclusion:

``view-file log/error.log: Err7 - Bad username or password. Please check your credentials and try again.``

After manually attempting to find the correct folder, I found the `.hidden` directory. Accessing it directly (`http://34.135.223.176:10404/view-file?file=.hidden`) resulted in the same "Is a directory" error.

Accessing `http://34.135.223.176:10404/view-file?file=.hidden/flag.txt` revealed the flag:

The flag: ``poctf{uwsp_4ll_w3_h4v3_70_d3c1d3}``