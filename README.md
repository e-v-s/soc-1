# soc-1
SOC level 1 THM

<h1>Cyber Defence Frameworks</h1>
<h2>MITRE</h2>
<h3>Projects</h3>

- <a href="https://attack.mitre.org/">ATT&CK</a>: <strong>A</strong>dversarial <strong>T</strong>actics, <strong>T</strong>echniques, <strong>&</strong> <strong>C</strong>ommon <stron>K</strong>nowledge

<p>
It's a documentation of common <i>TTPs</i>.<br>
<a href="https://mitre-attack.github.io/attack-navigator">ATT&CK Navigator for Carbanak.</a>
</p>

- CAR: <strong>C</strong>yber <strong>A</strong>nalytics <strong>R</strong>epository Knowledge Base

<p>
   Provides a set of validated and well-explained analytics.<br>
   <a href="https://mitre-attack.github.io/attack-navigator/">CAR navigator layer</a>
</p>

- <a href="https://d3fend.mitre.org/">ENGAGE</a>: It's a framework for planning and discussing adversary engagement operations. <a href="https://engage.mitre.org/starter-kit/">Starter kit</a>

- D3FEND: <b>D</b>etection, <b>D</b>enial, and <b>D</b>isruption <b>F</b>ramework <b>E</b>mpowering <b>N</b>etwork <b>D</b>efense

<p>
It's a graph of countermeasures. Provides the definition, how it works, considerations and how to use the technique.
</p>

- <a href="https://mitre-engenuity.org/">AEP</a>: <b>A</b>TT&CK <b>E</b>mulation <b>P</b>lans

<p>
These are a step-by-tep guide on how to mimic the specific threat group. <a href="https://github.com/center-for-threat-informed-defense/adversary_emulation_library">Emulation plan lib</a>
</p>

<b>Tactics</b>: goal
<b>Technique</b>: how to achieve the goal
<b>Procedure</b>: how the technique is executed

<h3>ATT&CK and Threat intelligence</h3>

The goal of threat intelligence is to make the TTPs actionable.

The main idea is to gather information about common threats aimed to a particular case scenario on your organization, so you can plan ahead.



<h2>Summit</h2>
<h3>Applying the concepts of the Pyramid of Pain</h3>

<h4>Hash values</h4>
<p>
It's used to identify a malicious artifact. You can upload the file on <a href="https://www.virustotal.com/gui/">virus total</a>, analyze and block it from being executed.<br><br>
<b>The problem:</b> if the attacker knows you blocked the hash of the malware they can recompile it.
</p>

<h4>IP Address</h4>

