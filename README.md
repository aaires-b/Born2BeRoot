# Born2BeRoot

# VM

A vm is a computer that runs on software , independent from the host computer . It uses the OS on a physical computer (host). Usually, gets the hardware from the host and stores the data on the VHD (virtual hard drive), imitating it.  A vm stores files. runs programs and has virtual hardware components.

2 TYPES:

system:  fully virtualized environment → runs its own OS

process : hides the OS underneath (host computers OS) , just executes a process .

### PROS:

- Creates a safe and secure environment for unstable program testing by preventing a problem to spreed around to the physical computer.
- Makes it possible to run numerous OS’s on the computer.
- Easy to implement.

## HYPERVISOR

The hypervisor is a software that create the VM. It manages hardware, separates physical resources from the virtual ones . Its like a “middle-man” between the PC and the VC (virtual computer / machine). 

Ex: If the vm user needs to access physical resources from the PC the hypervisor manages that request and gives him permission for it.

## VHD (Virtual Hard Disk)

The virtual hard disk is a file in the computer mounted as hard drive . The vm stores the settings of the system: amount of CPU , RAM details , hard disks , etc.. . The VHD stores the real data (data volumes, boot volumes, etc..)

## LVM (Logical Volume Management)

The LVM is a system for managing logical volumes. It is much more advanced and flexible that managing volumes directly from the disk. This logical volumes are dynamic partitions , which means that they can be resized , created and deleted without being necessary to reboot the system on the terminal for the Kernel to acknowledge the changes.

## UNIX

The unix OS is divided in 3 essential parts : programs , shell and kernell.

### Kernel

The kernel is the hub of the OS . Its allocates time and memory to programs and handles the filestore and communications.

**The OS:** program that , when initialized by a boot system , manages all apps (requests for services through an API (application programming interface) ).

SHELL (== CLI (command-line interpreter))

The shell acts like an interface between the user and the kernel . It interpreters the commands that the user types in the terminal. 

## Debian vs Rocky

**Debian**                                                                ||            **Rocky ( follows CentOS)**

Best for software                                                         ||            Best for servers

Old Linux Server Distribution                                             ||            Recent distribution (2021)

Base for numerous linux distributions                                     ||            Secure Boot

Needs constant updates                                                    ||            Free of charge

Free of charge                                                            ||            Stable and Modern

Supports various software architectures                                    ||           Few updates 

Stable and Reliable                                                        ||           More heavy

Lets users makes adjusts

Has lots of packages 

Less heavy in terms of space that occupies    


## APT (Advanced package tool)

The APT is a tool that handles software installation and removal through the command-line , not needing a GI(Graphical Interface) to work. It downloads and installs both the dependencies for a package and the package tools. Also , it is an open-source tool. 

## APTITUDE

Te aptitude tool is similar to apt however  it is a front-end tool that gives access to the user to the user-interface for accessing functionalities. It also installs and removes packages but thought an user-interface, by default.

## APPARMOR

Apparmor is a Linux Kernel Security module . It reinforces / supports the Linux user and permissions based on groups to constrain programs to a certain type of resources. This “armor” protects the computer from any problem that might occur , being an independent defense for attacks.

Apparmor is configured through linked profiles in order to permit the access needed for a specific program. They can be run in enforce mode (blocks access to disabled resources) or complain mode (reports violations).

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**LOGIN**

- root: su-
- update && upgrade: apt update / apt  upgrade
- install sudo : apt install sudo

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SUDO (Super-user do)

Sudo is a program to let admins give permissions to some users as root . It also serves as a way to check who has used it and when.

## GROUP

All users that belong to a group have the same permissions for a certain file. Others with access to the file belong to the category of others.

## SUDO GROUP

Group of super users that have the same privileges/permissions to access root commands .

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**USER**

- Add : sudo adduser aaires-b
- Del : sudo deluser aaires-b
- Change user: sudo -u aaires-b -s
- Change pass: sudo passwd aaires-b
- See all users: sudo getent passwd

**GROUPS**

- Create group: sudo addgroup user42
- Add user to sudo group : sudo adduser aaires-b sudo
- Add user to group : sudo adduser aaires-b user42
- To check : sudo getent sudo

**VERSION OF OS** 

- cd cat /etc/os-release

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**PASS PROTOCOL (Linux PAM)**

- Linux PAM is a suite of libraries that lets system admins config methods of user authentication.

**Install** : sudo apt install libpam-crack

//////////////////////////////////////////////////////////////////////////////////////////////////////

**PASS CONFIG**

- Open pass file : nano /etc/pam.d/common-password
- Add next to passwd     :
- retry=3: limit number of password tries
- lcredit=-1 : password needs to have at least one lowercase character
- dcredit=-1: password needs to have at least one digit
- ucredit=-1: password needs to have at uppercase character
- difok=7 : number of characters different from the previous password
- reject_username : pass can’t include the username
- enforce_for_root : implement the same rules for root

