---
# Network Security Essentials

**Data:** 17/09/2026 | **Categoria:** Network Security

## O que aprendi
- **Fundamentos de Proteção:** importância da estruturação de redes para segurança e monitoramento proativo do perímetro
- **Componentes de Segurança:** firewalls para filtragem baseada em regras, IDS para monitoramento de padrões suspeitos, IPS para bloqueio ativo
- **Análise de Logs:** compreensão de logs e fontes de dados diárias em operações SOC incluindo firewall, IDS/IPS e monitoramento
- **Cenários de SOC:** investigação de padrões de tráfego anormais em empresa de serviços financeiros com infraestrutura recém-implantada
- **Correlação de Eventos:** técnica de conectar diferentes eventos e logs para formar quadro completo de atividades na rede

## Prática
Analisei logs de segurança, investiguei alertas e correlacionei múltiplas fontes de dados em cenário corporativo:

```bash
# Comandos para análise de logs de firewall
tail -f /var/log/firewall.log | grep "DENY"
grep "203.0." /var/log/ids.log
cat /var/log/suricata/fast.log | grep -i "alert"

# Análise de tráfego suspeito
tcpdump -nn -vv -r investigation.pcap 'port 443'
tshark -r case.pcap -Y "http.request.method == POST"

# Monitoramento de perímetro
iftop -i eth0 -n
nethogs eth0
vnstat -l -i eth0

# Verificação de regras de firewall
iptables -L -n -v
ufw status verbose
firewall-cmd --list-all
```

Resultado: os comandos permitiram identificar tráfego anormal da rede 203.0.0.0/16, analisar logs de IDS para detecção precoce, monitorar tráfego em tempo real e verificar configurações de firewall para pontos fracos na proteção do perímetro.

## Referência
https://tryhackme.com/room/networksecurityessentials