This is homework for VPN lesson on Otus platform.

Here are the files:
ansible.cfg 
README.md
Vagrantfile
ansible/hosts
ansible/main.yml
ansible/openvpn.service
ansible/provision_ras.yml
ansible/provision_tun.yml
ansible/server_client.conf.j2
ansible/server_rasclient.conf
ansible/eserver_ras.conf
ansible/server_server.conf.j2

To configure VPN in TUN mode:
ansible-playbook -i ansible/hosts ansible/provision_tun.yml

To configure VPN in RAS mode:
ansible-playbook -i ansible/hosts ansible/provision_ras.yml

TUN/TAP results:

TAP:
```
root@client:/home/vagrant# iperf3 -c 10.10.10.1 -t 40 -i 5
Connecting to host 10.10.10.1, port 5201
[  5] local 10.10.10.2 port 39482 connected to 10.10.10.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-5.00   sec  31.0 MBytes  52.1 Mbits/sec   12    228 KBytes
[  5]   5.00-10.00  sec  32.3 MBytes  54.3 Mbits/sec   34    146 KBytes
[  5]  10.00-15.00  sec  38.1 MBytes  63.9 Mbits/sec   35    155 KBytes
[  5]  15.00-20.00  sec  40.9 MBytes  68.7 Mbits/sec   19    201 KBytes
[  5]  20.00-25.00  sec  39.0 MBytes  65.5 Mbits/sec    7    249 KBytes
[  5]  25.00-30.00  sec  38.4 MBytes  64.4 Mbits/sec   37    199 KBytes
[  5]  30.00-35.00  sec  36.2 MBytes  60.7 Mbits/sec   15    197 KBytes
[  5]  35.00-40.00  sec  38.3 MBytes  64.3 Mbits/sec   27    128 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-40.00  sec   294 MBytes  61.7 Mbits/sec  186             sender
[  5]   0.00-40.06  sec   294 MBytes  61.5 Mbits/sec                  receiver

iperf Done.
root@client:/home/vagrant#
```
TUN:
```
root@client:/home/vagrant# iperf3 -c 10.10.10.1 -t 40 -i 5tl restart openvpn@server
Connecting to host 10.10.10.1, port 5201
[  5] local 10.10.10.2 port 35890 connected to 10.10.10.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-5.00   sec  43.0 MBytes  72.1 Mbits/sec   87    114 KBytes
[  5]   5.00-10.00  sec  43.0 MBytes  72.1 Mbits/sec   24    210 KBytes
[  5]  10.00-15.00  sec  44.0 MBytes  73.9 Mbits/sec   98    184 KBytes
[  5]  15.00-20.00  sec  45.6 MBytes  76.4 Mbits/sec   12    174 KBytes
[  5]  20.00-25.00  sec  39.2 MBytes  65.8 Mbits/sec    6   51.5 KBytes
[  5]  25.00-30.00  sec  42.0 MBytes  70.4 Mbits/sec    5    226 KBytes
[  5]  30.00-35.00  sec  39.1 MBytes  65.7 Mbits/sec   44    186 KBytes
[  5]  35.00-40.00  sec  39.1 MBytes  65.6 Mbits/sec   45    132 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-40.00  sec   335 MBytes  70.3 Mbits/sec  321             sender
[  5]   0.00-40.04  sec   334 MBytes  70.0 Mbits/sec                  receiver

iperf Done.
root@client:/home/vagrant#
```
