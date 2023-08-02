# Forensics Workshop - DREAM 2023

## Tools

You are welcome to use your own VM / setup, but it is assumed that you have access to Linux.

Below is the list of the tools we will be using, as well as installation instructions for each. They are all good to have for future CTFs.

Alternatively (or in addition) you can use the online toolkit "CyberChef": https://gchq.github.io/CyberChef/. It comes with a wide range of operations you can apply to your input. The operations can be chained into a "recipe" and make it very easy to play around with different files and inputs. Not all tasks can be solved with CyberChef, but some of the first ones can.

### Linux

#### File Analysis

**xxd** (hex dump)

     sudo apt install xxd

**hexedit** (CLI hex editor)

     sudo apt install hexedit

**ghex** (GUI hex editor)

     sudo apt install ghex

**exiftool** (extract metadata)

     sudo apt install EXIFtool

**pngcheck** (check PNG files)

     sudo apt install pngcheck

#### Steganography

**bgrep** (binary grep)

     sudo apt install curl
     mkdir -p $HOME/.local/bin
     curl -L 'https://github.com/tmbinc/bgrep/raw/master/bgrep.c' | sudo gcc -O2 -x c -o /usr/local/bin/bgrep -

**binwalk** (file carving)

     sudo apt install binwalk

**foremost** (file carving)

     sudo apt install foremost

**stegsolve** (GUI image stego)

     wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve
     chmod +x stepsolve

Requires Java! Ride along

     java -jar stegsolve

Move if necessary to a specific folder and create an alias

     mkdir ~/tools
     etc. stepsolve /tools
     alias stegsolve='java -jar ~/tools/stegsolve'

Now the program can just be run with the `stegsolve` command in your terminal. Add any alias to your `.bashrc` to persist it to the next session.

**stego hide** (stego tool)

     sudo apt install stephide

**stegseek** (crack steghide)

     wget https://github.com/RickdeJager/stegseek/releases/download/v0.6/stegseek_0.6-1.deb
     sudo apt install ./stegseek_0.6-1.deb
     rm stegseek_0.6-1.deb

`stegseek' needs a wordlist of passwords it can check. By default, it looks for the wordlist `rockyou.txt`, which comes with Kali and is the most used password list. If you don't have Kali (or you want to use another wordlist), you can find a number of options here: https://github.com/danielmiessler/SecLists.

**zsteg** (PNG/BMP textual stego)

     sudo apt install ruby
     sudo save install zstep

#### Memory Analysis

For memory analysis we must use the program Volatility. It comes in versions 2 and 3. Version 3 is a little easier to use, but version 2 still has some plugins that aren't available for version 3 yet. It is a good idea to install both so that you have all the features ready.

Volatility 2 is easiest to download and use as a standalone program. Unzip and run the program via a terminal:

- Linux: http://downloads.volatilityfoundation.org/releases/2.6/volatility_2.6_lin64_standalone.zip
- Windows: http://downloads.volatilityfoundation.org/releases/2.6/volatility_2.6_win64_standalone.zip
- Mac: http://downloads.volatilityfoundation.org/releases/2.6/volatility_2.6_mac64_standalone.zip

Volatility 3 requires Python 3 and dependencies are installed with Pip. Make sure both are installed with

     sudo apt install python3 python3-pip

Download and install volatility3 and its dependencies:

     git clone https://github.com/volatilityfoundation/volatility3.git
     cd volatility3
     pip3 install -r requirements.txt

Volatility uses symbol tables for different operating systems to analyze them correctly. Download the following ZIP files and place them in the `volatility3/symbols/` folder (inside the main folder, so `volatility3/volatility3/symbols` from the outside):

- Windows: https://downloads.volatilityfoundation.org/volatility3/symbols/windows.zip
- Linux: https://downloads.volatilityfoundation.org/volatility3/symbols/linux.zip
- MacOS: https://downloads.volatilityfoundation.org/volatility3/symbols/mac.zip

Note that the files do not depend on which operating system you are using, but which operating system you have to analyze a memory dump from. You can skip MacOS from the start, it is seen somewhat less often in a CTF challenge, and we will not use it in the workshop (nor Linux, but it is seen regularly).

### Windows

If you use Windows, it is quick to set up a Linux in WSL:

1. Open PowerShell as administrator and run

   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

2. Restart Windows
3. Open Powershell as administrator and run

   wsl --set-default-version 2

4. Open Microsoft Store, search for "kali" and install "Kali Linux"
5. You have now installed Kali Linux on your Windows. Run the program
6. On the first run, you must set up a new user - it asks you to choose a username and password yourself
7. Run `sudo apt update` and `sudo apt upgrade` to run the first update (the password it asks for is the one you just chose)

## Ressources

Here's some links for good forensics training

- CTF Field Guide: https://trailofbits.github.io/ctf/forensics/
- HackTricks: https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology
- Forensics labs: https://cyberdefenders.org/blueteam-ctf-challenges/
- More forensics labs: https://blueteamlabs.online/
- 13Cubed: https://www.youtube.com/c/13cubed
- Stego-toolkit: https://github.com/DominicBreuker/stego-toolkit
- Aperi'solve: https://aperisolve.com/
