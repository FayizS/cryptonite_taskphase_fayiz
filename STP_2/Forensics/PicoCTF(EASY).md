## CanYouSee
- The question provides this file:
<img src="images\ukn_reality.jpg">
- I used up the first hint:
<img src="images\canyouseeHINT.png">
- So I searched on google and found a [website](https://www.metadata2go.com) to view the metadata of an image.
- I added this image and found a line which looked encrypted.
<img src="images\canyousee1.png">
- Looks like base64 so I put it in a decrypter online and got the flag.
<img src="images\canyousee2.png">

## Verify
- Needed to learn a bit of things before starting:
    - `sha256sum` is used to compute and verify SHA-256 checksums for files. It generates a unique 64-character string (the SHA-256 hash) for a given file, which can be used to verify the integrity of the file.
    - A checksum is a value calculated from a data set, such as a file or a message, to detect errors or verify data integrity.
- I launched the instance and connected to the secure shell.
- I did ls and found 3 files, I tried to run the _decrypt.sh_ file and found out that I needed to run it with another file as an arguement, naturally I tried running it with the other file in the directory.
```console
ctf-player@pico-chall$ ls
checksum.txt  decrypt.sh  files
ctf-player@pico-chall$ decrypt.sh
Expected usage: decrypt.sh <filename>
ctf-player@pico-chall$ ./decrypt.sh
Expected usage: decrypt.sh <filename>
ctf-player@pico-chall$ decrypt.sh checksum.txt
bad magic number
Error: Failed to decrypt 'checksum.txt'. This flag is fake! Keep looking!
```
- Next I read the checksum.txt file.
```console
ctf-player@pico-chall$ cat checksum.txt
55b983afdd9d10718f1db3983459efc5cc3f5a66841e2651041e25dec3efd46a
```
- After a bit of thinking I thought of checking out the other directory present.
```console
ctf-player@pico-chall$ ls ./files
0SgkM1fC  5HAN1XjT  ABh1G8a0  FYfLvi5w  KhnreD4t  PoAr7OrB  VBHAXd7G  ZZzeAnnA  g1qINnts  n6yqXRv8  rXWuGW1m  y2XXKk9C
0aer7B0J  5ntikrlo  AUijzvDq  FcWqkSIP  L9tRKUkW  PtRzswzh  VM5DLaA2  aDI9kNj8  gewOpz6a  nSepPhk6  rgZiIAPZ  y8THzTYH
0b3lt0HK  5ymaOO07  AWnJiVoE  FhDH2g8j  LZgQIZ9b  QBtXtwy6  VU1Tnx8J  aUzSODcp  gr99Nl0G  nTEqj1Ol  rjta4881  yOmzIQym
.... and so on
```
- Got this, I ran these using the `sha256sum`.
```console
ctf-player@pico-chall$ sha256sum ./files/*
bfdc01f76e8bc1005b776a1ec5549e36be5fb4c1e7f4f74df1b6d6131cee8cea  ./files/0SgkM1fC
5a17f5fc0a4155df971ab0203d2fb05cc7195987b59140761f32f6d5c31b9de6  ./files/0aer7B0J
f73351bd65fe61f42271034530a5407d7d55eb3db76fbc9bb571364d3ea68555  ./files/0b3lt0HK
03745554bdecc96203cc3247cf90c727ee99c93308664a9dc5cd59e2aa15721c  ./files/0ia8IBYb
afd9ef148f40ceed70513115c42d089a897f50427caf999b2f555c6060bb2f67  ./files/0uUAy06x
7aff8340cdf99b9fe05035e5baf5a89668702e14ff3fc0f00b77eec42225bf56  ./files/17iH5ioj
56582ffb01b8f43e23e4d2ede263f5679588391ccd22ae307845fcf23f91b572  ./files/1CY2Hque
9b54d11b62e34e9e98d3c19acc3ce58f3c981b52a73fcabd8e0e67fd2f34ae08  ./files/1LPOMJE7
d00acb64414a2159cd79dd4d3f44f7e50d0ce6713e69e28ca3dca17e348a1545  ./files/1P5dsfLj
d99059d151a6953d015df736a672b2dd0ad3cc859f13114afa127ee36beaef74  ./files/1Tst6fbt
1b719d246e51b1b188f40449246eb1654cee5b0f625a57f5c8cd653076eda4bf  ./files/2CyEUmhf
..... and so on for all the files.
```
Note:
    - Use `sha256sum <directory>/*` to run all the files in a directory.
- Then I thought of searching the content of the `checksum.txt` in the previous output.
```console
ctf-player@pico-chall$ sha256sum ./files/* | grep "55b983afdd9d10718f1db3983459efc5cc3f5a66841e2651041e25dec3efd46a"
55b983afdd9d10718f1db3983459efc5cc3f5a66841e2651041e25dec3efd46a  ./files/2cdcb2de
```
- Using this file with the _decrypt.sh_ got me the flag.
```console
ctf-player@pico-chall$ decrypt.sh ./files/2cdcb2de
picoCTF{trust_but_verify_2cdcb2de}
```

## Scan Surprise
- Pretty straightforward, just scanned the QR code.

## Secret of Polyglot
- Came with a pdf file that contained the second half of the file.
- I found the First half of the file when I opened the file using VLC.

## information
- Same as **Can You See** Challenge, put the image in the metadata viewer website then saw a line that looked encoded, put it into a base64 decoder and got the flag.

## Glory of the Garden
- Challenge came with an image, which had nothing interesting, needed to use the clue which told me about a hex editor.
<img src="images\garden1.png">
- I found an [online hex editor](https://hexed.it) where I put the image and searched for "pico" and found the flag, I couldnt copy it directly so I copied it in hex and used a [hex to string converter](https://codebeautify.org/hex-string-converter).
