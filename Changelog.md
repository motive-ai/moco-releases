## 7.2.0 (5/22/2020) ##
### Features ###
* joint calibration program
* config read/write utilities (moco_config_reader and moco_config_maker)
### Bugfixes ###
* Fix memory leak upon release of USB device
### Notes ###
* This release splits the graphical apps into a separate "extras" package

## 7.1.1 (5/15/2020) ##
### Bugfixes ###
* (firmware) Include all error string messages. Fixes possible out-of-bounds access

## 7.1.0 (5/7/2020) ##
### Features ###
* ChainSim - easy connection to Simulator instances
* Simulator encoders match hardware resolution
* (firmware) add warning if encoder values don't match

### Bugfixes ###
* (firmware) output calibrated sensor data in SystemData packet

#### Notes ####
* Default port for simulator is moved to 6610, 6611

## 7.0.3 (2/17/2020) ##
### Bugfixes ###
* Transmit commutation warning if motor does not have phase alignment

## 7.0.2 (2/7/2020) ##
### Bugfixes ###
* Check for invalid raw encoder values

## 7.0.1 (12/4/2019) ##
### Bugfixes ###
* Fix SSI encoder commutation when used as motor encoder (ie: in wrist)

## 7.0.0 (12/4/2019) ##
### Features ###
* Reworked position and velocity controllers
* Parameters for position and velocity mode updated
* Position mode now requires a velocity target in its command

## 6.1.0 (11/25/2019) ##
### Features ###
* Wrist board compatibility updates 

## 6.0.1 (11/13/2019) ##
### Bugfixes ###
* Fix moco_commander not launching

## 6.0.0 (10/23/2019) ##
### Features ###
* Absolute motor encoder support. Allows for phase-lock-less electrical angle
    commutation.
* Documentation updates
* Generalize encoder support
* Hardline E-stop support
### Bugfixes ###
* Velocity command was not working in API

## 5.9.1 (5/6/2019) ##
### Bugfixes ###
* Remove API build dependency on moco_version.h

## 5.9.0 (5/5/2019) ##
### Features ###
* Velocity control mode
* Disconaut support
* Allow Fan control and P-Brake control on Disconaut
* Temperature sensing support (Disconaut)
* Commutation lock detection
* USB reset function
### Bugfixes ###
* pthread initialization error

## 5.8.0 (3/28/2019) ##
### Features ###
* MocoUSBManager class to consolidate USB querying
   -  Caches information for improved performance
* Logging API
### Bugfixes ###
* Possible race condition in USB device release
* Fix absolute encoder offset setup so that the initial reading will be
    consistent based on the low/high limit. Previously the 'rollover' value
    could change based on where the initial reading was taken from.

## 5.7.2 (1/15/2019) ##
### Bugfixes ###
* Improve Hall Effect Sensor commutation algorithm
* Documentation Updates

## 5.7.1 (12/18/2018) ##
### Features ###
* Multi-DoF example in SDK
### Bugfixes ###
* Build-server side issue with reporting zmq debug library

## 5.7.0 (12/11/2018) ##
### Features ###
* Improved flash writing utilities
* Chain API easier to setup
* Documentation updates

### Bugfixes ###
* Sending exactly 64 byte packets would hang
* Broadcast packets not sent correctly over ZMQ
* Fix for large packets (> 'GenericData' bytes)

## 5.6.1 (11/29/2018) ##
### Bugfixes ###
* Fix startup packet timing

## 5.6.0 (11/28/2018) ##
### Features ###
* Store config packets in Flash
* Updated json config format
* Documentation updates

### Bugfixes ###
* Fix SPI communication with DRV8323
* Allow USB packets to be up to 4k in size

## 5.5.0 (11/07/2018) ##
### Features ###
* Support configurable analog or SPI torque sensors (WOC-737)
* Store data packets in flash (WOC-678)
* Improve motor simulator (WOC-748)
* Hall encoder velocity support

