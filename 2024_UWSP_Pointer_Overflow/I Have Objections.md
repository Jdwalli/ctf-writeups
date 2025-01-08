# I Have Objections
Web, 100 points

## Description:
Ok, I'm a little nervous about this one. It seemed like a good idea when I came up with it and I suppose it's too late to back out now... This next challenge will involve compromising a live stream site and to make sure it's as real as possible, I've set up a camera and will be broadcasting LIVE 24/7 until the end of the contest! Join right away, and you'll be treated to a little behind-the-scenes walk-through of Prof Johnson's lab and while you're there see if you can find the flag!

NOTE: Since this is a 100-level challenge, let me save you a little time: /flag

## Solution:

Trying to access ``/flag`` will just give us a 403 error. If we click on the Report Abuse / Service Issue button, we can see there is a field for input. This field is vulnerable to Server-Side Template Injection (SSTI).

The following injection reads the app.py file and gives us the flag:
 ``{{request.application.__globals__.__builtins__.__import__('os').popen('cat app.py').read()}}``


The flag: ``poctf{uwsp_71m3_15_4n_1llu510n}``