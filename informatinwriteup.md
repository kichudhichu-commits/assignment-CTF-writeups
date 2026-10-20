# picoCTF 2021 - information (forensics)

## Challenge Metadata
- **category:** Forensics
- **Difficulty:** Easy
- **Description:** Files can always be changed in a secret way

---

## Summary
- actual flag was hidden in the metadata

---

## Initial steps

- **File Type:** JPEG image file was given with the challenge
- **Checking Metadata:**
```bash
exiftool cat.jpg
ExifTool Version Number         : 13.50
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2026:10:20 17:00:26+00:00
File Access Date/Time           : 2026:10:20 17:00:34+00:00
File Inode Change Date/Time     : 2026:10:20 17:00:33+00:00
File Permissions                : -rwxrwxrwx
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 13.25
License                         : YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```
- Here in **License**, a **Base64 encoded string** is given

```bash

echo 'YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9' | base64 -d

academy{the_m3tadata_1s_modified}
```

## Flag

**academy{the_m3tadata_1s_modified}**
