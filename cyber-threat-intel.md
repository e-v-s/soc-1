<h1>Cyber Threat Intelligence</h1>

<h2>CIT</h2>

<ul>
<li>Data: são indicadores discretos. Ex.: IP, urls, hashes;</li>
<li>Information: são os dados que quando combinados dizem algo;</li>
<li>Intelligence: é a correlação entre <i>data</i> e <i>information</i></li>
</ul>

O objetivo do CIT é ter as seguintes informações:

<ul>
<li>Quem?</li>
<li>Motivações</li>
<li>Capacidade</li>
<li>Artefatos e IOC a serem investigados</li>
</ul>

<h3>Threat Intel Classification</h3>

<ul>
<li>Strategic</li>
<li><b>Technical:</b> evidência e artefatos</li>
<li><b>Tactical:</b> avalia os TTPs e aborda vulnerabilidades através de uma investigação em tempo real</li>
<li><b>Operational:</b> olha para a motivação e os assets críticos que podem ser o objetivo do atacante</li>
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
<img src="https://github.com/user-attachments/assets/64ac0ef2-3307-486f-9c9b-19e190e13322">
</li>
</ul>
</ul>

        
<h2>Yara Tools</h2>
<h3>Pythons'PE Module</h3>
<h3>LOKI</h3>
Free opensource IOC scanner.<br>
<a href="https://github.com/Neo23x0/Loki">Github</a>
<h3>THOR</h3>
<a href="https://www.nextron-systems.com/thor-lite/">Here</a>
<h3>FENRIR</h3>
<a href="https://github.com/Neo23x0/Fenrir">Here</a>


<h2>LOKI</h2>
Tem que escanear diretamente no endpoint, via CLI.<br><br>
No diretório, tem que usar --update para adicionar o diretório signature-base, que é o que vamos usar para investigar os arquivos. Também podemos usar python loki.py -h para ver os comandos que podemos usar.
<ul>
<li>Passos</li>
<ul>
<li>Entrar na pasta onde está o arquivo que vc quer investigar</li>
<li>Rodar o Loki: python ../../tools/Loki/loki.py -p .</li>
</ul>
</ul>


<h2>yarGen</h2>
Usado para criar regras quando as regras que temos não são suficientes.<br><br>
<ul>
<li>Passos</li>
<ul>
<li>Ir pro diretório da ferramenta: tools/yarGen</li>
<li>python3 yarGen.py --update</li>
<li>Agora adicionamos a regra da seguinte maneira:<br><br>
python 3 yarGen.py -m /caminho/do/diretorio/onde/esta/o/<b>arquivo<b> --excludegood -o /caminho/do/diretorio/onde/esta/o/<b>arquivo.yar<b>
</li>
<li>Agora precisamos mover esta regra para as regras do Loki, para então podermos scanear o arquivo novamente:<br>
mv caminho/do/diretorio/onde/esta/o/<b>arquivo.yar<b> tools/Loki/signature-n-sei-que/yara</li>
<li>Agora podemos voltar para o diretório onde está o arquivo que queremos scanear e fazer o scan com o Loki</li>
</ul>
</ul>

<h2>Valhalla</h2>
Podemos usar o sha256 gerado no scan do Loki para buscar mais sobre o scan no <a href="https://www.nextron-systems.com/valhalla/">Valhalla</a>


<h1>OpenCTI</h1>



        






