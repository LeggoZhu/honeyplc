# HoneyPLC

HoneyPLC is a high interaction PLC honeypot designed to simulate multiple PLC models from different vendors. It can log S7comm interactions and can store Ladder Logic programs injected by an attacker. It can also log SNMP get requests and HTTP login attempts.

It is brought to you by the cybersecurity lab [SEFCOM at Arizona State University](http://sefcom.asu.edu) and [Efrén López](https://efrenlopezm.github.io/).

The S7comm portion of HoneyPLC is built on top of [Snap7](https://github.com/SCADACS/snap7)

## Reference Research Papers

* [HoneyPLC: A Next-Generation Honeypot for Industrial Control Systems (ACM CCS 2020)](https://www.sigsac.org/ccs/CCS2020/)

## Demo

Some interesting logs from a live Kippo installation below (viewable within a web browser with the help of Ajaxterm). Note that some commands may have been improved since these logs were recorded.

  * [2009-11-22](http://kippo.rpg.fi/playlog/?l=20091122-075013-5055.log)
  * [2009-11-23](http://kippo.rpg.fi/playlog/?l=20091123-003854-3359.log)
  * [2009-11-23](http://kippo.rpg.fi/playlog/?l=20091123-012814-626.log)
  * [2010-03-16](http://kippo.rpg.fi/playlog/?l=20100316-233121-1847.log)

## Features

S7comm features:
* Fake PLC memory blocks with the ability to upload and download ladder logic programs.
* Possibility to read PLC hardware information, e.g., firmware, name, model.
* Interaction logs that include source IP address, S7comm function commands, blocks accessed, blocks downloaded/uploaded.
* Possibility to capture Ladder logic programs and save them to filesystem for future analysis. 

## Requirements

Software required:

* An operating system (tested on Ubuntu 18 LTS 64-bit)
* [Honeyd](https://github.com/DataSoft/Honeyd)
* Python 2.5+
* [python-nmap](https://pypi.org/project/python-nmap/)
* [snmpsim](https://github.com/etingof/snmpsim)
* [lighttpd](https://www.lighttpd.net/)

## How to install it?

Install [Honeyd](https://github.com/DataSoft/Honeyd) and all its dependencies.

* Append the necessary nmap fingerprints to the Honeyd fingerprint database:

`/usr/share/honeyd/nmap-os-db`

## How to run it?

Edit kippo.cfg to your liking and start the honeypot by running:

`./start.sh`

start.sh is a simple shell script that runs Kippo in the background using twistd. Detailed startup options can be given by running twistd manually. For example, to run Kippo in foreground:

`twistd -y kippo.tac -n`

By default Kippo listens for ssh connections on port 2222. You can change this, but do not change it to 22 as it requires root privileges. Use port forwarding instead. (More info: [MakingKippoReachable](https://github.com/desaster/kippo/wiki/Making-Kippo-Reachable)).

Files of interest:

* dl/ - files downloaded with wget are stored here
* log/kippo.log - log/debug output
* log/tty/ - session logs
* utils/playlog.py - utility to replay session logs
* utils/createfs.py - used to create fs.pickle
* fs.pickle - fake filesystem
* honeyfs/ - file contents for the fake filesystem - feel free to copy a real system here

## Profiler Tool

The Profiler tool creates a PLC Profile that can later be simulated by HoneyPLC.

usage: profiler.py &lt;address&gt; &lt;profile&gt;

Run profiler.py to create a new HoneyPLC profile.
Write the IP address of the PLC host.
Write the name of the profile to be created.
A new directory with the profile data will be created.

Example
`python profiler.py 192.168.0.100 NewProfile`

## Experimental Data

* [PLC Profiles](https://github.com/sefcom/honeyplc/tree/master/experiment-data/plc-profiles)
* [AWS pcaps](https://drive.google.com/drive/folders/1xA3mu7gBI9aPSSlrjJo1S9r-VvZg_izl?usp=sharing)


## I have some questions!

I ~~am~~ _might be_ reachable via e-mail: *edlopezm* at *asu* dot *edu*.
