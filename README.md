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
- SSH keys located in `~/.ssh/raspberry-pi` and `~/.ssh/raspberry-pi.pub`

## Hardware Setup

![Office monitoring Raspberry Pi instructions](https://github.com/Advertile/office-monitoring/blob/master/documentation/images/instructions.png "Office monitoring Raspberry Pi instructions")

## Software Setup

### Prepare micro SD card

In this chapter you will prepare the micro SD card used by the Raspberry Pi. After you insert the card and spin up the Raspberry Pi it will automatically connect to the desired network.

- Download the latest version of RASPBIAN from [raspberrypi.org](https://www.raspberrypi.org/downloads/raspbian/).
- Insert the micro SD card to your computer (use USB adapter if needed).
- Burn the RASPBIAN image on the micro SD card

  On Ubuntu use the Disks utility.

- Create and adjust WiFi [configuration file](provisioners/shell/files/etc/wpa_supplicant/wpa_supplicant.conf.example):

  ```
  cp provisioners/shell/files/etc/wpa_supplicant/wpa_supplicant.conf.example provisioners/shell/files/etc/wpa_supplicant/wpa_supplicant.conf
  ```

- use the `prepare-card` script to copy the required files to your micro SD card:

  ```
  ./scripts/prepare-card
  ```

### Find the Raspberry Pi IP

- Connect to the same network as the Raspberry Pi.
- Use `nmap` (if you prefer GUI Zenmap) to find the IP of the Raspberry Pi

  ```
  nmap -T4 -A -v <network IP>/24
  ```

  This might take a while.

  Find the network IP (`<network IP>`) with `ifconfig`

### Use Ansible to Provision

This chapter describes how to install the chromium browser in "kiosk" mode.

- Create and adjust variables in the [`group_vars/all` file](provisioners/ansible/group_vars/all.example):

  ```
  cp provisioners/ansible/group_vars/all.example provisioners/ansible/group_vars/all
  ```
- Provision with Ansible:

  ```
  ansible-playbook -i '<Raspberry Pi IP>,' --user=pi --ssh-extra-args='-o PreferredAuthentications=password -o PubkeyAuthentication=no' --become --ask-pass setup-playbook.yml
  ```

  If you don't have Ansible locally you can run it inside a Docker container by using this script:

  ```
  touch configuration/ssh/known_hosts
  scripts/provision
  ```
