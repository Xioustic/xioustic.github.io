---
layout: post
title: Windows Hypervisor Benchmarks (Ubuntu)
comments: true
tags:
 - virtualization
 - windows
 - benchmarks
 - hyper-v
 - vmware workstation
 - windows subsystem for linux
 - virtualbox
---
I figured I'd benchmark a standard Ubuntu Server install using each hypervisor (Hyper-V, VMWare Workstation, VirtualBox, Windows Subsystem for Linux (WSL)) in order to approximate how much sacrifice you're making between each. It should be noted these are not "apples-to-apples" comparisons. Hyper-V is a Type 1 Hypervisor (runs bare metal), VMWare Workstation & VirtualBox are Type 2 Hypervisors (runs within the host OS, in this case Windows), and WSL actually runs on a abstraction layer within Windows.

## Reasoning
I've had to teach newbies in many of my workshops how to stick a hypervisor on their Windows machine in Linux-based workshops. This is when booting from a Live CD or Dual Booting is not an option. Many of them end up picking VirtualBox as the most convenient option. I've also been in a similar situation from time-to-time, especially in dev environments where we need to be done quick-and-dirty, where convenience and performance is something to be weighed.

Surprisingly I could not find anyone else doing these benchmarks on a modern install of Windows running Ubuntu. This is probably like, as prior mentioned, these are not apples-to-apples. Perhaps this is too unique a use-case to be useful for most. Regardless I will post the results for future reference in case it helps others.

## The Tests
Benchmarks run include Bench.sh, Unixbench.sh, and Unixbench.sh running in parallel mode. Each machine got the following configuration where possible:
- Windows Pro 10.7.17763 Host
- Ubuntu 18.04.2 Server with updates as the VM
- Intel i7-4770 @ 3.40 GHz with 4cores assigned to the VM
- 24GB of RAM with 8GB assigned to the VM
- Samsung SSD 840 EVO with 80GB assigned to the VM
- Everything else left at default settings (including disk caching, memory caching/ballooning, NAT or Bridge, etc)

In some cases we cannot stick to the spec directly. In WSL's instance, we cannot allocate specific amounts of CPU or RAM since it is integrated into the host operating system (not true virtualization).

Essentially the process for provisioning was as follows:
- Default install, then `sudo sh -c "apt update && apt upgrade && apt dist-upgrade && apt autoclean && apt autoremove"` with reboots as needed
- `git clone https://github.com/teddysun/across.git`
- `bash bench.sh`
- `sudo bash unixbench.sh | tee unixbench.log`

## The Results
### Table

