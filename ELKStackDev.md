UNIT 13 PROJECT SUBMISSION
- A new vNet located in the same resource group.

![Screenshot of Original VM](Pictures/createVN.png)

- Create a Peer connection between vNets. Allows traffic to pass between vNets and regions. Makes both a connection from the first vNet to the Second vNet _And_ a reverse connection from the second vNet back to the first vNet, allowing traffic to pass in both directions.

![Screenshot of Add Peering](Pictures/AddPeering.png)

- Select vNet and view 'Peerings'.
- Create a new Peerings named Elk-to-Red
- RedTeam vNet in the dropdown labeled 'Virtual Network'.
- Named the resulting connection from  RedTeam Vnet to Elk vNet. "Red-to-Elk" 
- All other settings at their defaults

 
 
 

### 2. Creating a New VM
Created a new virtual machine to run ELK.

![Screenshot of Add Peering](Pictures/CreatingNewVN1.png)
![Screenshot of Add Peering](Pictures/CreatingNewVM2.png)
 
(public key
(ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDVhGkoToPcxT696ubUk95xm4V5kDXhg451dOrYkKr2hiZR+mHY6vMOJvgm+Hu8FpdR4CJ7CKOH1UcJm6C/JiaGJe3EvCOsfr6wf/RytpQ9R1wZpjAZorCCRLOBjpV5Bj/+4fP0VXro0KG+nghe1eG3kxWYX/a6Q+XjY2/bqsmqDsgNHuHsLZVEDvukO10BTOfvX5Y70LS6sfA0dQX+Feq/Yxhbb8AzUlOg6kYleCRfq57dTeXm5a9qUxg+MjMbewoVIcYb/8GRtizQe3y9inBpopBpR3sJMeB0wcH76T4uzEJdbzkhHzw+u/pgjUxxerlsYK/XwnS3UEFI0fxzyeOB root@81ba418706b6)

![Screenshot of Add Peering](Pictures/jumpboxprovisioner576.png)
SSH into Jump-Box

![Screenshot of Add Peering](Pictures/SSH1.png)
![Screenshot of Add Peering](Pictures/SSH2.png)

- Check for your Ansible container:
- Locate the container name:
  ```bash
  sysadmin@Jump-Box-Provisioner:~$ sudo docker container list -a


  ```
 
- Start the container:
  ```
 
- Connect to the Ansible container:
  ```
 
 
 

- Copy the SSH key from the Ansible container on your jump box:
cat ~/.ssh/id_rsa.pub

 
(public key)
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDVhGkoToPcxT696ubUk95xm4V5kDXhg451dOrYkKr2hiZR+mHY6vMOJvgm+Hu8FpdR4CJ7CKOH1UcJm6C/JiaGJe3EvCOsfr6wf/RytpQ9R1wZpjAZorCCRLOBjpV5Bj/+4fP0VXro0KG+nghe1eG3kxWYX/a6Q+XjY2/bqsmqDsgNHuHsLZVEDvukO10BTOfvX5Y70LS6sfA0dQX+Feq/Yxhbb8AzUlOg6kYleCRfq57dTeXm5a9qUxg+MjMbewoVIcYb/8GRtizQe3y9inBpopBpR3sJMeB0wcH76T4uzEJdbzkhHzw+u/pgjUxxerlsYK/XwnS3UEFI0fxzyeOB root@81ba418706b6)


INSERT THIS PUBLIC KEY INTO YOUR NEW AZURE WM PASSWORDS & update
 

Make sure you can ssh into your vm
 
Exit out of this

Configure a new VM using that SSH key.
    - Make sure this VM has at least 4 GB of RAM.
    - Make sure it has a public IP address.
    - Make sure it is added to your new vNet (ELK_VN) and create a new Security Group for it.

#### 3. Downloading and Configuring the Container
In this step, you had to:
- Add your new VM to the Ansible `hosts` file.
 
 
The IP address is the VMs private ip.
Save this
 

