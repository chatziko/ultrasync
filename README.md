# Interlogix UltraSync ZeroWire Hub
[Interlogix](https://www.interlogix.com/) provides security solutions. One of which is their [Self Contained (ZeroWire) Hub](https://www.interlogix.com/intrusion/product/ultrasync-selfcontained-hub):<br/>![ZeroWire Hub Image](https://raw.githubusercontent.com/caronc/ultrasync/master/static/zerowire_hub.jpeg)

This is just a small library and accompaning CLI tool I wrote to allow me to interface with it.

[![Paypal](https://img.shields.io/badge/paypal-donate-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MHANV39UZNQ5E)

## How Does It Work?
1. First you need to install it; this part is easy:
   ```bash
   pip install ultrasync
   ```

2. Create a configuration file that identifies:
   1. The location the ZeroWire hub can be found on in your local nework.
   1. Your ZeroWire login User ID
   1. Your ZeroWire login pin

   **Note**: You can only be logged into the ZeroWire hub with the same user *once*; a subsequent login with the same user logs out the other. Since this tool/software actively polls and maintains a login session to your Hub, it can prevent you from being able to log into at the same time elsewhere (via it's website).  It is strongly recommended you create a second user account on your Hub dedicated to just this service.

   ```python
   # An example of what would be found in your configuration file:
   # Use hashtags/pound symbols (#) to optionally add comments
   # Syntax is simply <key>: <value>
   #
   # You must specify hostname, user, and pin
   #
   host: 192.168.0.30
   user: My Username
   pin: 1234
   ```
3. Use the **--scene** (*-s*) to set your security system's alarm scene.  The possible options are: `disarm`, `away`, and `stay`.
   ```bash
   # By default if no --config= (-c) is specified; one will be automatically
   # loaded from the following location (if present):
   #  ~/.ultrasync
   #  ~/.config/ultrasync
   
   # Windows users can store their default configuration files here:
   #  %APPDATA%/UltraSync/config
   #  %LOCALAPPDATA%/UltraSync/config
   
   # Disarm your security system
   ultrasync --scene disarm
   
   # Arm your security system and acctivate all of your sensors when setting the
   # away mode macro
   ultrasync --scene away
   
   # Arm your security system and only activate your perimiter sensors:
   ultrasync --scene stay
   ```

## What Else Can It Do?
- You can put up a live monitor of your device by typing the following:
  ```bash
  # A live monitoring of your home security system:
  ultrasync --watch
  ```
- You can generate a snapshot (in JSON format) that greatly details everything taking place through your security home setup. It provides MUCH greater detail than the `--watch` process and will eventually become the key that will make integration with [Home Assistant](https://www.home-assistant.io/) possible *eventually*.
  ```bash
  # Print a JSON formated snapshot of all home security details
  ultrasync --details
  ```
- You can perform a dump of all of the web based files (*that I've found to be useful so far*) to disk.  This makes troubleshooting incredibly much easier.
  ```bash
  # Extracts information from your UltraSync Hub that can be
  # incredibly useful in debugging and/or adding enhancments
  ultrasync --debug-dump
  ```
  The debug content gets written to a directory (residing in the same folder you ran this command from) in the form of: `YYYYmmddHHMMSS.ultrasync-dump`.

# Disclaimer
This software was created by reverse engineering my own personal security system. All of this code was generated through trial and error since there is no documentation that I could find that explains the registers. If you can help out by filling in some of the blanks throughout the code base, I would be greatly appreciative of it! Alternatively [buying me a coffee](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MHANV39UZNQ5E) greatly inspires me to continue improving the application.

Otherwise, please feel free to file bugs and use this at your sole discretion as I have no control over how your own security system might have been set up. But what has been written here *should* work for all owners.
