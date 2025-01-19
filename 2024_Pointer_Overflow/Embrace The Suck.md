# Embrace the Suck
Misc, 200 points

## Description:
💁‍♀️ Lily: so… ignoring me this weekend huh 👀

🧑‍💻 Ben: what? nooo lol. just got this big ctf thing, super hyped for it 😅

💁‍♀️ Lily: right. the *ctf*. didn’t know i was competing w ur hacker obsession 🙄

🧑‍💻 Ben: it’s literally just a weekend. chill. i’ll text u, keep u updated n stuff

💁‍♀️ Lily: “updated” so i get like... play-by-plays? 🥱 “flag captured,” “firewall bypassed”? thrilling.

🧑‍💻 Ben: lmaoo stoppp 😂 ok how bout this: i’ll send u clues. lil secrets

💁‍♀️ Lily: ok now ur talking. spill 👀

🧑‍💻 Ben: alright, first one: *hub 0bbv1 cw hub jr0n*. see if u can crack it 😏

💁‍♀️ Lily: …is that supposed to mean something to me?? 😑 or just some nerd code to keep me quiet while ur off “capturing flags” or whatever

🧑‍💻 Ben: idk maybe it does 😏 or maybe i just know u hate unsolved mysteries

💁‍♀️ Lily: omg. yeah, maybe u just don’t wanna talk to me 😒 mystery solved

🧑‍💻 Ben: c’mon don’t be like that 😅 it’s one weekend. i’ll text u, drop hints, keep u close

💁‍♀️ Lily: u better. bc if all i get is “hub 0bbv1” and zero actual texts, i’m taking my “flag” somewhere else 😈

🧑‍💻 Ben: haha chillll. u know ur the only flag i’m tryna capture ❤️ gimme a lil luck?

💁‍♀️ Lily: whatever. good luck w ur nerd stuff 🖤 just remember who’s actually running the game 👋

## Solution:

We can solve the encrypted flag ``hub 0bbv1 cw hub jr0n`` by figuring out the substitution used. First, we can remove all numbers and replace them with their corresponding letters: ``hub obbvi cw hub jron``. Then we can use a frequency analysis tool like [quipquip](https://quipqiup.com/) to determine the substitution: **the needs of the many**.

Now we can use our Python tool to convert the text to leet speak get the flag! 

```python
char_set = '4bcd3f6h1jklmn0pqr57uvwxyz'
text = "the needs of the many"
mapping = dict(zip("abcdefghijklmnopqrstuvwxyz", char_set))
flag = ""
for char in text:
    if char == " ":
        flag += "_"
    else:
        flag += str(mapping[char.lower()])
    
print(f"poctf{{uwsp_{flag}}}")
```

The flag: ``poctf{uwsp_7h3_n33d5_0f_7h3_m4ny}``
