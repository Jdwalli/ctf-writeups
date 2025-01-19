# Well Said but Poorly Heard
Reverse, 100 points

## Description:
So there I was, knee deep in wet newspaper, a puppy under each arm, and a lion hovering over me on the back of a giant dragonfly. Only one thing separating me from certain death at the hands of the President of Murder was the Sphinx and its riddle.

"Ask your riddle, Peptopotamus!" The puppy under my right arm commanded. Its stone face moved, kicking off ancient dust, turning its glowing eyes to us. It spoke its riddle.

"True to false and false to true
What you did before, now undone,
And when you're wrong, reverse your sight.
What am I?"

The lion laughed, but he did not know what I knew. He did not know that I created the attached program when I was only 18 months old, and not only did I know the answer to his riddle - I was its master. Now, I give the program to you, so you too can be prepared if you find yourself in a similar situation.

## Solution:
Running the program gives us nothing useful so we need to open it in Ghidra. The main function looks like this:

```c++
undefined8 main(void)
{
  undefined8 local_38;
  undefined8 local_30;
  undefined8 local_28;
  undefined7 local_20;
  undefined4 uStack_19;
  
  local_38 = 0x77757b6674636f70;
  local_30 = 0x31775f6e315f7073;
  local_28 = 0x33723368375f336e;
  local_20 = 0x7572375f35315f;
  uStack_19 = 0x7d6837;
  obfuscate(&local_38);
  printf("Encoded flag: %s\n",&local_38);
  return 0;
}
```

When can write a short Python script to decode the hex values and give is the string:

```python
hex_parts = ["77757b6674636f70", "31775f6e315f7073", "33723368375f336e", "7572375f35315f", "7d6837"]
flag = "".join(bytes.fromhex(part).decode('utf-8')[::-1] for part in hex_parts)
print(flag)
```

The flag: ``poctf{uwsp_1n_w1n3_7h3r3_15_7ru7h}``


