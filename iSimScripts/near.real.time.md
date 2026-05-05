# VCF Operations 9.1 - Real-Time Metrics Demo Script

---

## INTRO

**VMware Cloud Foundation 9.1 introduces Real-Time Metrics in VCF Operations.**

These are metrics collected near real-time at 20 second duration for all VCF components:
- vSphere
- ESX
- VMs
- vSAN
- NSX

The workbench also introduces Integrated Metrics, Logs and Network Flows to analyze and compare logs ingested at different time intervals with network traffic flow and topology visibility.

**We are currently logged in to VCF Operations Product home page.**

---

## SECTION 1: ACCESS WORKBENCH

1. Click on **Workbench**

**We will now troubleshoot the vSphere cluster backing our VCF workload domain.**

---

## SECTION 2: SEARCH & SELECT CLUSTER

1. Click on **Search** to find clusters
2. Click to **Drill down** and select workload cluster
3. Click to select workload domain cluster **"cluster-wld-01a"**
4. Click to set **Time range to 24-hours**

**We are taken to the Evidence screen where we see:**
- Summary of recent events
- Recent configuration changes
- List of metrics exhibiting unusual behavior

*This information helps identify potential issues affecting the cluster.*

---

## SECTION 3: REAL-TIME ANALYSIS TAB

1. Click on **Real-Time Analysis Tab**

**Here we see a summary of CPU and memory usage for the cluster.**

*Note the recent spike in CPU utilization.*

1. Click on the **Spiked metric**
2. Click to **Zoom in**
3. Click on **Data point** (1st)
4. Click on **Data point** (2nd)
5. Click on **Data point** (3rd)

**Clicking on all 3 data points, we can see the graph is being updated every 20 seconds.**

---

## SECTION 4: INVESTIGATE CPU SPIKE - VMs TAB

**To investigate the sudden CPU spike, we navigate to the VMs tab.**

1. Click on **Select View tab** (Overview)
2. Click to select **VMs tab**

**Here we can query the top objects associated with a given metric.**

*We see the top 10 VMs consuming the most CPU and memory.*

1. Click on the **Spiked metric**
2. Click to **Zoom in**
3. Click on the **data point** (1st)
4. Click on the **data point** (2nd)

**After zooming in, we can identify that this spike is being caused by:**

**AI RAG WORKLOADS**

---

## SECTION 5: FIND ESX HOST - HOSTS TAB

1. Click on **Select View tab** (VMs)
2. Click to select **Hosts**

**Here we search for the ESX host associated with the CPU spike observed in the vSphere cluster.**

1. Click on the **Spiked Metric**
2. Click to **Zoom in**
3. Click on the **data point**

**After Zooming in, we see that the associated ESX host is: ESX-07**

---

## SECTION 6: CUSTOM QUERIES

**In addition to viewing top objects for a metric, real-time metrics also supports custom queries using Prometheus query language (PROMQL).**

1. Click on **Custom Query Tab**

**We can build our own custom queries to pull metrics required for troubleshooting an issue.**

*Note: There is a helpful "Need Help" link below the add query field.*

1. Click on the **Need Help link**

**The Query help builder helps us build custom queries.**

1. Click on **Sample Queries**

**We will use a sample query to list the CPU capacity usage for each host in the workload cluster.**

1. Click to **copy query: cpu.capacity.usage.HOST**
2. Click on **Add Query field** to paste query
3. Click **RUN**

**The results of this query show the ESX host associated with the CPU spike observed in the vSphere cluster.**

---

## SECTION 7: LOGS ANALYSIS

1. Click on **Logs Tab**

**The workbench allows ability to analyze logs for the associated VCF components.**

1. Click on **Add Filter**
2. Click on the **text tab** to enter **ESX-07a**
3. Click to **Search**

**Here we view and analyze logs for ESX-07a for further troubleshooting the issue.**

---

## SECTION 8: COMPARE LOGS

**We can also Compare logs that are based on the same query criteria but ingested at different times.**

**Here we search for ESX logs at different time intervals. We can select a query tab on the left side and on right side to compare the log results.**

1. Click on **Compare Logs**