| Type                  | Subtype                               | Hyper-V | Vbox   | Vmware  | WSL    | Hyper-V | Vbox    | Vmware  | WSL     |
|-----------------------|---------------------------------------|---------|--------|---------|--------|---------|---------|---------|---------|
| Bench.sh              | I/O Speed                             | 1911.5  | 429.7  | 1280.5  | 343    | 100.00% | 22.48%  | 66.99%  | 17.94%  |
| Bench.sh              | CacheFly                              | 7.35    | 8.13   | 7.25    | 6.58   | 90.41%  | 100.00% | 89.18%  | 80.93%  |
| Bench.sh              | Linode Tokyo                          | 6.76    | 6.9    | 6.98    | 6.7    | 96.85%  | 98.85%  | 100.00% | 95.99%  |
| Bench.sh              | Linode Singapore                      | 5.34    | 5.4    | 5.58    | 5.55   | 95.70%  | 96.77%  | 100.00% | 99.46%  |
| Bench.sh              | Linode London                         | 0.934   | 2.47   | 1.7     | 2.54   | 36.77%  | 97.24%  | 66.93%  | 100.00% |
| Bench.sh              | Linode Frankfurt                      | 5.66    | 6.17   | 6.49    | 5.93   | 87.21%  | 95.07%  | 100.00% | 91.37%  |
| Bench.sh              | Linode Fremont                        | 6.63    | 6.29   | 1.49    | 7.06   | 93.91%  | 89.09%  | 21.10%  | 100.00% |
| Bench.sh              | Softlayer Dallas                      | 2.32    | 5.22   | 4.15    | 5.16   | 44.44%  | 100.00% | 79.50%  | 98.85%  |
| Bench.sh              | Softlayer Seattle                     | 2.25    | 4.46   | 5.22    | 2.2    | 43.10%  | 85.44%  | 100.00% | 42.15%  |
| Bench.sh              | Softlayer Frankfurt                   | 2.03    | 3.86   | 3.8     | 0.641  | 52.59%  | 100.00% | 98.45%  | 16.61%  |
| Bench.sh              | Softlayer Singapore                   | 1.81    | 3.79   | 3.36    | 0.875  | 47.76%  | 100.00% | 88.65%  | 23.09%  |
| Bench.sh              | Softlayer HongKong                    | 1.37    | 3.34   | 3.3     | 1.08   | 41.02%  | 100.00% | 98.80%  | 32.34%  |
| Unixbench.sh          | Dhrystone 2                           | 3747    | 679.3  | 3802.2  | 3839.5 | 97.59%  | 17.69%  | 99.03%  | 100.00% |
| Unixbench.sh          | Double-Prevision Whetstone            | 648.8   | 644.7  | 646     | 644.7  | 100.00% | 99.37%  | 99.57%  | 99.37%  |
| Unixbench.sh          | Execl Throughput                      | 1124.7  | 579.8  | 1081    | 95.6   | 100.00% | 51.55%  | 96.11%  | 8.50%   |
| Unixbench.sh          | File Copy 1024 bufsize 2000 maxblocks | 2282.2  | 915.4  | 2282.4  | 382.6  | 99.99%  | 40.11%  | 100.00% | 16.76%  |
| Unixbench.sh          | File Copy 256 bufsize 500 maxblocks   | 1445.8  | 561.3  | 1491.1  | 235.6  | 96.96%  | 37.64%  | 100.00% | 15.80%  |
| Unixbench.sh          | File Copy 4096 bufsize 8000 maxblocks | 4470.8  | 2165   | 3788    | 782.9  | 100.00% | 48.43%  | 84.73%  | 17.51%  |
| Unixbench.sh          | Pipe Throughput                       | 1085.2  | 481    | 1078.5  | 285.3  | 100.00% | 44.32%  | 99.38%  | 26.29%  |
| Unixbench.sh          | Pipe-based Context Switching          | 40.1    | 150.9  | 243.6   | 165.8  | 16.46%  | 61.95%  | 100.00% | 68.06%  |
| Unixbench.sh          | Process Creation                      | 523.6   | 552.9  | 707.6   | 57.4   | 74.00%  | 78.14%  | 100.00% | 8.11%   |
| Unixbench.sh          | Shell Scripts (1 concurrent)          | 2667.6  | 1205.1 | 2790.3  | 244    | 95.60%  | 43.19%  | 100.00% | 8.74%   |
| Unixbench.sh          | Shell Scripts (8 concurrent)          | 5782.9  | 2743.8 | 5932.2  | 539.5  | 97.48%  | 46.25%  | 100.00% | 9.09%   |
| Unixbench.sh          | System Call Overhead                  | 647.4   | 488.5  | 651.8   | 252    | 99.32%  | 74.95%  | 100.00% | 38.66%  |
| Unixbench.sh          | System Benchmarks Index Score         | 1203    | 716.5  | 1422.5  | 327.2  | 84.57%  | 50.37%  | 100.00% | 23.00%  |
| Unixbench.sh Parallel | Dhrystone 2                           | 11799.5 | 2658.2 | 12225.3 | Err    | 96.52%  | 21.74%  | 100.00% | Err     |
| Unixbench.sh Parallel | Double-Prevision Whetstone            | 2491    | 2517.8 | 2477.1  | Err    | 98.94%  | 100.00% | 98.38%  | Err     |
| Unixbench.sh Parallel | Execl Throughput                      | 3905.3  | 2224.6 | 3481.8  | Err    | 100.00% | 56.96%  | 89.16%  | Err     |
| Unixbench.sh Parallel | File Copy 1024 bufsize 2000 maxblocks | 3486.9  | 1851.5 | 3596.6  | Err    | 96.95%  | 51.48%  | 100.00% | Err     |
| Unixbench.sh Parallel | File Copy 256 bufsize 500 maxblocks   | 2195.2  | 1110.7 | 2285    | Err    | 96.07%  | 48.61%  | 100.00% | Err     |
| Unixbench.sh Parallel | File Copy 4096 bufsize 8000 maxblocks | 7458.3  | 4523.7 | 6753    | Err    | 100.00% | 60.65%  | 90.54%  | Err     |
| Unixbench.sh Parallel | Pipe Throughput                       | 3687.9  | 1876.4 | 3712.5  | Err    | 99.34%  | 50.54%  | 100.00% | Err     |
| Unixbench.sh Parallel | Pipe-based Context Switching          | 2242.3  | 1071.2 | 2307.5  | Err    | 97.17%  | 46.42%  | 100.00% | Err     |
| Unixbench.sh Parallel | Process Creation                      | 2350.3  | 1638.2 | 1841.8  | Err    | 100.00% | 69.70%  | 78.36%  | Err     |
| Unixbench.sh Parallel | Shell Scripts (1 concurrent)          | 6586.4  | 3166.2 | 6554.8  | Err    | 100.00% | 48.07%  | 99.52%  | Err     |
| Unixbench.sh Parallel | Shell Scripts (8 concurrent)          | 6953.6  | 3291.7 | 6726.1  | Err    | 100.00% | 47.34%  | 96.73%  | Err     |
| Unixbench.sh Parallel | System Call Overhead                  | 2263.4  | 1904   | 2294.8  | Err    | 98.63%  | 82.97%  | 100.00% | Err     |
| Unixbench.sh Parallel | System Benchmarks Index Score         | 3920.9  | 2136.6 | 3809.5  | Err    | 100.00% | 54.49%  | 97.16%  | Err     |

### Graphs
To be done at a later date; note if higher or lower is better per graph.

### Notes
To be done at a later date. Need to split into Disk I/O, Network I/O, CPU-based, Memory-based, Filesystem-based tests. Need to average those out per hypervisor.

Summarizing up by test type averages:
| Benchmark               | Hyper-V | Vbox   | VMWare | WSL    |
|-----------              |---------|--------|--------|--------|
| Bench.sh                | 69.15%	 | **90.41%** |	84.13% |	66.56% |
| Unixbench.sh            | 89.38%	 | 53.38%	| **98.37%**	| 33.84% |
| Unixbench.sh (Parallel) | **98.74%**	 | 56.85%	| 96.14%	| NA     |
| Overall                 | 86.19%  |	66.26%	| **93.11%** | NA     |

## Conclusions
To be done at a later date. tl;dr VMWare Workstation is a great option if you can get it, Hyper-V is second best if you have it available as an OS feature, Virtualbox is a last resort. Windows Subsystem on Linux barely cuts it and in fact fails at running parallel processes (I think fork failed?).

I'd be very interested in running the same systems through other benchmarks like `iperf` and others. I tried gathering suggestions on Reddit but mostly received criticism for wanting to do these benchmarks in the first place, which was unhelpful. I realize many are useless the way they are (like `bench.sh` speed testing to a remote datacenter, since my connection is certainly not consistent).
