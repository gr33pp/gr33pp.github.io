## What is this?
### Category: Misc

![Image of challenge](https://i.imgur.com/Z7vWYaY.png)

>**I have some files. But I have no idea what are these!!**

Here we were given a zip file to download. The zip contains one image file and over 300 unknown files. The files are in sequence and named flag_aa, flag_ab,....,flag_ba, flag_bb,... to flag_np.

On viewing the image file (flag_aa), I realized that it was incomplete, only a black strip at the top showed. 

![Image of incomplete photo](https://i.imgur.com/JfuWnAD.png)

The first idea I got is that the other files came from the photo. On checking the hex values of few files apart from flag_aa, they had no "magic number".. Magic number is what makes a png file be recognisable as a png file by a computer..

Next I proceeded to manually copy the hex of flag_ab and append it to flag_aa using bless, a gui hex editor.. It worked, a strip of pixel was recovered. I couldn't do it by hand for over 300 files, so I wrote a python code to do the task

``` py

def merge_hex_files(file_prefix, num_parts, output_path):
    merged_hex = b""
    for i in range(num_parts):
        letter1 = chr(97 + (i // 26))  
        letter2 = chr(97 + (i % 26))
        part_file = f"{file_prefix}_{letter1}{letter2}"
        with open(part_file, 'rb') as f:
            hex_data = f.read()
            merged_hex += hex_data

    with open(output_path, 'wb') as f: 
        f.write(merged_hex)

    print(f"Image parts merged successfully bro! Saved to {output_path}")

if __name__ == "__main__":
    file_prefix = "flag"
    num_parts = 354
    output_path = "merged_image.png"

    merge_hex_files(file_prefix, num_parts, output_path)

```
or just this command

```bash
$ cat * > finalflag.png
```

Success, it appended each file to flag_aa as they were named alphabetically...

![Image of merged photo](https://i.imgur.com/IPUfPg5.png)

Flag: `BDSEC{1tS_@_PnG_f1LE_}`
