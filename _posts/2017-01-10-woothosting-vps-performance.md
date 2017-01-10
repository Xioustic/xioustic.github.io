---
layout: post
title: WootHosting New Year Special BOGO 2048MB VPS Review
comments: true
tags:
 - vps
 - woothosting
 - benchmark
---

A review for the "WootHosting – BOGO 2GB OpenVZ VPS for $36/yr" deal posted on LowEndBox.

## The Deal
This deal was purchased per the deal on LowEndBox [here](https://lowendbox.com/blog/woothosting-bogo-2gb-openvz-vps-for-36yr-and-more/). The pricing is $36 USD annually, but you get two identical VPS at the advertised specifications for the price.

## Advertised Specs:
> **Host Node Specifications:**
> - Intel Xeon E3-1230 V2 3.30 GHz
> - 32GB DDR3 RAM
> - 4x 2TB HDDs
> - Hardware RAID10
> - Full Duplex 1Gbps uplink
> 
> **VPS Specifications:**
> - 2048MB RAM
> - 2048MB Swap
> - 2x vCPU
> - 30GB HDD space
> - 2TB transfer
> - 1Gbps uplink
> - 1x IPv4
> - 30x IPv6
> - OpenVZ/SolusVM
> - No Coupon Needed
> - $36/year

## Benchmarks
I used the hostbench.io benchmark script located [here](https://github.com/Lomand/hostbench.sh). Portions of their site and functionality are broken, but the benchmark seems to run fine regardless. It builds sysbench-1.0 (for CPUscore), fio (for IO testing), and aria2 (for bandwidth tests) from scratch for its benchmarks.

### Benchmark 1 (VPS #1)
```
Distro: "Ubuntu 16.04.1 LTS"
DiskSize: 30 GB
RAMSize: 2048 MB
Checking CPU specs...
CPU(s): 2
model name      : Intel(R) Xeon(R) CPU E3-1230 V2 @ 3.30GHz
cpu MHz         : 3299.935
cache size      : 8192 KB
Virtualization: openvz

Benchmarking CPU...
CPUScore: 4165.0 points

Benchmarking RAM bandwith...
RAMBandwith: 1660.33 MB/s

Benchmarking Write Speed  and IOPS of 4K blocks...
Write4K:4068.8 KB/s
WIOPS:1017 IOPS

Benchmarking Write Speed of 64K blocks...
Write64K: 77.9619 MB/s

Benchmarking Write Speed of 512K blocks...
Write512K: 161.707 MB/s

Benchmarking Read Speed and IOPS of 4K blocks...
Read4K:562953B/s KB/s
RIOPS:137 IOPS

Benchmarking Read Speed of 64K blocks...
Read64K: 7.5791 MB/s

Benchmarking Read Speed of 512K blocks...
Read512K: 33.6338 MB/s

Benchmarking maximum throughput between server and single user in different location...
(Keep in mind that this is not equivalent to maximum download speed of the server.)

[ 1/ 20] Testing download speed from Amsterdam, The Netherlands (Ping: 144.515 ms)
17MiB/s

[ 2/ 20] Testing download speed from Chennai, India (Ping: 224.798 ms)
98KiB/s

[ 3/ 20] Testing download speed from Dallas, USA (Ping: 31.046 ms)
4.5MiB/s

[ 4/ 20] Testing download speed from Frankfurt, Germany (Ping: 153.032 ms)
2.3MiB/s

[ 5/ 20] Testing download speed from Hong Kong, China (Ping: 177.122 ms)
1.9MiB/s

[ 6/ 20] Testing download speed from London, England (Ping: 138.144 ms)
1.6MiB/s

[ 7/ 20] Testing download speed from Melbourne, Australia (Ping: 484.615 ms)
1.4MiB/s

[ 8/ 20] Testing download speed from Milan, Italy (Ping: 156.671 ms)

1.7MiB/s

[ 9/ 20] Testing download speed from Montreal, Canada (Ping: 74.511 ms)
1.9MiB/s

[ 10/ 20] Testing download speed from Paris, France (Ping: 154.995 ms)
2.0MiB/s

[ 11/ 20] Testing download speed from Queretaro, Mexico (Ping: 52.898 ms)
3.8MiB/s

[ 12/ 20] Testing download speed from San Jose, USA (Ping: 17.049 ms)
7.3MiB/s

[ 13/ 20] Testing download speed from Sao Paulo, Brazil (Ping: 176.847 ms)
2.0MiB/s

[ 14/ 20] Testing download speed from Seattle, USA (Ping: 33.984 ms)
5.7MiB/s

[ 15/ 20] Testing download speed from Singapore, Singapore (Ping: 187.762 ms)
1.7MiB/s

[ 16/ 20] Testing download speed from Sydney, Australia (Ping: 480.201 ms)
1.3MiB/s

[ 17/ 20] Testing download speed from Seoul, Korea (Ping: 379.171 ms)
1.4MiB/s

[ 18/ 20] Testing download speed from Tokyo, Japan (Ping: 344.920 ms)
1.4MiB/s

[ 19/ 20] Testing download speed from Toronto, Canada (Ping: 60.677 ms)
3.4MiB/s

[ 20/ 20] Testing download speed from Washington, D.C., USA (Ping: 154.974 ms)
1.8MiB/s
```

### Benchmark 2 (VPS #2)
```
Distro: "Ubuntu 16.04.1 LTS"
DiskSize: 30 GB
RAMSize: 2048 MB
Checking CPU specs...
CPU(s): 2
model name      : Intel(R) Xeon(R) CPU E3-1230 V2 @ 3.30GHz
cpu MHz         : 3299.935
cache size      : 8192 KB
Virtualization: openvz

Benchmarking CPU...
CPUScore: 4328.2 points

Benchmarking RAM bandwith...
RAMBandwith: 1856.57 MB/s

Benchmarking Write Speed  and IOPS of 4K blocks...
Write4K:78069 KB/s
WIOPS:19517 IOPS

Benchmarking Write Speed of 64K blocks...
Write64K: 76.7412 MB/s

Benchmarking Write Speed of 512K blocks...
Write512K: 249.169 MB/s

Benchmarking Read Speed and IOPS of 4K blocks...
Read4K:539987B/s KB/s
RIOPS:131 IOPS

Benchmarking Read Speed of 64K blocks...
Read64K: 7.74023 MB/s

Benchmarking Read Speed of 512K blocks...
Read512K: 39.5264 MB/s

Benchmarking maximum throughput between server and single user in different location...
(Keep in mind that this is not equivalent to maximum download speed of the server.)

[ 1/ 20] Testing download speed from Amsterdam, The Netherlands (Ping: 182.864 ms)
376KiB/s

[ 2/ 20] Testing download speed from Chennai, India (Ping: 225.385 ms)
122KiB/s

[ 3/ 20] Testing download speed from Dallas, USA (Ping: 31.047 ms)
12MiB/s

[ 4/ 20] Testing download speed from Frankfurt, Germany (Ping: 156.531 ms)
14MiB/s

[ 5/ 20] Testing download speed from Hong Kong, China (Ping: 171.326 ms)
15MiB/s

[ 6/ 20] Testing download speed from London, England (Ping: 138.544 ms)
16MiB/s

[ 7/ 20] Testing download speed from Melbourne, Australia (Ping: 484.381 ms)
11MiB/s

[ 8/ 20] Testing download speed from Milan, Italy (Ping: 163.571 ms)
11MiB/s

[ 9/ 20] Testing download speed from Montreal, Canada (Ping: 74.714 ms)
22MiB/s

[ 10/ 20] Testing download speed from Paris, France (Ping: 141.693 ms)
9.3MiB/s

[ 11/ 20] Testing download speed from Queretaro, Mexico (Ping: 53.306 ms)
18MiB/s

[ 12/ 20] Testing download speed from San Jose, USA (Ping: 16.980 ms)
28MiB/s

[ 13/ 20] Testing download speed from Sao Paulo, Brazil (Ping: 179.068 ms)
7.9MiB/s

[ 14/ 20] Testing download speed from Seattle, USA (Ping: 34.043 ms)
23MiB/s

[ 15/ 20] Testing download speed from Singapore, Singapore (Ping: 181.727 ms)
12MiB/s

[ 16/ 20] Testing download speed from Sydney, Australia (Ping: 470.650 ms)
6.5MiB/s

[ 17/ 20] Testing download speed from Seoul, Korea (Ping: 420.372 ms)
5.7MiB/s

[ 18/ 20] Testing download speed from Tokyo, Japan (Ping: 341.126 ms)
8.4MiB/s

[ 19/ 20] Testing download speed from Toronto, Canada (Ping: 60.127 ms)
21MiB/s

[ 20/ 20] Testing download speed from Washington, D.C., USA (Ping: 167.651 ms)
6.4MiB/s
```

### Results
Oddly, the two machines benchmarked at very different download speeds. I contacted support to verify both were on a 1Gbps line, so still awaiting their reply on that. Will repost benchmarks if any change is noticed.

## Other Concerns
This host sends usernames and passwords through plaintext via e-mail, but that seems par for the course for most providers. Still terrible practice.

More worrying is that the panel to reinstall your OS (https://manage.woothosting.com/) has no valid cert. It is a self-signed cert by "PHX1-2008", which I am assume is PhoenixNAP's internal certificate. It has no connection to any certificate chain though, so you cannot verify its validity to prevent a man-in-the-middle attack which could be used to trivially hijack your server and/or account. In addition, even if the cert had a valid certificate chain, its signature uses a SHA1 hash which is trivial to brute force and imitate for many black hats today. No good.

You can avoid the above issues by *never* accessing the manage.woothosting.com panel, asking customer support to perform the reinstall if needed, and change all passwords immediately after your account is opened.
