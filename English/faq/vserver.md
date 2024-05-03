# vServer

### \[vServer] Why does the Server restart not come up?&#x20;

Please access the console and enter the root password -> check the content of /etc/fstab --> edit if incorrect.

### \[vServer] Why haven't I received the OTP SMS activation after registering for an account?

Please check the Captcha code to get the OTP, verify if the phone number is correct. If you still haven't received it, please call 19001549 and press 2 for technical support.

### \[vServer] Why can't I open the Server Console?&#x20;

Some browsers may block pop-ups and Java. Please select the pop-up to allow Java, then the server console will open normally.

### \[vServer] Why can't I SSH to the Linux Server?&#x20;

In addition to entering the correct port 234 (different from the default SSH port, which is 22), you need to check if the Security Group has allowed port 234.

### \[vServer] Why can't I Remote Desktop to the Windows VPS?&#x20;

In addition to entering the correct port 3490, you need to check if the Security Group has allowed port 3490.

### \[vServer] Why can't I connect to the listening ports on the VPS?&#x20;

Please check the security group. The security group (SEC) on the portal may not allow the port, or it may not allow the correct group applied to the Server.

### \[vServer] Why does the VPS have WANIP but only shows a Private IP inside the VPS?&#x20;

The system uses 1-1 NAT, so users only see the Private IP. Inside the server, it listens according to the private IP, while outside, it accesses using the public IP.

### \[vServer] How do I enable root login ssh on VPS Linux?&#x20;

Change the ssh permission in /etc/ssh/sshd\_config (PermitRootLogin yes), restart the ssh service. We recommend users not to use root to minimize the risk of brute-force attacks, stackops privileges are equivalent to root privileges.

### \[vServer] Does Extend Disk cause data loss?&#x20;

You can extend the disk for the server without data loss.

### \[vServer] Does Extend Disk require a Server reboot?&#x20;

Depending on the case, the server may need to be restarted to expand the capacity.

### \[vServer] How do I extend the disk in Linux?&#x20;

You can do as follows: Extend the disk on the VNG Cloud portal: <mark style="color:blue;">Expand Volume with Linux operating system.</mark>

### \[vServer] How do I extend the disk in Windows?&#x20;

<mark style="color:blue;">Expand Volume with the Windows operating system</mark>. You can do as follows: Extend the disk on the VNG Cloud portal.

### \[vServer] Do I need to reinstall the OS?&#x20;

You can delete to create a new server. Currently, VNG Cloud does not support reinstalling a new OS on an already created Server.

### \[vServer] How do I access the server after creation?&#x20;

You can access via open console on the portal just created. For Linux servers, you can use SSH, for Windows servers, you can use Remote Desktop.

### \[vServer] Does Resize VPS require a reboot?&#x20;

Yes, if you resize the Server, it must be rebooted.

### \[vServer] My VPS has expired and been deleted, what should I do?&#x20;

If the Server has expired, it will show as Expired on the homepage interface, this status will be retained for 7 days. If you do not renew the Server, it will be permanently deleted and cannot be restored.

### \[vServer] My VPS is hanging, can you help me Reboot?&#x20;

To reboot the Server, please refer to your Server's Reboot page.

### \[vServer] I want to Reset the Server's password?&#x20;

You cannot reset the password for your Server yourself. To reset the password for the Server, please send a request on our <mark style="color:blue;">Support page</mark>.

### \[vServer] I cannot allow some ports on Webmin vServer?&#x20;

Please check the Security Group on the portal to see if the corresponding port has been allowed. If it has been allowed but still not working, please check if the port is listening on the Server.

### \[vServer] My Server cannot access the internet?&#x20;

Please restart the server and set the DNS to 8.8.8.8.

### \[vServer] How do I switch from Simple Farm to vPC Farm?&#x20;

Currently, we no longer support Simple Farm.

### \[vServer] Can you help with deploying an OVA file?&#x20;

