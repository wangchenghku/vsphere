# vSphere Installation and Setup

## Installing and Setting Up ESXi

### Preparing for Installing ESXi
#### Media Options for Booting the ESXi Installer
##### Format a USB Flash Drive to Boot the ESXi Installation or Upgrade

https://rufus.akeo.ie/

### Setting Up ESXi
#### Configuring Network Settings
ESXi requires one IP address for the management network.
##### Choose Network Adapters for the Management Network

1. From the direct console, select `Configure Management Network` and press Enter.

2. Select `Network Adapters` and press Enter.

3. Select a network adapter and press Enter.

#### Configuring IP Settings for ESXi

When you have access to the direct console, you can optionally configure a static network address.
##### Configure IP Settings from the Direct Console
1. Select `Configure Management Network` and press Enter.

2. Select `IP Configuration` and press Enter.

3. Select `Set static IP address and network configuration`.

4. Enter the IP address, subnet mask, and default gateway and press Enter.

## Deploying the vCenter Server Appliance and Platform Services Controller Appliance

The vCenter Server Appliance installer contains executable files for GUI and CLI deployments, which you can use alternatively.
- The GUI deployment is a two stage process. The first stage is a deployment wizard that deploys the OVA file of the appliance on the target ESXi host or vCenter Server instance. After the OVA deployment finishes, you are redirected to the second stage of the process that sets up and starts the services of the newly deployed appliance.


### Preparing for Deployment of the vCenter Server Appliance and Platform Services Controller Appliance

#### Download and Mount the vCenter Server Appliance Installer

1. From the VMware Web site, download the vCenter Server Appliance ISO image.

2. Mount or extract the ISO image to the client machine from which you want to deploy, upgrade, migrate, or restore the appliance.

   For Ubuntu 14.04, you can use Disk Image Mounter.

### GUI Deployment of the vCenter Server Appliance and Platform Services Controller Appliance
#### Deploy the vCenter Server Appliance with an Embedded Platform Services Controller by Using the GUI
##### Stage 1 - Deploy the OVA File as a vCenter Server Appliance with an Embedded Platform Services Controller
1. In the vCenter Server Appliance installer, navigate to the `vcsa-ui-installer` directory, go to the subdirectory for your operating system, and run the installer executable file.
   - For Linux OS, go to the `lin64` subdirectory, and run the `installer` file.
2. On the Home page, click `Install` to start the deployment wizard.
3. Review the Introduction page to understand the deployment process and click `Next`.
4. Read and accept the license agreement, and click `Next`.
5. On the Select a deployment type page, select `Platform Services Controller` and click `Next`.
6. Connect to the target server on which you want to deploy the Platform Services Controller appliance and click `Next`.

   Option | Steps
   ------------ | -------------
   You can connect to an ESXi host on which to deploy the appliance | 1. Enter the FQDN or IP address of the ESXi host. <br/> 2. Enter the user name and password of a user with administrative privileges on the ESXi host, for example, the root user. <br/> 3. Click Next. <br/> 4. Verify that the certificate warning displays the SHA1 thumbprint of the SSL certificate that is installed on the target ESXi host, and click Yes to accept the certificate thumbprint.
   You can connect to a vCenter Server instance and browse the inventory to select an ESXi host or DRS cluster on which to deploy the appliance. | 

7. On the Set up appliance VM page, enter a name for the Platform Services Controller appliance, set the password for the root user, and click `Next`.
8. Select the deployment size for the vCenter Server Appliance for your vSphere inventory.
9. Select the storage size for the vCenter Server Appliance, and click `Next`.
10. From the list of available datastores, select the location where all the virtual machine configuration files and virtual disks will be stored.
11. On the Configure network settings page, set up the network settings.
   The IP address or the FQDN of the appliance is used as a system name. It is recommended to use an FQDN. However, if you want to use an IP address, use static IP address allocation for the appliance, because IP addresses allocated by DHCP might change.

   Option | Action
   ------------ | -------------
   IP assignment | Select how to allocate the IP address of the appliance. <br/> - static <br/> &nbsp; The wizard prompts you to enter the IP address and network settings.

