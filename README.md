<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/8b3d4817-cd74-487a-af67-5bf76cb7fe41" height="20%" width="20%" alt="Hping3 logo"/>
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
Continuing from where we left off, we were stuck at our pings not being able to go through to the Windows Virtual Machine we have. Now, what if we were able to do that because the Windows Firewall was turned off.

Let's go to our Windows Virtual Machine. We are going to turn off Firewall. Now, you may ask why exactly we are turning off our Windows 10 Firewall or what a firewall is. A firewall is an inter-network connection device that prevents and administrated data traffic and data communication inside and between networks. Firewalls, for the everyman, are software installed on computers in order to prevent viruses but they can also be dedicated hardware like switches that have their own software installed and can be connected to the networks themselves physically.
</p>

<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/0b8989d8-73b6-4c71-ae8d-b2884764c879" height="60%" width="60%" alt="Firewall"/>
</p>

<p>
In this case, with VirtualBox Manager we will just simply need for you to turn off the firewall on the Windows Virtual Machine. Click on the Windows Icon in the bottom left and then type in Firewall and click on Windows Defender Firewall. Once you click on it, please go ahead and click on "Turn Windows Defender Firewall on or off" and make sure for both/all networks that the firewall is off.

Now, let's backtrack to our Kali Linux Virtual Machine. I want you to open up the console again if you haven't before. If you use the same Nmap command I had asked you to do, you will get some more information than you had before due to said firewall being down. At least 3 ports have been shown as open. 
</p>

<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/c3c4b1dd-a008-4552-a61c-7ddea0b8831b" height="60%" width="60%" alt="Ping Kali"/>
</p>

<p>
Now, try pinging the Windows IP  address like we had done before and capturing it via Wireshark. As the packets come from we can see two parts of the three-part handshake. We can see the Kali Linux computer sends a packet of requests towards the Windows Computer and in turn, the Windows Computer sends back a reply. And if you look back on the Kali Linux we can see the pings coming back to our console. 
</p>

<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/cecc9a34-3a38-42fa-b947-a6a1b55fc683" alt="3 Way Handshake"/>
</p>

<p>
For reference, the three-way handshake is a method used in networks for computers and servers to establish a connection. The client (us) sends a SYN packet as a way to want to state the client wants to communicate with the server. The server in turn sends a SYN ACK packet to the client stating that it is ready for communication and the client sends the server one last packet called an ACK packet stating that it will begin doing business with the server.
</p>


<p>
With this in mind, we are going to start using hping3. hping3 is a network tool able to send custom data packets whether they be ICMP, UDP, and TCP packets, and is automatically installed in Kali Linux so we do not need to install it. In this case, we are first going to send a packet to one of the ports we had seen open from the scans of Nmap. We are only going to send a few so type in the following command.
sudo hping3 -p (one open port from the previous Nmap scan) (Windows IP Address).

We use sudo because for some commands we need admin privileges which in Linux's case is called sudo rather than admin like how Windows would use. -p is for TCP Push flag which is a data packet used to indicate that the device needs to deliver said data as soon as it can rather than buffering it. This is good for what we are going to do next.

Now, hping3 can be used for malicious purposes if possible. Seeing as we are able to experiment and it's our own network we don't need to ask for permission but if it wasn't, then we would have to, or else we would break the law.
</p>

<p>
Moving on from that, one thing hping3 can do is called a SYN flood. We will be sending a large number of SYN packets to the server or in this case our Windows Computer. To clarify, hping3 sends these packets to the server using spoofed IP addresses causing the server to send SYN-ACK packets to hosts that do not exists. By flooding the server, the server will have to use more CPU and Memory to handle traffic which will lead to the server not being able to serve client requests. This is called a DOS (Denial-of-service) attack.

Simply put, we will need you to type in the following command. 
</p>

<p>
sudo hping3 -c 15000 -d 120 -S -w 64 -p 80 --flood --rand-source (Windows IP address)
</p>


<p align="center">
<img src="https://github.com/niloymridul/hpingflood/assets/139414980/39c574e9-9b35-4f62-a2ef-c7806616dcb3" height="60%" width="60%" alt="Firewall"/>
</p>


<p>
Now I will explain what each of these means:
</p>

<h2></h2>

- 1 - sudo - provide admin privileges so that we can use the command.
- 2 - hping3 - used to tell the console what tool we are using.
- 3 - -c 15000 - We are sending this amount of packets.
- 4 - -d 120 - the size of each packet.
- 5 - -S - the type of flag which in this case is an SYN flag
- 6 - -w 64 - TCP windows size. Don't worry too much about this
- 7 - --rand-source - Generates spoofed IP addresses to disguise the real source and avoid detection
- 8 - --flood - Sends packets as fast as possible


<p>
If you want, you can take a look and open up the resource monitor to see the usage of the CPU, you can see the CPU being used more than it has before. And if you use Wireshark, you can see the flood of TCP packets coming in. This is how hping3 can perform packet flooding. Again, I cannot stress this enough, please do not use this on any other network unless you have permission.
</p>



