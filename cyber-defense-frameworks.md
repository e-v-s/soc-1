
# Cyber Defence Frameworks
## MITRE
### Projetos

- <a href="https://attack.mitre.org/">ATT&CK</a><br>
  **A**dversarial<br>
  **T**actics
  **T**echniques<br>
  **&**<br>
  **C**ommon<br>
  **K**nowledge<br>

  Documentação de *TTPs* comuns.<br>
<a href="https://mitre-attack.github.io/attack-navigator">ATT&CK Navigator for Carbanak.</a>

- CAR: **C**yber **A**nalytics **R**epository Knowledge Base<br>
  Disponibiliza sets de análises explicadas e validadas.<br>
   <a href="https://mitre-attack.github.io/attack-navigator/">CAR navigator layer</a>

- <a href="https://d3fend.mitre.org/">ENGAGE</a>: É um framework para planejamento e discussão de operações de engajamento. <a href="https://engage.mitre.org/starter-kit/">Starter kit</a>

- D3FEND: **D**etection, **D**enial, and **D**isruption **F**ramework **E**mpowering **N**etwork **D**efense
  É uma ferramenta de grafo de contramedidas. Disponibiliza definições, "como funciona", considerações e como usar as técnicas.

- <a href="https://mitre-engenuity.org/">AEP</a>: **A**TT&CK **E**mulation **P**lans

  São guias passo-a-passo em como mimetizar grupos de ameaça específicos. <a href="https://github.com/center-for-threat-informed-defense/adversary_emulation_library">Emulation plan lib</a>

**Tactics**: goal<br>
**Technique**: how to achieve the goal<br>
**Procedure**: how the technique is executed<br>

### ATT&CK and Threat intelligence

O objetivo do *threat intelligence* é de tornar os TTPs acionáveis.

A ideia principal se planejar com antecedência ao coletar informações sobre ameaças comuns que tem como objetivo uma situação específica na sua organização.


## Summit
### Aplicando os conceitos da Pyramid of Pain

#### Valores de hash

It's used to identify a malicious artifact. You can upload the file on <a href="https://www.virustotal.com/gui/">virus total</a>, analyze and block it from being executed.<br><br>
**The problem:** if the attacker knows you blocked the hash of the malware they can recompile it.

#### IP Address

If the *threat actor* changes its malware to evade the hash from being blocked, you cannot evade it by analyzing each file that infects your device. It's better to move on and **deny**, **block** or **drop** inbound requests from malicious IP related to the execution of the malware.<br><br>
By analyzing it with the virustotal tool we can see if there are any **GET** requests being made by the malware and then block this IP.<br><br>
The block is made on the firewall level (as it's an application layer request).<br><br>
**The problem:** The attacker can use <a href="https://en.wikipedia.org/wiki/Fast_flux">Fast Flux</a> to hide its *comman and control server* (C&C).


#### Domain names


Supposing the attacker changed his IP, you have to deal with this by blocking the domain/sub-domain, because changing the IP address is easy, but changing the DNS is a pain in the ass.<br><br>
**We can create a DNS rule to block the domain/sub-domain.**<br><br>
We can see in the sandbox the communications made by the malware:<br>

- HTTP GET requests
- Connections
- DNS requests (they use it to see if there's internet connectivity, if it hasn't then it's useless)


**The problem:** the attacker can go forward with it, by a new domain and hide the DNS records.<br><br>
*Punycode*: changing the name of a domain to look legit.<br><br>
Also, attackers use url shorteners to hide malicious url. But you can see to where it redirects by appending **+** at the and of the tiny.url, bit.ly and goo.gl.


#### Host artifacts


These are traces of the malwere on the system to evade the monitoring of the system for example, like:<br>


- Registry values
- Process execution
- IOC
- Files dropped



In this case we search for something related to the malware and create a sigma rule related to the artifact and blocking the malware.


#### Network Artifacts


If we can block the malware by detecting the *host artifacts*, then the attacker has to change his approach (tactics and tools). Network artifacts can be:<br>


- User-agent strings
- C2 information
- URI patterns followed by HTTP POST resquest



We detect them in **Wireshark** PCAPs by using **network protocol analyzers** such as *TShark* or by exploring **IDS logging** using *Snort*. We block them by creating a sigma rule to block outgoing connections related to the malware.


#### Tools


At this point the attacker would let it go. But if not, he/she would have to change his/her tool and create maldocs. At this stage we should use *antivirus signatures*, *detection rules* and *YARA rules*.

Tools: malwareBazaar, Malshare, SOC prime threat detection marketplace (this one is to create rules for =/= threats that are around).




**addendum**: <a href="https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack">pass-the-hash attacks</a>
