# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(wireguard-wifi)

target_include_directories(app PUBLIC ${ZEPHYR_BASE}/subsys/net/ip)

target_sources(                     app PRIVATE src/wg_main.c)
target_sources(                     app PRIVATE src/wifi.c)
target_sources_ifdef(CONFIG_NET_UDP app PRIVATE src/wg_comm.c)
target_sources(                     app PRIVATE src/wg_tun.c)
target_sources(                     app PRIVATE src/wireguard_vpn.c)
target_sources(                     app PRIVATE src/wireguardif.c)
target_sources(                     app PRIVATE src/wireguard.c)
target_sources(                     app PRIVATE src/wireguard-platform.c)
target_sources(                     app PRIVATE src/wg_timer.c)
target_sources(                     app PRIVATE src/crypto.c)
target_sources(                     app PRIVATE src/crypto/blake2s.c)
target_sources(                     app PRIVATE src/crypto/chacha20.c)
target_sources(                     app PRIVATE src/crypto/chacha20poly1305.c)
target_sources(                     app PRIVATE src/crypto/poly1305-donna.c)
target_sources(                     app PRIVATE src/crypto/x25519.c)
