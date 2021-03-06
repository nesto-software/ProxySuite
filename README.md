Proxy Suite for Raspberry Pi 4B (armhf)   
========

<p align="center">
  <img src=".github/imgs/project_logo_v2.png">
</p>

[![.github/workflows/proxy-suite-tests.yml](https://github.com/nesto-software/ProxySuite/actions/workflows/proxy-suite-tests.yml/badge.svg)](https://github.com/nesto-software/ProxySuite/actions/workflows/proxy-suite-tests.yml)
[![https://github.com/nesto-software/cross-toolchain-armhf](https://img.shields.io/badge/built%20using-cross--toolchain--armhf-blue)](https://github.com/nesto-software/cross-toolchain-armhf)

The Proxy Suite is a collection of open-source software which allows intercepting traffic between a target system and its peripherals using a Raspberry Pi 4B device. It is an effort to standardize data exfiltration of (wired) connections between closed-source systems using commodity hardware. The software which is referenced under this umbrella project is a slightly modified version of well-known open-source projects by individual developers and security researchers from all over the world. We at Nesto try to enhance the existing approaches and release our efforts under the same software license as the original project.

Features
---------

- :eyes: Gives access to (unencrypted) data passed between common wired interfaces
- :dollar: Built for affordable/commodity hardware: Raspberry Pi 4B
- :star: Built using forks of well-known software projects
- :sunglasses: Lets you build your own analysis layer using any high-level language due to IPC components (ZMQ + msgpack)
- :hourglass_flowing_sand: Saves you time if you want to get data out of target systems without writing emulators for client devices (e.g. virtual printer protocol stacks)
- :raised_hands: Many real-world use cases, such as virtual printers or human interface devices (e.g. keyloggers)
- :tongue: Circumvents hardware vendor restrictions often seen with closed (source) systems - no access to software on host or client device is needed; only wiring of peripherals to be changed
- :microscope: Provides out-of-band (hardware) approaches for fully transparent, passive filtering - allowing unaltered operation of present systems
- :guardsman: Provides in-band (software) approaches for active data forwarding - giving you full control over the data stream
- :bulb: Reference for everyone who wonders how to code for all of these (retro) interfaces using a Raspberry Pi (or similar arm devices)
- :runner: Fast dev environment setup if you want to support this project due to [VSCode Remote Docker Containers](https://code.visualstudio.com/docs/remote/containers) integration

Device Support
---------
- **Device**: [Raspberry Pi 4B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/)
- **OS:** Linux
- **Distribution**: Raspberry Pi OS / Raspbian (i.e. Debian's packaging system)
- **Architecture**: armhf

Components
---------

<table>

  <tr><th>Component</th><th>Interface Type</th><th>Proxy Type</th><th>Status</th></tr>
  
  <tr><td><a href="https://github.com/nesto-software/USBProxy">USBProxy</a><br /><sub><sup>(based on: <a href="https://github.com/usb-tools/USBProxy-legacy">usb-tools/USBProxy-legacy</a>)</sub></sup></td><td rowspan="2">USB</td><td>Software<sup>*</sup></td><td>RTM :heavy_check_mark:</td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/USBProxy2">USBProxy2</a></td><td>Hardware <sub><sup><a href="https://luna.readthedocs.io/en/latest/features.html#reference-boards">[LUNA]</a></sub></sup></td><td>TBD :soon:</td></tr>
  
  <tr><td rowspan="2"><a href="https://github.com/nesto-software/EthernetProxy">EthernetProxy</a><br /><sub><sup>(based on: <a href="https://github.com/simsong/tcpflow">simsong/tcpflow</a>)</sub></sup></td><td rowspan="2">Ethernet</td><td>Software</td><td>TBD :gear:</td></tr><tr><td>Hardware <sub><sup><a href="https://www.tp-link.com/us/business-networking/easy-smart-switch/tl-sg105e/">[TL-SG105E]</a><a href="https://greatscottgadgets.com/throwingstar/">[Throwing Star LAN Tap]</a></sub></sup></td><td>RTM :heavy_check_mark:</td></tr>
  
  <tr><td rowspan="2"><a href="https://github.com/nesto-software/SerialProxy">SerialProxy</a><br /><sub><sup>(based on: <a href="http://www.earth.li/projectpurple/progs/sersniff.html">sersniff</a>)</sub></sup></td><td rowspan="2">RS-232</td><td>Software<sup>*</sup></td><td>RTM :heavy_check_mark:</td></tr>
  <tr><td>Hardware <sub><sup><a href="https://www.keelog.com/serial-logger/">[AirDrive Serial Logger]</a></sub></sup></td><td>RTM :heavy_check_mark::warning:<sup>**</sup></td></tr>

  <tr><td rowspan="2"><a href="https://github.com/nesto-software/LPTProxy">LPTProxy</a><br /><sub><sup>(based on: retro-printer capture code)</sub></sup></td><td rowspan="2">IEEE 1284 (Centronics / LPT)</td><td>Software <sub><sup><a href="https://www.retroprinter.com/">[using retro-printer module]</a></sub></sup></td><td>PoC :soon:</td></tr><tr><td>Hardware</td><td>--- :question:<sup>***</sup></td></tr>

</table>
<sub><sup>* no special hardware required</sub></sup><br />
<sub><sup>** there are currently issues with the hardware when running proxy for some health check protocols</sub></sup><br />
<sub><sup>*** we are not aware of any solutions on the marked that support this feature</sub></sup>
<br /><br />

We distinguish between a solution which does the actual proxying purely in software (i.e. using the board's CPU) and one which does it in specialized hardware. The latter is generally more performant and robust as it is *out-of-band*. Unfortunately, it is not possible to achieve this with commodity hardware for all types of interfaces yet. We keep an eye on active development that is going on though, particularly the teams at [Great Scott Gadgets](https://greatscottgadgets.com/), [Keelog](https://www.keelog.com/software/) and [Retro-Printer](https://www.retroprinter.com/).

Approach
---------

With this project, we want to contribute by...
- ...providing an IPC layer which abstracts away the details of the interface being targeted.
- ...joining forces with the global community of open-source enthusiasts, working on making common peripheral interfaces more accessible for everyone.

<img src=".github/imgs/concept.png" />

Status
--------

We are able to extract data from every non-encrypted wired communication channel between a POS system and its printers that is known to us!

We noticed that wireless connections are rarely used for thermal printers. We can probably work around Wi-Fi (IEEE 802.11) by spawning a custom access point and using EthernetProxy between the AP and the POS. Support for Bluetooth (IEEE 802.15) might be added to this project in the future as we see more and more people using Bluetooth thermal printers. In both wireless cases, we must make sure that traffic flows through the proxy device. Observing traffic passively, like in the hardware approach of the EthernetProxy component, is too risky since we cannot make sure that we see all packets between the target devices.

Applicability
--------

Most thermal printers on the market use the [JetDirect](https://en.wikipedia.org/wiki/JetDirect) or the AppSocket protocol to receive print jobs over the network. It is a simple TCP connection over port 9100, which transports data in plain text. No encryption is used for other transports over interfaces such as USB, Serial, or LPT either. Thus, the ProxySuite components gain access to all of the invoice content transferred between the POS system and its printer. Once the data is intercepted, it can be analyzed as is. The ZMQ layer provided by all ProxySuite components makes the analysis a lot easier by letting you choose the programming language you want to use. There is a clear separation between "low-level" components that extract the data for you and the final analysis, which you might code in any language that has a binding for [ZMQ](http://wiki.zeromq.org/bindings:_start) and [msgpack](https://msgpack.org/).

Releases & Downloads
---------

<table>

  <tr><th>Component</th><th>Release</th><th>Download</th><th>Status</th></tr>

  <tr><td><a href="https://github.com/nesto-software/USBProxy">USBProxy</a></td><td><a href="https://github.com/nesto-software/USBProxy/releases/tag/nightly-latest">nightly</a><br /><a href="https://github.com/nesto-software/USBProxy/releases/tag/v0.1.0">v0.1.0</a></td><td><code>bash -c "$(curl -fsSL https://raw.githubusercontent.com/nesto-software/USBProxy/master/scripts/install-from-release.sh)"</code></td><td><a href="https://github.com/nesto-software/USBProxy/actions/workflows/build-app-nightly.yaml"><img src="https://github.com/nesto-software/USBProxy/workflows/.github/workflows/build-app-nightly.yaml/badge.svg?branch=dev" /></a><br /><a href="https://github.com/nesto-software/USBProxy/actions/workflows/build-app-release.yaml"><img src="https://github.com/nesto-software/USBProxy/workflows/.github/workflows/build-app-release.yaml/badge.svg" /></a></td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/EthernetProxy">EthernetProxy</a></td><td><a href="https://github.com/nesto-software/EthernetProxy/releases/tag/latest">latest</a></td><td><code>bash -c "$(curl -fsSL https://raw.githubusercontent.com/nesto-software/EthernetProxy/master/scripts/install-from-release.sh)"</code></td><td><a href="https://github.com/nesto-software/EthernetProxy/actions/workflows/build-binaries.yml"><img src="https://github.com/nesto-software/EthernetProxy/actions/workflows/build-binaries.yml/badge.svg" /></a></td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/SerialProxy">SerialProxy</a></td><td><a href="https://github.com/nesto-software/SerialProxy/releases/tag/latest">latest</a></td><td><code>bash -c "$(curl -fsSL https://raw.githubusercontent.com/nesto-software/SerialProxy/master/scripts/install-from-release.sh)"</code></td><td><a href="https://github.com/nesto-software/SerialProxy/actions/workflows/build-binaries.yml"><img src="https://github.com/nesto-software/SerialProxy/actions/workflows/build-binaries.yml/badge.svg" /></a></td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/LPTProxy">LPTProxy</a></td><td><a href="https://github.com/nesto-software/LPTProxy/releases/tag/latest">latest</a></td><td><code>bash -c "$(curl -fsSL https://raw.githubusercontent.com/nesto-software/LPTProxy/master/scripts/install-from-release.sh)"</code></td><td><a href="https://github.com/nesto-software/LPTProxy/actions/workflows/build-lptproxy.yml"><img src="https://github.com/nesto-software/LPTProxy/actions/workflows/build-lptproxy.yml/badge.svg" /></a></td></tr>
  
</table>

Dependencies & Tools
---------
<table>

  <tr><th>Component</th><th>Shared Runtime Lib Dependencies (dpkg/apt)</th><th>Programming Language(s)</th><th>Build System(s)</th></tr>

  <tr><td><a href="https://github.com/nesto-software/USBProxy">USBProxy</a></td><td>
  libusb-1.0-0<br />
  libudev1<br />
  libzmq3-dev
  </td><td>C/C++</td><td>CMake, Make</td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/EthernetProxy">EthernetProxy</a></td><td>
  libpcap0.8<br />
  openssl<br />
  libzmq3-dev
  </td><td>C++</td><td>Autotools, Make</td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/SerialProxy">SerialProxy</a></td><td>
  libzmq3-dev
  </td><td>C++</td><td>CMake, Make</td></tr>
  
  <tr><td><a href="https://github.com/nesto-software/LPTProxy">LPTProxy</a></td><td>
  wiringpi=2.50<br />
  libzmq3-dev
  </td><td>C</td><td>CMake, Make</td></tr>
  
</table>

FAQ
---------
### Why ZMQ?

We use the IP layer to privide inter-process communication (IPC) functionality. 
The ZMQ library has bindings for a large variety of programming languages and provides very easy means to pass data around.

You can write an analysis layer in any programming language you want, import the ZMQ library and start receiving data from any ProxySuite component using a ZMQ subscriber.

We chose to use ZMQ for any ProxySuite component, so you can swap ProxySuite components (i.e. wired interfaces) at will and still reuse your analysis layer code. We (almost) fully abstract away all details of the interface being targeted. 

### Why msgpack?

Some newer interfaces such as Ethernet and USB allow multiplexing different data channels over a single physical wire.
In order to pass information about ports, IPs, interface numbers, and other **metadata** for the observed connection, we send structured data over ZMQ. Data is serialized/deserialized using the msgpack library.

Non-multiplexed connections such as serial and parallel do not depend on msgpack.   
There is an idea to unify the ProxySuite components and increase interoperability by always using msgpack, see [#8](https://github.com/nesto-software/ProxySuite/issues/8).

### What is Greengrass?

Each ProxySuite component consists of a CLI binary and a corresponding Greengrass binary.
AWS IoT Greengrass is an open source edge runtime and cloud service that helps you build, deploy, and manage IoT software on the AWS platform.
The Greengrass binary conforms to a special type of Lambda function called **Lambda executable**.

It is all about bringing data into the cloud nowadays.  
As time to market (TTM) is crucial, we believe that - on the enterprise level - using open-source AWS technology is a secure and reliable way to accomplish it as fast as possible.

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
