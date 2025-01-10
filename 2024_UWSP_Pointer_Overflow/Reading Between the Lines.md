# Reading Between the Lines
Stego, 100 points

## Description:
Good news, everyone! I've decided it's time to write my memoirs. After a lifetime of interesting experiences, I think it's time the astounding story of my life be recorded for the benefit and advancement of humanity. I can tell everyone about the time that I... Hmm... Ok, maybe my life isn't so interesting after all...

...But it can be! I'm going to throw in a couple interesting details! Give it a little something extra! No one will notice if I embellish a little as long as I don't change it too much. I can always just put a disclaimer on it that its only based on true events - a little transparency is a good thing.

## Solution:

This description gives us a hint that there will be hidden characters using an online [tool](https://www.soscisurvey.de/tools/view-chars.php) allows us to see these zero width characters. 

We can then write a script to extract them and convert them into binary.

```python
text = open("Stego100-2.txt").read()
zero_width = ''.join(c for c in text if c in ['\u200b', '\u200c'])
print(zero_width.replace('\u200b', '1').replace('\u200c', '0'))
```

After converting the binary to ASCII we are able to see the flag!

The flag: ``poctf{uwsp_b3w4r3_7h3_j4bb3rw0ck}`` 