Deploying to Cloud Server only supports RAW or QCOW2 file formats.

### \[vServer] How can I check the payment history or refund information?&#x20;

Please go to Account -> Payment Method to view the information.

### \[vServer] Why can't I open port 21 but other IPs can still access?&#x20;

Please delete rule 65535, as rule 65535 is Allow all port.

### \[vServer] Why don't I have the password for the administrator user?&#x20;

When creating the Server, the admin user is disabled. If you want to use it, you can go to management to set a password and use the administrator user normally.

### \[vServer] Where is the history of payments or refunds after creating an Image?&#x20;

To view the created Image information, please access the <mark style="color:blue;">Image page</mark>.

### \[vServer] Why can't I \[connect] to the \[ports] listening on my VPS?

The security group (SEC) on the portal may not have allowed the port, or it may not have allowed the correct group applied to the server. The user's local firewall may not have allowed the port. Log in to the Portal. Go to Cloud Servers -> Click on the server to check the SEC -> Security Group section -> Select the applied Security group. By default, the outbound direction (Egress) has been allowed all, for inbound direction, just need to add the required port. In the Rule section, choose Custom TCP, Direction select Ingress to open for inbound direction, enter the port to be opened. CIDR defaults to all external ranges accessing.

### \[vServer] How to enable \[root login]\[SSH] on VPS \[Linux]?&#x20;

You need to change the SSH permissions in /etc/ssh/sshd\_config (PermitRootLogin yes), restart the SSH service. It is recommended that users avoid using root to minimize the risk of brute-force attacks, and stackops permissions are equivalent to root permissions.

### \[vServer] How to access the server after creation?&#x20;

Access through the open console on the newly created portal and enter the server information to access it. For Linux servers, you can use SSH, for Windows servers, you can use Remote Desktop.

### \[vServer] Why can't I \[ping] my VPS?&#x20;

Please access the portal's security group to allow the ICMP rule.

### \[vServer] I can't \[SSH] / \[Remote] into the VPS?&#x20;

You can check the service SSH on the portal, whether the port is allowed on the security group, whether telnet to the SSH port is working, and whether ping is working.

### \[vServer] If a customer wants to change account information, email.&#x20;

### \[vServer] How do I set up Reverse DNS from IP 61.28.X.X to the company's mail?&#x20;

Please create a ticket for VNG Cloud and provide the server IP information and the mail address that needs reverse DNS.

### \[vServer] Support for increasing quota?&#x20;

Please create a ticket for support to increase the quota and specify the amount you need to increase.

### \[vServer] Support for viewing RAM, CPU, network?&#x20;

Currently, VNG Cloud has a vMonitor service in beta version for free trial that can monitor these parameters. You can access it on the <mark style="color:blue;">vServer homepage</mark>, and view RAM, CPU, Network information on the Server details page / Monitor tab or directly on the <mark style="color:blue;">vMonitor homepage</mark>.

### \[vServer] How do I keep the old WANIP for the new server?&#x20;

Once the WAN IP is deleted, it cannot be recovered. If you want to keep the WAN IP, you need to detach that WAN IP and then attach it to the server you want to use.

### \[vServer] Does vServer have bandwidth limits? What happens if I exceed the bandwidth?&#x20;

Currently, we limit the bandwidth to 100mbps. If you want to increase it, please contact the sales staff or send a request on the <mark style="color:blue;">Support page</mark> for us to assist you in increasing the bandwidth. Note that increasing bandwidth will incur additional costs.

### \[vServer] Can I increase the security policy quota?&#x20;

Currently, the default security policy is full 10. Customers who want to increase it are only supported up to a maximum of 20 security policies.

### \[vServer] Can I create a server with a HDD and a 1TB volume?&#x20;

