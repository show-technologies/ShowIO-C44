# ShowIO C44 - User Documentation
The ShowIO C44 is a multipurpose show control device with the following features:

### Digital I/O
  * ✅ 12-24V DC I/O power connection
  * ✅ (4) 500mA digital outputs
  * 🔜 (4) contact closure digital inputs

### Wired networking
  * ✅ 10/100MBPS Ethernet connection
  * ✅ OSC I/O control
  * ✅ OSC device configuration
  * 🔜 Multi-protocol support (sACN, Art-Net, MIDI-over-Ethernet, etc.)
    
### Wireless networking
  * 🔜 802.11 WiFi network connection
  * 🔜 Wireless OSC functionality
    
### USB interface
  * ✅ 5V core power over USB
  * ✅ Plug-and-play I/O control with OSC-over-USB
  * ✅ Plug-and-play device configuration
    
### Dual isolated RS-485 Serial Transcievers
  * 🔜 DMX controller functionality
  * 🔜 DMX receiver functionality
  * 🔜 Daisy-chain multiple ShowIO devices together

### Software Integrations
  * ✅ Designed for use with ShowNET
  * ✅ TouchOSC (OSC)
  * ✅ QLab (OSC)
  * ✅ EOS (OSC)

# Getting Started

### Powering Your C44
  * R.03 of the C44 uses a 5v USB power supply to power the core. Each device will pull up to 2.5w. With the core powered, the C44 will connect over an Ethernet network and run its firmware. With the debugging LEDs, you can try out your show control programs before hooking your device up to field power.
  * IMPORTANT: Your R.02 or R.03 C44 is equipped with a switch labeled "USB" and "DC." Flipping this switch to "DC" will power the core on field power. This is not recommended on R.02 or R.03 C44s that do not have external cooling.
  * Field power is provided with a 24VDC external power supply connected to the external power connector. At this point, your outputs will be live at 24v.
  * IMPORTANT: Ensure your outputs are wired correctly for your C44. R.03 C44s have GND and 24v labeled on the circuitboards.

### Connecting Your C44 To Your PC
  * Your C44 is configured using a USB Serial connection to its USB-C port. To connect it to a PC, simply plug your C44 into a computer's USB-A or -C port using a compatible cable.

### Connecting Your C44 To Your Network
  *  Your C44 comes pre-configured with a local socket (IP address and receiving port), a remote socket (IP address and port that it will send UDP messages to) by default, and a MAC address. Your board is delivered with the local IP and port labeled.
  *  All network configuration settings can be changed over Serial using your PC.
  *  By default, C44s are configured with a /16 subnet mask. This means that in order to communicate with your network, each device's IP address's first *two* numbers should match every device on the LAN that it will be expected to communicate with.
  *  Your C44s will send a "/reset" OSC message to their configured remote socket at powerup. This allows you to easily test your network configuration by power cycling the device or pressing the "reset" button.
  *  Your C44s use *static IP addresses*. This makes their networks simple to set up and reliable. However, by default, most personal computers dynamically allocate IP addresses. This means that it is possible that a computer on your LAN *could* change its IP address to one that is different that the one you configured as your C44s remote socket. In this case, as long as your C44 is on the same subnet, your C44 will still receive UDP messages, but will not be able to send UDP messages to the show control computer. We recommend setting computers on your show control network to static IP addresses.

 # Communicating With Your C44 Using Open Sound Control (OSC)
   * All Show Technologies devices communicate using OSC messages. A full explanation of the protocol can be found at https://ccrma.stanford.edu/groups/osc/index.html. In brief, OSC messages consist of an address and one or more arguments. The address is one or more words connected with forwards slashes. These words **cannot** have spaces. The argument can be one of several data types, but C44s typically use floats or ints.
   * Messages for C44s follow a generally simple addressing scheme: /board name (assigned in ShowNET)/function/object/address. For example, to set the #1 output on a C44 I've named "Board 1", my address will start with /board1. To "set" a "digital output", we use /set/do. We want to set input 1, so our complete message will be **/board1/set/do/1**.
   * ShowNET automatically appends an argument to an address to form an OSC message with the correct type tag. However, some softwares (especially home brewed show controllers) may not. If you are sending OSC messages directly to the C44, ensure that the address, type tag, argument, and extra data bits are configured correctly.
