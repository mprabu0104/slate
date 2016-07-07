### Cloudant on Bluemix Local
<a href="http://www-01.ibm.com/support/knowledgecenter/SSTPQH/SSTPQH_welcome.html" target="_blank">IBM Cloudant on Bluemix Local</a> is a NoSQL database-as-a-service (DBaaS) built from the ground up to scale globally, run non-stop, and handle a wide variety of data types like JSON, full-text, and geospatial. Cloudant is an operational data store optimized to handle concurrent reads & writes, and provide high availability and data durability.

#### Hardware Requirements for Cloudant on Bluemix Local
Before you install Cloudant® on Bluemix Local, confirm that your system meets these requirements. The requirements include hardware, cluster,  requirements, Cloudant virtual machine distribution and physical host recommendations, and Logmet hardware requirements for installing the product.

##### Operating system
Cloudant uses Debian version 8 operating system exclusively.

##### Clusters
Cloudant in Bluemix Local requires two clusters minimum. One cluster internally
powers the Bluemix platform, while the other cluster powers external customer accounts and data.

#####Hardware requirements	
 
<table>
<tr>
<th>Type</th>
<th>Count</th>
<th>Optional?</th>
<th>Name format</th>
<th>min vCPU</th>
<th>recommended vCPU</th>
<th>min RAM (GB)</th>
<th>recommended RAM (GB)</th>
<th>Disk-OS (GB)</th>
<th>Disk Config - OS</th>
<th>min Disk - Data (GB)</th>
<th>recommended min Disk - Data (GB)</th>
<th>Disk Config - Data</th>
<th>Network (Gbps)</th>
</tr>

<tr>
<td>Infra</td>
<td>1</td>
<td>No</td>
<td>infra1.bml-<customer></td>
<td>8</td>
<td>8</td>
<td>16</td>
<td>16</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>3000</td>
<td>3000</td>
<td>VMDK - thin/independent persistent</td>
<td>1</td>
</tr>

<tr>
<td>SAPI</td>
<td>2</td>
<td>No</td>
<td>sapi<#>.bml-<customer></td>
<td>4</td>
<td>4</td>
<td>4</td>
<td>4</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>1</td>
</tr>

<tr>
<td>Load Balancer (Bluemix Ops Cluster)</td>
<td>2</td>
<td>No</td>
<td>lb<#>.bml-ops-<customer>001</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>1</td>
</tr>

<tr>
<td>Load Balancer (Customer Cluster)</td>
<td>2</td>
<td>No</td>
<td>lb<#>.bml-<customer>001</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>1</td>
</tr>

<tr>
<td>DB Node (Bluemix Ops Cluster)</td>
<td>3</td>
<td>No</td>
<td>db<#>.bml-ops-<customer>001</td>
<td>8</td>
<td>8</td>
<td>16</td>
<td>16</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>800</td>
<td>800</td>
<td>VMDK - thick eager-zeroed / independent persistent</td>
<td>1</td>
</tr>

<tr>
<td>DB Node (Customer Cluster) </td>
<td>3</td>
<td>No</td>
<td>db<#>.bml-<customer>001</td>
<td>8</td>
<td>48</td>
<td>16</td>
<td>64</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>800</td>
<td>1000</td>
<td>VMDK - thick eager-zeroed/independent persistent</td>
<td>1</td>
</tr>

<tr>
<td>Load Balancer (Backup Cluster)</td>
<td>2</td>
<td>Yes</td>
<td>lb<#>.bml-<customer>-bk001</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>8</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>1</td>
</tr>

<tr>
<td>DB Node (Backup Cluster)</td>
<td>3</td>
<td>Yes</td>
<td>db<#>.bml-<customer>-bk001</td>
<td>8</td>
<td>24</td>
<td>16</td>
<td>64</td>
<td>10</td>
<td>VMDK - thick eager-zeroed</td>
<td>800</td>
<td>18000</td>
<td>VMDK - thin/independent persistent</td>
<td>1</td>
</tr>

</table>

