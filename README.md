# In ansible master

  ## Ansible installation 
  In Centos (Ansible master) make sure ansible installed, if not follow below steps 

  - yum update -y
  - sudo pip install ansible  
  - verify the ansible installation by running  ```ansible localhost -m ping```

  ## define the Windows host or system on a host file on the Ansible control node

  - vim /etc/ansible/hosts

  - copy below content to hosts file by changing required things as your (host ip, windows user_name and windows password) 

        [winhost]
        Ip_address  #change this to your windows ip 

        [winhost:vars]
        ansible_user=user_name     #windows username 
        ansible_password=********   #windows password 
        ansible_connection=winrm
        ansible_winrm_server_cert_validation=ignore

  ## Unlike in Unix systems where Ansible uses SSH to communicate with remote hosts, with Windows it’s a different story altogether. To communicate with Windows hosts, you need to install Winrm.

  -  pip install pywinrm

# Configuring Windows Node

 prerequisite
 
- Your Windows host system should be Windows 7 or later. For Servers, ensure that you are using Windows Server 2008 and later versions.
- Ensure your system is running .NET Framework 4.0 and later.
- Windows PowerShell should be Version 3.0 & later

## Download the WinRM script on Windows 10 host
- WinRM can be installed using a script that you can download from this https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1. Copy the entire script and paste it onto the notepad editor. Thereafter, ensure you save the WinRM script at the most convenient location. In our case, we have saved the file on the Desktop under the name  ConfigureRemotingForAnsible.ps1
- Run the WinRM script on Windows 10 host

      Navigate to the script location and run it. In this case, we have navigated to the Desktop location where we saved the script. Next, proceed and execute the WinRM script on the WIndows host:
      
      .\ConfigureRemotingForAnsible.ps1

![Run-PowerShell-as-Administrator](https://user-images.githubusercontent.com/29688323/81408838-979e3200-915b-11ea-8682-ebc9dc4ff69f.jpg)
      
      This takes about a minute and you should get the output shown below. The output shows that WinRM has successfully been installed.
      
      
![set-up-WinRM-on-Windows10](https://user-images.githubusercontent.com/29688323/81408784-7a696380-915b-11ea-85a4-03de412c8e81.jpg)   

## Connecting to Windows Node from Ansible Control Node

- To test connectivity to the Windows 10 host, run the command: ``` ansible winhost -m win_ping ```

below should be the output 

![Ansible-ping-windows-host-machine](https://user-images.githubusercontent.com/29688323/81409047-ffed1380-915b-11ea-9aff-d5092d3f1814.jpg)

