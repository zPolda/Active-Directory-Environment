# Active Directory Environment

## Objective

Projeto que integra Active Directory com Splunk para criar telemetria avançada através da simulação de ataques reais (ex: Kerberoasting, lateral movement). Objetivo: detectar ameaças em tempo real, validar regras de correlação e fortalecer a segurança do ambiente AD.

### Skills Learned

- Configuração de Splunk Universal Forwarder para coleta centralizada de logs em endpoints.

- Simulação de ataques direcionados a Active Directory usando Atomic Red Team.

- Correlação de eventos entre Windows Event Log, Sysmon e tráfego de rede.

- Desenvolvimento de regras de detecção para técnicas MITRE ATT&CK em ambientes AD.

- Análise forense de atividades maliciosas (ex: Kerberoasting, lateral movement).

### Tools Used

- Active Directory – Infraestrutura de domínio Windows.

- Splunk + Universal Forwarder – Coleta e análise centralizada de logs.

- Sysmon – Monitoramento detalhado de processos e conexões.

- Atomic Red Team – Framework para simulação de ataques realistas.

- Kali Linux – Ferramentas auxiliares (ex: Impacket, Mimikatz).

- PowerShell – Automação e geração de telemetria personalizada.

## Step 1: Criação do Diagrama de Arquitetura

Objetivo: Projetar visualmente a infraestrutura do ambiente Active Directory integrado ao Splunk para definir fluxos de dados, componentes críticos e pontos de coleta de telemetria.

