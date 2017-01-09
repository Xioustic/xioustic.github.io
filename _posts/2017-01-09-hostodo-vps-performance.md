---
layout: post
title: Hostodo VPS Performance
comments: true
tags:
 - vps
 - hostodo
 - benchmark
---

Just quickly dumping a benchmark for my $14/yr Hostodo VPS, purchased on the deal from LowEndBox [here](https://lowendbox.com/blog/hostodo-kvm-and-openvz-offer-from-14year/).

Advertised Specs:
> [b]Host Node Specifications:[/b]
> – Dual Intel Xeon E5-2620 Hex Core
> – 96GB DDR3 RAM
> – 4x 2TB HDDs
> – Hardware RAID-10 via LSI 9271-4i w/CVM
> – 1Gbps uplink
> [b]VPS Specifications:[/b]
> - OpenVZ-1024
> - 1024MB RAM
> - 1024MB vSwap
> - 90GB Disk Space
> - 5TB Bandwidth
> - 4 vCPU Cores
> - 1 IPv4 Address
> - /112 IPv6 Subnet
> - Internal networking available to communicate between VPSs in the same location
> - 1Gbit Port
> - 3Gbit DDoS Protection / 1.5 Million PPS
> - OpenVZ/Virtualizor Control Panel

I used the hostbench.io benchmark script located [here](https://github.com/Lomand/hostbench.sh). Portions of their site and functionality are broken, but the benchmark seems to run fine regardless.

Will start posting benchmarks for all of my VPS deals.

```
Distro: "Debian GNU/Linux 7 (wheezy)"
DiskSize: 88 GB
RAMSize: 1024 MB
Checking CPU specs...
CPU(s): 6
model name      : Intel(R) Xeon(R) CPU E3-1240 v3 @ 3.40GHz
cpu MHz         : 3401.000
cache size      : 8192 KB
Virtualization: openvz

Benchmarking CPU...
CPUScore: 2771.0 points

Benchmarking RAM bandwith...
RAMBandwith: 891.63 MB/s

Benchmarking Write Speed  and IOPS of 4K blocks...
Write4K:8512.7 KB/s
WIOPS:2128 IOPS

Benchmarking Write Speed of 64K blocks...
Write64K: 12.5947 MB/s

Benchmarking Write Speed of 512K blocks...
Write512K: 55.502 MB/s

Benchmarking Read Speed and IOPS of 4K blocks...
Read4K:1426.1 KB/s
RIOPS:356 IOPS

Benchmarking Read Speed of 64K blocks...
Read64K: 4.30859 MB/s

Benchmarking Read Speed of 512K blocks...
Read512K: 20.4297 MB/s

Benchmarking maximum throughput between server and single user in different location...
(Keep in mind that this is not equivalent to maximum download speed of the server.)

[ 1/ 20] Testing download speed from Amsterdam, The Netherlands (Ping: 149.475 ms)
5.6MiB/s

[ 2/ 20] Testing download speed from Chennai, India (Ping: 372.294 ms)
2.8MiB/s

[ 3/ 20] Testing download speed from Dallas, USA (Ping: 28.924 ms)
12MiB/s

[ 4/ 20] Testing download speed from Frankfurt, Germany (Ping: 163.104 ms)
5.2MiB/s

[ 5/ 20] Testing download speed from Hong Kong, China (Ping: 154.874 ms)
5.2MiB/s

[ 6/ 20] Testing download speed from London, England (Ping: 145.459 ms)
5.5MiB/s

[ 7/ 20] Testing download speed from Melbourne, Australia (Ping: 203.476 ms)
5.4MiB/s

[ 8/ 20] Testing download speed from Milan, Italy (Ping: 175.657 ms)
5.4MiB/s

[ 9/ 20] Testing download speed from Montreal, Canada (Ping: 63.167 ms)
5.9MiB/s

[ 10/ 20] Testing download speed from Paris, France (Ping: 147.974 ms)
5.5MiB/s

[ 11/ 20] Testing download speed from Queretaro, Mexico (Ping: 48.253 ms)
7.2MiB/s

[ 12/ 20] Testing download speed from San Jose, USA (Ping: 7.825 ms)
16MiB/s

[ 13/ 20] Testing download speed from Sao Paulo, Brazil (Ping: 173.064 ms)
6.0MiB/s

[ 14/ 20] Testing download speed from Seattle, USA (Ping: 24.764 ms)
10MiB/s

[ 15/ 20] Testing download speed from Singapore, Singapore (Ping: 209.608 ms)
5.4MiB/s

[ 16/ 20] Testing download speed from Sydney, Australia (Ping: 175.939 ms)
3.8MiB/s

[ 17/ 20] Testing download speed from Seoul, Korea (Ping: 131.178 ms)
5.5MiB/s

[ 18/ 20] Testing download speed from Tokyo, Japan (Ping: 115.000 ms)
5.1MiB/s

[ 19/ 20] Testing download speed from Toronto, Canada (Ping: 54.728 ms)
8.2MiB/s

[ 20/ 20] Testing download speed from Washington, D.C., USA (Ping: 59.411 ms)
6.0MiB/s
```
