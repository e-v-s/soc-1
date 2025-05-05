# Cyber Threat Intelligence

## CIT

- Data: são indicadores discretos. Ex.: IP, urls, hashes;
- Information: são os dados que quando combinados dizem algo;
- Intelligence: é a correlação entre *data* e *information*

O objetivo do CIT é ter as seguintes informações:

- Quem?
- Motivações
- Capacidade
- Artefatos e IOC a serem investigados

### Threat Intel Classification

Strategic
Technical: evidência e artefatos
Tactical: avalia os TTPs e aborda vulnerabilidades através de uma investigação em tempo real
Operational: olha para a motivação e os assets críticos que podem ser o objetivo do atacante

### CTI Lifecycle

- **Direção:** os objetivos são baseados em:

  - Assets e informações da organização que necessitam serem defendidos;
  - Impacto;
  - Fontes dos dados/intel que podem ser usados para mitigar um exploit;
  - Ferramentas e recursos necessários para defender os assets.

- **Coleta:** Automatizar a coleta de dados alinhados com os objetivos;

- **Processamento:** Extração, classificação, organização, taggeamento e graphing das informações coletadas de logs, detecções de malware, tráfego de rede, etc;

- **Análise:** Insights e decisões a serem tomadas;

- **Disseminação:** Das informações pelos *stakeholders*;

- **Feedback:** Das implementações dos controles de segurança entre analistas e *stakeholders*.

### CTI Standards & Frameworks

- MITRE ATT&CK

  - [TAXII](https://oasis-open.github.io/cti-documentation/taxii/intro">): define os protocolos usados na troca de inteligência de ameaças para detecta/previnir/mitigar em tempo real:
    - Collection
    - Channel
<br><br>
  - <a href="https://oasis-open.github.io/cti-documentation/stix/intro">STIX</a>: language for specification, characterisation and communication of std CIT
<br><br>
- Cyber Kill Chain: ajuda a identificar em qual etapa está o ataque:
  - Recon: OSINT, mídias sociais, network scans, emails;
  - Weaponisation: uso de um malware que esteja alinhado com a motivação do ataque;
  - Delivery: como o malware é enviado;
  - Exploitation: estabelecer persistência;
  - Installation: instalação do malware e de ferramentas para ganhar acesso;
  - C2: controle remoto, movimento lateral, escalamento de privilégios;
  - Ações e objetivos.
<br><br>
- The Diamond Model
  - Adversary
  - Victim
  - Infra
  - Capabilities


## Threat Intelligence Tools

### <a href="https://urlscan.io/">Urlscan.io</a>
Escaneia e analisa urls.

### [Abuse.ch](https://abuse.ch/)
Identifica e monitora botnets

- <a href="https://bazaar.abuse.ch/">MalwareBazaar</a>;
- <a href="https://feodotracker.abuse.ch/">FeodoTracker:</a> monitorar botnets C2;
- <a href="https://sslbl.abuse.ch/">SSL Blacklist:</a> ID e detecta conexões SSL maliciosas;
- <a href="https://urlhaus.abuse.ch/">URLhaus:</a> URLs maliciosas usadas para distribuir malware;
- <a href="https://threatfox.abuse.ch/">ThreatFox:</a> IOCs associadas à malware.

### [PhishTool](https://www.phishtool.com/)

- Faz uma análise de emails usando os metadados;
- Usa inteligência heurística e OSINT para entender os TTPs usados;
- Faz classificação e relatório.

**Defang IP address:** https://gchq.github.io/CyberChef/

### [Talos Intelligence](https://talosintelligence.com/)


# YARA
Identifica informações baseandos-e nos binários e padrões textuais contidos no arquivo

## Como criar regras?

- Crie um ```arquivo.yar```:

  Começamos adicionando uma condição de que o arquivo analisado existe:
  ```
  rule exampleRule {
    condition: true
  }
  ```

  Para rodar a regra, usamos o seguinte comando:
  
  ```
  yara arquivo.yar arquivo-a-ser-analisado
  ```

- [Aqui](https://yara.readthedocs.io/en/stable/writingrules.html) temos mais regras.

- Algumas conditions:<br>
  **meta** & **desc** --> adicionam comentários à regra;<br>
  **strings** --> usamos para buscar por texto ou um valor em hexadecimal, ex.:
  ```
  rule check_for_helloworld {
    strings:
      $hello_world = "Hello World!"
      $hello_world_lowercase = "hello world"
      $hello_world_uppercase = "HELLO WORLD"
    condition:
      any of them
  }
  ```

  - Usamos ```$``` para definir uma variável.
  
  - Podemos usar **and**, **not**, **or**, **operators** como ```<=```, `>=` ou `!=`, ex.: se precisamos buscar por arquivos que contenham `hello world` mas que seja menor que 10Kb, usamos:
    ```
    condition: any of them and filesize < 10KB
    ```
  <img src="https://github.com/user-attachments/assets/64ac0ef2-3307-486f-9c9b-19e190e13322">


## Yara Tools

### Pythons'PE Module

### LOKI
É um scanner de IOCs gratuito e *opensource*.
[Github](https://github.com/Neo23x0/Loki)

### THOR
[Aqui](https://www.nextron-systems.com/thor-lite/)

### FENRIR
[Aqui](https://github.com/Neo23x0/Fenrir)


## LOKI
Tem que escanear diretamente no endpoint, via CLI.
No diretório, tem que usar --update para adicionar o diretório signature-base, que é o que vamos usar para investigar os arquivos. Também podemos usar python loki.py -h para ver os comandos que podemos usar.

- Passos
  - Entrar na pasta onde está o arquivo que vc quer investigar
  - Rodar o Loki: python ../../tools/Loki/loki.py -p .

## yarGen
Usado para criar regras quando as regras que temos não são suficientes.

- Passos
  - Ir pro diretório da ferramenta: tools/yarGen
    ```
    python3 yarGen.py --update
    ```
  - Agora adicionamos a regra da seguinte maneira:
    ```
    python 3 yarGen.py -m /caminho/do/diretorio/onde/esta/o/arquivo --excludegood -o /caminho/do/diretorio/onde/esta/o/arquivo.yar
    ```
  - Agora precisamos mover esta regra para as regras do Loki, para então podermos scanear o arquivo novamente:
    ```
    mv caminho/do/diretorio/onde/esta/o/arquivo.yar tools/Loki/signature-n-sei-que/yara
    ```
  - Agora podemos voltar para o diretório onde está o arquivo que queremos scanear e fazer o scan com o Loki


## Valhalla
Podemos usar o sha256 gerado no scan do Loki para buscar mais sobre o scan no [Valhalla](https://www.nextron-systems.com/valhalla/).


# OpenCTI

[OpenCTI](https://github.com/OpenCTI-Platform/opencti) é uma plataforma open-source que serve para fazer a gestão de CTI através de armazenamento, análise, visualização e apresentação de ameaças, malwares e IOCs.


## Modelo de dados do OpenCTI

Usa o std STIX2 *structured threat information expression*, um formato usado no compartilhamento de *threat intelligence*.


Você pode configurar conectores e *data schemas*.


[Download](https://docs.opencti.io/latest/deployment/installation/)


# MISP

## Malware Information Sharing Platform










        