### Bugfixes ###
* DRV8323 communication fixes
* Fix encoders on Disco boards

## 5.4.0 (8/15/2018) ##
### Features ###
 * Windows support for Moco SDK
 * Ubuntu 18.04 support for Moco SDK
 * SDK examples updated
### Bugfixes ###
 * Fix linking issue with USB library in SDK

## 5.3.0 (7/31/2018) ##
### Features ###
* Support Disco boards

## 5.2.0 (7/20/2018) ##
### Features ###
* Add Joint-state packet
* Add joint Chain and robot state
* High-level packet interface
    - Provides abstraction to position, torque and impedance control
* Improve USB performance (WOC-726)
* Support Etherlab 3
* Impedance Velocity Limit

### Bugfixes ###
* Improve encoder velocity estimates
* Moco Commander accepts decimal-first values, ie: ".15" instead of having to type "0.15"
* send_cmd forces usage of serial or all boards
* Improve board timing
* Standardize 'velocity' and 'feed_forward' nomenclature

## 5.1.2 (6/14/2018) ##
### Bugfixes ###
* Fix Sin Position Mode startup behavior

## 5.1.1 (6/11/2018) ##
### Bugfixes ###
* Fix API library linking issues
    - Better PIC support. This was causing issues on Ubuntu 18.04

## 5.1.0 (6/8/2018) ##
### Features ###
#### Firmware ####
* Position mode will start from current position instead of 0 (WOC-718)
    - Previously, when sending sending a position mode packet, the actuator would slew to 0 position. With this change, the actuator will stay at it's current position, and only update when a position command is sent.
* Support one-time packet responses with `DATA_FMT_IMMEDIATE_REQUEST` (WOC-528)
    - Client can request a single packet of any Status type, which will be immediately returned.

#### API ####
* Config validation (WOC-717)
    - New `validate_config` function in `Moco` to check that all keys in a json config are valid as compared to GenericData, and that there are no missing keys
* Simulink library auto-generation (WOC-715)
    - Add matlab script to produce a simulink library from the compiled mex functions
    - Also updates the build script for easier usage

### Bugfixes ###
* rework `libusb` building so that installed libs use correct paths
    - previously, the build system path was added to CMake export file `MocoTargets.cmake`
* Update default config
    - `DSPStackV1_1_Defaults.json` didn't get updated with new packet keys in 5.0.0


