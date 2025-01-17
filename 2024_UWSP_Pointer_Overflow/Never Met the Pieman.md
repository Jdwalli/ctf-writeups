# Never Met the Pieman
Forensics, 200 points

## Description:
The title of this challenge isn't a clue. It's a complaint. I took the family on vacation last summer. Can't remember where. Some city in Europe or Italy or Zealand or something. The wife wanted to go to some museum where they had some statue called the Pieman. Flew all the way there and stood in line all day. I ask the wife when we're going to see the Pieman, and she gives me this look like I'm speaking alien. No idea what I'm talking about. Whatever, by this point I'm so bored and the wife is telling me to record some of this stuff so we have memories for later. I pull out my camera and shoot this video. Decided to spruce it up a little with my awesome video editing skills. I guess none of this really matters for the purposes of this challenge, but feel free to check it out for yourself.

## Solution:

Running ``exiftool`` on the .mov file returns:

```shell
........
Layout Flags                    : Stereo
Audio Channels                  : 2
Track 2 Name                    : cG9jdGZ7dXdzcF83MW0zXzNuMHVnaF9mMHJfbDB2M30=
Matrix Structure                : 1 0 0 0 1 0 0 0 1
Media Header Version            : 0
...........
```

``Track 2 Name`` looks like it holds a base64 encoded string. We can decode it with this command:

```shell
echo 'cG9jdGZ7dXdzcF83MW0zXzNuMHVnaF9mMHJfbDB2M30=' | base64 -d
```

The flag: ``poctf{uwsp_71m3_3n0ugh_f0r_l0v3}``