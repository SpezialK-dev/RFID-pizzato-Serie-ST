# General Information about the Tag
SR DD420MK-D1T

Pin 1 and 3 are the power pins as specified by the manual. 
-> takes 24 V constantly 
-> around 12mA when ideling and no tag in range 
-> around 15~16mA when ideling and tag in range

-> It can ONLY hold a single tag as valid -> no multi tag support in our Version 
It appears to use the EM4100 Tags for identification. 

A2 is ground(sort of)

if Tag is recognized O3 is high(23.2 V) otherwiese its at 0.331V
-> messured between pin 5 and - output from bench powersupply 

## Behaviour with tags 

-> If tag with modified data (that does not match the original tag 2 modiefied bits in hex decimal) The reader does not throw out any visable error code -> it only gives an output in form of 
and LED lighting up green when the correct tag is held infront of it. 

-> it has an extreamly narrow range, of only a few cm, so its hard to even fit something between the Tag and the reader. -> extending the range by a few cm would be interesing
-> the flipper 0 has a slightly longer range than the Pizzato Reader 

# Copying and emulating the Tag

## Output from the Proxmark 3

The following thing also backs the flipper results
```
+] EM 410x ID A02A060F59
[+] EM410x ( RF/64 )
[=] -------- Possible de-scramble patterns ---------
[+] Unique TAG ID      : 055460F09A
[=] HoneyWell IdentKey
[+]     DEZ 8          : 00397145
[+]     DEZ 10         : 0705040217
[+]     DEZ 5.5        : 10758.03929
[+]     DEZ 3.5A       : 160.03929
[+]     DEZ 3.5B       : 042.03929
[+]     DEZ 3.5C       : 006.03929
[+]     DEZ 14/IK2     : 00687899807577
[+]     DEZ 15/IK3     : 000022890475674
[+]     DEZ 20/ZK      : 00050504060015000910
[=] 
[+] Other              : 03929_006_00397145
[+] Pattern Paxton     : 2686078297 [0xA01A4D59]
[+] Pattern 1          : 591822 [0x907CE]
[+] Pattern Sebury     : 3929 6 397145  [0xF59 0x6 0x60F59]
[+] VD / ID            : 160 / 0705040217
[+] Pattern ELECTRA    : 41002 397145
[=] ------------------------------------------------

[+] Valid EM410x ID found!
```



## Flipper


I was hopting that this would be more difficult, it wasnt. The flipper can just read + emulate the Tags. 
They are EM - Micro EM4100 Tags-> atleast from what the flipper is saying. Industrial standart ones,
-> The flipper zero also already has the possibility for doing a bit of fuzzing for this standart

[Datasheet for EM200](https://www.emmicroelectronic.com/sites/default/files/products/datasheets/em4200_ds.pdf)
[Datasheet for EM100](https://www.alldatasheet.com/html-pdf/154654/EMMICRO/EM4100/293/1/EM4100.html)


Since that was so easy and could not really be called research I looked into some other ways to missuse this thing. 

# Other evenues of attack 

- the pins on the back 
- maybe power analyis ? 
- generating abitrary keys with the flipper -> doable using the then write pin
- extending range of original tag?
  -> replay attacks

# How Keys are generated 

A further deep dive into EM100. 

## Notes to take away 

- Keys are etched into the Hardware so rewriting them _should_ not be possibel. 
- only a coild is needed to recieve power ? -> very simple logic should allow for replay attacks

### Possible Encodings
- Manchester 
- Biphase code 
- PSK

Currently it is unknown what encoding is used here.

# Replay Attacks 
originl messurable distance before light starts to blink orange/green 11.77mm this messurement ist perfekt but should give a baseline.

A [Forum post ](https://electronics.stackexchange.com/questions/99135/what-can-i-do-to-increase-passive-hf-rfid-read-range) about a similar topic. That could help me find things that could work to extend its range.

A [research paper ](https://www.sciencedirect.com/science/article/abs/pii/S0167923619302234) into that topic, that could be of interest.


# generating abitrary tags with the flipper


After simply copying the tag we are able to modify the hex value of the tag.
+
In the following images you show you the two modified tags
![modified tages](./images/modified_pizzato_Tag_information_flipper.png)

![original tag](./images/original_pizzato_Tag_information_flipper.png)

these can be saved to the device, 

# Sniffing with SDR


[Replay ](https://www.blackhillsinfosec.com/how-to-replay-rf-signals-using-sdr/)

This didnt turn out as planned and did not work with my cheap RTL-SDR. I didnt manage to detect anything my thing might have not been sensitiv enough
