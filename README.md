# Wifiphisher
Wifiphisher wifi 
Wifiphisher is a rogue Access Point framework for conducting red team engagements or Wi-Fi security testing. Using Wifiphisher, penetration testers can easily achieve a man-in-the-middle position against wireless clients by performing targeted Wi-Fi association attacks. Wifiphisher can be further used to mount victim-customized web phishing attacks against the connected clients in order to capture credentials (e.g. from third party login pages or WPA/WPA2 Pre-Shared Keys) or infect the victim stations with malwares.

Wifiphisher is...

...powerful. Wifiphisher can run for hours inside a Raspberry Pi device executing all modern Wi-Fi association techniques (including "Evil Twin", "KARMA" and "Known Beacons").

...flexible. Supports dozens of arguments and comes with a set of community-driven phishing templates for different deployment scenarios.

...modular. Users can write simple or complicated modules in Python to expand the functionality of the tool or create custom phishing scenarios in order to conduct specific target-oriented attacks.

...easy to use. Advanced users can utilize the rich set of features that Wifiphisher offers but beginners may start out as simply as "./bin/wifiphisher". The interactive Textual User Interface guides the tester through the build process of the attack.

...the result of an extensive research. Attacks like "Known Beacons" and "Lure10" as well as state-of-the-art phishing techniques, were disclosed by our developers, and Wifiphisher was the first tool to incorporate them.

...supported by an awesome community of developers and users.

...free. Wifiphisher is available for free download, and also comes with full source code that you may study, change, or distribute under the terms of the GPLv3 license.

How it works
Wi-Fi phishing consists of two steps:

The first step involves the process of associating with Wi-Fi clients unknowingly, or in other words, obtaining a man-in-the-middle (MITM) position. Wifiphisher uses a number of different techniques to achieve this including:

Evil Twin, where Wifiphisher creates a fake wireless network that looks similar to a legitimate network.
KARMA, where Wifiphisher masquerades as a public network searched for by nearby Wi-Fi clients.
Known Beacons, where Wifiphisher broadcasts a dictionary of common ESSIDs, that the around wireless stations have likely connected to in the past.
At the same time, Wifiphisher keeps forging “Deauthenticate” or “Disassociate” packets to disrupt existing associations and eventually lure victims using the above techniques.


Performing MiTM attack

(Optionally) There are a number of different attacks that can be carried out once Wifiphisher grants the penetration tester with a man-in-the-middle position. For example, the tester may perform data sniffing or scan the victim stations for vulnerabilities.

Using Wifiphisher, advanced web phishing techniques are possible by gathering information from the target environment and victim user. For example, in one of our scenarios, Wifiphisher will extract information from the broadcasted beacon frames and the HTTP User-Agent header to display a web-based imitation of Windows network manager in order to capture the Pre-Shared Key.


Fake web-based network manager

Requirements
Following are the requirements for getting the most out of Wifiphisher:

A working Linux system. People have made Wifiphisher work on many distros, but Kali Linux is the officially supported distribution, thus all new features are primarily tested on this platform.
One wireless network adapter that supports AP & Monitor mode and is capable of injection. Drivers should support netlink.
Installation
To install the latest development version type the following commands:

git clone https://github.com/wifiphisher/wifiphisher.git # Download the latest revision
cd wifiphisher # Switch to tool's directory
sudo python setup.py install # Install any dependencies
Alternatively, you can download the latest stable version from the Releases page.

Usage
Run the tool by typing wifiphisher or python bin/wifiphisher (from inside the tool's directory).

By running the tool without any options, it will find the right interfaces and interactively ask the user to pick the ESSID of the target network (out of a list with all the ESSIDs in the around area) as well as a phishing scenario to perform. By default, the tool will perform both Evil Twin and KARMA attacks.

wifiphisher -aI wlan0 -jI wlan4 -p firmware-upgrade --handshake-capture handshake.pcap
Use wlan0 for spawning the rogue Access Point and wlan4 for DoS attacks. Select the target network manually from the list and perform the "Firmware Upgrade" scenario. Verify that the captured Pre-Shared Key is correct by checking it against the handshake in the handshake.pcap file.

Useful for manually selecting the wireless adapters. The "Firmware Upgrade" scenario is an easy way for obtaining the PSK from a password-protected network.

wifiphisher --essid CONFERENCE_WIFI -p plugin_update -pK s3cr3tp4ssw0rd
Automatically pick the right interfaces. Target the Wi-Fi with ESSID "CONFERENCE_WIFI" and perform the "Plugin Update" scenario. The Evil Twin will be password-protected with PSK "s3cr3tp4ssw0rd".

Useful against networks with disclosed PSKs (e.g. in conferences). The "Plugin Update" scenario provides an easy way for getting the victims to download malicious executables (e.g. malwares containing a reverse shell payload).

wifiphisher --essid "FREE WI-FI" -p oauth-login -kB
Simply spawn an open Wi-Fi network with ESSID "FREE WI-FI" and perform the "OAuth Login" scenario. Furthermore, mount the "Known Beacons" Wi-Fi automatic association technique.

Useful against victims in public areas. The "OAuth Login" scenario provides a simple way for capturing credentials from social networks, like Facebook.

Following are all the options along with their descriptions (also available with wifiphisher -h):

git clone https://github.com/wifiphisher/wifiphisher.git # Download the latest revision
cd wifiphisher # Switch to tool's directory
sudo python setup.py install # Install any dependencies

wifiphisher -aI wlan0 -jI wlan4 -p firmware-upgrade --handshake-capture handshake.pcap
https://github.com/wifiphisher/wifiphisher

https://github.com/AdrMXR/KitHack/blob/master/docs/TOOLS.md#wifi-attacks