## 5.0.0 (5/31/2018) ##
### Features ###
- Report motor torque instead of motor current
- Add impedance mode
- Separate packet to clear fault flags
- Send connected message on positive USB connection
- Support SPI Modes (https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus#Mode_numbers)
- Support different SPI frequencies
- In two-encoder system, support automatically setting bias on QEP encoder from absolute encoder (WOC-706)
- add separate version to data packets
- Support SPI accelerometers
- Low-level, high-speed current tuning mode (WOC-707)

### Bugfixes ###
- fix SSI rollover

### Developer ###
- New C++ API

## 4.4.0 (4/24/2018) ##
### Features ###
- Improve performance in `graph`
- `moco_commander` can read config from `moco_manager`
- Allow specifying motor commutation direction in config
- Allow specifying motor phase ordering in config
- Show incoming log message time in `moco_graph`
- Simplify GenericData packet format
- Cogging map easier to produce
- Send message with DRV faults

### Bugfixes ###
 - `GetConfig` response returns expected data
 - fix zmq on Windows

## 4.3.2 (3/9/2018) ##
- Fix `unified` setting in `usb_tcp`

## 4.3.1 (3/7/2018) ##
- Fix `moco_manager` from hanging on Windows

## 4.3.0 (3/7/2018) ##
### Features ###
 - simulate plug-and-play on Windows

### Firmware ###
 - DFU erasing now sector by sector (WOC-633)
 - Add current bias filter
 - support for v1.2a
 - analog deadband
 - encoder error re-added

### Developer ###
 - swap command line parser to CLI11 (remove Boost dependency)
 - `libusb` updated to latest (1.0.22rc3)
 - support for hardware in the loop testing
 - Updated documentation

## 4.2.0 (2/14/2018 ❤️) ##
### Features ###
 - Display mean and std dev. statistics in graph when paused (WOC-613)
 - Use flags in header to send a response to received commands (WOC-528)
 - Hall sensing (WOC-472)
 - FunctionGenerator has more accurate timing (WOC-620)
 - Better SPI fault flags

### Bugfixes ###
 - Fix length of string packets sent from firmware
 - Fix length of string packets received in python
 - Put bash completion file in correct directory
 - Fix Firmware time rollover (WOC-617)
 - Add logger and process_manager to SDK files
 - `libusb` has correct RPATH on macOS
 - exclude libdrm from linux builds
 - make bundled version of `moco_manager` not hang

### Developer ###
 - SDK cleanup

## 4.1.0 (1/15/2018) ##
### Features ###
 - Add `ControllerData` packet
 - Report time from Moco board in microseconds

### Bugfixes ###
- Plug memory leaks in firmware USB
- Plug memory leaks in client USB


## 4.0.0 (11/16/2017) ##
### Features ###
- Support python 3 (WOC-579)
- `moco_manager`
    - Configure multiple moco boards in INI file
### Bugfixes ###
- Fix window title in `moco_commander`

## 3.4.0 (10/6/2017) ##
### Features ###
- Support response packets (WOC-528)

### Bugfixes ###
- Analog B channel filter fixed
- Position mode velocity noise improved

## 3.3.0 (9/19/2017) ##
### Features ###
 - Added hardware documentation
 - startup config script
 - `usb_tcp` lists firmware version (WOC-508)
 - `multisim` allows running multiple simulators at once, and in concert with actual MoCo boards (ARM-8)
 - soft limits for SSI encoder (WOC-507)
 - report DRV8301 errors (WOC-504)
 - view URDF files (ARM-21)
 - IK position control (ARM-21)

### Firmware ###
- SPI functionality
- string packet now sends correct number of bytes (WOC-503)

### Bug Fixes ###
- `write_program_to_dsp` no longer overwrites Sector A


## 3.2.0 (7/28/2017) ##
### Features ###
 - Add `dfu-util` to release
 - Add firmware in `.bin` format to release
 - Brushed motor simulator
 - Graph: Add 'Clear' option, which keeps graph variables, but removes past data
 - Graph: optionally plots x-axis using absolute time instead of relative
 - File plotter. Currently plots CSV files
 - macOS release

### Bug Fixes
 - Fix JSON support in Graph

### Developer
 - Using C++11 JSON library (https://github.com/nlohmann/json)
 - simulator libraries are now optionally built as shared libs
 - remove unneeded programs (serial_tcp, motive_vr) from release


## 3.1.0 (7/10/2017) ##
### Features ###
 - SDK:
    - C API with libs, includes, CMakefile and example
    - Python module with examples (WOC-495)
 - documentation: Expanded User guide and developer docs, external API docs (for SDK) and updated internal docs (WOC-477)

### Bug Fixes ###
 - `mpd_zmq` now has correct support for addressing mode (ie: sending serial number as multi-part zmq)

## 3.0.0 (7/3/2017) ##
### Features ###
 - DFU mode for USB firmware flashing (WOC-473)
 - Add `serial` argument to command_ui
 - Simplified startup script
 - Add Voltage limit parameters (WOC-456)
 - Documentation improvements

### Bugfixes ###
 - fix verbosity setting in `usb_tcp` (WOC-475)

### Firmware ###
 - Massively reorganize code to make loops more modular
 - SSI Encoder Support (WOC-465)
 - Reorganize command data (WOC-463)

### Developer ###
 - update python requirements
 - `usb_tcp` uses c++11

## 2.0.0 (4/16/2017) ##
### Features ###
- Save configs in MoCo Commander (WOC-233)
- Simulink can receive commands (WOC-257)
- usb_tcp improvements: ( #121 WOC-264)
  - support USB hotplug (linux / macOS only)
  - usb_tcp allows multiple boards
  - aggregate communication from multiple boards to one port, using serial # as address (multi-part ZMQ)
  - change default ports to: 6500 for data from moco to client, and 6501 for data from client to moco
  - allow for "broadcast" messages, send to all boards
- allow removal of plots in `graph` ( #122 WOC-228)
- added end-user documentation to docs.motive.ai ( #128 WOC-435)

### Firmware ###
- Function Generator ( #114 WOC-366)
- Cogging Map ( #116 WOC-367)
- Add SystemData packet ( #117 WOC-404)
- QEP Improvements ( #117 WOC-404 )
- Independent current gains for ABC ( #118 WOC-405)
- Dual analog configuration
- Add VR mode ( #123 WOC-343)
- Position rate limiting ( #125 WOC-425)
- Support WCID for driverless install ( #126 WOC-433)

### Bugfixes ###
- PWM startup fixes (WOC-242)
- Sin Fixes ( #111 )
- PWM Frequencies ( #112 WOC-359, WOC-360)
- Doxygen supports all recent versions ( #103 )

### Other ###
- firmware flashing scripts improved ( #129 )


## 1.8.1 (1/4/2017) ##
### Bugfixes ###
- Fixes memcopy in CLA

## 1.8.0 (12/29/2016) ##
### Features ###
- Command UI Keeps last value (WOC-209)
- Show host and port in title in graph and commander (WOC-219)
- Firmware support for dynamically setting packet rates and types (WOC-126)
- documentation improvements (WOC-225)
- Graph displays list of packet in sidebar, and support drag-and-drop graph creation (WOC-192)

### Bugfixes ###
- initialization error in graph
- startup script improvements

### Other ###
- Firmware has undergone minor reorg (WOC-130)
- build issues with pyinstaller parallel builds


## 1.7.2 (12/12/2016) ##
### Bugfixes ###
- Pyinstaller issue what requires LD_LIBRARY_PATH to be set on linux
- Allow Simulink blocks to be linked to libraries

## 1.7.0 (12/9/2016) ##
### Features ###
- Bash completion (WOC-177)
- Simulink real-time support (WOC-203)
- Support different PWM modes (WOC-202)

### Bug Fixes ###
- USB fixes (WOC-204, WOC-205, WOC-215, WOC-218)
- Set executable bit for GUI programs on linux (WOC-213)

### Other ###
- 14.04 build support

## 1.6.0 (11/30/2016) ##
### Features ###
- Oscilloscope pin probe support (WOC-168)
- Timing data packet (WOC-27)
- Simulink block creation
- High performance graphing tool (WOC-192)
- Windows x64 native support (WOC-198)
- Full-state control
- Encoder Index Checking (WOC-167)

### Bug Fixes ###
- Some USB packets dropped at high data rates (WOC-179)
- SPI startup issues (WOC-181)

## 1.5.0 (11/14/2016) ##
### Features ###
- USB Support (WOC-102)
- Windows support for USB (WOC-170)
- SPI support
- Simulink block creation (WOC-87)
- Support Pins for MoCo-DSPv1.1 (WOC-151)
- Serial Numbers (WOC-150)
- Support I2C
- Feed-forward position control
- Command Sending via dynamic lookup from data packets
- Proper packaging (WOC-145)
- Bode plots

### Bugfixes ###
- Support USB Packets greater than 64 bytes (WOC-163)
- USB HWConfig messages not working (WOC-153)
- USB stuck when using serial communication (WOC-154)
- Incorrect header sizes (WOC-141)

## 1.4.0 (9/21/2016) ##
