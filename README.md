# Project1-elk Philippe HENRY

The goal of this project is to show my ability to build a Cloud IAAS solution on Azure that host 3 Webservers which hosts the same dvwa web container behind an Azure load balancer and then build a ELK server on a separated virtual network in another region and configure communicaitons via peering with the 3 Web VMs to send logs and metric back to ELK so our SOC analyst can visualize and hunt for threats.

We use Ansible container to deploy and configure the 3 web VMs and the ELK VM.

We create on our Azure, 2 Security groups, 1 rule to allow from Internet Access to our ELK web interface called KIBANA only from our home ip address for security reason as we are using default credential for this project as it is a demo and 1 rule to allow from Internet Access to our Jumpbox which host ansible as a container.

----------------------------------------------------------------------------------------------------------------------------------------

1. **Restate the Problem**
   - When restating the question in your own words, add additional details to demonstrate you understand what is being asked and why.

    - Example: "It's important that organizations control access to a cloud network, especially since it has resources that only the engineering team should be able to access. Following the principle of least privilege, you want to make sure engineers can access it easily, but no one else can." 


2. **Provide a Concrete Example Scenario**

   - Use the parameters of the question to create an example scenario of the problem you just restated. This makes the problem easier to talk through and further demonstrates your experience with the topic. 

   - Use your class experience to form scenarios. All your assignments are legitimate evidence of your technical background and experience, and can be referenced in your answers to open-ended questions.

   - Example: "In Project 1 of my cybersecurity bootcamp, we solved an almost identical problem. In that project, we deployed a virtual network containing several VMs to Azure, which only we and our instructional team were supposed to be able to access. Just as an organization would limit cloud network access to only engineers, we had to implement remote access controls limiting access to only a handful of authorized individuals."


3. **Explain the Solution Requirements**


    - Before explaining the details of your solution, explain the high-level actions you took at each step and what they accomplished.


    - Example: "After deploying the network, I first had to configure a network security group around the whole subnet. This blocked traffic from all IP addresses, except for mine, my partners', and my instructors'. This NSG allowed inbound access to only one machine on the internal network, the jump box.
    
       Then, I configured additional NSGs on the VMs within the subnet. This allowed connections only between the jump box and other local IP addresses.


       Finally, I forced the use of SSH keys to eliminate vulnerability to password-based brute-force."


    - Note: This example lists three high-level steps, including tools used and what each step accomplished. It does not explain exactly how you implemented each step.


4. **Identify Advantages and Disadvantages** 

* Point out why your solution works in general. Then acknowledge any potential shortcomings and how you would address them.


    - Example:  "This solution worked well for my project because it ensured only the selected users had access. However, it is difficult to maintain and scale because it requires updating the NSG every time a new user requires access to the network. In addition, securely using SSH keys can be tricky in the long run. An alternative solution addressing these shortcomings would be implementing a VPN gateway to the private network. This would allow us to manage and monitor users more safely and scalably."


    - Note: This reflection further demonstrates to the interviewer that you understand not only the problem and solution, but also the tradeoffs of your solution.


5. **Explain the Solution Details**

    - Now that you explained the high-level steps and reflected on the pros and cons, explain the specifics of how you would implement the solution. The examples below are shortened for brevity, but real answers would typically include considerably more detail.

    - Example: "To configure access controls around the entire subnet, I created an NSG with the following ruleset: […] These rules allow access to the jump box from only the specified IP addresses specified.

       Then, to configure access controls within the subnet, I created NSGs with the following ruleset: […] These rules allow the VMs within the network to communicate only with each other and with the jump box.

       To force the use of SSH keys, I modified the following configurations in the VMs on the network: [...] This ensures that password brute-force attacks will always fail."