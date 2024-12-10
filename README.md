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

$ cd ~/ncs/ <br>
$ __nrfutil toolchain-manager launch --shell__ <br>
(v2.8.0) chyi@earth:~/ncs$ __source zephyr/zephyr-env.sh__ <br>
(v2.8.0) chyi@earth:~/ncs$ cd zephyr/ <br> <br>
(v2.8.0) chyi@earth:~/ncs/zephyr $ __vi ../nrf/samples/net/wireguard/prj.conf__ <br>
-> Fix some configurations <br>
CONFIG_WIFI_CREDENTIALS_STATIC_SSID="Myssid" <br>
CONFIG_WIFI_CREDENTIALS_STATIC_PASSWORD="Mypassword" <br>
CONFIG_NET_CONFIG_MY_IPV4_ADDR="192.168.1.99" <br>
CONFIG_NET_CONFIG_MY_IPV4_NETMASK="255.255.255.0" <br>
CONFIG_NET_CONFIG_MY_IPV4_GW="192.168.1.1" <br>
CONFIG_NET_CONFIG_VPN_IPV4_ADDR="10.1.1.50" <br>
CONFIG_NET_CONFIG_VPN_IPV4_NETMASK="255.255.255.0" <br> <br>
(v2.8.0) chyi@earth:~/ncs/zephyr $ __vi ../nrf/samples/net/wireguard/src/wireguard_vpn.h__ <br>
-> Fix some configurations <br>
#define WG_LOCAL_ADDRESS        IPADDR4_INIT_BYTES(10, 1, 1, 50)   // my vpn ip address <br>
#define WG_LOCAL_NETMASK        IPADDR4_INIT_BYTES(255, 255, 255, 0) <br>
#define WG_LOCAL_NETWORK        IPADDR4_INIT_BYTES(10, 1, 1, 0) <br>
#define WG_CLIENT_PRIVATE_KEY   "kL/HdaoIlqlDmrjtIkb/0PmF+3N7eApdkrjUQvsbK0c=" <br>
#define WG_CLIENT_PORT          51820 <br> <br>
#define WG_PEER_PUBLIC_KEY      "isbaRdaRiSo5/WtqEdmpH+NrFeT1+QoLvnhVI1oFfhE=" <br>
#define WG_PEER_PORT            51820 <br>
#define WG_ENDPOINT_ADDRESS     IPADDR4_INIT_BYTES(192, 168, 8, 139)  //peer endpoint(real) ip address <br> <br>
(v2.8.0) chyi@earth:~/ncs/zephyr $ __west build -b nrf7002dk/nrf5340/cpuapp ../nrf/samples/net/wireguard__ <br>
(v2.8.0) chyi@earth:~/ncs/zephyr $ __west flash__ <br><br>
The code above was tested with nRF7002 DK board.<br>
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