###### Logmet hardware requirements							
<table>
<tr>
<th>Type</th>
<th>Count</th>
<th>Optional?</th>
<th>min vCPU</th>
<th>recommended vCPU</th>
<th>min RAM (GB)</th>
<th>recommended RAM (GB)</th>
<th>min Disk (GB)</th>
<th>recommended Disk (GB)</th>
</tr>
<tr>
<td>Logmet Core</td>
<td>3</td>
<td>No</td>
<td>4</td>
<td>4</td>
<td>20</td>
<td>20</td>
<td>900</td>
<td>900</td>
</tr>
<tr><td>Logmet HAProxy
</td>
<td>2</td>
<td>No</td>
<td>1</td>
<td>1</td>
<td>4</td>
<td>4</td>
<td>40</td>
<td>40</td></tr>
<tr>
<td>Logmet Manager
</td>
<td>1</td>
<td>No</td>
<td>1</td>
<td>1</td>
<td>4</td>
<td>4</td>
<td>40</td>
<td>40</td></tr>
<tr><td>Logmet Expansion
</td>
<td>3</td>
<td>Yes</td>
<td>3</td>
<td>3</td>
<td>12</td>
<td>12</td>
<td>600</td>
<td>600</td>
</tr>
<td>CFS Ops
</td>
<td>1</td>
<td>No</td>
<td>2</td>
<td>2</td>
<td>8</td>
<td>8</td>
<td>350</td>
<td>350</td>
</tr>
</table>

##### Cloudant virtual machine distribution and physical host recommendations			
These recommendations assume that you are using the recommended hardware outlined above as well as using a backup cluster.		

<table>
<tr>
<th>Host</th>
<th>vCPU</th>
<th>RAM used</th>
<th>VMs deployed</th>
</tr>

<tr><td>1</td>
<td>48</td>
<td>64</td>
<td>db1.bml-<customer>001</td>
</tr>
<tr><td>2</td>
<td>48</td>
<td>64</td>
<td>db2.bml-<customer>001</td>
</tr>
<tr><td>3</td>
<td>48</td>
<td>64</td>
<td>db3.bml-<customer>001</td>
</tr>
<tr><td>4</td>
<td>48</td>
<td>96</td>
<td>lb1.bml-<customer>001
lb1.bml-ops-<customer>001
db1.bml-ops-<customer>001
db1.bml-<customer>-bk0011</td>
</tr>
<tr><td>5</td>
<td>48</td>
<td>96</td>
<td>lb2.bml-<customer>001
lb2.bml-ops-<customer>001
db2.bml-ops-<customer>001
db2.bml-<customer>-bk0011</td>
</tr>
<tr><td>6</td>
<td>44</td>
<td>92</td>
<td>lb1.bml-<customer>-bk001
db3.bml-ops-<customer>001
db3.bml-<customer>-bk001
sapi1.bml-<customer></td>
</tr>
<tr><td>7</td>
<td>20</td>
<td>38</td>
<td>lb2.bml-<customer>-bk001
sapi2.bml-customer
infra1.bml-customer</td>
</tr>
</table>

##### Virtual machine requirements
In order to ensure the highest possible performance for your database deployment, Cloudant requires that each virtual machine meet the following specifications.  

*	Set up VMs using a thick provision eager zeroed disk.
*	Configure the infra-auxiliary VM and the three data partitions for the backup database VMs using thin provisioning.

This configuration equals 7 TB thick and 21 TB thin virtual disks. Initially, you must prepare to use 8 TB virtual disk space out of the box.

###### Supported VMware versions
Cloudant on Bluemix Local supports VMware versions 5.5 an 6.0. 

##### Network requirements for Cloudant
Set the maximum transmission unit (MTU) value to 9000 for virtual switches.

##### External internet access requirement 
External internet access is required. However, there is no need to make any networking changes. The Cloudant initial architecture design routes external internet traffic to pypi, rubygems, github, and dynect through the tether. Future versions will pull all dependencies in to the local deployment, eliminating this requirement.

#### Frequently Asked Questions about Cloudant on Bluemix Local


*Does Cloudant have an architecture diagram for deployments in Bluemix Local?*
<p>Yes, it can be found here: https://ibm.box.com/s/7kycwiiyyoz4a651l6lkuafkylu0eo6p</p>

**How is Cloudant for Bluemix Local deployed?**
<p>You must download the OVA and ISO files and upload them to the datastore. You must
provide Cloudant information on the network, datastore, and locations of the OVA and ISO files. Cloudant runs a script and wraps ovftool. This process creates the VMs with the proper settings and ISOs mounted. A startup
script, packaged in the OVA, configures the networking and sets up reverse-ssh tunneling. Chef configuration management runs the remaining provisioning tasks.</p>

**Can Cloudant be deployed within a normal customer maintenance window?**
<p>Deploying Cloudant in your data center is still a lengthy process. Currently, Cloudant needs about 1-2 weeks of time to deploy and verify. Support is working to improve the deployment and automation process. </p>

**Does Cloudant follow the same Bluemix CR/DR process? Can I decide when changes are deployed?**
**Can I review the changes before they are deployed?**
<p>Cloudant does not follow the CR/DR process. Cloudant is delivered as a service and manages thousands of
machines between public DBaaS and Bluemix Local. Support uses Chef to handle configuration management across
our infrastructure, including clusters in Bluemix Local. As a result, non-disruptive changes are delivered
regularly multiple times a week and sometimes multiple times per day. Therefore, changes and updates are not
bound to predetermined maintenance windows. Cloudant does not require customer sign-off on
changes and updates to their clusters in Bluemix Local.</p>

