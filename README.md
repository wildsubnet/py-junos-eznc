[![Build Status](https://travis-ci.org/jeremyschulman/py-junos-eznc.png?branch=master)](https://travis-ci.org/jeremyschulman/py-junos-eznc)

The repo is under active development on release 0.0.3.  If you take a clone, you are getting the latest, and perhaps not entirely stable code.  

Early Adopter version 0.0.2 is now in PyPi, see [Installation](#installation).

## ABOUT

_Junos EZ_ is a Python library to remotely manage/automate Junos devices.  The user is ***NOT*** required: (a) to be a "Software Programmer™", (b) have sophisticated knowledge of Junos, or (b) have a complex understanding of the Junos XML API.  

This library was built for two types of users:

### For "Non-Programmers" - Python as a Power Shell

This means that "non-programmers", for example the _Network Engineer_, can use the native Python shell on their management server (laptop, tablet, phone, etc.) as their point-of-control for remotely managing Junos devices. The Python shell is an interactive environment that provides the necessary means to perform common automation tasks, such as conditional testing, for-loops, macros, and templates.  These building blocks are similar enough to other "shell" enviornments, like Bash, to enable the non-programmer to use the Python shell as a power-tool, rather than a programming language.  From the Python shell a user can manage Junos devices using native hash tables, arrays, etc. rather than device-specific Junos XML or resorting to 'screen scraping' the actual Junos CLI.

### For "Programmers" - Open and Extensible

There is a growing interest and need to automate the network infrastructure into larger IT systems.  To do so, traditional software programmers, DevOps, "hackers", etc. need an abstraction library of code to further those activities.  _Junos EZ_ is designed for extensibility so that the programmer can quickly and easily add new widgets to the library in support of their specific project requirements.  There is no need to "wait on the vendor" to provide new functionality.   _Junos EZ_ is not specifically tied to any version of Junos or any Junos product family. 

## FEATURES

_Junos EZ_ is designed to provide the same capabilties as a user would have on the Junos CLI, but in an environment built for automation tasks.  These capabiltieis include, but are not limited to:

* Provide "facts" about the device such as software-version, serial-number, etc.
* Retrieve the "operational" or "run-state" information (think "show" commands)
* Make configuration changes
* Provide common utilities for tasks such as secure copy of files and software updates

_Junos EZ_ uses the Junos XML API via the NETCONF protocol.  This level of detail is generally shielded from the user.  At times, you may need to access the API, and this library provides an easy meta-programming mechanism to do so.  

## INSTALLATION

    pip-2.7 install git+https://github.com/Juniper/ncclient.git
    pip-2.7 install junos-eznc
 

## HELLO, WORLD

The following is a quick "hello, world" example to ensure that the softare was installed correctly.  This code will simply connect to a device and display the known facts of the device, like serial-number, model, etc.

````python
from pprint import pprint
from jnpr.junos import Device

dev = Device(host='my_host_or_ipaddr', user='jeremy', password='jeremy123' )
dev.open()

pprint( dev.facts )

dev.close()
````
Example output for an SRX-210 device:
````python
>>> pprint(dev.facts)
{'2RE': False,
 'RE0': {'last_reboot_reason': '0x20:power-button soft power off',
         'model': 'RE-SRX210H',
         'status': 'OK',
         'up_time': '10 minutes, 3 seconds'},
 'domain': 'workflowsherpas.com'         
 'fqdn': 'srx210.workflowsherpas.com',
 'hostname': 'srx210',
 'ifd_style': 'CLASSIC',
 'model': 'SRX210H',
 'personality': 'SRX_BRANCH',
 'serialnumber': 'AD2909AA0096',
 'switch_style': 'VLAN',
 'version': '12.1X44-D10.4',
 'version_info': junos.versino_info(major=(12, 1), type=X, minor=(44, 'D', 10), build=4)}
````
## DOCUMENTATION

Please refer to the [_docs_](docs) directory.

## DEPENDENCIES

This module requires Python 2.7.  

  * [lxml](http://lxml.de/index.html) - XML programming library
  * [ncclient](https://github.com/juniper/ncclient) (_Juniper edition_) - NETCONF base library
  * [paramiko](https://github.com/paramiko/paramiko) - SSH library (also used by ncclient)
  * [scp](https://github.com/jbardin/scp.py) - SCP library
  * [jinja2](http://jinja.pocoo.org/docs) - templating library
  * [netaddr](https://pypi.python.org/pypi/netaddr/) - Network IPv4,IPv6 address library

## LICENSE

BSD-2
  
# CONTRIBUTORS

  - Jeremy Schulman (@nwkautomaniac), Core developer
