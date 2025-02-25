[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: ZHANG Yixuan
### Student Id: 21072226
### Email: yzhangsr@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The measurement tool used for the tests is the Phoronix Test Suite. For CPU performance, I executed the command phoronix-test-suite run pts/compress-7zip, which assesses the CPU's ability to perform compression tasks using the 7-Zip algorithm. This test is relevant because compression is a CPU-intensive operation, and the results are measured in MIPS (Million Instructions Per Second), providing a clear indication of processing capability.

    > For memory performance, I used the command phoronix-test-suite run pts/ramspeed, specifically testing the "Copy Integer" benchmark. This benchmark evaluates memory bandwidth by measuring how quickly data can be copied in memory. The results are reported in MB/s (Megabytes per second), reflecting the speed of memory operations.

    > For network performance, I utilized iPerf / iPerf3. The server was set up using iperf -s, while the client ran iperf -c <server_ip>. This setup measures TCP bandwidth and latency between instances. The results are displayed in Mbps (Megabits per second) for bandwidth and milliseconds (ms) for round-trip time (RTT), giving insights into network performance.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |    3940 MIPS             |      11154.55 MB/s              |
    | `t2.medium`  |  4080 MIPS               |   11298.89 MB/s                 |
    | `c5d.large` |   8042 MIPS	              |   14734.68 MB/s                 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    > The performance measurements indicate that as the instance type increases from t2.micro to c5d.large, both CPU and memory performance improve significantly. Specifically, the t2.micro instance has a CPU performance of 3940 MIPS and a memory performance of 11154.55 MB/s, while the t2.medium instance shows a slight increase to 4080 MIPS and 11298.89 MB/s. The c5d.large instance demonstrates a substantial enhancement, achieving 8042 MIPS in CPU performance and 14734.68 MB/s in memory performance. This trend clearly shows that the performance of EC2 instances does increase commensurate with the increase in the number of vCPUs and memory resources.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |     994           |   1.204       |
    | `m5.large` - `m5.large`   |    1930            |    0.878      |
    | `c5n.large` - `c5n.large` |  4960              |  0.152        |
    | `t3.medium` - `c5n.large` |  2320              | 0.726         |
    | `m5.large` - `c5n.large`  |  3230              |   0.474       |
    | `m5.large` - `t3.medium`  |   1020             |    0.489      |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    > The network performance measurements reveal notable differences in TCP bandwidth and round-trip time (RTT) between various instance types. The t3.medium instances show a TCP bandwidth of 994 Mbps with an RTT of 1.204 ms. In contrast, m5.large instances exhibit improved performance with a bandwidth of 1930 Mbps and an RTT of 0.878 ms. The c5n.large instances demonstrate the highest bandwidth of 4960 Mbps and the lowest RTT of 0.152 ms. Additionally, when comparing different types, the t3.medium to c5n.large connection shows a bandwidth of 2320 Mbps and an RTT of 0.726 ms, while the m5.large to c5n.large connection achieves a bandwidth of 3230 Mbps and an RTT of 0.474 ms. Overall, these results indicate that network performance generally improves with higher instance types.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |   23.1             |   72.3       |
    | N. Virginia - N. Virginia |    9300            |    0.098      |
    | Oregon - Oregon           |    4950            |     0.146   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    > The network performance measurements between instances deployed in different regions indicate significant variations in TCP bandwidth and round-trip time (RTT). The connection from N. Virginia to Oregon shows a TCP bandwidth of 23.1 Mbps with an RTT of 72.3 ms, highlighting the impact of geographical distance on network performance. In contrast, the connection within N. Virginia demonstrates a much higher bandwidth of 9300 Mbps and a minimal RTT of 0.098 ms, reflecting the benefits of local networking. The Oregon to Oregon connection also shows a robust bandwidth of 4950 Mbps and an RTT of 0.146 ms. Overall, these results illustrate that network performance is affected by both regional distance and local infrastructure capabilities.
