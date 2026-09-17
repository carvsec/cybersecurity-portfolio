---
# Network Traffic Basics

**Data:** 17/09/2026 | **Categoria:** Network Traffic Analysis

## O que aprendi
- **Network Traffic Analysis (NTA):** processo de captura, inspeção e análise de dados conforme fluem na rede para visibilidade completa
- **Diferença NTA vs Ferramentas:** NTA não é sinônimo de Wireshark, é disciplina analítica usando múltiplas ferramentas
- **Fontes de Tráfego:** endpoints clientes, servidores, dispositivos de rede (roteadores, switches), infraestrutura de segurança
- **Fluxos de Tráfego:** internet para redes privadas e vice-versa, com encapsulamento que pode esconder dados maliciosos
- **DNS Tunneling:** técnica de abuso onde dados são encapsulados em consultas DNS para contornar controles de segurança

## Prática
Identifiquei protocolos, analisei fontes/fluxos de tráfego e detectei técnicas de evasão como DNS tunneling:

```bash
# Comandos básicos de análise de tráfego
tcpdump -i eth0 -w capture.pcap
tcpdump -nn -vvv -r capture.pcap
tcpdump -r dns.pcap 'port 53'

# Identificação de protocolos com tshark
tshark -r traffic.pcap -Y "http"
tshark -r traffic.pcap -Y "dns"
tshark -r traffic.pcap -Y "ftp"

# Detecção de DNS tunneling
tshark -r suspicious.pcap -Y "dns.qry.name matches .*[A-Za-z0-9+/=]{20,}.*"
tcpdump -nn -r dns_tunnel.pcap 'port 53' | grep -E '[A-Za-z0-9+/=]{30,}'

# Análise de fontes e fluxos
iftop -i eth0
nethogs eth0
vnstat -i eth0 -tr 60

# Métodos de captura avançados
tcpdump -i eth0 -s 0 -G 300 -W 48 -w capture_%H%M.pcap
dumpcap -i eth0 -b filesize:100000 -b files:10 -w rotation.pcap

# Análise com ferramentas especializadas
zeek -r network_traffic.pcap
suricata -r capture.pcap -c /etc/suricata/suricata.yaml
```

Resultado: os comandos permitiram capturar tráfego em tempo real, identificar protocolos HTTP/DNS/FTP em arquivos PCAP, detectar consultas DNS com payloads codificados base64, analisar fontes e fluxos de tráfego, e implementar métodos de captura rotativa para investigações prolongadas.

## Referência
https://tryhackme.com/room/networktrafficbasics