# General Information about the Tag

Pin 1 and 3 are the power pins as specified by the manual. 
-> takes 24 V constantly 
-> around 12mA when ideling and no tag in range 
-> around 15~16mA when ideling and tag in range

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

I was hopting that this would be more difficult, it wasnt. The flipper can just read + emulate the Tags. 
They are EM - Micro EM4100 Tags-> atleast from what the flipper is saying. Industrial standart ones,
-> The flipper zero also already has the possibility for doing a bit of fuzzing for this standart

[Datasheet for EM200](https://www.emmicroelectronic.com/sites/default/files/products/datasheets/em4200_ds.pdf)
[Datasheet for EM100](https://www.alldatasheet.com/html-pdf/154654/EMMICRO/EM4100/293/1/EM4100.html)


Since that was so easy and could not really be called research I looked into some other ways to missuse this thing. 

# Other evenues of attack 

- the pins on the back 
- maybe power analyis ? 
- generating abitrary keys with the flipper
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


