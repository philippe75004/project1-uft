####                                     Project1-AZURE-ELK-ANSIBLE-Philippe HENRY

The goal of this project is to show my ability to build a Cloud IAAS solution on Azure that host 3 Webservers within the same availability set which hosts the same dvwa web docker container behind an Azure load balancer and then build a ELK server on a separated virtual network in another region and configure communicaitons via peering with the 3 Web VMs to send logs and metric back to ELK so our SOC analyst can monitor, visualize and hunt for threats.

We use Ansible container to deploy and configure the 3 web VMs and the ELK VM.

We create on our Azure, 2 Security groups, 1 rule to allow from Internet Access to our ELK web interface (TCP 5601) called KIBANA only from our home ip address for security reason as we are using default credential for this project and it is a demo and 1 rule to allow from Internet Access to our Jumpbox which host ansible as a container via SSH keys.

| Name     | Publicly Accessible | IP Addresses             |
|----------|---------------------|--------------------------|
| Jump-Box-Provisioner Yes       | 10.1.0.4 /20.124.236.227 |
| ELK      |           Yes       | 10.2.0.4 /20.122.48.236  |
| LoadBalancer         Yes       |20.25.9.111               |
| Web1     |           No        | 10.1.0.5 /20.25.9.111    |
| Web2     |           No        | 10.1.0.6 /20.25.9.111    |
| Web3     |           No        | 10.1.0.7 /20.25.9.111    |

----------------------------------------------------------------------------------------------------------------------------------------

#### Question Logging and monitoring

Here is my questions / answers from the Logging and monitoring domain:

1. **Restate the Problem**

    - Organizations must monitor what happening in their network, for performance and security reasons and whitout proper tools 
	you will have poor visibility on your own network and therefore will not be able to detect and response if an attack or issue happens.

	An ELK solutions must be in placed in ordered to log and monitor all our devices on the network.

2. **Scenario**

	- During the UFT Bootcamp, we implemented and ELK solutions from scartch on Azure to monitor our 3 Servers hosting web containers.
	
	- We were able to log and monitor via filebeat and metricbeat our 3 Servers hosting docker web containers and review and detect abnormal behaviours.
	
	- Based on the analys of the logs and monitoring we implemented more security in our ssh and web access.
	
3. **Solution Requirements**


    - Our solution required to build from Scracth on Azure Cloud an: Infrasctucture as a Service solution that include one VM management server with Ansible as a docker container + 3 linux VM  on the same availability set group with each the WEB (DVWA) docker containers deployed via Ansible behind a standard Azure load balancer and protected by 2 network security groups that only my public address as access .
	
	- Finally we deploy 1 Linux VM and install via Ansible the ELK solution in order to log and monitor our WEB DVWA applications hosted on the 3 VM.
	
	- We install and configure filebeat and metribeat in order to be able to have a better view of our systems.It does not explain exactly how you implemented each step.

    - Between the virtual networks, the network security group is configure to any / any and  from AzureLoadBalancer to virtual network, also any / any.


4. **Advantages and Disadvantages** 

	- This Azure solution was easy and fast to deploy as a demo or proof of concepts however it does not follow the best practices
	in terms of accesses.
    
    - We should in real life scenario not just use the Network security group but add also a Next Generation Firewall solution which will act also as an IPS and block known attacks as the solution we implemented did not include any blocking protection withing the internal network, only logging and monitoring.
	

5. **Solution Details**

    - To restrict access to our solution I created 1 Network security group with port TCP/22 open to access our Jump server with Ansible container.

	- We configure SSH keys on our Jump server and disable password authentification and force the use of SSH keys for external access.

	- Then on our Jump server where Ansible is installed, I created a SSH RSA keys and copy it to the web servers for Ansible to run playbook /  configure target devices (our 3 web serevrs in our case)