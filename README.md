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

## User Stories
###

## Security Concept

The rfid chips are the main part of interface. Not only to give access, but also to give commands to the door device. Auhtentification  and authorization is implemented by using trusted signatures with assymetric encryption. The second target to manipulation is the microcontroller itself. Its integrity relies on the physical access security, which might only have a level of a reliable breach detection.

### Setting up truested key set
This procedure 
