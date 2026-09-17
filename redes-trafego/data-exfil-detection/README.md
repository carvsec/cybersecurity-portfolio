---
# Data Exfil Detection

**Data:** 17/09/2026 | **Categoria:** Data Security

## O que aprendi
- **Exfiltração de Dados:** transferência não autorizada de dados sensíveis para infraestrutura controlada por atacantes via insiders ou sistemas comprometidos
- **Objetivo de Atacantes:** após violar rede, exfiltração representa objetivo principal para extrair informações confidenciais do perímetro
- **Técnicas de Exfiltração:** abordagens que emulam atividades normais de rede usando protocolos como DNS, HTTP, SSH, FTP, ICMP para evitar detecção
- **Detecção por Anomalias:** identificação de consultas DNS anormais para domínios aleatórios com dados codificados em subdomínios
- **Caça em Logs:** análise de logs de DNS, HTTP e outros protocolos para centenas de consultas suspeitas e transferências incomuns

## Prática
Analisei logs de DNS, investiguei transferências HTTP suspeitas e detectei padrões de exfiltração em cenários reais:

```bash
# Detecção de exfiltração por DNS tunneling
tshark -r exfil.pcap -Y "dns.qry.name contains .base32. or dns.qry.name contains .base64."
zeek -r dns_tunnel.pcap
dnscat2-detector -p dns_traffic.pcap

# Análise de logs de DNS para anomalias
grep -E '[A-Za-z0-9+/=]{30,}' /var/log/dns.log
cat dns_queries.log | awk '{print $9}' | sort | uniq -c | sort -nr

# Detecção de exfiltração por HTTP
tshark -r http_exfil.pcap -Y "http.request.method == POST and http.content_length > 1000000"
tcpdump -nn -r transfer.pcap 'tcp port 80 and tcp[20:2] = 0x4854'

# Monitoramento de transferências de dados grandes
iftop -i eth0 -F 192.168.1.0/24
nethogs -t eth0
vnstat -tr -i eth0

# Análise com ferramentas de exfiltração
exiftool -r /var/log/
strings suspicious_file.bin | grep -E '[A-Za-z0-9+/=]{20,}'
```

Resultado: os comandos permitiram detectar consultas DNS com payloads codificados base64 em subdomínios, identificar transferências HTTP POST com volumes anormais de dados, monitorar fluxos de dados suspeitos em tempo real e analisar arquivos para dados codificados.

## Referência
https://tryhackme.com/room/dataexfildetection