## Blue Team: Summary of Operations

### Table of Contents

* Network Topology
* Description of Targets
* Monitoring the Targets
* Patterns of Traffic & Behavior
* Suggestions for Going Further

### Network Topology

The following machines were identified on the network:

* Azure Hyper-V
  - **Operating System:** Windows
  - **Purpose:** the main host machine
  - **IP Address:** 192.168.1.1
 
* Kali
  - **Operating System:** Linux
  - **Purpose:** The main attacking machine
  - **IP Address:** 192.168.1.90
* Elk
  - **Operating System:** Linux
  - **Purpose:** Keeping logs
  - **IP Address:** 192.168.1.100
* Target 1
  - **Operating System:** Linux
  - **Purpose:** The target machine to be attacked
  - **IP Address:** 192.168.1.110
  
### Description of Targets

The target of this attack was: Target 1 (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

**Excessive HTTP Errors**

Excessive HTTP Errors is implemented as follows:
* **Metric:** WHEN count() GROUPED OVER top 5 'http.response.status_code' 
* **Threshold:** above 400 for the last 5 minutes
* **Vulnerability Mitigated:** failed to get into folders or files
* **Reliability:** High reliability

**HTTP Request Size Monitor**

HTTP Request Size Monitor is implemented as follows:
* **Metric:** WHEN sum() of http.request.bytes OVER all documents
* **Threshold:** above 3500 for the last minute
* **Vulnerability Mitigated:** port scans
* **Reliability:** medium reliability

**CPU Usage Monitor**

CPU Usage Monitor is implemented as follows:
* **Metric:** WHEN max() OF system.process.cpu.total.pct OVER all documents
* **Threshold:** Above 0.5 for the last 5 minutes
* **Vulnerability Mitigated:** Take control of the computer. Possibly scan for malware
* **Reliability:** medium reliability

### Suggestions for Going Further 
* Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain how to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
* Open Port
  - **Patch:** Install firewall to filter open ports and block ICMP requests
  - **Why It Works:** It will block any incoming traffic and wont respond at all to requests
* Weak Passwords
  - **Patch:** Make more complicated passwords
  - **Why It Works:** More complicated passwords makes it much more difficult to break
* Wordpress Enumeration
  - **Patch:** Install the chrome extension WPintel 
  - **Why It Works:** enumerate the WordPress usernames for you by exploiting the REST API vulnerability discussed above

