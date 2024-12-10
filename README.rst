.. zephyr:code-sample:: wireguard
   :name: wireguard (advanced)
   :relevant-api: bsd_sockets virtual interface

   Implement a wireguard application.

Overview
********

Requirements
************

Building and Running
********************
$ cd ~/ncs/
$ nrfutil toolchain-manager launch --shell
$ source zephyr/zephyr-env.sh
(v2.8.0) chyi@earth:~/ncs$ cd zephyr/

(v2.8.0) chyi@earth:~/ncs/zephyr $ vi ../nrf/samples/net/wireguard/prj.conf
-> Fix some configurations
CONFIG_WIFI_CREDENTIALS_STATIC_SSID="Myssid"
CONFIG_WIFI_CREDENTIALS_STATIC_PASSWORD="Mypassword"
CONFIG_NET_CONFIG_MY_IPV4_ADDR="192.168.1.99"
CONFIG_NET_CONFIG_MY_IPV4_NETMASK="255.255.255.0"
CONFIG_NET_CONFIG_MY_IPV4_GW="192.168.1.1"
CONFIG_NET_CONFIG_VPN_IPV4_ADDR="10.1.1.50"
CONFIG_NET_CONFIG_VPN_IPV4_NETMASK="255.255.255.0"

(v2.8.0) chyi@earth:~/ncs/zephyr $ vi ../nrf/samples/net/wireguard/src/wireguard_vpn.h
#define WG_LOCAL_ADDRESS        IPADDR4_INIT_BYTES(10, 1, 1, 50)   // my vpn ip address
#define WG_LOCAL_NETMASK        IPADDR4_INIT_BYTES(255, 255, 255, 0)
#define WG_LOCAL_NETWORK        IPADDR4_INIT_BYTES(10, 1, 1, 0)

#define WG_CLIENT_PRIVATE_KEY   "kL/HdaoIlqlDmrjtIkb/0PmF+3N7eApdkrjUQvsbK0c="
#define WG_CLIENT_PORT          51820

#define WG_PEER_PUBLIC_KEY      "isbaRdaRiSo5/WtqEdmpH+NrFeT1+QoLvnhVI1oFfhE="
#define WG_PEER_PORT            51820
#define WG_ENDPOINT_ADDRESS     IPADDR4_INIT_BYTES(192, 168, 8, 139)  //peer endpoint(real) ip address

(v2.8.0) chyi@earth:~/ncs/zephyr $ west build -b nrf7002dk/nrf5340/cpuapp ../nrf/samples/net/wireguard --pristine
(v2.8.0) chyi@earth:~/ncs/zephyr $ west flash
