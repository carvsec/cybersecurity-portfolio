---
# Wireshark Traffic Analysis

**Data:** 17/09/2026 | **Categoria:** Network Forensics

## O que aprendi
- **Detecção de ARP Spoofing:** identificação de anúncios ARP duplicados, conflitos de endereços MAC e pacotes HTTP redirecionados
- **Tunelamento DNS/ICMP:** análise de payloads ocultos em consultas DNS com labels codificadas e túneis ICMP para evasão de firewall
- **Credenciais FTP em Texto Claro:** extração de autenticações FTP não criptografadas e acompanhamento de transferências de arquivos
- **Identificação de Hosts:** mapeamento de endereços MAC para IPs via DHCP, resolução de nomes NetBIOS e análise de tickets Kerberos
- **Correlação de Pacotes:** síntese de conhecimento analítico com funcionalidades do Wireshark para detecção de anomalias

## Prática
Investiguei ataques MITM, analisei tunelamento de protocolos e extraí informações de identificação de hosts:

```bash
# Filtros para detecção de ARP spoofing
arp.duplicate-address-detected
arp.isgratuitous
!(arp.src.hw_mac == arp.dst.hw_mac)

# Análise de tunelamento DNS
dns.qry.name contains ".base64."
dns.qry.name matches ".*[A-Za-z0-9+/=]{20,}.*"

# Identificação de hosts via DHCP/NBNS
bootp.option.hostname
nbns.name
kerberos.CNameString

# Extração de credenciais FTP
ftp contains "USER"
ftp contains "PASS"
ftp.request.command == "PASS"

# Contagem de pacotes específicos
frame.number > 1000 and tcp.port == 80
```

Resultado: os filtros permitiram detectar 284 requisições ARP do atacante, 90 pacotes HTTP interceptados, 6 credenciais snifadas e identificar hosts específicos como Galaxy-A12 e usuário u5 com IP 10.1.12.2.

## Referência
https://tryhackme.com/room/wiresharktrafficanalysis