**What about changes that are disruptive?**
<p>While the vast majority of updates are non-disruptive, Cloudant might deploy changes that cause a temporary outage. These outages are rare. In the event of an outage, Cloudant support will coordinate with you to find a maintenance window that is the least disruptive to deploy these types of releases.</p>

*What operating systems are available for Cloudant?*
<p>Cloudant uses Debian 8 exclusively.</p>

**Where are the Cloudant VMs being deployed?**
<p>The VMs deploy within the private VLANs inside of your Bluemix Local deployment.</p>

**How does Cloudant obtain IP addresses for the VMs?**
<p>Cloudant is on the private network inside of Bluemix Local and only requires private IPs, which are provided by the Bluemix team.</p>

**What name will display in the catalog for Cloudant service?**
<p>The Cloudant service name will display as "Local".</p>

*How many Cloudant clusters do I need?*
<p>Cloudant in Bluemix Local requires two clusters minimum. One cluster internally
powers the Bluemix platform, while the other cluster powers external customer accounts and data.</p>

**Who is responsible for the Cloudant service broker?**
<p>Support will make the appropriate changes to the service broker. If you have an existing dedicated cluster, support must configure the broker to point to the new local cluster. Support will follow the normal Bluemix
CR/DR process.</p>

*Does Cloudant require external internet access?*
<p>Yes, external internet access is required. However, there is no need to make any networking changes. The Cloudant initial architecture design routes external internet traffic to pypi, rubygems, github, and dynect through the tether. Future versions will pull all dependencies into the local deployment, eliminating this requirement.
</p>

**How does the Cloudant operations team access my Bluemix Local environment?**
<p>The Cloudant team uses the existing tether/relay provided by Bluemix. No new networking
requirements are required for Cloudant support to access the your environment.</p>

**What is Logmet? Why does Cloudant need it?**
<p>Logmet is our logging infrastructure. Logmet requires its own hardware resources. Cloudant sends logs to
Logmet so that your information can be stored locally. Logmet is a separate deployment. You do not need one
Logmet deployment per Cloudant cluster. All Cloudant clusters, within one Bluemix Local environment, can
share the same Logmet instance.</p>

**Where do you send metrics and monitoring information?**
<p>Metrics and monitoring information is sent to Cloudant through the tether. Without it, you could not properly maintain your local cluster.<p>

*Is thick provision eager zeroed required?*
<p>In order to ensure the highest possible performance for your database deployment, Cloudant requires that each virtual machine meet the following specifications.  

*	Set up VMs using a thick provision eager zeroed disk.
*	Configure the infra-auxiliary VM and the three data partitions for the backup database VMs using thin provisioning.

This configuration equals 7 TB thick and 21 TB thin virtual disks. Initially, you must prepare to use 8 TB virtual disk space out of the box.</p>

*How much disk space will I need on day 1?*
<p>Initially, you must prepare to use 8 TB virtual disk space out of the box.</p>

**How is VMware clustering set up for Cloudant, Logmet, and Bluemix?**
<p>Cloudant must be on a VMware cluster separate from Bluemix to prevent noisy neighbor
problems. Logmet must be in the same cluster with Bluemix.</p>

*Which versions of VMware are supported?*
<p>Versions 5.5 and 6.0.</p>

**How are VMs distributed across hosts?**
<p>Cloudant determines which VMs deploy and on which hosts. The goal is to keep database nodes and
load balancers separate, so if one host goes down, the cluster continues to operate. Research is in progress to  determine how to enable DRS with specific rules in order to keep VMs separated.</p>

*Are there any network requirements specific to Cloudant?*
<p>Yes. You must set the MTU to 9000 on the virtual switches.</p>

**Does Cloudant feed logs to the QRadar deployment that is included with Bluemix Local?**
<p>Yes. Cloudant sends `auth` and `auditd` logs to QRadar and stores them for 1 year.</p>

**How does backup work?**
<p>Cloudant offers a backup service that schedules and runs incremental backups of your data. It is strongly
recommended that you purchase a separate cluster, specifically dedicated to storing backup data. The Cloudant backup cluster must be inside the same Bluemix Local environment. More information on backing up your data can be found here, https://docs.cloudant.com/backup-guide.html.</p>

<p>Both the customer and ops cluster can backup to the same location. If you do not want to use the Cloudant
backup product, you are responsible for backing up your data.</p>

**Where can I find Bluemix Local documentation?**
<p>Blue Mix documentation is located here, https://console.ng.bluemix.net/docs/local/index.html#local.</p>