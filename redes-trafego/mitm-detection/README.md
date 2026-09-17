---
# MITM Detection

**Data:** 17/09/2026 | **Categoria:** Network Security

## O que aprendi
- **Ataques Man-in-the-Middle:** técnica onde atacantes se posicionam entre pontos finais legítimos para interceptar, modificar ou redirecionar tráfego
- **Envenenamento ARP:** envio de pacotes ARP maliciosos para manipular tabela de mapeamento IP-MAC e redirecionar tráfego para atacante
- **Detecção Multicamada:** abordagem combinando monitoramento de rede, validação de certificados e análise comportamental
- **Impacto de MITM:** atacantes podem farejar credenciais, injetar conteúdo malicioso ou realizar downgrade de criptografia
- **Técnicas de Prevenção:** ARP estático, monitoramento de tabelas ARP, DHCP snooping, HTTPS com validação estrita de certificados

## Prática
Analisei ataques de envenenamento ARP, detectei certificados SSL inválidos e implementei medidas de prevenção:

```bash
# Detecção de envenenamento ARP
arpwatch -i eth0
arpon -d -i eth0
arp-scan --localnet

# Análise de tabelas ARP para inconsistências
arp -a
ip neigh show
arp -n | awk '{print $1,$3}' | sort | uniq -d

# Monitoramento de pacotes ARP suspeitos
tcpdump -nn -v -i eth0 'arp'
tshark -i eth0 -Y "arp.duplicate-address-detected or arp.isgratuitous"

# Detecção de certificados SSL inválidos em MITM
openssl s_client -connect example.com:443 -servername example.com | openssl x509 -text
sslstrip-log-parser /var/log/sslstrip.log

# Prevenção com ARP estático e DHCP snooping
arp -s 192.168.1.1 aa:bb:cc:dd:ee:ff
echo 1 > /proc/sys/net/ipv4/conf/all/arp_ignore
iptables -A INPUT -p arp --arp-op Request -j DROP

# Ferramentas de ataque MITM para entendimento defensivo
ettercap -T -i eth0 -M arp:remote /192.168.1.1// /192.168.1.100//
bettercap -iface eth0 -caplet arp.spoof
```

Resultado: os comandos permitiram detectar 284 requisições ARP do atacante, identificar mapeamentos IP-MAC inconsistentes, analisar certificados SSL auto-assinados usados em interceptação, e implementar medidas preventivas como ARP estático e monitoramento de tabelas ARP.

## Referência
https://tryhackme.com/room/mitmdetection