# Setting Up a Raspberry Pi ADS-B Receiver for Flightradar24

**Date:** 2026-07-25  
**Topic:** Raspberry Pi, ADS-B, and Flightradar24  
**Status:** Completed

## What I Worked On

I learned how to prepare a Raspberry Pi as an ADS-B receiving station and connect it to Flightradar24.

The station uses a 1090 MHz antenna and a USB RTL-SDR receiver to detect ADS-B transmissions from nearby aircraft. The Raspberry Pi processes the received information and sends it to Flightradar24 through the internet.

The basic signal path is:

```text
Aircraft
→ 1090 MHz antenna
→ USB RTL-SDR receiver
→ Raspberry Pi
→ Internet
→ Flightradar24
```
I also documented how to:

Install Raspberry Pi OS.
Configure remote access through SSH.
Update the Raspberry Pi.
Install the Flightradar24 feeder software.
Verify that the receiver and feeder service are working.
Access the local Flightradar24 status page.
Troubleshoot common receiver and connection problems.
Protect private credentials and system information.
Hardware Used

The system requires:

Raspberry Pi
Compatible Raspberry Pi power supply
MicroSD card
USB RTL-SDR or ADS-B receiver
1090 MHz ADS-B antenna
Coaxial cable and the necessary adapters
Ethernet or Wi-Fi connection
Computer with a microSD card reader
Optional Raspberry Pi case and cooling

Examples of compatible receivers include:

FlightAware Pro Stick
RTL-SDR Blog receiver
Nooelec SDR receiver
Generic RTL2832U/R820T2 DVB-T receiver

A receiver designed or filtered specifically for ADS-B reception will generally perform better than a basic television receiver.

Installation Process
1. Prepare the MicroSD Card

Download and install Raspberry Pi Imager from the official Raspberry Pi website:

Raspberry Pi installation documentation

Using Raspberry Pi Imager:

Select the correct Raspberry Pi model.
Select Raspberry Pi OS Lite (64-bit).
Select the correct microSD card.
Configure the operating-system settings.
Create a username and strong password.
Set a hostname such as:
adsb-receiver
Configure Wi-Fi if Ethernet will not be used.
Set the correct wireless country.
Enable SSH.
Write and verify the operating system.

Writing the operating system erases the selected card, so the storage device must be checked carefully before continuing.

2. Assemble the Receiver

With the Raspberry Pi disconnected from power:

Insert the prepared microSD card.
Connect the 1090 MHz antenna to the SDR receiver.
Connect the SDR receiver to a USB port.
Connect Ethernet if applicable.
Connect the Raspberry Pi power supply.
Allow the Raspberry Pi a few minutes to boot.
3. Connect Through SSH

From PowerShell, connect using the configured hostname:

ssh YOUR_PI_USERNAME@adsb-receiver.local

If the hostname is not detected, use the Raspberry Pi’s local IP address:

ssh YOUR_PI_USERNAME@YOUR_PI_IP_ADDRESS

The password will not appear on the screen while it is being entered. This is normal terminal behavior.

4. Update Raspberry Pi OS

Update the package information:

sudo apt update

Install available system updates:

sudo apt full-upgrade -y

Remove unnecessary packages:

sudo apt autoremove -y

Restart the Raspberry Pi:

sudo reboot
5. Install Flightradar24

Reconnect through SSH and run the official Flightradar24 installation command:

wget -qO- https://fr24.com/install.sh | sudo bash -s

During installation, the system may request:

Flightradar24 account email
Flightradar24 sharing key
Receiver type
Antenna latitude
Antenna longitude
Antenna altitude
Additional receiver settings

For an RTL-SDR connected directly through USB, select the appropriate DVB-T/RTL-SDR receiver option.

Installer options can change, so the option descriptions should be read carefully instead of relying exclusively on an option number from an older guide.

6. Verify the Service

Check the Flightradar24 service:

sudo systemctl status fr24feed

A correctly running service should display:

active (running)

Press Q to close the status view.

Restart the service if necessary:

sudo systemctl restart fr24feed

Enable automatic startup:

sudo systemctl enable fr24feed

View recent service logs:

sudo journalctl -u fr24feed --no-pager -n 50
7. Open the Local Status Page

From a browser on the same local network, open:

http://YOUR_PI_IP_ADDRESS:8754

The interface can display:

Receiver status
Flightradar24 feed status
Receiver or radar ID
Aircraft messages received
Connection status
MLAT status

Port 8754 should normally remain available only inside the local network. It should not be exposed directly to the internet.

8. Confirm USB Receiver Detection

Check whether Linux detects the USB receiver:

lsusb

The result may mention an RTL2832, RTL-SDR, DVB-T, FlightAware, Nooelec, or similar device.

9. Confirm Data Sharing

Verify that:

The USB receiver is detected.
The antenna is connected.
Aircraft messages are being received.
The feeder is connected to Flightradar24.
A receiver or radar ID has been assigned.
The Flightradar24 account recognizes the feeder.

Once valid information is being received, the account may be upgraded to the Flightradar24 Contributor plan. This process may not happen immediately.