When you create a new Server, we will default to creating a Root Volume partition with an SSD format and support a minimum capacity of 20GB and a maximum of 3000GB, with a minimum of 200 IOPS and a maximum of 10000. So you can choose to create a Server with a Volume partition that supports a capacity of 1TB (1000GB), but please note that we no longer support HDD format for Volumes.

### \[vServer] How many volumes can I add to a server?&#x20;

Currently, you can add a maximum of 2 volumes to a server. The root volume partition can choose a minimum capacity of 20GB and a maximum of 500GB. New data volumes can choose a minimum capacity of 20GB and a maximum of 10TB.

### \[vServer] How do I SSH to the server as root user?&#x20;

Please follow these steps:&#x20;

\#Edit /etc/ssh/sshd\_config

PermitRootLogin no -->> PermitRootLogin yes&#x20;

\#Restart sshd to apply changes&#x20;

\#For CentOS&#x20;

service sshd restart&#x20;

\#For Ubuntu service ssh restart&#x20;

Then use the root user to connect with password, sshkey of root user.

### \[vServer] Why can't my server copy/paste through the remote desktop interface?&#x20;

Please check if the Clipboard mode in Local Resources of the Remote Desktop program has been unstick. If you have already enabled Clipboard mode in Local Resources and still have issues, please proceed as follows: Open Task Manager on the remote machine. Stop the rdpclip.exe process, then in Task Manager, select File -> New Task (Run), enter rdpclip.exe. Now try connecting again.

### \[vServer] What is the maximum number of users that can simultaneously access a website?&#x20;

The maximum number of users that can simultaneously access a website depends not only on the server's configuration but also on the application and optimization of the Customer's system.

### \[vServer] Why can't I delete old Certificates and Keys, and how can I use new Certificates and Keys?&#x20;

Currently, we do not support deleting old Certificates and Keys on the Load Balancer. If you want to use new Certificates and Keys, please upload the new Certificate on the <mark style="color:blue;">Certificate Homepage</mark> (without the same Certificate name as the old one), then go to the <mark style="color:blue;">Load Balancer Homepage</mark> to update the new Certificate details on the LB details page.

### \[vServer] Why can't I telnet to port XYZ? Even though I have allowed the firewall, ACL on the policy group, and checked that port XYZ is listening.&#x20;

