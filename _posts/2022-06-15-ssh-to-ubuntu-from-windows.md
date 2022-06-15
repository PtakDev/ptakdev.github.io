---
title: SSH to Ubuntu machine from Windows
date: 2022-06-15 12:45:00 +0100
categories: [Windows, Ubuntu 20.04]
tags: [ssh, powershell]     # TAG names should always be lowercase
---

1.
On the Ubuntu machine, open a terminal and generate private and public keys.
```bash
ssh-keygen -t rsa
```

2.
Now we need to copy public key from Linux to our Windows machine that we will be logging from. 

```powershell
scp id_rsa.pub <UBUNTU_USER>@<IP_UBUNTU>:./ssh/authorized_keys
```

> If it didn't work, you may have to create a id_rsa.pub file in C:\Users\<USER>\.ssh directory.
{: .prompt-warning }


3.
Test the connection.

```powershell
ssh <UBUNTU_USER>@<IP_UBUNTU>
```


##### References: 
[`How to Use SCP Command to Securely Transfer Files`](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/){:target="_blank"}
