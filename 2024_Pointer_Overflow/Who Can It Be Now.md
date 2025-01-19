# Who Can It Be Now
OSINT, 100 points

## Description:
A trip through time through the power of open-source intelligence! Start by finding the location in this image:

![Image](images/OSINT100-1.jpg)

Boy, I bet it's changed a lot in a century or so. You should find out. If you do, you'll see a business on the corner with a rustic chic style. Convert the words on the awning closest to the intersection into a flag using the alphabet in the rules and accept your daily bread. (i.e. poctf{uwsp_ _ _ })


## Solution:
After downloading the image, we can use a tool like ``exif`` to examine any metadata that hasn't been removed from the photo.

```console
EXIF tags in 'OSINT100-1.jpg' ('Motorola' byte order):
--------------------+----------------------------------------------------------
Tag                 |Value
--------------------+----------------------------------------------------------
Orientation         |Top-left
X-Resolution        |300.0000
Y-Resolution        |300.0000
Resolution Unit     |Inch
Software            |Adobe Photoshop CS5 Windows
Date and Time       |2016-01-06T13:18:33-05:00
Exif Version        |Exif Version 2.2
Pixel X Dimension   |1200
Pixel Y Dimension   |1137
FlashPixVersion     |FlashPix Version 1.0
Color Space         |Uncalibrated
--------------------+----------------------------------------------------------
```
Since `exif` doesn't yield any actionable results, we can use an online reverse image search tool like [TinEye](https://tineye.com/) to determine the image's origin.

We see several results, one of which is from [this](https://www.buzzfeed.com/gabrielsanchez/incredible-photos-of-nyc-100-years-ago-compared-to-today) BuzzFeed article titled "12 Remarkable Pictures Of NYC's Fifth Ave In 1911 Vs. Today." 

Our image appears first on the website with the title "West 8th Street and 5th Avenue in 1911 vs. Today."

Now that we know the image was taken on West 8th Street and 5th Avenue, we can look for the building. 

[Google Maps](https://www.google.com/maps/@40.732253,-73.9963624,3a,15y,-31.9h,90.21t/data=!3m7!1e1!3m5!1sWfmSs3bkyWWj7trpNop3tw!2e0!6shttps:%2F%2Fstreetviewpixels-pa.googleapis.com%2Fv1%2Fthumbnail%3Fcb_client%3Dmaps_sv.tactile%26w%3D900%26h%3D600%26pitch%3D-0.20528332999987242%26panoid%3DWfmSs3bkyWWj7trpNop3tw%26yaw%3D-31.901337225717697!7i16384!8i8192!5m1!1e1?entry=ttu&g_ep=EgoyMDI1MDEwMi4wIKXMDSoASAFQAw%3D%3D) shows us that the building's name is `Le Pain Quotidien`. 

We just need to convert that text to text that aligns with the flag's format. 

```python
char_set = '4bcd3f6h1jklmn0pqr57uvwxyz'
    text = "le pain quotidien"
    mapping = dict(zip("abcdefghijklmnopqrstuvwxyz", char_set))
    flag = ""

    for char in text:
        if char == " ":
            flag += "_"
        else:
            flag += str(mapping[char.lower()])
    
    print(f"poctf{{uwsp_{flag}}}")
```

The flag: ```poctf{uwsp_l3_p41n_qu071d13n}```