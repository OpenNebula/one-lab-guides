---
layout: default
title: Lab 4 - Host Management
parent: Module 4 - Hosts
---
# Module 4 - Lab 3: Host Management
{: .no_toc}

## Table of Contents
{: .no_toc}

<details markdown="block">
  <summary>
    Expand to access the In-page navigation
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>


## Objective(-s):
- Change the State of a Host with ID 0.

### Change the State of a Host with ID 0.

## 4.3.1

From the Node 1's Command Line execute the **disable** subcommand to Disable the Host with ID 0.

```console
onehost disable 0
```

List the hosts.

```console
onehost list
```

```console
ID NAME                 CLUSTER    TVM      ALLOCATED_CPU      ALLOCATED_MEM STAT
   3 lab-2108-node3     default      0       0 / 200 (0%)     0K / 3.8G (0%) on
   2 lab-2108-node2     default      0       0 / 200 (0%)     0K / 3.8G (0%) on
   1 63.187.6.115       default      0       0 / 200 (0%)     0K / 3.8G (0%) on
   0 18.153.12.108      default      0       0 / 200 (0%)     0K / 3.8G (0%) dsbl
```
## 4.3.2

Tail the log file and locate messages that are similar to the highlighted below.

Note that date/time in your output is going to be different.

```console
tail -n10 /var/log/one/monitor.log
```

```console
Mon Aug 10 08:10:36 2026 [Z0][HMM][I]: Successfully monitored host: 3
Mon Aug 10 08:11:01 2026 [Z0][HMM][I]: Successfully monitored host: 2
Mon Aug 10 08:11:02 2026 [Z0][HMM][I]: --Mark--
Mon Aug 10 08:12:30 2026 [Z0][HMM][I]: Successfully monitored host: 0
Mon Aug 10 08:12:30 2026 [Z0][HMM][I]: Successfully monitored host: 1
Mon Aug 10 08:12:37 2026 [Z0][HMM][I]: Successfully monitored host: 3
Mon Aug 10 08:13:02 2026 [Z0][HMM][I]: Successfully monitored host: 2
Mon Aug 10 08:13:45 2026 [Z0][HMM][D]: Updated Host 0, state DISABLED
Mon Aug 10 08:14:30 2026 [Z0][HMM][I]: Successfully monitored host: 0
Mon Aug 10 08:14:30 2026 [Z0][HMM][I]: Successfully monitored host: 1
```

{: .note}
> Now return back to [Module 4 - Lab 3 - Step 4.2.5](/one-lab-guides/ca-labs/module-4-3.html#425) and verify if a custom metric is gathered.

# Congratulations, you've completed the assignment!
{: .no_toc}