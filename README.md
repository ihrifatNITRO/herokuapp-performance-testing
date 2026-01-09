# Herokuapp Performance Testing

## Project Summary
This project involves comprehensive performance testing of the **Booking API** on Herokuapp to evaluate system stability under normal load and identify breaking points under extreme stress. The testing was conducted using Apache JMeter, focusing on Throughput (Requests Per Second) and Error Rates.

### 1. Load Testing
The objective was to verify if the system could handle the expected traffic volume of **120,000 users over a 12-hour period**. This was broken down into shorter test phases to validate the target throughput of **2.778 requests/second**.

* **Step #1 (1 min):** Simulated **167 users**. The system maintained **0.00% Error Rate** and achieved the expected throughput of **2.778 TPS**.
* **Step #2 (5 min):** Scaled to **833 users**. The system remained stable with **0.00% Error Rate** and consistent throughput.
* **Step #3 (10 min):** Scaled to **1667 users**. The system showed negligible errors (**0.06%**), proceeded to find the bottleneck **0.04%** error at 14 min.

### 2. Stress Testing (Bottleneck Analysis)
The objective was to push the server beyond its limits to find the **"Lower Bottleneck"**—the exact point where the system fails to meet quality standards.

* **Strategy (Timeouts):** We implemented a strict **2,000ms (2s) response timeout**. While the server could technically handle the load, it often responded with high latency (8s+). By enforcing a standard 2-second acceptance threshold, we converted these "slow successes" into "errors" to realistically reflect user dissatisfaction.
* **Execution:** The load was incrementally increased from **1667 users** up to a peak load of **11,334 samples**.
* **Findings:** The system remained resilient with error rates fluctuating between **0.04% - 0.19%** during the initial ramp-up.
* **Bottleneck Identified:** At the peak load of **11,334 samples**, the system's error rate spiked to **0.64%**, crossing the acceptable threshold of 0.5%. This point is marked as the system's Lower Bottleneck.

## Technology Used
* **Apache JMeter:** For creating test scripts.
* **Java (JDK):** Required runtime environment for JMeter.
* **CMD/Terminal:** For executing "Non-GUI" mode tests.
* **Microsoft Excel:** For calculating throughput targets.

## Pre-requisites
Before running the scripts, ensure you have the following installed and configured:

1. **Java Development Kit (JDK):**
2. **Apache JMeter:**
3. **System Configuration:**
   * Set the **HEAP memory** to at least 4GB before running heavy tests to prevent `OutOfMemoryError`:
     ```cmd
     set HEAP=-Xms1g -Xmx4g -XX:MaxMetaspaceSize=256m
     ```
4. **Knowledge of API**

## JMX Reports
1. **Load Testing**
   <img width="1546" height="706" alt="image" src="https://github.com/user-attachments/assets/471d33fe-6061-4f69-a644-ad0408ae74f2" />
   <img width="1487" height="372" alt="image" src="https://github.com/user-attachments/assets/f6ebb6ab-a939-4843-8484-e483fa9d9fe9" />
   <img width="1512" height="558" alt="image" src="https://github.com/user-attachments/assets/0198d28a-ef41-4ca7-af05-86edcfb124f0" />

2. **Stress Testing**
   <img width="1542" height="712" alt="image" src="https://github.com/user-attachments/assets/b685a577-f2c6-45ac-852d-9b1cb0abdeef" />
   <img width="1550" height="426" alt="image" src="https://github.com/user-attachments/assets/11766d10-a6b3-4578-a2c5-c8b63f12ab9c" />
   <img width="1509" height="874" alt="image" src="https://github.com/user-attachments/assets/705575c4-baf8-4893-b74a-70e41bd4c28d" />





