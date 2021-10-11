# VPN for access to local network

- [VPN for access to local network](#vpn-for-access-to-local-network)
  - [Wireguard](#wireguard)
    - [Issues](#issues)
  - [tailscale](#tailscale)

## Wireguard

- https://www.wireguard.com/
- Vpn mentioned on MSDevShow
  - https://msdevshow.com/2021/01/linux-dev-environment-with-rick-rainey/
- Setting up wireguard with Home Assistant
  - https://www.youtube.com/watch?v=aGIg6N9HzSg

- This turned out to be a good tutorial
  - Server
    - https://tech.serhatteker.com/post/2021-01/how-to-set-up-wireguard-vpn-server-on-ubuntu/
  - Android client
    - https://tech.serhatteker.com/post/2021-01/how-to-set-up-wireguard-client-on-android/

### Issues

Had an issue: I was connected but no network traffic. 

Turned out to be because I was behind a NAT:
https://askubuntu.com/questions/1294533/wireguard-handshake-works-but-no-internet-access

Needed PreUp, PreDown instead of PostUp, PostDown:
``` config
[Interface]
Address = NewServerIp/32
SaveConfig = true
PreUp = iptables -t nat -A POSTROUTING -j MASQUERADE -o eno1
PreDown = iptables -t nat -D POSTROUTING -j MASQUERADE -o eno1
ListenPort = 51820
PrivateKey = Server_Private_Key

[Peer]
PublicKey = Android_Public_key
AllowedIPs = NewAndroidIp/32
Endpoint = MyPublicIp:50519
```

## tailscale

- https://tailscale.com/
- Install on each machine
- Can route traffic through one of your "nodes"
  - Coffee shop vpn etc
  - https://tailscale.com/kb/1103/exit-nodes/
- James told me about it
  

