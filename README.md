# free-fokat

1

Identify your hardware and available resources
Exact FPGA board, operating system, development tools and existing source code.


----> how we connected the zuc 102 fpga board to laptop in ubuntu 

1. USB devices
lsusb

2. Serial ports
ls /dev/ttyUSB* /dev/ttyACM* 2>/dev/null

3. Latest connection logs
sudo dmesg | tail -40

sudo apt update
sudo apt install picocom
sudo picocom -b 115200 /dev/ttyUSB0

Step 2 — Download OAI
Software: Git
Purpose: Download the OAI 5G NR source code.
If you have not cloned OAI onto the ZCU102 itself, run:
cd ~
git clone --depth 1 https://github.com/OPENAIRINTERFACE/openairinterface5g.git





2

Obtain an L1 PHY implementation
Find a suitable implementation with runnable PHY tests.


instructions list NR PHY test programs such as nr_dlschsim, nr_dlsim, nr_ulsim, nr_ulschsim, nr_pbchsim, and ldpctest

----> how we connect the internet to fpga board 
connect the ethernet 
Run these commands one by one in Ubuntu through `picocom`.

1\. Check Ethernet interface

```
ip -br link
```

2\. Enable Ethernet (replace `eth0` if your interface has another name)

```
sudo ip link set eth0 up
```

3\. Check IP address

```
ip -br addr
```

4\. Request an IP address

```
sudo udhcpc -i eth0
```

5\. Check the gateway

```
ip route
```

6\. Test internet

```
ping -c 4 8.8.8.8
```

7\. Test DNS

```
ping -c 4 google.com
```

If you still get `Network is unreachable`, send me the output of steps 1, 3 and 5.



now install the required software to implement the phy 
--> Install the basic development tools

sudo apt update
sudo apt install -y git build-essential cmake ninja-build pkg-config

verify the installation 
git --version
gcc --version
cmake --version
ninja --version




List the NR PHY simulator source directory
ls openair1/SIMULATION/NR_PHY

shows all the test files 


Check the OAI build script
Run:
ls -l cmake_targets/build_oai




3

Build the software reference
Run the PHY test environment on your computer.



4

Run basic PHY tests
Verify modulation, demodulation and FFT/IFFT using known vectors.



5

Test complete PHY processing
Add channel coding, resource mapping and the relevant TX/RX functions.



6

Measure correctness and performance
Record errors, throughput, latency and numerical accuracy.

7

Move the relevant functions to FPGA
Use an existing hardware implementation or implement the required RTL accelerators.



8

Validate on FPGA
Compare FPGA outputs against the trusted software reference.


https://chatgpt.com/share/6acf0aa6-7370-83ee-bd31-76252127bd5e?ogimg=plain