12. On the Ready to complete stage 1 page, review the deployment settings for the vCenter Server Appliance and click `Finish` to start the OVA deployment process.
13. On the Ready to complete stage 1 page, review the deployment settings for the Platform Services Controller appliance and click `Finish` to start the OVA deployment process.
14. Wait for the OVA deployment to finish, and click `Continue` to proceed with stage 2 of the deployment process to set up and start the services of the newly deployed appliance.

##### Stage 2 - Set up the Newly Deployed vCenter Server Appliance with an Embedded Platform Services Controller
1. Review the introduction to stage 2 of the deployment process and click `Next`.

2. Configure the time settings in the appliance. For vCenter Server High Availability (HA), enable SSH access.

   Option | Description
   ---------------------------------------------------------------------------------------- | -----------------------------------------------------------------------------------------
   Synchronize time with the ESXi host | Enables periodic time synchronization, and VMware Tools sets the time of the guest operating system to be the same as the time of the ESXi host.

3. On the SSO configuration page, create the vCenter Single Sign-On domain, and click Next.
   
   3.1 Enter the domain name, for example, `vsphere.local`
   
   3.2 Set the password for the vCenter Single Sign-On administrator account.
   
   - This is the password for the user administrator@your_domain_name.
   
   - After the deployment, you can log in to vCenter Single Sign-On and to vCenter Server as administrator@your_domain_name.
   
   3.3 Enter the site name for vCenter Single Sign-On

4. Review the VMware Customer Experience Improvement Program (CEIP) page and choose if you want to join the program.

5. On the Ready to complete page, review the configuration settings for the vCenter Server Appliance, click `Finish`, and click `OK` to complete stage 2 of the deployment process and set up the appliance.

6. (Optional) After the initial setup finishes, click the https://vcenter_server_appliance_fqdn/vsphere-client to go to the vSphere Web Client and log in to the vCenter Server instance in the vCenter Server Appliance, or click the https://vcenter_server_appliance_fqdn:443 to go the vCenter Server Appliance Getting Started page.

7. Click `Close` to exit the wizard.

You are redirected to the vCenter Server Appliance Getting Started page.

# vSphere Storage
## Creating Datastores
### Create an NFS Datastore
1. In the vSphere Web Client navigator, select `Global Inventory Lists > Datastores`.

2. Click the `New Datastore` icon.

3. Type the datastore name and if necessary, select the placement location for the datastore.

4. Select NFS as the datastore type.

5. Specify an NFS version.

6. Type the server name or IP address and the mount point folder name.

7. Select `Mount NFS read only` if the volume is exported as read-only by the NFS server.

8. If you are creating a datastore at the data center or cluster level, select hosts that mount the datastore.

9. Review the configuration options and click `Finish`.

# vSphere Networking
## Setting Up Networking with vSphere Standard Switches
### Create a vSphere Standard Switch

1. In the vSphere Web Client, navigate to the host.

2. On the `Configure` tab, expand `Networking` and select `Virtual switches`.

3. Click `Add host networking`.

4. Select a connection type for which you want to use the new standard switch and click `Next`.

   Option | Description
   ------------ | -------------
   VMkernel Network Adapter | Create a new VMkernel adapter to handle host management traffic, vMotion, network storage, fault tolerance, or Virtual SAN traffic.

5. Select `New standard switch` and click `Next`.

6. Add physical network adapters to the new standard switch.

   a. Under Assigned adapters, click `Add adapters`.

   b. Select one or more physical network adapters from the list.

   c. Click `OK`.

7. If you create the new standard switch with a VMkernel adapter, enter connection settings for the adapter.

   Option | Description
   ------------ | -------------
   VMkernel adapter | a. Enter a label that indicates the traffic type for the VMkernel adapter, for example `vMotion`. <br/> b. If you use the default TCP/IP stack, select from the available services. <br/> c. Configure IPv4 and IPv6 settings.

8. On the Ready to Complete page, click `OK`.

# vSphere Availability
## Creating and Using vSphere HA Clusters
### Creating a vSphere HA Cluster
#### Create a vSphere HA Cluster
1. In the vSphere Web Client, browse to the data center where you want the cluster to reside and click `Create a Cluster`.

