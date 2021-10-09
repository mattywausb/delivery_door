# Delivery Door

## Motivation

The general access concept for houses with multiple flats consists of keys for every flat, 
that also opens the front door to the staircase. Alternatively you can  ring a bell via a bell board on the front door so the person in 
the targeted flat can provide access by activatng a door opener.

Since some services (mail, news paper delivery) also need regular access to the staircase and would have to 
disturb the inhabitants on a daily base. Therefore those services are also provided with a key, that only gives access to the front door.

Unfortunatly, theses keys sometimes get lost, stolen or - even worse - get sold to criminal channels.

Because of the costs for exchanging all locks and keys, wich would be necessary to invalidate the "leaked" key, it is normally not done. 
Getting a "delivery" key for a known address  provides a high chance to get access to the houses staircase, even after month of notice and replacement of the key loss.

This project provides an alternative to the "classic" delivery boy key.

## Basic idea

Instead of handing out normal door keys to the delivery services, they will get a rfid chip which will activate the door opener, when hold against the proper place on the door or nearby panel.
The chips are indivudually coded for every service. In case of a loss, the specific service get a new code  and the old code is removed from the access list.
To prevent/detect copies of the chip, logging and checking for unusual behaviour can provide a barrier. Also a usage restriction, e.g. timewindow of repetivie use, can be a barrier 

## Considerations about User interface 

In daily use, the existence of the device should only be visible by a marking on the door or panel, where to place the rfid chip. The main feedback to the user is the opening of the door. To assist the user in case of incorrect handling, an acousting signal should be provided in case of an invalid key or reading error.

Validating replacement keys and invalidating old keys, should not require physical contact to the device by the administrator.

Adding a new key must be a secured process, so nobody, exept an authorized user can register a new key or keyset. This can be achieved by enforcing the need of physical access to the device and keeping necessary elements in locked compartments.

Extended external communication of the device should also only be activated by operations, that need physical access to the device. In normal operations mode, the device should never provide other interfaces then the RFID sensor, the door opener and probably some command buttons and a display in a locked compartment.

Power supply should be compatible to anything, already available in the door bell board.

Beside the door controlling compontend there needs to be a key configuration device, where the rfid key will get the proper settings. This device must be kept securely locked by the administrator, since it can be used to create new valid keys.

## Components

The main components for every door will be
* some microcontroller (probably with optional WiFi and Webserver capabilites)
* an rfid read interface
* acoustic singalling device (beeper)
* Releais and driver to switch door opener
* optional LCD Matrix display
* Power Supply

The main components for the RFID programmer
* some microcontroller with WiFi and Webserver capabilites
* RFID read interface

## Content of the RFID Keys
### normal key
* Command (10 Bytes): "Open"
* Series identification String (20 Bytes) e.g. "Yellow-Mail-Man", "Green-Mail-Man", "NewYorkTimes"
* Series sequence number (4 Bytes) (beginning randomly somewhere beween 123456 and 923456 and counting up in random (1-100) steps) 
* Signature from all above signed with private key (128 Bytes) 

### Command key
* Command (10 Bytes): "Register new Series"
* Command specific Content (Length Depending on Command)
* Signature from all above signed with private key (128 Bytes) 

## User Stories

### Initializing the main security keys

#### on the RFID programmer
* Generate RSA 1024 bit(128 Bytes) public/private key pair
* Access configuration UI of the programmer via Webbrowser
* choose: "Setup Master Key"
* copy private and public key into a secure store to keep it as backup on case of loss of the programmer
* copy private and public key into web form fields "new private" , "new public" 
* ensure, current private key is set
* place rfid(2KB) on programmer and activate "write key change master key"

#### on every door
* place "write key master key" RFID on "Read surface"
* No Reaction if RFID content as no vaild signature (must besinged with current valid master key)
* copy public key from rfid to internal storage, remove old key and give short+long beep

### Initializing a new keyset for a new service
* Access configuration UI of the programmer via Webbrowser
* choose: "Setup key series"

### provide a follow up key for a key set


### remove an active keyset
* Generate a replacement key for the key set
* use the replacement key on every door 



### Getting Access (including replacig key with follow up key)
* place RFID on "Read surface"
* No Reaction if RFID content as no vaild signature
* Door Device beeps 4 times, if RFID is old key
* Door Device beeps 2 times, if RFID is valid but not in allowed time window
* Door Device acitivates door opener , if RFID is currently valid or follow up key(higher sequence number) of currently valid key
* Door Device marks old RFID as "deleted" and stores new RFID key as valid

### Registering a new keys (first keys of every series)
* User places RFID on "Reade surface"
* No Reaction if RFID content as no vaild signature
* IF RFID contains a "Register new key" command beep 1 time
* Wait for next key
* User places RFID on "Reade surface"
* if RFID content has no vaild signature, Reset procedure and give 4 beeps 
* Register new key as valid, beep 3 times
* wait for next key (see previous 3 steps)
* in case of 20 seconds without a new key, give 4 bees and go back to normal operation


## Security Concept

The rfid chips are the main part of interface. Not only to give access, but also to give commands to the door device. Auhtentification  and authorization is implemented by using trusted signatures with assymetric encryption. The second target to manipulation is the microcontroller itself. Its integrity relies on the physical access security, which might only have a level of a reliable breach detection.

### Setting up truested key set
This procedure 