When checking the LISTEN port, see if it is listening on 0:0:0:0: XYZ. Some services, when running on a port, only run on localhost 127.0.0.1, so they cannot be telneted from the outside (depending on the service's configuration, adjust this part).

### \[vServer] Why does the system prompt "Please select a network" when I create a server to the payment stage?&#x20;

When creating a Server at the VPC site, you need to create a Network first for the Server (Go to the Network section on the Portal, select Add, then enter the Name -> Create), and then create the Server (it will use that Network class).

### \[vServer] How can I increase the HDD capacity but only get up to 200GB?&#x20;

You can go to the Storage section on the Portal to add additional Volumes, up to a maximum of 10TB for your Server, following the instructions on the <mark style="color:blue;">Volume Size Increase</mark> page.

### \[vServer] Is creating an image always full of all disks or only the C disk (or Root partition)?

Creating an image means creating a full image of all disks/partitions.

### \[vServer] I accidentally deleted all the rules in the Security Policy and now I can't ssh into the server?&#x20;

Please go to the Default Group and re-add the default Ingress and Egress rules as <mark style="color:blue;">instructed</mark> to be able to ssh back into the server.

### \[vServer] "vServer: I can't create additional security groups?"&#x20;

By default, each user is only allowed to create up to 10 security groups. If you need to create more, please contact the technical support department or send an email to [https://helpdesk.vngcloud.vn/](https://helpdesk.vngcloud.vn/) for assistance, however, the maximum is 20 security groups.

### \[vServer] Why does the console interface keep reporting 'no map for 231' error?&#x20;

You can turn off unikey, then close and reopen the console interface to enter the password.

### \[vServer] "What are the differences between General v1 Instances and High Performance v2 Instances? Why is there a price difference?"&#x20;

We no longer differentiate between General and High Performance, but we only have Flavors with different configurations.

### \[vServer] How many snapshots can I create on one volume?&#x20;

Currently, the Snapshot feature has been removed, instead you can use the Backup Server feature to backup the Volume.

### \[vServer] How long does it take to create an image?&#x20;

The time depends on the volume size, the larger the volume size, the longer it takes to initialize the Image.

### \[vServer] How high can I increase the IOPS?&#x20;

We allow you to increase the IOPS up to a maximum of 200 to 10000.

### \[vServer] How many volumes can I add to a server?&#x20;

Currently, you can add a maximum of 2 volumes to a server. The root volume partition can choose a minimum capacity of 20GB and a maximum of 3000GB. The Data volume partition can choose a minimum capacity of 20GB and a maximum of 4000.

### \[vServer] Remote Desktop only allows 2 users to access, if a third user tries to access, it will kick out the 2 active users. Is there a way to allow more than 2 users?&#x20;

You can follow the instructions here: [https://support.managed.com/kb/a1816/how-to-enable-disable-multiple-rdp-sessions-in-windows-2012.aspx](https://support.managed.com/kb/a1816/how-to-enable-disable-multiple-rdp-sessions-in-windows-2012.aspx).

### \[vServer] How do I rollback the server if it is infected with a virus?&#x20;

You can use the Backup Server feature on our homepage to perform a Server rollback.

### \[vServer] Why did my server renewal payment via Zalopay deduct the money but the account has not been renewed?&#x20;

Please note that if you make a payment, do not close the browser to avoid errors.

### \[vServer] How do I check the disk read speed IOPS on the server after upgrading?&#x20;

You can refer to the following links for checking:

&#x20;For Linux operating system:

&#x20;[https://arstech.net/how-to-measure-disk-performance-iops-with-fio-in-linux/](https://arstech.net/how-to-measure-disk-performance-iops-with-fio-in-linux/)&#x20;

For Windows operating system:

&#x20;[https://blog.sqlterritory.com/2018/03/27/how-to-use-diskspd-to-check-io-subsystem-performance/](https://blog.sqlterritory.com/2018/03/27/how-to-use-diskspd-to-check-io-subsystem-performance/)

### \[vServer] How do I change the OTP receiving phone number?&#x20;

You can log in to the portal and select to change the phone number: [https://register.vngcloud.vn/changephonenumber?hl=vi](https://register.vngcloud.vn/changephonenumber?hl=vi)

### \[vServer] Mounting a volume into vServer displays sdc but shows sdb on the web portal.&#x20;

Attach, Detach twice, so the system recognizes it as sdc. Detach and Attach again, then it becomes sdd. If you want to return to sdb: detach the volume -> reboot -> attach.

### \[vServer] Mounting a volume into vServer Windows shows offline.&#x20;

**Method 1:** Open disk management, right-click the offline disk and select online, then right-click to Initialize Disk, select GPT and click OK, then you can create a partition.&#x20;

**Method 2**: Access Server Manager\File and Storage Services\Volumes\Disks and turn it online, then initialize the disk.

### \[vServer] Information about chip and clock speed of High Performance vServer package.&#x20;

Currently, we support 2 types of chip for High Performance vServer:&#x20;

* Intel(R) Xeon(R) Gold 6242 CPU @ 2.80GHz&#x20;
* Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz

### \[vServer] Why does my Windows server RDP report account password has expired?&#x20;

Please log in to the console interface to change the password, then you can use RDP.

### \[vServer] How do I split vServer into another portal account?&#x20;

Currently, VNG Cloud does not support splitting servers into another portal.

### \[vServer] Why does it report unable to access the server if I mistakenly switch farms?&#x20;

You can try to access the server again. If the error still persists, please send a bug report to us through the <mark style="color:blue;">Support page</mark>.

