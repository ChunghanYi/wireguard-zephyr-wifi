# wireguard-zephyr-wifi
<span style="color:#d3d3d3">WireGuard for Zephyr RTOS in the Wi-Fi environment</span>
## Generate a wireguard static key(Curve25519 private/public keypair)
$ cd scripts <br>
$ __./genkey.sh__ <br>
-rw-rw-r-- 1 chyi chyi 45 11월 17 09:28 privatekey <br>
-rw-rw-r-- 1 chyi chyi 45 11월 17 09:28 publickey <br>
## How to build and run
  Caution: <br>
  You must first copy this folder under samples/net in the Nordic NRF Connect SDK. <br>
  You must edit the prj.conf and src/wireguard_vpn.h files for vpn settings.<br><br>
$ __west build -b nrf7002dk/nrf5340/cpuapp ../nrf/samples/net/wireguard__ <br>
$ __west flash__ <br><br>
The code above was tested in a zephyr 3.7.0 environment with nRF7002 DK board.<br>
## My blog posting for this project
  For more information, please read the blog posting below.<br>
  https://slowbootkernelhacks.blogspot.com/2024/12/wireguard-for-zephyr-rtos.html <br><br>
  Caution: <br>
  <span style="color:red">You must first proceed with the patch by referring to the subsys/net/ip/icmpv4.c.patch file.</span> <br><br>
## Limitations
  <span style="color:blue">It is still in the early stages of development.</span><br>
## Reference codes
  https://github.com/smartalock/wireguard-lwip <br>
  The code is copyrighted under BSD 3 clause Copyright (c) 2021 Daniel Hope (www.floorsense.nz)<br><br>
  nrf/samples/wifi/sta <br>
  zephyr/samples/net/sockets <br>
  zephyr/samples/net/virtual <br>
  <br>
  (***) WireGuard is a registered trademark of Jason A. Donenfeld.