2. Complete the New Cluster wizard.
   
   Do not turn on vSphere HA (or DRS).

3. Click `OK` to close the wizard and create an empty cluster.

4. Based on your plan for the resources and networking architecture of the cluster, use the vSphere Web Client to add hosts to the cluster.

5. Browse to the cluster and enable vSphere HA.
   
   a. Click the `Configure` tab.
   
   b. Select `vSphere Availability` and click `Edit`.	
   
   c. Select `Turn ON vSphere HA`.
   
   d. Select `Turn ON Proactive HA` to allow proactive migrations of VMs from hosts on which a provider has notified a health degradation.

6. Under `Failures and Responses` select `Enable Host Monitoring`

   With Host Monitoring enabled, hosts in the cluster can exchange network heartbeats and vSphere HA can take action when it detects failures. Host Monitoring is required for the vSphere Fault Tolerance recovery process to work properly.

7. Select a setting for `VM Monitoring`.
   
   Select `VM Monitoring Only` to restart individual virtual machines if their heartbeats are not received within a set time.

8. Click `OK`.

## Providing Fault Tolerance for Virtual Machines
### Fault Tolerance Requirements, Limits, and Licensing
#### Limits
In a cluster configured to use Fault Tolerance, two limits are enforced independently.

- `das.maxftvmsperhost`
  - The maximum number of fault tolerant VMs allowed on a host in the cluster. Both Primary VMs and Secondary VMs count toward this limit. The default value is 4.
- `das.maxftvcpusperhost`
  - The maximum number of vCPUs aggregated across all fault tolerant VMs on a host. vCPUs from both Primary VMs and Secondary VMs count toward this limit. The default value is 8.

### Preparing Your Cluster and Hosts for Fault Tolerance
#### Fault Tolerance Checklist
You must meet the following cluster requirements before you use Fault Tolerance.
- Fault Tolerance logging and VMotion networking configured.
- vSphere HA cluster created and enabled. vSphere HA must be enabled before you can power on fault tolerant virtual machines or add a host to a cluster that already supports fault tolerant virtual machines.

#### Configure Networking for Host Machines
On each host that you want to add to a vSphere HA cluster, you must configure two different networking switches (vMotion and FT logging) so that the host can support vSphere Fault Tolerance.

1. In the vSphere Web Client, browse to the host.

2. Click the `Configure` tab and click `Networking`.

3. Select `VMkernel Network Adapter`.

4. Click the `Add host networking` icon.

5. Provide appropriate information for your connection type.

6. Click Finish.

After you create both a vMotion and Fault Tolerance logging virtual switch, you can create other virtual switches, as needed. Add the host to the cluster and complete any steps needed to turn on Fault Tolerance.

### Using Fault Tolerance
#### Turn On Fault Tolerance

1. In the vSphere Web Client, browse to the virtual machine for which you want to turn on Fault Tolerance.

2. Right-click the virtual machine and select `Fault Tolerance > Turn On Fault Tolerance`.

3. Click `Yes`.

4. Select a datastore on which to place the Secondary VM configuration files. Then click `Next`.

5. Select a host on which to place the Secondary VM. Then click `Next`.

6. Review your selections and then click `Finish`.

# vSphere Monitoring and Performance
## Monitoring Inventory Objects with Performance Charts
### Overview Performance Charts
#### Hosts
##### Network Rate 
The Network Rate chart displays network bandwidth on a host.

The Network Data Transmitted/Received chart for hosts is located in the `Home` view of the Host `Performance` tab.

Chart Label | Description
------------ | -------------
Data Transmit Rate | Rate at which data is transmitted across the top ten physical NIC instances on the host. This represents the bandwidth of the network.

# Troubleshooting
## Install the Flash plug-in

1. Activate the Canonical Partner repository


   The Canonical Partner repository offers some proprietary applications that don't cost any money to use but are closed source. They include software like *Skype* and *Adobe Flash Plugin*. Software in this repository will appear in *Ubuntu Software* search results but won't be installable until this repository is enabled.

   To enable the repository, open the Other Software tab in *Software & Updates*. If you see the Canonical Partners repository in the list, make sure it is checked then close the *Software & Updates* window.

2. Install the adobe-flashplugin package.