**Query 1:**
2. Click to select **Time for Query 1**
3. Click to select **Data for Query 1**
4. Click on **Add Filter**
5. Click on **text** to enter **ESX-07a**
6. Click on **Add Query**

**Query 2:**
7. Click to select **Time for Query 2**
8. Click to select **Date for Query 2**
9. Click to **Add Filter**
10. Click on **text** to enter **ESX-07a**

**Execute:**
11. Click on **COMPARE**

**The log comparison is displayed as a stacked line chart with results side by side in query tabs under the chart.**

1. Click to **drill down**
2. Click to **expand Query 1 Log**
3. Click to **expand Query 2 Log**

---

## SECTION 9: FLOWS - NETWORK ANALYSIS

**The workbench also introduces Flows to analyze network flows by:**
- Traffic
- Volume
- Session count
- Flow count

1. Click on **Flows tab**

**Here we see all top talking entities associated within the workload domain cluster.**

1. Click on **Top Talkers page**
2. Click to select a **VM-VM Flow Path**
3. Click on **"+"** to expand the page detail

**We further drill down to see network flow, VM to VM path and associated vSphere properties.**

---

## SECTION 10: NETWORK PATH TOPOLOGY

1. Click on **View Network Path**

**We see an End-to-End topology path view.**

1. Click to view **Source VM**
2. Click to view **Distributed PortGroup**
3. Click to view **Destination VM**
4. Click to view **Path details**

**We see the Source VM, Distributed port groups through which the traffic passes to reach the Destination VM with network path details.**

---

## SECTION 11: NETWORK PERFORMANCE

1. Click on **Back to Flows Results**
2. Click to **close the page**
3. Click on **Network Performance**
4. Click to view **Flows by TCP RTT**

**The Network Performance widget also helps find and visualize Abnormal flows for various ranges of TCP Round Trip Time (RTT) values based on selected criteria.**

---

## SECTION 12: RESOLVE ISSUE - VM TERMINAL

1. Click **anywhere on screen** to go to **VM Terminal**
2. Click to **cancel the process**

**In this example, the CPU spike was caused due to open-source tools used for AI RAG workloads and LLM inference.**

1. Click to **exit the VM terminal**

---

## SECTION 13: VERIFY RESOLUTION

1. Click on **Real-Time Analysis**
2. Click on the **CPU metric**

**We can see here that after stopping the process, the CPU spike is getting back to normal.**

---

## SECTION 14: ADD NOTES TO SESSION

**As this is a shared lab, it would be helpful to annotate the cause of the spike so that anyone else who may be monitoring the cluster is aware of the root cause.**

1. Click on the **3 dots**
2. Click on **Add to Notes**

**I've added the supported metric chart to Notes.**

1. Click on **Notes tab**
2. Click on **ADD**
3. Click on **text field** to enter **root cause analysis**

**I've added the findings and steps taken to resolve the issue in Notes.**

1. Click **OK**
2. Click to **close the session**

**The troubleshooting session is automatically saved so anyone who opens the session will see the note.**

---

## SECTION 15: NSX EDGE DASHBOARDS

**Real-time metrics also supports collecting 20sec granular data at the NSX Edge / network level using the Prometheus query language widget which allows admins to build troubleshooting Dashboards for support teams.**

1. Click to **expand the Left Navigation**
2. Click on **Dashboards**
3. Click on **Edge-Real Time Metrics Dashboard**
4. Click on **Edge node: vcf-edge-mgmt-01b**

**Here is an example of the Network monitoring dashboard showing NSX Edge metrics:**
- Load Balancer sessions
- Data-path CPU
- Service CPUs being consumed
- All at 20 second granularity

---

## CONCLUSION

**We have demonstrated that Real-Time Metric service is part of the new VCF services platform:**

✓ Once enabled, we access real-time metrics using the VCF operations troubleshooting workbench

✓ In the workbench, we saw metrics being collected at 20-second intervals

✓ We quickly identified the top objects associated with given metrics

✓ We created a custom query using PROMQL

✓ The workbench allowed us to compare system logs and network traffic visibility with end-to-end topology views

✓ We added a note to our troubleshooting session to facilitate collaboration

---
