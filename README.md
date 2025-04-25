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

    <p>
        The goal of threat intelligence is to make the TTPs actionable.<br>
        The main idea is to gather information about common threats aimed to a particular case scenario on your organization, so you can plan ahead.
    </p>


<h1>Summit</h1>
<h2>Applying the concepts of the Pyramid of Pain</h2>

- Hash Values

<ul>
    <li>
        Hash values
    </li>
    <p>
        It's used to identify a malicious artifact. You can upload the file on <a href="https://www.virustotal.com/gui/">virus total</a>, analyze and block it from being executed.<br>
        <b>The problem:</b> if the attacker knows you blocked the hash of the malware they can recompile it.
     </p>
    <li>
        IP Address
    </li>
    <p>
        If the <i>threat actor</i> changes its malware to evade the hash from being blocked, you cannot evade it by analyzing each file that infects your device. It's better to move on and <b>deny</b>, <b>block</b> or <b>drop</b> inbound requests from malicious IP related to the execution of the malware.<br>
        By analyzing it with the virustotal tool we can see if there are any <b>GET</b> requests being made by the malware and then block this IP.<br>
        The block is made on the firewall level (as it's an application layer request).<br>
        <b>The problem:</b> The attacker can use <a href="https://en.wikipedia.org/wiki/Fast_flux">Fast Flux</a> to hide its <i>comman and control server</i> (C&C).
    </p>
    <li>
        Domain names
    </li>
    <p>
        Supposing the attacker changed his IP, you have to deal with this by blocking the domain/sub-domain, because changing the IP address is easy, but changing the DNS is a pain in the ass.<br>
        We can create a DNS rule to block the domain/sub-domain.<br>
        <b>The problem:</b> the attacker can go forward with it, by a new domain and hide the DNS records.<br>
        <i>Punycode</i>
    </p>
    <li>
        
    </li>
</ul>