![k2bYi1O](https://github.com/user-attachments/assets/f0394f27-0513-4a55-b7cd-5511ce0d97a0)

#### Texto explicativo: O diagrama demonstra a infraestrutura gerada para os testes, com informações adicionais para complementar o entendimento de todo o fluxo de informações. Inclui a interação entre Active Directory, endpoints Windows com agentes (Splunk UF + Sysmon), servidor Splunk como SIEM central, e a máquina Kali Linux para execução de simulações de ataques. Setas destacam o caminho dos logs desde a geração até a análise no Splunk.

## Step 2: Instalação e Configuração do Splunk e Universal Forwarder

Objetivo:
Instalar o Splunk em um servidor dedicado e deployar o Splunk Universal Forwarder na máquina target (Windows) para coleta e envio de logs ao SIEM central.

<img width="804" height="599" alt="PgNd2Zc" src="https://github.com/user-attachments/assets/2a0d9e29-f39d-43cc-afce-1ef2fd6f85a1" />

<img width="1028" height="773" alt="e4a22e8c-1fe5-4d07-a8a1-b834b78d8a27" src="https://github.com/user-attachments/assets/bd8051c1-f437-4a4d-a51c-a7e0bd5ceeac" />

<img width="1027" height="770" alt="13f64ad3-7a4f-48d1-a67a-cb4ee1117b71" src="https://github.com/user-attachments/assets/62748294-6c52-4ada-a631-36849f966086" />

Texto explicativo:
O Splunk foi instalado em um servidor Ubuntu 20.04 LTS separado da rede de produção, configurado como instância única para receber e indexar logs. Na máquina target (Windows 10), o Splunk Universal Forwarder foi instalado e configurado para enviar logs locais (Windows Event Log, Sysmon) para o Splunk central via porta 9997.


## Step 3: Configuração do Active Directory e Implementação do Domínio

Objetivo:
Configurar um controlador de domínio (Active Directory) em uma máquina Windows Server e integrar a máquina target ao domínio para simular um ambiente corporativo real.

<img width="1026" height="775" alt="26LUjK0" src="https://github.com/user-attachments/assets/b5923fd6-f543-4108-b90a-0548209c5579" />

<img width="1021" height="770" alt="4d3ac4ab-39a0-45b6-82d2-691939177f02" src="https://github.com/user-attachments/assets/10561b94-fc67-454a-a7b5-39532170c82a" />

<img width="988" height="697" alt="f4f2af8c-8232-48cd-8099-4a6ebf608182" src="https://github.com/user-attachments/assets/135cd824-68a9-4f5c-b613-a9af04c04e25" />

Texto explicativo:
"Um servidor Windows Server 2022 foi configurado como controlador de domínio (DC) para o domínio SEC.LOCAL, com serviços de AD DS, DNS e DHCP ativos. A máquina target (Windows 10) foi então ingressada no domínio, permitindo a autenticação centralizada de usuários e a aplicação de políticas de grupo (GPOs). Essa estrutura é fundamental para gerar telemetria realista de ambientes corporativos e testar ataques direcionados ao Active Directory."

## Step 5: Simulação de Brute Force Attack e Detecção no Splunk

Objetivo:
Simular um ataque de força bruta (brute force) a partir do Kali Linux contra o Active Directory e detectar as tentativas de login maliciosas no Splunk em tempo real.

<img width="646" height="744" alt="38bd1dc0-31d6-4bf9-b2a2-11bde308927c" src="https://github.com/user-attachments/assets/3b0c4860-1058-40c8-b67b-0a5cc72b338e" />

<img width="1034" height="777" alt="e95c404d-b626-4d7d-bc01-d20fc9955729" src="https://github.com/user-attachments/assets/a0179cae-6342-46ab-a5be-541ad8747aee" />

<img width="1023" height="771" alt="b1375515-5021-42b5-94e3-a8111c1db10c" src="https://github.com/user-attachments/assets/ac2eb3a9-cff5-490e-8e87-9d582b56cea4" />

Texto explicativo:
"Um ataque de força bruta foi simulado a partir do Kali Linux (IP: 192.168.10.250) contra o controlador de domínio (SEC.LOCAL), utilizando a ferramenta Hydra para tentativas de login via SMB. O Splunk capturou os eventos de falha de autenticação (Windows Event ID 4625) gerados pelo Active Directory, destacando o IP originário do ataque, usuários alvejados e horários das tentativas. 

## Step 6: Simulação de Execução de Comando com Atomic Red Team (T1059.001) e Detecção no Splunk

Objetivo:
Utilizar o Atomic Red Team para simular a execução de comandos maliciosos via PowerShell (T1059.001) e detectar a atividade em tempo real no Splunk, validando a telemetria do ambiente.

<img width="785" height="591" alt="6690ab60-92cd-480a-87a8-f527d000eb43" src="https://github.com/user-attachments/assets/4b4a3ffd-5bb6-4a05-bd4d-7be4a0bca45c" />

<img width="860" height="719" alt="d87ed2bd-6c8f-4cfd-ac5a-3e7d2dc36aee" src="https://github.com/user-attachments/assets/01a160b6-4d2c-4406-84e2-1fbc2d16d373" />

<img width="1021" height="770" alt="ac10d0b2-6056-4a2d-b352-2dbfded3eea1" src="https://github.com/user-attachments/assets/83d61d43-9bff-47ca-98a6-6ded3cc9e283" />


Texto explicativo:
*"O Atomic Red Team foi acionado para simular a técnica T1059.001 (PowerShell) do MITRE ATT&CK. O comando executado via cmd.exe iniciou um script PowerShell malicioso que carregou um XML remoto (hostado no GitHub) para execução de código arbitrário (IEX). O Splunk capturou o evento do Sysmon (EventID 1) com detalhes completos, incluindo a linha de comando, hashes do processo, usuário (SEC\Administrator) e contexto de integridade (High). A detecção destaca o uso de flags de bypass (-exec bypass) e o carregamento de conteúdo externo, típico de ataques de staging ou command-and-control."*

## Conclusão
Este projeto implementou um ambiente de Active Directory com Splunk para geração e análise de telemetria, simulando ataques reais como brute force RDP e execução de comandos maliciosos via Atomic Red Team. Os logs foram correlacionados com técnicas MITRE ATT&CK (ex: T1059.001, T1110), validando a detecção proativa de ameaças.

Próximas atualizações podem incluir:

Integração com EDR (Windows Defender for Endpoint).

Automação de respostas via Splunk SOAR.

Expansão para técnicas avançadas (lateral movement, exfiltração).
