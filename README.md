# delivery_door

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


setup and design restrictions

The basic setup onl
