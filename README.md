# soc-1
SOC level 1 THM

<h1>MITRE</h1>
<h2>Projects</h2>

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

<h2>ATT&CK and Threat intelligence</h2>

The goal of threat intelligence is to make the TTPs actionable.

The main idea is to gather information about common threats aimed to a particular case scenario on your organization, so you can plan ahead.



<h1>Summit</h1>
<h2>Applying the concepts of the Pyramid of Pain</h2>

<ul>
<li>Hash values</li>

<p>
It's used to identify a malicious artifact. You can upload the file on <a href="https://www.virustotal.com/gui/">virus total</a>, analyze and block it from being executed.<br>
<b>The problem:</b> if the attacker knows you blocked the hash of the malware they can recompile it.
 </p>

<li>IP Address</li>

<p>
If the <i>threat actor</i> changes its malware to evade the hash from being blocked, you cannot evade it by analyzing each file that infects your device. It's better to move on and <b>deny</b>, <b>block</b> or <b>drop</b> inbound requests from malicious IP related to the execution of the malware.<br>
By analyzing it with the virustotal tool we can see if there are any <b>GET</b> requests being made by the malware and then block this IP.<br>
The block is made on the firewall level (as it's an application layer request).<br>
<b>The problem:</b> The attacker can use <a href="https://en.wikipedia.org/wiki/Fast_flux">Fast Flux</a> to hide its <i>comman and control server</i> (C&C).
</p>

<li>Domain names</li>

<p>
Supposing the attacker changed his IP, you have to deal with this by blocking the domain/sub-domain, because changing the IP address is easy, but changing the DNS is a pain in the ass.<br>
<b>We can create a DNS rule to block the domain/sub-domain.</b><br>
We can see in the sandbox the communications made by the malware:<br>
HTTP GET requests<br>
Connections<br>
DNS requests (they use it to see if there's internet connectivity, if it hasn't then it's useless)<br>
<b>The problem:</b> the attacker can go forward with it, by a new domain and hide the DNS records.<br>
<i>Punycode</i>: changing the name of a domain to look legit.<br>
Also, attackers use url shorteners to hide malicious url. But you can see to where it redirects by appending <b>+</b> at the and of the tiny.url, bit.ly and goo.gl.
</p>

<li>Host artifacts</li>

<p>
These are traces of the malwere on the system to evade the monitoring of the system for example, like:<br>

<i>Registry values</i>

<i>Process execution</i>

<i>IOC</i>

<i>Files dropped</i>

In this case we search for something related to the malware and create a sigma rule related to the artifact and blocking the malware.
</p>

<li>Network Artifacts</li>

<p>
If we can block the malware by detecting the <i>host artifacts</i>, then the attacker has to change his approach (tactics and tools). Network artifacts can be:<br>

<i>User-agent strings</i>

<i>C2 information</i>

<i>URI patterns followed by HTTP POST resquests</i>

We detect them in <b>Wireshark</b> PCAPs by using <b>network protocol analyzers</b> such as <i>TShark</i> or by exploring <b>IDS logging</b> using <i>Snort</i>. We block them by creating a sigma rule to block outgoing connections related to the malware.
</p>

<li>Tools</li>

<p>
At this point the attacker would let it go. But if not, he/she would have to change his/her tool and create maldocs. At this stage we should use <i>antivirus signatures</i>, <i>detection rules</i> and <i>YARA rules</i>.

Tools: malwareBazaar, Malshare, SOC prime threat detection marketplace (this one is to create rules for =/= threats that are around).
</p>
</ul>




