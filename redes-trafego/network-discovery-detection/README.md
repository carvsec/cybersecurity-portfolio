---
# Network Discovery Detection

**Data:** 17/09/2026 | **Categoria:** Network Monitoring

## O que aprendi
- **Descoberta de Rede por Atacantes:** primeira fase do ciclo de ataque para identificação de ativos publicamente acessíveis (superfície de ataque)
- **Técnicas de Reconhecimento:** varredura ativa com Nmap para hosts online, portas abertas e serviços; técnicas passivas de coleta de informações
- **Objetivos de Descoberta:** identificação de endereços IP, portas, serviços em execução, versões de serviços e vulnerabilidades exploráveis
- **Detecção de Atividades:** reconhecimento de padrões como tráfego SYN para múltiplas portas, requisições ICMP para range de IPs e comportamento anormal
- **Importância para SOC:** descoberta de rede é uma das fases de ataque mais comuns observadas em turnos, permitindo detecção precoce

## Prática
Analisei atividades de varredura externa, identifiquei padrões de descoberta e reconheci técnicas de reconhecimento em logs:

```bash
# Comandos Nmap para reconhecimento (como atacante faria)
nmap -sS -p 1-1000 192.168.1.0/24
nmap -sU -p 53,123,161 10.0.0.1-100
nmap -sV -O 203.0.113.0/24
nmap --script discovery 192.168.1.1

# Detecção de varreduras em logs (como defensor analisa)
grep "SYN.*from.*to multiple ports" /var/log/ids.log
tshark -r scan.pcap -Y "tcp.flags.syn == 1 and tcp.flags.ack == 0"
tcpdump -nn -vv 'icmp[icmptype] == icmp-echo' -c 100

# Análise de tráfego de reconhecimento
zeek -r discovery.pcap
bro -r scanning.pcap local

# Monitoramento de atividades suspeitas
psad --status
fail2ban-client status sshd
snort -c local.rules -r nmap_scan.pcap -A console
```

Resultado: os comandos permitiram simular atividades de reconhecimento para entender técnicas atacantes, detectar padrões de varredura SYN e ICMP em logs, e monitorar atividades de descoberta em tempo real para resposta precoce.

## Referência
https://tryhackme.com/room/networkdiscoverydetection