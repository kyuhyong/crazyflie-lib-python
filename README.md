# cflib: Crazyflie python library [![Build Status](https://api.travis-ci.org/bitcraze/crazyflie-lib-python.svg)](https://travis-ci.org/bitcraze/crazyflie-lib-python)

cflib is an API written in Python that is used to communicate with the Crazyflie
and Crazyflie 2.0 quadcopters. It is intended to be used by client software to
communicate with and control a Crazyflie quadcopter. For instance the [cfclient][cfclient] Crazyflie PC client uses the cflib.

See [below](#platform-notes) for platform specific instruction.
For more info see our [wiki](http://wiki.bitcraze.se/ "Bitcraze Wiki").
---
### Linux

#### Setting udev permissions

The following steps make it possible to use the USB Radio without being root.
```
sudo groupadd plugdev
sudo usermod -a -G plugdev <username>
```
Create a file named ```/etc/udev/rules.d/99-crazyradio.rules``` and add the
following:
```
SUBSYSTEM=="usb", ATTRS{idVendor}=="1915", ATTRS{idProduct}=="7777", MODE="0664", GROUP="plugdev"
```
#### Wireless Setup for PX4 Connection
Connecting via MAVLink:
* Download the crazyflie-lib-python source code:
Git Clone this project
* Build a virtual environment (local python environment) with package dependencies using the following method:
```sh
  pip install tox --user
```
* Navigate to the crazyflie-lib-python folder and type:
```sh
  make venv
```
* Activate the virtual environment:
```sh
  source venv-cflib/bin/activate
```
* Install required dependencies:
```sh
  pip install -r requirements.txt --user
```
To connect Crazyflie 2.0 with crazyradio, launch cfbridge by following these steps:

* Power off and power on Crazyflie 2.0 and wait for it to boot up.
* Connect a Crazyflie radio device via USB.
* Navigate to the crazyflie-lib-python folder.
* Activate the environment:
```sh
source venv-cflib/bin/activate 
```
Navigate to the examples folder:
```sh
  cd examples
  ```
Launch cfbridge:
```sh
  python cfbridge.py <Port number>
```
---
## Development
### Developing for the cfclient
* [Fork the cflib](https://help.github.com/articles/fork-a-repo/)
* [Clone the cflib](https://help.github.com/articles/cloning-a-repository/), `git clone git@github.com:YOUR-USERNAME/crazyflie-lib-python.git`
* [Install the cflib in editable mode](http://pip-python3.readthedocs.org/en/latest/reference/pip_install.html?highlight=editable#editable-installs), `pip install -e path/to/cflib` 
* [Uninstall the cflib](http://pip-python3.readthedocs.org/en/latest/reference/pip_uninstall.html), `pip uninstall cflib`

Note: If you are developing for the [cfclient][cfclient] you must use python3.

### Linux, OSX, Windows
* Build a [virtualenv (local python environment)](https://virtualenv.pypa.io/en/latest/) with package dependencies
  * `pip install virtualenv`
  * `virtualenv venv`
  * `source venv/bin/activate`
* `pip install -r requirements.txt`
* Activate the environment: `source venv/bin/activate`
* Connect the crazyflie and run an example: `python examples/basiclog`
* Deactivate the virtualenv if you activated it `deactivate`

Note: For systems that support [make](https://www.gnu.org/software/make/manual/html_node/Simple-Makefile.html), the first four steps can be replaced with `make venv`

Note: The first three steps can be skipped if you don't mind installing cflib dependencies system-wide.


# Testing
### With docker and the toolbelt

For information and installation of the 
[toolbelt.](https://wiki.bitcraze.io/projects:dockerbuilderimage:index)
  
* Check to see if you pass tests: `tb test`
* Check to see if you pass style guidelines: `tb verify`

Note: Docker and the toolbelt is an optional way of running tests and reduces the 
work needed to maintain your python environmet. 

### Native python on Linux, OSX, Windows
 [Tox](http://tox.readthedocs.org/en/latest/) is used for native testing: `pip install tox`
* If test fails after installing tox with `pip install tox`, installing with  `sudo apt-get install tox`result a successful test run

* Test package in python2.7 `TOXENV=py27 tox`
* Test package in python3.4 `TOXENV=py34 tox`
* Test package in python3.6 `TOXENV=py36 tox`

Note: You must have the specific python versions on your machine or tests will fail. (ie. without specifying the TOXENV, `tox` runs tests for python2.7, 3.3, 3.4 and would require all python versions to be installed on the machine.)


## Contribute

Everyone is encouraged to contribute to the CrazyFlie library by forking the Github repository and making a pull request or opening an issue.
