# Office Monitoring

The goal of this repository is to setup monitoring inside your office (based on commodity hardware) as easy as possible.

## Requirements

- screen - for our setup we used Dell UltraSharp U2311H 23" - find a used one on eBay
- screen arm - find one on eBay
- Raspberry Pi 3
- Raspberry Pi power supply (tested on `5,1V` / `2,5A`)
- Raspberry Pi case
- micro SD memory card
- micro SD card USB adapter - optional if you have an micro SD card slot in your computer
- HDMI cable

## Setup

### Prepare micro SD card

In this chapter you will prepare the micro SD card used by the Raspberry Pi. After you insert the card and spin up the Raspberry Pi it will automatically connect to the desired network.

- Download the latest version of RASPBIAN from [raspberrypi.org](https://www.raspberrypi.org/downloads/raspbian/).
- Insert the micro SD card to your computer (use USB adapter if needed).
- Burn the RASPBIAN image on the micro SD card

  On Ubuntu use the Disks utility.

- Create and adjust your WiFi configuration file:

  ```
  cp provisioners/shell/files/etc/wpa_supplicant/wpa_supplicant.conf.example provisioners/shell/files/etc/wpa_supplicant/wpa_supplicant.conf
  ```

- use the `prepare-card` script to copy the required files to your micro SD card:

  ```
  ./scripts/prepare-card
  ```
