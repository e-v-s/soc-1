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
<br>
<li><a href="https://oasis-open.github.io/cti-documentation/taxii/intro">TAXII</a>: defines protocols used to exchange threat intel to detect/prevent/mitigate in real-time
<ul>
<li>Collection</li>
<li>Channel</li>
</ul>
</li>
<br>
<li><a href="https://oasis-open.github.io/cti-documentation/stix/intro">STIX</a>: language for specification, characterisation and communication of std CIT</li>
<br>
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
<br>
<li>The Diamond Model
<ul>
<li>Adversary</li>
<li>Victim</li>
<li>Infra</li>
<li>Capabilities</li>
</ul>
</li>
</ul>

<h2>Threat Intelligence Tools</h2>


<h3><a href="https://urlscan.io/">Urlscan.io</a></h3>
It scans and analyses websites.

<h3><a href="https://abuse.ch/">Abuse.ch</a></h3>
Identifies and track malware and botnets using:<br>
<ul>
<ul>
<li><a href="https://bazaar.abuse.ch/">MalwareBazaar:</a> resource to share malware samples</li>
<li><a href="https://feodotracker.abuse.ch/">FeodoTracker:</a> used to track C2 botnets</li>
<li><a href="https://sslbl.abuse.ch/">SSL Blacklist:</a> ID and detect malicious SSL connections</li>
<li><a href="https://urlhaus.abuse.ch/">URLhaus:</a> malicious URLs used for malware distribution</li>
<li><a href="https://threatfox.abuse.ch/">ThreatFox:</a> IOCs associated with malware</li>
</ul>
</ul>

<h3><a href="https://www.phishtool.com/">PhishTool</a></h3>
<ul>
<ul>
<li>Email analytics from metadata</li>
<li>Heuristic intelligence and OSINT to understand the TTPs used</li>
<li>Classification and reporting</li>
</ul>
<br>
<b>Defang IP address:</b> https://gchq.github.io/CyberChef/
</ul>

<h3><a href="https://talosintelligence.com/">Talos Intelligence</a></h3>


<h1>YARA</h1>
It identifies info based on binary and textual patterns contained within a file.

<h2>How to create rules?</h2>
<ul>
<ul>
<li>Create the file.yar: </li>
We start by adding the condition that the file to be analyzed has to exist first:<br>
    rule exampleRule {<br>
          condition: true<br>
    }<br>
To run the rule we use the following command:<br>
yara file.yar file-to-be-analyzed
<br><br>
<li><a href="https://yara.readthedocs.io/en/stable/writingrules.html">Here</a> we can se more rules</li><br>
<li>Some conditions to know<br>
<b>meta</b> & <b>desc</b> --> these are to add descriptions, it's like commenting a code;<br><br>
<b>strings</b> --> we use this to search for a text or hexadecimal in files or programs, like:<br><br>
rule check_for_helloworld {<br>
    strings:<br>
        $hello_world = "Hello World!"<br>
        $hello_world_lowercase = "hello world"<br>
        $hello_world_uppercase = "HELLO WORLD"<br>
    condition:<br>
        any of them<br>
}<br><br>
We use <b>$</b> to define a variable.<br>
We use <b>condition</b> $hello_world to make the rule valid or if there's a lot of rules we use <b>any of them</b>.<br>
We also can use <b>and</b>, <b>not</b>, <b>or</b>, <b>operators</b> lie <=, >= or !=, ex.: if we want to search files containing "hello world"but with a filesize less than 10Kb, we use:<br>
    <b>condition:<br> any of them and filesize < 10KB</b><br>
![yara_rules](https://github.com/user-attachments/assets/4ad396cc-3aa9-4662-8cde-c3dca50def25)

</li>

</ul>
</ul>





