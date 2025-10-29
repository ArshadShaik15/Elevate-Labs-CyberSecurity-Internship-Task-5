# Elevate-Labs-CyberSecurity-Internship-Task-5

<br>

### Task 5 : Capture And Analyze Network Traffic Using Wireshark

<br>

### 🎯 Objective:

The primary goal of this task is to capture live network packets using **Wireshark** and practice identifying fundamental **protocols** and analyzing different types of network traffic.<br>
<br>
<br>

### 🛠️ Lab Setup: <br><br>
### Wireshark:
<p align="left">• If you are using a Windows machine without a virtual machine (VM), you can directly download <strong>Wireshark</strong> to complete this task.</p>
<p align="left">•	Official Website: Navigate to the Wireshark download page https://www.wireshark.org/download.html <br> </p>

### Kali Linux:
• I have used <strong>Kali Linux Virtual Machine (VM)</strong> for this task as it provides a safe environment.<br>
<br>
<br>

### Step-1: Start Capturing On Your Active Network Interface<br>

<br>  <img width="1919" height="1067" alt="image" src="https://github.com/user-attachments/assets/b70217f7-36da-470a-8dbb-8cd4d5438667" />  <br>

<p align="left">• In the Kali VM, the <strong>'eth0'</strong> interface was selected, as indicated by the active packet flow visible during the test phase.</p><br>
<br>

### Step-2: Browse A Website Or Ping A Server To Generate Traffic<br>

<p align="left">• To ensure a variety of protocols, browsing a secure site (Generates DNS, TCP, QUIC, and TLS traffic) is necessary.</p>
<p align="left">• So i decided to run <strong>Youtube</strong> in the dedicated browser - <strong>Mozilla Firefox</strong> in Kali Linux VM</p><br>
<br>

### Step 3: Stop Capture After A Minute<br>

• The capture was stopped by clicking the **"red square stop button"** in the Wireshark toolbar.<br>
<br>
<br>

### Step 4: Filtering The Captured Packets By Protocol<br>
<p align="left">• Display filters are used to isolate traffic for analysis. To view packets of each protocol seperately, simply type the protocol name in the display filter above.</p>
<p align="left">• To view a set of identified protocols simultaneously, type <strong>dns || http || quic</strong> in the display filter above.</p>
<br>
<br>

### Step 5: Identify The Different Protocols In The Capture<br>
<br>

<p align="left"><strong>1. DNS (Domain Name System)</strong><br>
  
<br>  <img width="1919" height="1199" alt="Screenshot 2025-10-27 144126" src="https://github.com/user-attachments/assets/0f87dfdb-a7c9-4afb-90fd-aec65b1608a1" />  <br>

• Protocol        -  DNS (Domain Name System)<br>
• OSI Layer       -  Application Layer (Layer 7)<br>
• Transport Type  -  Uses UDP<br>
• Port            -  UDP Port 53<br>
• Function        -  Translates <strong>youtube.com</strong> into the numerical <strong>IP address</strong> required to initiate any connection.</p><br>

<p align="left"><strong>2. HTTP/2 (Hyper Text Transfer Protocol)</strong><br>
  
<br>  <img width="1919" height="1199" alt="Screenshot 2025-10-27 161702" src="https://github.com/user-attachments/assets/5274a0f0-2730-470b-8609-9e4612c3501b" />  <br>

  
• Protocol        -  HTTP/2 (Hyper Text Transfer Protocol)<br>
• OSI Layer       -  Application Layer (Layer 7)<br>
• Transport Type  -  Runs over TLS<br>
• Port            -  Port 443<br>
• Function        -  The application protocol used to request and receive the main webpage content and resources.</p>

<p align="left">Now, you must be wondering why there is one more protocol named <strong>OSCP</strong> showing when i typed only <strong>HTTP</strong> on the display filter?</p>
<p align="left">Well, that is because OCSP often uses HTTP as its carrier protocol. OCSP (Online Certificate Status Protocol) is a small, essential security check that happens during the initial HTTPS setup. Before the browser trusts a site's security certificate, it sends a quick request to verify that the certificate hasn't been revoked. So, when you type http into the Wireshark filter:<br>
  
1.  It shows the primary HTTP content requests (or the faster HTTP/2 requests).<br>
2.  It also shows any other tiny pieces of traffic that used HTTP as their transport method, like the OCSP status check.</p><br>

