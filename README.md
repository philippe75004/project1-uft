# Project1-elk Philippe HENRY

The goal of this project is to show my ability to build a Cloud IAAS solution on Azure that host 3 Webservers which hosts the same dvwa web container behind an Azure load balancer and then build a ELK server on a separated virtual network in another region and configure communicaitons via peering with the 3 Web VMs to send logs and metric back to ELK so our SOC analyst can visualize and hunt for threats.

We use Ansible container to deploy and configure the 3 web VMs and the ELK VM.

We create on our Azure, 2 Security groups, 1 rule to allow from Internet Access to our ELK web interface called KIBANA only from our home ip address for security reason as we are using default credential for this project as it is a demo and 1 rule to allow from Internet Access to our Jumpbox which host ansible as a container.