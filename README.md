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