**SET DAYS**

- Open sudo nano/etc/login.defs
- change expire days to 30 and min to 2

////////////////////////////////////////////////////////////////////////////////////////////////

## SSH (Secure Shell)

The ssh is a network communication protocol, in other words, lets 2 PC’s communicate e share data. Usually this protocol is used for secure logins . But HOW DO THEY COMMUNICATE ? Easy , by encryption based keys. This makes it suitable for insecure networks. 

**OPENSSH** == open source implementation of the ssh protocol .

## **SSH KEY**

pair of public and private keys used to authenticate and establish an encrypted communication channel  between client and remote machine , via Internet.

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**SSH COMMANDS** 

- Install : sudo apt install openssh-server
- Verify : sudo systemctl ssh status
- Start : sudo systemctl start ssh
- Stop : sudo systemctl stop ssh
- Add port 4242: cd /etc/ssh && sudo nano /sshd_config
- #Port 22 → Port 4242
- Access VM via ssh : ssh aaires-b@localhost -p 4242

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## HOSTNAME && FIREWALL

**FIREWALL** (aka barreira)

The firewall is a network security device that monitors incoming and outgoing network traffic based on policy rules .

It acts like a “wall” between a private internal network and public Internet.

**UFW (Uncomplicated firewall)** : uses command-line interface and iptables for configuration.

**HOSTNAME**

A hostname is a label signed to a machine that identifies it in a network.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**UFW**

- Install : sudo apt install ufw
- Activate : sudo ufw enable
- Check: sudo systemctl status ufw
- Add rules: sudo ufw allow 80

**HOSTNAME**

- IPAddress : hostname -I
- Current User  : whoami
- change hostname : sudo hostname set -newhostname

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SUDO POLICY === TTY

TTY stands for teletype which is a command that displays the info related to the terminal .It allows the user to interact with the system by passing data  .

**VISUDO**

Visudo is a command that opens a text editor and validates a file’s syntax after it has been saved. This way, configuration errors and prevented of blocking sudo operations.

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

**SET UP** : 

- cd /etc/sudoers.d && sudo visudo
- enable tty : Defaults requiretty
- select right folder for log files: Defaults /var/log/sudo/sudo.log
- archive all sudo: Defaults iolog_dir = “ /var/log/sudo”
- inputs and outputs to /var/log/sudo: Defaults log_input, log out_put
- pass retries: Defaults passwd_tries=3
- set wrong pass: Defaults badpass_message “wrong”

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## CRON

Crontab is a command that creates a table/ list of commands that is going to be executed by the operating system at a specified time and on a  regular schedule. 

**CONFIG**

- sudo apt-get update -y
- sudo apt-get install -y net_tools
- cd /home/aaires-b
- touch monitoring.sh
- chmod 777 monitoring.sh
- run script as su (root) : sudo /home/aaires-b/monitoring.sh -sh
- config cron as root: sudo crontab -u root -e

## SCRIPT (bash)

- sudo vim /home/aaires-b/monitoring.sh

**#!/bin/bash**

- wall == command-line utility that displays a mensage in the terminal of all logged-in-users.

**ARQUITETURA:** 

- uname -a → prints all system info.

**PHYSICAL CPU**

- grep “physical id” /proc/cpuinfo | sort | uniq | wc -l  → number of cpu’s\

**VIRTUAL CPU**

- grep “^processor” /proc/cpuinfo | wc -l → number of virtual processors

**FREE RAM and USAGE %**

- free -m (output in MB)  | grep Mem (only Mem row) | awk ‘{print $4}’ (awk searches for the lines that match a specified pattern and executes the actions associated with it, here it is going to print the value in the 4th column)
- total RAM Mem : free -m | grep Mem | awk ‘{print $2}’

**% USAGE** 

- free -m | grep Mem | awk ‘{printf(”%.2f”), $3 / $2*100}’

**FREE SERVER SPACE AND USAGE**

- df -m : show disk space in Mb
- df -Bg : show disk in Gb
- `df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{fdisk += $4} END {print fdisk}'`
- `df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{tdisk += $2} END {print tdisk}'`
- `df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{fdisk += $3} {tdisk += $2} END {printf("%.2f"), fdisk/tdisk*100}'`

Than u will need to construct commands to show the CPU Usage, the last reboot , LVM use , TCP connections, User login , IP and MAC addresses and number of sudo commands that I’m not going to enter in detail here . 

Finally , there’s only the **signature.txt** left to do in the mandatory part.

## SIGNATURE.TXT

- Open terminal
- Type cd sgoinfre/goinfre/Perso/your_user/born2beroot
- Then type shasum VirtualBox.vdi or whatever your Virtual Machine .vdi file is called.
- you should see an output like this: 6e657c4619944be17df3c31faa030c25e43e40af
- Copy the signature number and create a .txt file and paste your number in the .txt file you just created, ready for submission.