- Create a new Ansible playbook to use for your new ELK virtual machine.
    - The header of the Ansible playbook can specify a different group of machines as well as a different remote user (in case you did not use the same admin name):


 

DOUBLE CHECK YOU ELK.YML TO MAKE SURE THERE ARE NO SPELLING ERRORS AND YOU HOSTS AND REMOTE USER ARE CORRECT
 

     

NOW RUN THE ANSIBLE-PLAYBOOK /ETC/ANSIBLE/ELK.YML
 
 


    - Before you can run the elk container, we need to increase the memory:

 
NEW PUBLIC KEY
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQHuEhReRo8KGb5r6u6NPwd9VG2gbSvZlCBzZv0gOdCnsTe5tQFOVhYPFiD6Jt2h4VDe/sG2EDt0whEGV5HhGtYbwIOkeVna1oeu5DFryyqUt3TEZz8tZY85MFLurrMnLth1UIdL/ikUz9aIMzeO/0Olr0KaGbejJyv5X0T7cEB4KkYBIySS0GIEAUWyCfl67KZZFHiWxnE2OFMEstneGd4FE/rz4QZuExJ3dlR3m6cuuNb9LQl96e3WVN0gHsim1xPrt9w/LQCpbpVXB3v4d10D7m/LHSYLUsD9Kofa1Mo8/2djQrY11JHRwM1MBBhvCm7NgYcOev6c4I9rCt9Rgb)
 
Use command <sysctl vw.max_map_count> to check current memory status
 
Use command <sysctl -w vm.max_map_count=262144> to increase memory
 