What I Learned
How aircraft broadcast ADS-B information on 1090 MHz.
How an RTL-SDR receiver can receive aircraft transmissions.
How the antenna, receiver, Raspberry Pi, and internet connection work together.
How to install Raspberry Pi OS using Raspberry Pi Imager.
How to configure a Raspberry Pi for headless operation.
How to connect to a Raspberry Pi remotely through SSH.
How to install and update Linux packages.
How to install the Flightradar24 feeder software.
How to manage a Linux service with systemctl.
How to inspect system logs using journalctl.
How to verify that a USB device is detected.
How to find the Raspberry Pi’s local IP address.
How to access the local Flightradar24 status interface.
Why antenna height, clear line of sight, cable quality, and power stability affect reception.
Why credentials, sharing keys, coordinates, and unedited logs must remain private.
Commands Used
# Connect to the Raspberry Pi using its hostname
ssh YOUR_PI_USERNAME@adsb-receiver.local

# Connect using the Raspberry Pi's local IP address
ssh YOUR_PI_USERNAME@YOUR_PI_IP_ADDRESS
# Update the package list
sudo apt update

# Install system updates
sudo apt full-upgrade -y

# Remove unnecessary packages
sudo apt autoremove -y

# Install the Flightradar24 feeder
wget -qO- https://fr24.com/install.sh | sudo bash -s

# Check the feeder service
sudo systemctl status fr24feed

# Restart the feeder service
sudo systemctl restart fr24feed

# Enable the feeder during startup
sudo systemctl enable fr24feed

# Display recent feeder logs
sudo journalctl -u fr24feed --no-pager -n 50

# Display connected USB devices
lsusb

# Display the Raspberry Pi's IP address
hostname -I

# Check available storage
df -h

# Check system uptime and load
uptime

# Restart the Raspberry Pi
sudo reboot

# Shut down the Raspberry Pi safely
sudo shutdown -h now
Challenges

Several parts of the process require careful attention:

Choosing the correct Raspberry Pi OS and microSD card.
Finding the Raspberry Pi on the local network.
Selecting the correct receiver type during installation.
Entering antenna altitude using the requested unit.
Confirming that the SDR receiver is detected.
Distinguishing between a receiver problem and a feeder-service problem.
Understanding that weak reception may be caused by antenna placement rather than software.
Avoiding accidental publication of private system information.

A feeder may appear offline even when the Raspberry Pi itself is functioning. The problem can instead be related to the receiver, antenna, internet connection, feeder configuration, or Flightradar24 service.

Solution

I divided troubleshooting into separate checks:

Confirm that the Raspberry Pi is powered and accessible.
Confirm internet connectivity.
Check whether the USB receiver appears in lsusb.
Check the fr24feed service.
Review recent service logs.
Verify the antenna and coaxial connections.
Open the local status interface.
Confirm that aircraft messages are being received.
Restart the feeder only when necessary.
Reboot the Raspberry Pi if the receiver or service remains unavailable.

For an offline feeder, the first commands to use are:

sudo systemctl restart fr24feed
sudo systemctl status fr24feed

To test internet connectivity:

ping -c 4 1.1.1.1

To test DNS resolution:

ping -c 4 flightradar24.com

To check the current IP address:

hostname -I

This structured approach helps identify the affected part instead of changing several settings at once.

Security and Privacy

The following information must not be included in a public repository:

Flightradar24 sharing key
Raspberry Pi password
Wi-Fi password
SSH private key
Exact home coordinates
Public IP address
Authentication codes
Unedited configuration files
Unedited logs
Screenshots containing private network information

Safe placeholders should be used in public documentation:

Placeholder	Meaning
YOUR_PI_USERNAME	Raspberry Pi account username
YOUR_PI_PASSWORD	Raspberry Pi password
YOUR_PI_IP_ADDRESS	Raspberry Pi local IP address
YOUR_FR24_EMAIL	Flightradar24 account email
YOUR_FR24_SHARING_KEY	Private feeder identification key
YOUR_LATITUDE	Antenna latitude
YOUR_LONGITUDE	Antenna longitude
YOUR_ALTITUDE	Antenna altitude
YOUR_WIFI_NAME	Wi-Fi network name
YOUR_WIFI_PASSWORD	Wi-Fi password

These placeholders must be replaced with real values only during the private installation process. Real values should never be committed to GitHub.

## Useful Resources
Flightradar24 Data Sharing
Raspberry Pi Setup Documentation
Raspberry Pi Remote Access Documentation
RTL-SDR Blog

## Next Steps
 Improve the antenna location.
 Weatherproof outdoor antenna connections.
 Create a DHCP reservation for the Raspberry Pi.
 Configure SSH-key authentication.
 Monitor receiver uptime and system storage.
 Learn how ADS-B messages are decoded.
 Compare the received aircraft count at different antenna heights.
 Document the feeder configuration using only safe placeholders.
 Create a maintenance checklist for the receiver.
 Learn more about MLAT and sharing data with multiple networks.

---

Receiving the sky, one packet at a time.

*Learning one commit at a time.*