<p align="left"><strong>3. TCP (Transmission Control Protocol)</strong><br>
  
<br>  <img width="1919" height="1199" alt="Screenshot 2025-10-27 144935" src="https://github.com/user-attachments/assets/d037fa74-2b00-4919-8070-601d1b3f85e9" />  <br>

  
• Protocol        -  TCP (Transmission Control Protocol)<br>
• OSI Layer       -  Transport Layer (Layer 4)<br>
• Transport Type  -  Uses TCP<br>
• Port            -  Varies (eg: TCP Port 443)<br>
• Function        -  Establishes the reliable, ordered connection used for initial communication, typically followed immediately by TLS.</p><br>

<p align="left"><strong>4. TLS (Transport Layer Security)</strong><br>
  
<br>  <img width="1919" height="1199" alt="Screenshot 2025-10-27 161750" src="https://github.com/user-attachments/assets/b8d2586a-8d5c-40b4-8f60-b305888e01eb" />  <br>

  
• Protocol        -  TLS (Transport Layer Security)<br>
• OSI Layer       -  Presentation Layer (Layer 6)<br>
• Transport Type  -  Runs over TCP/QUIC<br>
• Port            -  Port 443<br>
• Function        -  The security layer that encrypts all browsing and streaming traffic (HTTPS) to ensure privacy.</p><br>

<p align="left"><strong>5. UDP (User Datagram Protocol)</strong><br>
  
<br>  <img width="1919" height="1199" alt="Screenshot 2025-10-27 144813" src="https://github.com/user-attachments/assets/e9128cfb-fa7a-45f7-9f91-38736dd511c7" />  <br>

  
• Protocol        -  QUIC (Quick UDP Internet Connections)<br>
• OSI Layer       -  Application/Transport Layer (Layer 4)<br>
• Transport Type  -  Uses UDP<br>
• Port            -  UDP Port 443<br>
• Function        -  The modern protocol used by Google/YouTube for fast, low-latency video streaming, leveraging UDP for speed.</p>
<br>
<br>

### Step 6: Export the capture as a .pcap file<br>

<p align="left">• The capture was saved using <strong>"File"</stron> $\rightarrow$ <strong>"Save As..."</strong> and exported to the host machine via a configured shared folder.</strong>p>
<p align="left">• I have attached the pcap file for your reference.</p><br>
<br>

### 📝 Summarizing The Findings and Packet Details<br>

<p align="left">The capture demonstrates the complexity of modern encrypted communication: the client first uses DNS (over UDP) for resolution, then utilizes TCP/TLS for security setup. For high-speed data transfer (like video), the connection shifts to the QUIC protocol (also over UDP), carrying the HTTP/2 application data securely and efficiently.</p>

### Wireshark Packet Capture Analysis:

| Field | Detail | Purpose |
|--------|---------|--------------------|
| **Packet No.** | 188 | The sequence number in the live capture file. |
| **Time** | 2025-10-27  13:18:31.45 | The time (in seconds) that passed since the capture started. |
| **Source IP** |10.0.2.15 | The client machine receiving the video stream. |
| **Destination IP** | 142.251.221.174 | The public IP address of the server sending the video content. |
| **Source Port** | 53716 | The temporary, dynamically assigned port on your Kali VM. |
| **Destination Port** | **443** | The standard, well-known port for secure web traffic (HTTPS/QUIC). |
| **Protocol** | **QUIC** | The protocol used for encrypted, low-latency streaming. |
| **Info** | Protected Payload (KP0), DCID=9f1b08 | Shows the state of the QUIC stream delivering the video content. |
<br>
<br>

### Conclusion:

<p align="left">This task successfully fulfilled all requirements by capturing live network traffic using Wireshark within a Kali Linux VM, thereby meeting the objective of hands-on packet analysis. The generated capture file (pcap) was analyzed to identify and document five distinct protocols namely, DNS, TCP, TLS, HTTP/2, and QUIC demonstrating a clear understanding of how modern, secure web traffic operates from initial resolution to encrypted video streaming. In total, the task confirmed proficiency in using a network analysis tool, interpreting fundamental network layers, and demonstrating essential analyzing skills.</p>
<br>
