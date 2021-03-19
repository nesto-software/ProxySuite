Proxy Suite for Raspberry Pi 4B (armhf)   
========

<p align="center">
  <img src=".github/imgs/project_logo.png">
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

| Project            | Interface Type       | Data Forwarding Component Type | Status |
|:-------------------|:-----------------|:----------------|:----------------|
| [**USBProxy**](https://github.com/nesto-software/USBProxy)       | USB | Software | RTM :heavy_check_mark: |
| [**EthernetProxy**](https://github.com/nesto-software/EthernetProxy)  | Ethernet | Hardware | PoC :soon: |
| [**SerialProxy**](https://github.com/nesto-software/SerialProxy)    | RS-232 | Software | RTM :heavy_check_mark: |
| *TBA* | IEEE 1284 (Centronics / LPT) | Software | TBD :gear: |

We distinguish between a solution which does the actual proxying purely in software and one which does it in specialized hardware. The latter is generally more performant and robust. Unfortunately, it is not possible to achieve this with commodity hardware for all types of interfaces yet. We keep an eye on active development that is going on though, particularly [the team at Great Scott Gadgets](https://greatscottgadgets.com/). 

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
