# Things Seen and Unseen
Stego, 100 points

## Description:
One of my first jobs in cybersecurity was at a major retailer in the USA. A multi-billion dollar, Fortune 500, international corporation. You'd think a business like that would have all kinds of resources invested in IT, but that wasn't the case.

The whole company hinged on an inventory system. If it went down the company started treading water immediately. This inventory system was released in 1986 and was written in Cobol. The original programmers were kept on retainer to handle problems when they cropped up, and these people were well in to their golden years.

I used to think about how untenable this was, and wondered to myself about what the company would do when their time finally came. By the time I came around, there were only three of them left, and only two of those had worked on the most important portions of the program. The last one only did code reviews on the least significant bits, and even he was part of the eternal work of maintaining this single program!

I asked DALL-E to whip up a representation of the lengths the company would go through to avoid change. Enjoy!

![Image](images/Stego100-1.png)

## Solution:

The clue is in this line from the description: *"The last one only did code reviews on the least significant bits, and even he was part of the eternal work of maintaining this single program!"*

We can use a tool called [zsteg](https://github.com/zed-0xff/zsteg) to examine the image's least significant bit and find the flag.


```shell
zsteg lsb Stego100-1.png
```



The flag: ``poctf{uwsp_wh47_15_d34d_m4y_n3v3r_d13}``

