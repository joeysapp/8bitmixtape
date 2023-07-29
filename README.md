# 8bitmixtape
I've tried four times over the past year trying to get the 8bitmixtape-neo working, but I hadn't really known what was going on and it stopped being fun at like hour 4 every time. I think I'm close to getting it working though. My current progress:


# Notes
The ATtiny85 needs a bootloader flashed onto it first. Then you can upload whatever to it. Porn. I think I struggled with this primarily because I'm not sure how to tell if the bootloader actually is flashed, but I think it works. I assume you do this a lot [@jasapp](https://github.com/jasapp)

I'm 80% confident I get this step done. Step 2 on this page here: [https://learn.sparkfun.com/tutorials/tiny-avr-programmer-hookup-guide/programming-in-arduino](https://learn.sparkfun.com/tutorials/tiny-avr-programmer-hookup-guide/programming-in-arduino)

However the next step is using the 8BitMixtape-Neo library/board manager to upload code. I get this error on my ARM and x86 laptop with any code, even just empty loops/setups:
```bash
Failed uploading: cannot execute upload tool: fork/exec /Users/zooey/Library/Arduino15/packages/8BitMixtape/hardware/avr/0.0.28/tools/hex2wav/macosx/hex2wav: bad CPU type in executable
```
I've searched around a bunch and never found anything super helpful. I thought it was macos silicon issue, but my x86 mac does the same thing. I'm not sure if this is indicative of the bootloader not being flashed properly, or what.

The hex2wav ([https://github.com/ATtinyTeenageRiot/hex2wav](https://github.com/ATtinyTeenageRiot/hex2wav)) repo is not exactly active or informative. I tried doing this step on my windows machine, but that was even worse installing usb drivers and chanting "hail satan".

So my next bootloader attempt (because I assume the hex2wav deal is in the above bootloader) is the TinyAudioBoot ([https://github.com/ATtinyTeenageRiot/TinyAudioBoot](https://github.com/ATtinyTeenageRiot/TinyAudioBoot)).

I am not entirely clear, but I think I can run this to flash the bootloader, then I can play hex files to it to get code onto it. I think ideally I would use the above bootloader, but I'm not really sure what's wrong with hex2wav.
```bash
avrdude -v -pattiny85 -c avrisp -P/dev/ttyACM0 -b19200 -Uflash:w:/home/dusjagr/Arduino/AttinySound-master/AudioBoot/AudioBootAttiny85_InputPB3_LEDPB1.hex:i
```
Except the tiny programmer doesn't show up anywhere under /dev/ that I can tell.


Sorry I never got this working. I kind of understand more what's going on, but not really.

# Jeff's Solution
![jeff is so clever and smart however he worships satan and smokes dank kushreef](https://github.com/joeysapp/8bitmixtape/blob/master/jeffs-solution.gif?raw=true)
```clojure
    (rich hickey)
```


# Further reading, or so I can close 100 tabs and go to bed
https://github.com/8BitMixtape/8Bit-Mixtape-NEO/wiki/0_1-Examples-8BitMixtape-NEO
https://8bitmixtape.github.io/

Method of .HEX files as audio with the mixtape hooked up via audio jack. It needs to have the bootloader before this. 
https://8bitmixtape.github.io/8Bit-Mixtape-NEO/webpage/

General IDE integration, for both flashing the bootloader and then the 8BitMixtape lib.
- The 8bitmixtape .json file won't register in my Windows IDE.
https://github.com/8BitMixtape/8Bit-Mixtape-NEO/wiki/4_3-IDE-integration

Some random chinese people
https://github-wiki-see.page/m/8BitMixtape/8Bit-Mixtape-NEO/wiki/4_5-Testing-the-prototypes

Ada talking about avrdude stuff
https://www.ladyada.net/learn/avr/setup-mac.html
