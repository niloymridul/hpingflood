<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/8b3d4817-cd74-487a-af67-5bf76cb7fe41" height="40%" width="40%" alt="Hping3 logo"/>
</p>

<h1>Hping3 - Packet Flooding</h1>
This tutorial details the steps of using and understanding packet-flooding software. <br />

<h2>Environments & Softwares Used</h2>

- VirtualBox (Virtual Machines/Computer)
- Kali Linux
- Windows 10
- Nmap
- Hping3
  
<h2>Project Steps</h2>
<p>
If you remember from our last tutorial, we installed the virtual machine software called VirtualBox Manager and set up two virtual machines for both Kali Linux and Windows. Now we still have only two things to do before we can actually get into the packet detection setup. 
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/206a2b3f-6670-4d89-b910-5b7d9ea78462" height="80%" width="80%" alt="VMBOX look"/>
</p>

<p>First I want you to open VirtualBox Manager if you haven't yet. Then I want you to click on tools above the named virtual machines. After you click on tools, I want you to click on Nat Networks and then Create. There are various forms of Networks you can make but for this lab, we will want to create NAT Network. The reason why is because this network mode allows us to connect both our host computer and our virtual machines. If you want, you can give it whatever name you want.
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/f9580457-4b8c-4d11-ad12-8d47e1c1aa07" height="80%" width="80%" alt="VMBOX look"/>
</p>

<p>
After that, go to both virtual machines and press the button that says settings because we have to make sure that both virtual machines can connect with each other. You will need to go to settings -> network -> adapter 1 for each virtual machine. Click on the dropdown menu, click on attached to, and click Nat Network. Afterward, you will need to click on the specific nat network that you made and named. Click ok and now the settings should be finalized. Again make sure that you do the same thing for both Virtual Machines!

Now you can finally start and log in to the virtual machines you have finally made. Click on Start for both of them and log in.
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/b2d6bdc1-4f84-4351-9b23-79283af3ddd3" alt="Wireshark logo"/>
</p>

<p>
Now you can finally start and log in to the virtual machines you have finally made. Click on Start for both of them and log in. We will have to install a program called Wireshark on the Windows computer. This will be the last thing we will need to install before we can start packet detection. Click the link below and we will start installing the software.
</p>

[Click here to go to the official download webpage of Wireshark!](https://www.wireshark.org/download.html)

<p>
The reason we use Wireshark is because Wireshark is not only capable of seeing traffic from the one running it but also from other computers running on the network as well. Just click next or noted for the most part unless you want to have a desktop icon then go ahead. Feel free to configure the installation process however you feel. Install npcap and usbpcap if desired as they will be needed to work with Wireshark.
</p>


<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/4e586eda-98b7-433f-82c1-6dc38adfa3d9" alt="Wireshark logo"/>
</p>


<p>
Once it is installed, search for it with the search function when hitting the Windows key or clicking the desktop icon if you had made one. Make sure to run as admin or else the program will give many prompts asking you for admin privileges. Click Ethernet to start capturing packets below the header that says Capture The image below explains what each part of the Wireshark interface does.  
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/fb17a524-9117-4403-9990-681047f9263c" height="80%" width="80%" alt="Wireshark logo"/>
</p>

<p>
There are four parts you want to keep in mind. 
</p>
<h2></h2>

- 1 - This is the filter bar. Type in what you want to see and the interface will filter results to what you desire.
- 2 - This is the packet list area. This display all the packets that were captured in the network and going throughout.
- 3 - This is the packet details panel. This shows all the protocols and the information that comes with it. You can open each protocol up for more details
- 4 - This is the packet bytes panel. This is the panel where all packet data is dumped and shown and decrypted.

<p>
Now what I want you to do is go to the Windows Console and type in ipconfig. The IPV4 address is the IP address of the Windows Virtual Machine. This is to check the IP address of the virtual machine so we can ping it and capture the data being sent.
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/5b2de2f9-9296-4adf-ba62-9c5f1bde7562" height="80%" width="80%" alt="Wireshark logo"/>
</p>


<p>
So with the Windows IP address in mind, we can go to the Kali Linux virtual machine and sign in. We will then have to open the console and type in ping and then the IP address. Seeing as we started to capture from Windows, nothing will happen yet until we hit enter in the Kali Linux virtual machine. 
</p>


<p>
As you can see, a lot of the pings on the Kali Linux side are not going through. The reason why is that the firewall is on. This is reflected on Wireshark as it states no response was found. But you can hit Ctrl and C on the Kali Linux machine to stop pinging. Go ahead and comb through the Windows Wireshark captured packets that it caught on the network.
</p>

<p>
To reinforce the idea that a firewall is effective, we will start to use Nmap. Nmap is also a network scanner but it doesn't come with a interface and is more for security auditing and network scanning. Now do not use this on public or private networks unless you own it or have permission as it is illegal. But for this case, we can.
</p>

<p>
Now Nmap has to be installed in other OS's but for this distro(distribution) of Linux, we can use this immediately as Linux comes preinstalled. Type in the following command with the IP address, hit enter and wait for a minute or two. nmap -p (insert IP address here). 
</p>

<p align="center">
<img src="https://github.com/niloymridul/klmwdetect/assets/139414980/0fcecaa4-308a-4a70-b9b1-7d0f029d7135" height="80%" width="80%" alt="VMBOX look"/>
</p>

<p>
The reason why we are doing this command is to see what ports are open or not on the Windows System. After scanning for a while, you will get a message telling you that the scan wasn't able to do much as it appears as if the host is down and it could not ping probes and will most likely tell you of one open port. In the next and final part of the tutorial, we will discuss what would happen if the firewall is down and if we could flood said network and computer.
</p>


