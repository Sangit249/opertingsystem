# Phase 3: Application Selection for Performance Testing

## 1. Application Selection Matrix

In this phase, the goal is to select applications that represent different workload types for performance evaluation. Below is the **Application Selection Matrix** with justifications for choosing each application.

| **Workload Type** | **Application** | **Justification** |
| --- | --- | --- |
| **CPU-intensive** | **stress-ng** | Simulates high CPU loads to test performance under stress. |
| **RAM-intensive** | **stress-ng** | Allocates large memory amounts to test RAM usage under heavy load. |
| **I/O-intensive** | **fio** | Tests disk I/O performance with flexible benchmarking tools. |
| **Network-intensive** | **iperf3** | Measures network bandwidth and latency for network testing. |
| **Server Application** | **nginx** | A popular web server used to test server load by handling many simultaneous connections. |

## 2. Installation Documentation

The following installation steps outline how to install each selected application for testing. 
 ### For stress-ng (CPU and RAM-intensive)

- Update system packages
- sudo apt-get update
- Install stress-ng
- sudo apt-get install stress-ng

![install](3.1.png)

 - Run stress-ng for CPU stress testing

-  stress-ng --cpu 4 --timeout 60s

![picture](3.1.2.png)

-  Run stress-ng for RAM stress testing
- stress-ng --vm 2 --vm-bytes 2G --timeout 60s
  ![picture](3.1.4.png)

### For fio (I/O-intensive)

- Update system packages
- sudo apt-get update
- install fio
- sudo apt-get install fio
  ![fio](fio.png)

### For iperf3 (Network-intensive)

- Update system packages
- sudo apt-get update
- nstall iperf3
- sudo apt-get install iperf3
   
  ![iperf3](iperf.png)

### For nginx (Server Application)

- Update system packages
- sudo apt-get update
- Install nginx
- sudo apt-get install nginx
- Start nginx server
- sudo systemctl start nginx
  ![nginx](nginx.png)

## 3. Expected Resource Profiles

Below are the expected resource profiles for each application, based on anticipated resource usage during the tests:

| **Application** | **CPU Usage** | **Memory Usage** | **Disk I/O** | **Network Usage** |
| --- | --- | --- | --- | --- |
| **stress-ng (CPU)** | Very High (during stress) | Low to Medium (minimal memory required) | Low (no disk usage) | Low (no network usage) |
| **stress-ng (RAM)** | Low (CPU usage stays low) | Very High (allocates large memory) | Low (no disk usage) | Low (no network usage) |
| **fio** | Low to Medium | Medium (depends on test size) | Very High (for disk read/write) | Low (minimal network usage) |
| **iperf3** | Low (network testing) | Low (minimal memory) | Low (no disk usage) | Very High (network throughput) |
| **nginx** | Medium | Low (memory usage for serving static files) | Low (serving static content) | High (due to many connections) |

## 4. Monitoring Strategy

To measure performance, the following tools and commands will be used to monitor CPU, RAM, I/O, and network usage during the tests.

## CPU Usage Monitoring

**Tool**: top, htop

**Command**: top or htop
![htop](htop3.png)


## Memory Usage Monitoring

**Tool**: free -m, vmstat
![free](free-m.png)


## Disk I/O Monitoring

- **Tool**: iostat

**Command**:  iostat -xz 1 
![iostat](iostat3.png)


## Network Usage Monitoring

- **Tool**: iftop, netstat
   
**Command**:  iftop
![iftop](iftop3.png)




## 5. Conclusion

The chosen applications cover a wide range of workload scenarios on CPU, Memory, I/O, Network, and Server application categories. Running these applications on the targeted system will enable simulating real-world scenarios and testing how the targeted system performs under stressful conditions. All the tools are installed and checked using common system resource usage tools to measure CPU, Memory, Disk I/O, and Network resource usage.