-	This is a system requirement for the ELK container. More info [at the `elk-docker` documentation](https://elk-docker.readthedocs.io/#prerequisites).

#### 4. Launching and Exposing the Container 
After Docker is installed, download and run the `sebp/elk:761` container.
  - The container should be started with these published ports:
    - `5601:5601` 
    - `9200:9200`
    - `5044:5044`
Your Ansible output should resemble the output below and not contain any errors:
NOW RUN THE ANSIBLE-PLAYBOOK /ETC/ANSIBLE/ELK.YML
Command <ansible-playbook /etc/ansible/elk.yml>
 

- SSH from your Ansible container to your ELK machine to verify the connection before you run your playbook.
- After the ELK container is installed, SSH to your container and double check that your `elk-docker` container is running.
Run `sudo docker ps`



 
#### 5. Identity and Access Management
 
This ELK web server runs on port `5601`. Create an incoming rule for your security group that allows TCP traffic over port `5601` from your IP address.
 

 
Verify that you can load the ELK stack server from your browser at `http://[your.VM.IP]:5601/app/kibana`. 
(NOTE, THE IP ADDRESS CHANGES EACH TIME YOU START THE VM IN AZURE)

## Day 2 Solution Guide: Filebeat Installation 
### 1. Installing Filebeat on the DVWA Container
First, make sure that our ELK server container is up and running.
- Navigate to http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created.
 


  - Run `docker container list -a` to verify that the container is on.
  - If it isn't, run `docker start elk`.
 

Install Filebeat on your DVWA VM:
- Open your ELK server homepage.
    - Click on **Add Log Data**.
 
    - Choose **System Logs**.
 
    - Click on the **DEB** tab under **Getting Started** to view the correct Linux Filebeat installation instructions.
 

### 2. Creating the Filebeat Configuration File
Next, create a Filebeat configuration file and edit this file so that it has the correct settings to work with your ELK server.
Open a terminal and SSH into your jump box:

 
Copy the provided configuration file for Filebeat to your Ansible container: [Filebeat Configuration File Template](config_files/filebeat-config.yml).

(FIRST -make the director)
 

- Run: `curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml`
 
 

 

Once you have this file on your Ansible container, edit this file as specified in the Filebeat instructions (the specific steps are also detailed below). 
•	Edit the configuration in this file to match the settings described in the installation instructions for your server.
-	**Hint:** Instead of using Ansible to edit individual lines in the `/etc/filebeat/filebeat-config.yml` configuration file, it is easier to keep a copy of the entire configuration file (preconfigured) with your Ansible playbook and use the Ansible `copy` module to copy the preconfigured file into place.
-	Because we are connecting your webVM's to the ELK server, we need to edit the file to include your ELK server's IP address. 
-	Note that the default credentials are `elastic:changeme` and should not be changed at this step.
•	Scroll to line #1106 and replace the IP address with the IP address of your ELK machine.
-	NANO INTO THE FILEBEAT-CONFIG.YML FILE TO EDIT”
-	*ATL G* TO SEARCH BY LINE
```bash
output.elasticsearch:
hosts: ["10.1.0.4:9200"]
username: "elastic"
password: "changeme"
```
 
•	Scroll to line #1806 and replace the IP address with the IP address of your ELK machine.
```
setup.kibana:
host: "10.1.0.4:5601"
```
Save this file in  `/etc/ansible/files/filebeat-config.yml`.
o	*CONTROL O*
o	*CONTROL X* TO SAVE

•	After you have edited the file, your settings 1806should resemble the below. Your IP address may be different, but all other settings should be the same, including ports.
  ```
  output.elasticsearch:
  hosts: ["10.1.0.4:9200"]
  username: "elastic"
  password: "changeme"
  ...
  setup.kibana:
  host: "10.1.0.4:5601"
  ```
 

 


### 3. Creating the Filebeat Installation Play
Create another Ansible playbook that accomplishes the Linux Filebeat installation instructions.
-	The playbook should:
o	Download the `.deb` file from [artifacts.elastic.co](https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb).
  - Install the `.deb` file using the `dpkg` command shown below:
	`dpkg -i filebeat-7.4.0-amd64.deb`
o	Copy the Filebeat configuration file from your Ansible container to your WebVM's where you just installed Filebeat.
o	You can use the Ansible module `copy` to copy the entire configuration file into the correct place.
o	You will need to place the configuration file in a directory called `files` in your Ansible directory.
-	Run the `filebeat modules enable system` command.
-	Run the `filebeat setup` command.
-	Run the `service metricbeat start` command.
-	Solution:
- [Filebeat Installation Play](config_files/filebeat-playbook.yml)
- After entering your information into the Filebeat configuration file and Ansible playbook, you should have run: `ansible-playbook filebeat-playbook.yml`.

-	Fyi – new puclic key created for web 1 and web 2 with username sysadmin
o	ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDVhGkoToPcxT696ubUk95xm4V5kDXhg451dOrYkKr2hiZR+mHY6vMOJvgm+Hu8FpdR4CJ7CKOH1UcJm6C/JiaGJe3EvCOsfr6wf/RytpQ9R1wZpjAZorCCRLOBjpV5Bj/+4fP0VXro0KG+nghe1eG3kxWYX/a6Q+XjY2/bqsmqDsgNHuHsLZVEDvukO10BTOfvX5Y70LS6sfA0dQX+Feq/Yxhbb8AzUlOg6kYleCRfq57dTeXm5a9qUxg+MjMbewoVIcYb/8GRtizQe3y9inBpopBpR3sJMeB0wcH76T4uzEJdbzkhHzw+u/pgjUxxerlsYK/XwnS3UEFI0fxzyeOB
 
 


### 4. Verifying Installation and Playbook 
Next, you needed to confirm that the ELK stack was receiving logs. Navigate back to the Filebeat installation page on the ELK server GUI.
- Verify that your playbook is completing Steps 1-4.
- On the same page, scroll to **Step 5: Module Status** and click **Check Data**.
o	Scroll to the bottom and click on **Verify Incoming Data**.
-	Solution:
-	If the ELK stack was successfully receiving logs, you would have seen: 
-	![](Images/data_success.png)

-	 






 


 