<p>
If the <i>threat actor</i> changes its malware to evade the hash from being blocked, you cannot evade it by analyzing each file that infects your device. It's better to move on and <b>deny</b>, <b>block</b> or <b>drop</b> inbound requests from malicious IP related to the execution of the malware.<br><br>
By analyzing it with the virustotal tool we can see if there are any <b>GET</b> requests being made by the malware and then block this IP.<br><br>
The block is made on the firewall level (as it's an application layer request).<br><br>
<b>The problem:</b> The attacker can use <a href="https://en.wikipedia.org/wiki/Fast_flux">Fast Flux</a> to hide its <i>comman and control server</i> (C&C).
</p>

<h4>Domain names</h4>

<p>
Supposing the attacker changed his IP, you have to deal with this by blocking the domain/sub-domain, because changing the IP address is easy, but changing the DNS is a pain in the ass.<br><br>
<b>We can create a DNS rule to block the domain/sub-domain.</b><br><br>
We can see in the sandbox the communications made by the malware:<br>
<ul>
<li>HTTP GET requests</li>
<li>Connections</li>
<li>DNS requests (they use it to see if there's internet connectivity, if it hasn't then it's useless)</li>
</ul>

<b>The problem:</b> the attacker can go forward with it, by a new domain and hide the DNS records.<br><br>
<i>Punycode</i>: changing the name of a domain to look legit.<br><br>
Also, attackers use url shorteners to hide malicious url. But you can see to where it redirects by appending <b>+</b> at the and of the tiny.url, bit.ly and goo.gl.
</p>

<h4>Host artifacts</h4>

<p>
These are traces of the malwere on the system to evade the monitoring of the system for example, like:<br>

<ul>
<li>Registry values</li>
<li>Process execution</li>
<li>IOC</li>
<li>Files dropped</li>
</ul>


In this case we search for something related to the malware and create a sigma rule related to the artifact and blocking the malware.
</p>

<h4>Network Artifacts</h4>

<p>
If we can block the malware by detecting the <i>host artifacts</i>, then the attacker has to change his approach (tactics and tools). Network artifacts can be:<br>

<ul>
<li>User-agent strings</li>
<li>C2 information</li>
<li>URI patterns followed by HTTP POST resquest</li>
</ul>


We detect them in <b>Wireshark</b> PCAPs by using <b>network protocol analyzers</b> such as <i>TShark</i> or by exploring <b>IDS logging</b> using <i>Snort</i>. We block them by creating a sigma rule to block outgoing connections related to the malware.
</p>

<h4>Tools</h4>

<p>
At this point the attacker would let it go. But if not, he/she would have to change his/her tool and create maldocs. At this stage we should use <i>antivirus signatures</i>, <i>detection rules</i> and <i>YARA rules</i>.

Tools: malwareBazaar, Malshare, SOC prime threat detection marketplace (this one is to create rules for =/= threats that are around).
</p>
</ul>


<b>addendum</b>: <a href="https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack">pass-the-hash attacks</a>

<h1>Cyber Threat Intelligence</h1>

<h2>CIT</h2>

<ul>
<li>Data: discrete indicators. Ex.: IP, urls, hashes</li>
<li>Information: combination of data that answers something</li>
<li>Intelligence: correlation of <i>data</i> and <i>information</i></li>
</ul>

The objective of CIT is to have the following:

<ul>
<li>Who?</li>
<li>Motivations</li>
<li>Capabilities</li>
<li>Artifacts and IOC should you look for</li>
</ul>

<h3>Threat Intel Classification</h3>

<ul>
<li>Strategic</li>
<li><b>Technical:</b> evidence and artefacts</li>
<li><b>Tactical:</b> assesses TTPs and addresses vulnerabilities thru real-time investigation</li>
<li><b>Operational:</b> looks into the motives and critical assets that are the objective of the adversary</li>
</ul>

<h3>CTI Lifecycle</h3>

<ol>
<li><b>Direction:</b> objective and goals based on:
<ul>
<li>Assets and business information that require defending</li>
<li>Impact</li>
<li>Srcs of data/intel that can be used to mitigate</li>
<li>Tools and resources required to defend the assets</li>
</ul>


<li><b>Collection:</b> Automate the collection of data to address the objectives</li>

<li><b>Processign:</b> Extraction, sorting, organization, tagging and graphing of the information gathered from logs, malware detection, network traffic, etc.</li>


<li><b>Analysis:</b> Insights and decisions to be made</li>


<li><b>Dissemination:</b> By the stakeholders</li>


<li><b>Feedback:</b> Between analysts and stakeholders about the implementation of security controls</li>
</ol>


<h3>CTI Stds & Frameworks</h3>

<ul>
<li>MITRE ATT&CK</li>


<li><a href="https://oasis-open.github.io/cti-documentation/taxii/intro">TAXII</a>: defines protocols used to exchange threat intel to detect/prevent/mitigate in real-time
<ul>
<li>Collection</li>
<li>Channel</li>
</ul>
</li>


<li><a href="https://oasis-open.github.io/cti-documentation/stix/intro">STIX</a>: language for specification, characterisation and communication of std CIT</li>


<li>Cyber Kill Chain: helps to identify the stage of the attack
<ul>
<li>Recon: OSINT, social media, network scans, emails</li>
<li>Weaponisation: using a malware based on intentions</li>
<li>Delivery: how the malware is sent</li>
<li>Exploitation: establish persistance</li>
<li>Installation: install malware and tools to gain access</li>
<li>C2: control remotely, lateral movement, elevate privileges</li>
<li>Actions on objectives</li>
</ul>
</li>

<li>The Diamond Model
<ul>
<li>Adversary</li>
<li>Victim</li>
<li>Infra</li>
<li>Capabilities</li>
</ul>
</li>
</ul>

<h2>Threat Intelligencec Tools</h2>
