Proxy Suite for Raspberry Pi 4B (armhf)   
========

<p align="center">
  <img src=".github/imgs/project_logo_v2.png">
</p>

The Proxy Suite is a collection of open-source software which allows to intercept traffic between a target system and its peripherals using a Raspberry Pi 4B device. It is an effort to standardize data exfiltration of (wired) connections between closed-source systems using commodity hardware. The software which is referenced under this umbrella project is a slightly modified version of well-known open-source projects by individual developers and security researchers from all over the world. We at Nesto try to enhance the existing approaches and release our efforts under the same software license as the original project.

Device Support
---------
- **Device**: [Raspberry Pi 4B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/)
- **OS:** Linux
- **Distribution**: Raspberry Pi OS / Raspbian (i.e. Debian's packaging system)
- **Architecture**: armhf

Projects
---------

<table>

  <tr><th>Project</th><th>Interface Type</th><th>Data Forwarding Component Type</th><th>Status</th></tr>
  
  <tr><td rowspan="2"><a href="https://github.com/nesto-software/USBProxy">USBProxy</a><br /><sub><sup>(based on: <a href="https://github.com/usb-tools/USBProxy-legacy">usb-tools/USBProxy-legacy</a>)</sub></sup></td><td rowspan="2">USB</td><td>Software<sup>*</sup></td><td>RTM :heavy_check_mark:</td></tr>
  <tr><td>Hardware <sub><sup><a href="https://luna.readthedocs.io/en/latest/features.html#reference-boards">[LUNA]</a></sub></sup></td><td>PoC :soon:</td></tr>
  
  <tr><td rowspan="2"><a href="https://github.com/nesto-software/EthernetProxy">EthernetProxy</a><br /><sub><sup>(based on: <a href="https://github.com/simsong/tcpflow">simsong/tcpflow</a>)</sub></sup></td><td rowspan="2">Ethernet</td><td>Software</td><td>TBD :gear:</td></tr><tr><td>Hardware <sub><sup><a href="https://www.tp-link.com/us/business-networking/easy-smart-switch/tl-sg105e/">[TL-SG105E]</a><a href="https://greatscottgadgets.com/throwingstar/">[Throwing Star LAN Tap]</a></sub></sup></td><td>RTM :heavy_check_mark:</td></tr>
  
  <tr><td rowspan="2"><a href="https://github.com/nesto-software/SerialProxy">SerialProxy</a><br /><sub><sup>(based on: <a href="http://www.earth.li/projectpurple/progs/sersniff.html">sersniff</a>)</sub></sup></td><td rowspan="2">RS-232</td><td>Software<sup>*</sup></td><td>RTM :heavy_check_mark:</td></tr>
  <tr><td>Hardware <sub><sup><a href="https://www.keelog.com/serial-logger/">[AirDrive Serial Logger]</a></sub></sup></td><td>PoC<sup>**</sup> :warning:</td></tr>

  <tr><td rowspan="2"><a href="https://github.com/nesto-software/LPTProxy">LPTProxy</a></td><td rowspan="2">IEEE 1284 (Centronics / LPT)</td><td>Software <sub><sup><a href="https://www.retroprinter.com/">[using retro-printer module]</a></sub></sup></td><td>TBD :gear:</td></tr><tr><td>Hardware<sup>***</sup></td><td>--- :question:</td></tr>

</table>
<sub><sup>* no special hardware required</sub></sup><br />
<sub><sup>** there are currently issues with the hardware when running proxy for some health check protocols</sub></sup><br />
<sub><sup>*** we are not aware of any solutions on the marked that support this feature</sub></sup>
<br /><br />

We distinguish between a solution which does the actual proxying purely in software (i.e. using the board's CPU) and one which does it in specialized hardware. The latter is generally more performant and robust. Unfortunately, it is not possible to achieve this with commodity hardware for all types of interfaces yet. We keep an eye on active development that is going on though, particularly the teams at [Great Scott Gadgets](https://greatscottgadgets.com/), [Keelog](https://www.keelog.com/software/) and [Retro-Printer](https://www.retroprinter.com/).


Approach
---------

With this project, we want to contribute by...
- ...providing an IPC layer which abstracts away the details of the interface being targeted.
- ...joining forces with the global community of open-source enthusiasts, working on making common peripheral interfaces more accessible for everyone.


GPG
---------

#### Add our key to your keychain!

We use [GPG](https://de.wikipedia.org/wiki/GNU_Privacy_Guard) to sign our binary releases.
In order to install packages from internal repositories, you must add our key for SecureApt to work.

<a target="_blank" href="https://keyoxide.org/F1C6636C27019FD0D29307DEAE25CBF30C0DDB0C" rel="Nesto Cloud Operations">![Nesto Cloud Operations](.github/imgs/gpg_qr.svg)</a> 

<img align="left" src=".github/imgs/openkeychain.png" width="50px">   
<a target="_blank" href="https://www.openkeychain.org/">Download OpenKeychain for Android</a><br />
<a target="_blank" href="https://gnupg.org/download/">Download GNU Privacy Guard for Linux</a>
<br clear="both">
<br />
<b>Keyserver: <a target="_blank" href="https://keys.openpgp.org/search?q=F1C6636C27019FD0D29307DEAE25CBF30C0DDB0C">keys.openpgp.org</a></b>
